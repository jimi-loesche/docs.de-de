---
title: "TimeSpan-Standardformatzeichenfolgen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Formatbezeichner, Standardzeitintervall"
  - "Formatbezeichner, Zeitintervalle"
  - "Formatzeichenfolgen"
  - "Formatieren [.NET Framework], Uhrzeit"
  - "Formatieren [.NET Framework], Zeitintervalle"
  - "Standardformatzeichenfolgen, Zeitintervalle"
  - "Formatzeichenfolgen für Standardzeitintervalle"
  - "TimeSpan-Standardformatzeichenfolgen"
  - "Zeit [.NET Framework], Formatierung"
  - "Zeitintervalle [.NET Framework], Formatierung"
ms.assetid: 9f6c95eb-63ae-4dcc-9c32-f81985c75794
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# TimeSpan-Standardformatzeichenfolgen
Eine standardmäßige <xref:System.TimeSpan>\-Formatzeichenfolge verwendet einen einzelnen Formatbezeichner, um die Textdarstellung eines <xref:System.TimeSpan>\-Werts zu definieren, der sich aus einem Formatierungsvorgang ergibt.  Jede Formatzeichenfolge, die mehr als ein Zeichen \(einschließlich Leerzeichen\) enthält, wird als benutzerdefinierte <xref:System.TimeSpan>\-Zahlenformatzeichenfolge interpretiert.  Weitere Informationen finden Sie unter [Benutzerdefinierte TimeSpan\-Formatzeichenfolgen](../../../docs/standard/base-types/custom-timespan-format-strings.md).  
  
 Die Zeichenfolgendarstellungen von <xref:System.TimeSpan>\-Werten werden durch Aufrufe der Überladungen der <xref:System.TimeSpan.ToString%2A?displayProperty=fullName>\-Methode und durch Methoden, die die kombinierte Formatierung unterstützen \(z. B. <xref:System.String.Format%2A?displayProperty=fullName>\), erzeugt.  Weitere Informationen finden Sie unter [Formatierung von Typen](../../../docs/standard/base-types/formatting-types.md) und [Kombinierte Formatierung](../../../docs/standard/base-types/composite-formatting.md).  Das folgende Beispiel veranschaulicht die Verwendung von Standardformatzeichenfolgen bei Formatierungsvorgängen.  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/formatexample1.cs#2)]
 [!code-vb[Conceptual.TimeSpan.Standard#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/formatexample1.vb#2)]  
  
 Standardmäßige <xref:System.TimeSpan>\-Formatzeichenfolgen werden auch von der <xref:System.TimeSpan.ParseExact%2A?displayProperty=fullName>\-Methode und <xref:System.TimeSpan.TryParseExact%2A?displayProperty=fullName>\-Methode verwendet, um das erforderliche Format von Eingabezeichenfolgen für Analysevorgänge zu definieren.  \(Beim Analysieren wird die Zeichenfolgendarstellung eines Werts in diesen Wert konvertiert.\) Das folgende Beispiel veranschaulicht die Verwendung von Standardformatzeichenfolgen bei Analysevorgängen.  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/parseexample1.cs#3)]
 [!code-vb[Conceptual.TimeSpan.Standard#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/parseexample1.vb#3)]  
  
<a name="top"></a> Die folgende Tabelle enthält die Standardzeitintervall\-Formatbezeichner.  
  
|Formatbezeichner|Name|Beschreibung|Beispiele|  
|----------------------|----------|------------------|---------------|  
|"c"|Konstantenformat \(unveränderlich\)|Dieser Bezeichner ist nicht kulturabhängig.  Er hat das Format `[-][d’.’]hh’:’mm’:’ss[‘.’fffffff]`.<br /><br /> \(Die "t"\- und "T"\-Formatzeichenfolgen erzeugen die gleichen Ergebnisse.\)<br /><br /> Weitere Informationen finden Sie unter [Der Konstantenformatbezeichner "c"](#Constant).|`TimeSpan.Zero` \-\> 00:00:00<br /><br /> `New TimeSpan(0, 0, 30, 0)` \-\> 00:30:00<br /><br /> `New TimeSpan(3, 17, 25, 30, 500)` \-\> 3.17:25:30.5000000|  
|"g"|Allgemeines kurzes Format|Dieser Bezeichner gibt nur aus, was benötigt wird.  Es ist kulturabhängig und besitzt das Format `[-][d’:’]h’:’mm’:’ss[.FFFFFFF]`.<br /><br /> Weitere Informationen finden Sie unter [Der allgemeine kurze Formatbezeichner "g"](#GeneralShort).|`New TimeSpan(1, 3, 16, 50, 500)` \-\> 1:3:16:50.5 \(en\-US\)<br /><br /> `New TimeSpan(1, 3, 16, 50, 500)` \-\> 1:3:16:50,5 \(fr\-FR\)<br /><br /> `New TimeSpan(1, 3, 16, 50, 599)` \-\> 1:3:16:50.599 \(en\-US\)<br /><br /> `New TimeSpan(1, 3, 16, 50, 599)` \-\> 1:3:16:50,599 \(fr\-FR\)|  
|"G"|Allgemeines Langformat|Dieser Bezeichner gibt immer Tage und sieben Dezimalstellen aus.  Es ist kulturabhängig und besitzt das Format `[-]d’:’hh’:’mm’:’ss.fffffff`.<br /><br /> Weitere Informationen finden Sie unter [Der allgemeine Langformatbezeichner "G"](#GeneralLong).|`New TimeSpan(18, 30, 0)` \-\> 0:18:30:00.0000000 \(en\-US\)<br /><br /> `New TimeSpan(18, 30, 0)` \-\> 0:18:30:00,0000000 \(fr\-FR\)|  
  
<a name="Constant"></a>   
## Der Konstantenformatbezeichner "c"  
 Der Formatbezeichner "c" gibt die Zeichenfolgendarstellung eines <xref:System.TimeSpan>\-Werts in der folgenden Form an:  
  
 \[\-\]\[*d*.\]*hh*:*mm*:*ss*\[.*fffffff*\]  
  
 Elemente in eckigen Klammern \(\[ und \]\) sind optional.  Der Punkt \(.\) und der Doppelpunkt \(:\) sind Literalsymbole.  In der folgenden Tabelle werden die restlichen Elemente beschrieben.  
  
|Element|Beschreibung|  
|-------------|------------------|  
|*\-*|Ein optionales negatives Vorzeichen, das ein negatives Zeitintervall angibt.|  
|*d*|Die optionale Anzahl von Tagen ohne führende Nullen.|  
|*hh*|Die Anzahl von Stunden zwischen "00" und "23".|  
|*mm*|Die Anzahl von Minuten zwischen "00" und "59".|  
|*ss*|Die Anzahl von Sekunden zwischen "0" und "59".|  
|*fffffff*|Der optionale Bruchteil einer Sekunde.  Der Wert kann zwischen "0000001" \(ein Tick oder ein Zehnmillionstel einer Sekunde\) und "9999999" \(9.999.999 Zehnmillionstel einer Sekunde oder eine Sekunde minus ein Tick\) liegen.|  
  
 Anders als die Formatbezeichner "G" und "g" ist der Formatbezeichner "c" nicht kulturabhängig.  Er erzeugt die Zeichenfolgendarstellung eines <xref:System.TimeSpan>\-Werts, der unveränderlich ist und für alle früheren Versionen von .NET Framework vor [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] verwendet wird. "  "c" ist die standardmäßige <xref:System.TimeSpan>\-Formatzeichenfolge. Die <xref:System.TimeSpan.ToString?displayProperty=fullName>\-Methode formatiert einen Zeitintervallwert mit der Formatzeichenfolge "c".  
  
> [!NOTE]
>  <xref:System.TimeSpan> unterstützt auch die standardmäßigen "t"\- und "T"\-Formatzeichenfolgen, die im Verhalten identisch mit der Standardformatzeichenfolge "c" sind.  
  
 Im folgenden Beispiel werden zwei <xref:System.TimeSpan>\-Objekte instanziiert, zum Ausführen arithmetischer Vorgänge verwendet, und das Ergebnis wird angezeigt.  In jedem Fall wird die kombinierte Formatierung verwendet, um den <xref:System.TimeSpan>\-Wert mithilfe des Formatbezeichners "c" anzuzeigen.  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/standardc1.cs#1)]
 [!code-vb[Conceptual.TimeSpan.Standard#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/standardc1.vb#1)]  
  
 [Zurück zur Tabelle](#Top)  
  
<a name="GeneralShort"></a>   
## Der allgemeine Kurzformatbezeichner "g"  
 Der <xref:System.TimeSpan>\-Formatbezeichner "g" gibt die Zeichenfolgendarstellung eines <xref:System.TimeSpan>\-Werts in einem kompakten Format an, indem nur die erforderlichen Elemente eingeschlossen werden.  Er hat das folgende Format:  
  
 \[\-\]\[*d*:\]*h*:*mm*:*ss*\[.*FFFFFFF*\]  
  
 Elemente in eckigen Klammern \(\[ und \]\) sind optional.  Der Doppelpunkt \(:\) ist ein Literalsymbol.  In der folgenden Tabelle werden die restlichen Elemente beschrieben.  
  
|Element|Beschreibung|  
|-------------|------------------|  
|*\-*|Ein optionales negatives Vorzeichen, das ein negatives Zeitintervall angibt.|  
|*d*|Die optionale Anzahl von Tagen ohne führende Nullen.|  
|*h*|Die Anzahl von Stunden zwischen "0" und "23" ohne führende Nullen.|  
|*mm*|Die Anzahl von Minuten zwischen "00" und "59".|  
|*ss*|Die Anzahl von Sekunden zwischen "00" und "59".|  
|*.*|Das Trennzeichen für Sekundenbruchteile.  Dies entspricht der <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>\-Eigenschaft der angegebenen Kultur ohne Benutzerüberschreibungen.|  
|*FFFFFFF*|Die Sekundenbruchteile.  Es werden so wenig Ziffern wie möglich angezeigt.|  
  
 Der Formatbezeichner "g" ist wie der Formatbezeichner "G" lokalisiert.  Das Trennzeichen für Sekundenbruchteile basiert auf der aktuellen Kultur oder der <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>\-Eigenschaft einer angegebenen Kultur.  
  
 Im folgenden Beispiel werden zwei <xref:System.TimeSpan>\-Objekte instanziiert, zum Ausführen arithmetischer Vorgänge verwendet, und das Ergebnis wird angezeigt.  In jedem Fall wird die kombinierte Formatierung zum Anzeigen des <xref:System.TimeSpan>\-Werts mit dem Formatbezeichner "g" verwendet.  Darüber hinaus wir der <xref:System.TimeSpan>\-Wert unter Verwendung der Formatierungskonventionen der aktuellen Systemkultur formatiert \(d. h. in diesem Fall Englisch \- USA oder en\-US\) und der Kultur Französisch \- Frankreich \(fr\-FR\)\).  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/standardshort1.cs#4)]
 [!code-vb[Conceptual.TimeSpan.Standard#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/standardshort1.vb#4)]  
  
 [Zurück zur Tabelle](#Top)  
  
<a name="GeneralLong"></a>   
## Der allgemeine Langformatbezeichner "G"  
 Der <xref:System.TimeSpan>\-Formatbezeichner "G" gibt die Zeichenfolgendarstellung eines <xref:System.TimeSpan>\-Werts in einem Langformat zurück, das immer Tage und Sekundenbruchteile enthält.  Die Zeichenfolge, die sich aus dem Standardformatbezeichner "G" ergibt, hat folgendes Format:  
  
 \[\-\]*d*:*hh*:*mm*:*ss*.*fffffff*  
  
 Elemente in eckigen Klammern \(\[ und \]\) sind optional.  Der Doppelpunkt \(:\) ist ein Literalsymbol.  In der folgenden Tabelle werden die restlichen Elemente beschrieben.  
  
|Element|Beschreibung|  
|-------------|------------------|  
|*\-*|Ein optionales negatives Vorzeichen, das ein negatives Zeitintervall angibt.|  
|*d*|Die Anzahl von Tagen ohne führende Nullen.|  
|*hh*|Die Anzahl von Stunden zwischen "00" und "23".|  
|*mm*|Die Anzahl von Minuten zwischen "00" und "59".|  
|*ss*|Die Anzahl von Sekunden zwischen "00" und "59".|  
|*.*|Das Trennzeichen für Sekundenbruchteile.  Dies entspricht der <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>\-Eigenschaft der angegebenen Kultur ohne Benutzerüberschreibungen.|  
|*fffffff*|Die Sekundenbruchteile.|  
  
 Der Formatbezeichner "g" ist wie der Formatbezeichner "G" lokalisiert.  Das Trennzeichen für Sekundenbruchteile basiert auf der aktuellen Kultur oder der <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>\-Eigenschaft einer angegebenen Kultur.  
  
 Im folgenden Beispiel werden zwei <xref:System.TimeSpan>\-Objekte instanziiert, zum Ausführen arithmetischer Vorgänge verwendet, und das Ergebnis wird angezeigt.  In jedem Fall wird die kombinierte Formatierung zum Anzeigen des <xref:System.TimeSpan>\-Werts mit dem Formatbezeichner "G" verwendet.  Darüber hinaus wir der <xref:System.TimeSpan>\-Wert unter Verwendung der Formatierungskonventionen der aktuellen Systemkultur formatiert \(d. h. in diesem Fall Englisch \- USA oder en\-US\) und der Kultur Französisch \- Frankreich \(fr\-FR\)\).  
  
 [!code-csharp[Conceptual.TimeSpan.Standard#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.timespan.standard/cs/standardlong1.cs#5)]
 [!code-vb[Conceptual.TimeSpan.Standard#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.timespan.standard/vb/standardlong1.vb#5)]  
  
 [Zurück zur Tabelle](#Top)  
  
## Siehe auch  
 [Formatierung von Typen](../../../docs/standard/base-types/formatting-types.md)   
 [Benutzerdefinierte TimeSpan\-Formatzeichenfolgen](../../../docs/standard/base-types/custom-timespan-format-strings.md)   
 [Analysieren von Zeichenfolgen](../../../docs/standard/base-types/parsing-strings.md)