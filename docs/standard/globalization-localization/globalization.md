---
title: "Globalisierung | Microsoft Docs"
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
  - "Globalisierung [.NET Framework], Informationen über die Globalisierung"
  - "Globale Anwendungen, Globalisierung"
  - "Internationale Anwendungen [.NET Framework], Globalisierung"
  - "Weltweit einsatzfähige Anwendungen, Globalisierung"
  - "Anwendungsentwicklung [.NET Framework], Globalisierung"
  - "Kultur, Globalisierung"
ms.assetid: 4e919934-6b19-42f2-b770-275a4fae87c9
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Globalisierung
Globalisierung bedeutet Gestaltung und Entwicklung von Apps, die lokalisierte Benutzeroberflächen und regionale Daten für Benutzer verschiedener Kulturen unterstützen. Bevor Sie mit der Entwurfsphase beginnen, sollten Sie festlegen, welche Kulturen die App unterstützen soll. Auch wenn eine App standardmäßig auf eine einzige Kultur oder Region ausgerichtet ist, kann Sie so entworfen und geschrieben werden, dass sie leicht auf Benutzer in anderen Kulturen oder Regionen ausgeweitet werden kann.  
  
 Als Entwickler haben wir alle bestimmte Annahmen über Benutzeroberflächen und Daten, die durch unsere Kulturen geformt werden. Für einen englischsprachigen Entwickler in den USA erscheint das Serialisieren von Datums\- und Uhrzeitangaben als Zeichenfolge im Format `MM/dd/yyyy hh:mm:ss` absolut plausibel. Das Deserialisieren dieser Zeichenfolge auf einem System in einer anderen Kultur könnte jedoch eine <xref:System.FormatException>\-Ausnahme auslösen oder falsche Daten generieren. Durch Globalisierung können wir solche kulturspezifischen Annahmen identifizieren sowie sicherstellen, dass sie den Entwurf oder den Code der App nicht beeinträchtigen.  
  
 In den folgenden Abschnitten werden einige zu beachtende Probleme erläutert sowie bewährte Methoden zur Behandlung von Zeichenfolgen, Daten\- und Uhrzeitwerten sowie numerischen Werten in einer globalisierten App vorgestellt.  
  
-   [Arbeiten mit Zeichenfolgen](../../../docs/standard/globalization-localization/globalization.md#HandlingStrings)  
  
    -   [Unicode intern verwenden](../../../docs/standard/globalization-localization/globalization.md#Strings_Unicode)  
  
    -   [Ressourcendateien verwenden](../../../docs/standard/globalization-localization/globalization.md#Strings_Resources)  
  
    -   [Suchen und Vergleichen von Zeichenfolgen](../../../docs/standard/globalization-localization/globalization.md#Strings_Searching)  
  
    -   [Testen von Zeichenfolgen auf Gleichheit](../../../docs/standard/globalization-localization/globalization.md#Strings_Equality)  
  
    -   [Ordnen und Sortieren von Zeichenfolgen](../../../docs/standard/globalization-localization/globalization.md#Strings_Ordering)  
  
    -   [Zeichenfolgenverkettung vermeiden](../../../docs/standard/globalization-localization/globalization.md#Strings_Concat)  
  
-   [Arbeiten mit Datumsangaben und Zeiten](../../../docs/standard/globalization-localization/globalization.md#DatesAndTimes)  
  
    -   [Beibehalten von Datums- und Zeitangaben](../../../docs/standard/globalization-localization/globalization.md#DatesAndTimes_Persist)  
  
    -   [Anzeigen von Datums- und Zeitangaben](../../../docs/standard/globalization-localization/globalization.md#DatesAndTimes_Display)  
  
    -   [Serialisierung und Unterstützung von Zeitzonen](../../../docs/standard/globalization-localization/globalization.md#DatesAndTimes_TimeZones)  
  
    -   [Ausführen von arithmetischen Datums- und Uhrzeitoperationen](../../../docs/standard/globalization-localization/globalization.md#DatesAndTimes_Arithmetic)  
  
-   [Arbeiten mit numerischen Werte](../../../docs/standard/globalization-localization/globalization.md#Numbers)  
  
    -   [Anzeigen von numerischen Werten](../../../docs/standard/globalization-localization/globalization.md#Numbers_Display)  
  
    -   [Beibehalten von numerischen Werten](../../../docs/standard/globalization-localization/globalization.md#Numbers_Persist)  
  
-   [Arbeiten mit kulturspezifischen Einstellungen](../../../docs/standard/globalization-localization/globalization.md#Cultures)  
  
<a name="HandlingStrings"></a>   
## Arbeiten mit Zeichenfolgen  
 Die Behandlung von Zeichen und Zeichenfolgen ist ein zentraler Schwerpunkt der Globalisierung, da jede Kultur bzw. Region u. U. unterschiedliche Zeichen und Zeichensätze verwendet und diese anders sortiert. Dieser Abschnitt enthält Empfehlungen für die Verwendung von Zeichenfolgen in globalisierten Apps.  
  
<a name="Strings_Unicode"></a>   
### Unicode intern verwenden  
 Standardmäßig verwendet .NET Framework Unicode\-Zeichenfolgen. Eine Unicode\-Zeichenfolge besteht aus null, einem oder mehreren <xref:System.Char>\-Objekten, die jeweils eine UTF\-16\-Codeeinheit darstellen. Es gibt eine Unicode\-Darstellung für nahezu jedes Zeichen in allen weltweit verwendeten Zeichensätzen.  
  
 Viele Anwendungen und Betriebssysteme, einschließlich das Windows\-Betriebssystem, können auch Codepages verwenden, um Zeichensätze darzustellen. Codepages enthalten normalerweise die ASCII\-Standardwerte von 0x00 bis 0x7F und ordnen andere Zeichen den restlichen Werten von 0x80 bis 0xFF zu. Die Interpretation der Werte von 0x80 bis 0xFF ist von der jeweiligen Codepage abhängig. Daher sollten Sie Codepages, soweit möglich, in globalisierten Apps vermeiden.  
  
 Das folgende Beispiel veranschaulicht die Risiken beim Interpretieren von Codepagedaten, wenn sich die Standardcodepage in einem System von der Codepage unterscheidet, auf der die Daten gespeichert wurden. \(Um dieses Szenario zu simulieren, werden im Beispiel explizit unterschiedliche Codepages angegeben.\) Zuerst wird im Beispiel ein Array definiert, das aus den Großbuchstaben des griechischen Alphabets besteht. Diese werden durch die Verwendung von Codepage 737 \(auch als MS\-DOS Greek bezeichnet\) in ein Bytearray codiert, das in eine Datei geschrieben wird. Wenn die Datei abgerufen und das Bytearray mit Codepage 737 decodiert wird, werden die ursprünglichen Zeichen wiederhergestellt. Wenn die Datei dagegen abgerufen und das Bytearray mit Codepage 1252 \(bzw. Windows\-1252 zur Darstellung der Zeichen im lateinischen Alphabet\) decodiert wird, gehen die ursprünglichen Zeichen verloren.  
  
 [!code-csharp[Conceptual.Globalization#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/codepages1.cs#1)]
 [!code-vb[Conceptual.Globalization#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/codepages1.vb#1)]  
  
 Durch die Verwendung von Unicode wird sichergestellt, dass die gleichen Codeeinheiten stets den gleichen Zeichen zugeordnet werden und dass die gleichen Zeichen immer den gleichen Bytearrays zugeordnet werden.  
  
<a name="Strings_Resources"></a>   
### Ressourcendateien verwenden  
 Auch wenn Sie eine App entwickeln, die auf eine einzige Kultur oder Region ausgerichtet ist, sollten Sie Ressourcendateien zum Speichern von Zeichenfolgen und anderen Ressourcen verwenden, die auf der Benutzeroberfläche angezeigt werden. Sie sollten diese niemals direkt in den Code einfügen. Die Verwendung von Ressourcendateien bietet eine Reihe von Vorteilen:  
  
-   Alle Zeichenfolgen befinden sich an einem einzigen Ort. Sie müssen nicht den gesamten Quellcode nach Zeichenfolgen durchsuchen, die für eine bestimmte Sprache oder Kultur geändert werden müssen.  
  
-   Zeichenfolgen müssen nicht dupliziert werden. Entwickler, die keine Ressourcendateien verwenden, definieren die gleiche Zeichenfolge oft in mehreren Quellcodedateien. Diese Duplizierung erhöht die Wahrscheinlichkeit, dass Instanzen übersehen werden, wenn eine Zeichenfolge geändert wird.  
  
-   Sie können Nicht\-Zeichenfolgenressourcen wie Bilder oder Binärdaten in die Ressourcendatei aufnehmen, anstatt diese in einer eigenständigen Datei zu speichern, sodass sie leicht abgerufen werden können.  
  
 Die Verwendung von Ressourcendateien hat insbesondere dann Vorteile, wenn Sie eine lokalisierte App erstellen. Wenn Sie Ressourcen in Satellitenassemblys bereitstellen, wählt die Common Language Runtime automatisch eine der Kultur entsprechende Ressource anhand der aktuellen Kultur der Benutzeroberfläche aus, wie von der <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>\-Eigenschaft definiert. Solange Sie eine entsprechende kulturspezifische Ressource bereitstellen und ein <xref:System.Resources.ResourceManager>\-Objekt ordnungsgemäß instanziieren oder eine stark typisierte Ressourcenklasse verwenden, werden die Details zum Abrufen der entsprechenden Ressourcen von der Laufzeit behandelt.  
  
 Weitere Informationen zum Erstellen von Ressourcendateien finden Sie unter [Erstellen von Ressourcendateien](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md). Informationen zum Erstellen und Bereitstellen von Satellitenassemblys finden Sie unter [Erstellen von Satellitenassemblys](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md) und [Verpacken und Bereitstellen von Ressourcen](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md).  
  
<a name="Strings_Searching"></a>   
### Suchen und Vergleichen von Zeichenfolgen  
 Behandeln Sie Zeichenfolgen möglichst als ganze Zeichenfolgen und nicht als eine Reihe einzelner Zeichen. Dies ist besonders wichtig, wenn Sie Teilzeichenfolgen sortieren oder danach suchen, um Probleme beim Analysieren von kombinierten Zeichen zu vermeiden.  
  
> [!TIP]
>  Sie können die <xref:System.Globalization.StringInfo>\-Klasse verwenden, um mit den Textelementen anstelle der einzelnen Zeichen in einer Zeichenfolge zu arbeiten.  
  
 Beim Suchen und Vergleichen von Zeichenfolgen wird häufig der Fehler begangen, die Zeichenfolge als Auflistung von Zeichen zu behandeln, die jeweils durch ein <xref:System.Char>\-Objekt dargestellt werden. Tatsächlich wird ein einzelnes Zeichen u. U. durch ein oder mehrere <xref:System.Char>\-Objekte gebildet. Solche Zeichen werden am häufigsten in den Zeichenfolgen von Kulturen gefunden, deren Alphabet aus Zeichen außerhalb des lateinischen Unicode\-Standardzeichenbereichs \(U\+0021 bis U\+007E\) besteht. Im folgenden Beispiel wird versucht, den Index des LATEINISCHEN GROSSBUCHSTABENS A MIT GRAVIS \(U\+00C0\) in einer Zeichenfolge zu suchen. Dieses Zeichen kann jedoch auf zwei verschiedene Arten dargestellt werden: als einzelne Codeeinheit \(U\+00C0\) oder als zusammengesetztes Zeichen \(zwei Codeeinheiten: U\+0021 und U\+007E\). In diesem Fall wird das Zeichen in der Zeichenfolgeninstanz von zwei <xref:System.Char>\-Objekten, U\+0021 und U\+007E, dargestellt. Der Beispielcode ruft die <xref:System.String.IndexOf%28System.Char%29?displayProperty=fullName>\- und die <xref:System.String.IndexOf%28System.String%29?displayProperty=fullName>\-Überladung auf, um die Position des Zeichens in der Zeichenfolgeninstanz zu suchen. Diese geben jedoch unterschiedliche Ergebnisse zurück. Der erste Methodenaufruf weist ein <xref:System.Char>\-Argument auf. Dieser führt einen ordinalen Vergleich durch und findet daher keine Übereinstimmung. Der zweite Aufruf weist ein <xref:System.String>\-Argument auf. Dieser führt einen kulturabhängigen Vergleich durch und findet daher eine Übereinstimmung.  
  
 [!code-csharp[Conceptual.Globalization#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/search1.cs#18)]
 [!code-vb[Conceptual.Globalization#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/search1.vb#18)]  
  
 Sie können die Mehrdeutigkeit in diesem Beispiel \(Aufrufe an zwei ähnliche Überladungen einer Methode, die unterschiedliche Ergebnisse zurückgeben\) teilweise vermeiden, indem Sie eine Überladung aufrufen, die einen <xref:System.StringComparison>\-Parameter wie z. B. <xref:System.String.IndexOf%28System.String%2CSystem.StringComparison%29?displayProperty=fullName> oder <xref:System.String.LastIndexOf%28System.String%2CSystem.StringComparison%29?displayProperty=fullName> enthält.  
  
 Suchen sind jedoch nicht immer kulturabhängig. Wenn der Zweck der Suche darin besteht, eine Sicherheitsentscheidung zu treffen oder Zugriff auf eine Ressource zu gewähren bzw. nicht zu gewähren, sollte der Vergleich ordinal sein, wie im nächsten Abschnitt erläutert wird.  
  
<a name="Strings_Equality"></a>   
### Testen von Zeichenfolgen auf Gleichheit  
 Bestimmen Sie zum Testen von zwei Zeichenfolgen auf Gleichheit nicht deren Übereinstimmung in der Sortierreihenfolge, sondern verwenden Sie die <xref:System.String.Equals%2A?displayProperty=fullName>\-Methode anstelle einer Zeichenfolgenvergleichsmethode wie <xref:System.String.Compare%2A?displayProperty=fullName> oder <xref:System.Globalization.CompareInfo.Compare%2A?displayProperty=fullName>.  
  
 Vergleiche auf Gleichheit werden in der Regel durchgeführt, um bedingt auf eine Ressource zuzugreifen. Beispielsweise können Sie einen Vergleich auf Gleichheit durchführen, um ein Kennwort zu überprüfen oder das Vorhandensein einer Datei zu bestätigen. Solche nicht linguistischen Vergleiche sollten immer ordinal anstatt kulturabhängig sein. Im Allgemeinen sollten Sie die <xref:System.String.Equals%28System.String%2CSystem.StringComparison%29?displayProperty=fullName>\-Instanzmethode Methode oder die statische <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=fullName>\-Methode mit dem Wert <xref:System.StringComparison?displayProperty=fullName> für Zeichenfolgen wie Kennwörter und mit dem Wert <xref:System.StringComparison?displayProperty=fullName> für Zeichenfolgen wie Dateinamen oder URIs aufrufen.  
  
 Vergleiche auf Gleichheit umfassen gelegentlich Suchen oder Teilzeichenfolgenvergleiche anstelle von Aufrufen der <xref:System.String.Equals%2A?displayProperty=fullName>\-Methode. In einigen Fällen können Sie eine Teilzeichenfolgensuche verwenden, um zu bestimmen, ob diese Teilzeichenfolge einer anderen Zeichenfolge entspricht. Wenn der Zweck dieses Vergleiches nicht linguistisch ist, sollte die Suche ebenfalls ordinal anstatt kulturabhängig sein.  
  
 Das folgende Beispiel veranschaulicht das Risiko einer kulturabhängigen Suche bei nicht linguistischen Daten. Die `AccessesFileSystem`\-Methode wurde entworfen, um den Dateisystemzugriff für URIs zu verweigern, die mit der Teilzeichenfolge "FILE" beginnen. Hierzu wird ein kulturabhängiger Vergleich unter Beachtung von Groß\- und Kleinschreibung zwischen dem Anfang des URI und der Zeichenfolge "FILE" durchgeführt. Da ein URI, der auf das Dateisystem zugreift, mit "FILE:" oder mit "file:" beginnen kann, ist die implizite Annahme, dass "i" \(U\+0069\) immer die Kleinbuchstabenentsprechung von "I" \(U\+0049\) ist. Auf Türkisch und Aserbaidschanisch ist die Großbuchstabenversion von "i" jedoch "İ" \(U\+0130\). Aufgrund dieser Diskrepanz gewährt der kulturabhängige Vergleich den Dateisystemzugriff, wenn er eigentlich verhindert werden soll.  
  
 [!code-csharp[Conceptual.Globalization#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/equals1.cs#12)]
 [!code-vb[Conceptual.Globalization#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/equals1.vb#12)]  
  
 Sie können dieses Problem vermeiden, indem Sie einen ordinalen Vergleich ohne Beachtung von Groß\- und Kleinschreibung ausführen, wie im folgenden Beispiel gezeigt wird.  
  
 [!code-csharp[Conceptual.Globalization#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/equals2.cs#13)]
 [!code-vb[Conceptual.Globalization#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/equals2.vb#13)]  
  
<a name="Strings_Ordering"></a>   
### Ordnen und Sortieren von Zeichenfolgen  
 In der Regel sollten geordnete Zeichenfolgen, die auf der Benutzeroberfläche angezeigt werden, auf Grundlage der Kultur sortiert werden. In den meisten Fällen werden solche Zeichenfolgenvergleiche von .NET Framework implizit behandelt, wenn Sie eine Methode aufrufen, die Zeichenfolgen sortiert, wie z. B. <xref:System.Array.Sort%2A?displayProperty=fullName> oder <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=fullName>. Standardmäßig werden Zeichenfolgen anhand der Sortierkonventionen der aktuellen Kultur sortiert. Das folgende Beispiel veranschaulicht den Unterschied beim Sortieren eines Zeichenfolgenarrays mit den Konventionen der Kulturen Englisch \(USA\) und Schwedisch \(Schweden\).  
  
 [!code-csharp[Conceptual.Globalization#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/sort1.cs#14)]
 [!code-vb[Conceptual.Globalization#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/sort1.vb#14)]  
  
 Der kulturabhängige Zeichenfolgenvergleich wird durch das <xref:System.Globalization.CompareInfo>\-Objekt definiert, das von der <xref:System.Globalization.CultureInfo.CompareInfo%2A?displayProperty=fullName>\-Eigenschaft jeder Kultur zurückgegeben wird. Kulturabhängige Zeichenfolgenvergleiche mit den <xref:System.String.Compare%2A?displayProperty=fullName>\-Methodenüberladungen verwenden ebenfalls das <xref:System.Globalization.CompareInfo>\-Objekt.  
  
 .NET Framework verwendet Tabellen zum Durchführen von kulturabhängigen Sortierungen für Zeichenfolgendaten. Der Inhalt dieser Tabellen, die Daten zu Sortierungsgewichtungen und Zeichenfolgennormalisierung enthalten, wird durch die Version des Unicode\-Standards festgelegt, der von einer bestimmten Version von .NET Framework implementiert wird. Die folgende Tabelle enthält die Unicode\-Versionen, die von den angegebenen Versionen von .NET Framework implementiert werden. Beachten Sie, dass diese Liste der unterstützten Unicode\-Versionen lediglich für den Zeichenvergleich und die Sortierung gilt. Sie gilt nicht für die kategorische Klassifizierung von Unicode\-Zeichen. Weitere Informationen finden Sie im Abschnitt „Zeichenfolgen und Unicode\-Standard“ im Artikel <xref:System.String>.  
  
|.NET Framework\-Version|Betriebssystem|Unicode\-Version|  
|-----------------------------|--------------------|----------------------|  
|.NET Framework 2.0|Alle Betriebssysteme|Unicode 4.1|  
|.NET Framework 3.0|Alle Betriebssysteme|Unicode 4.1|  
|.NET Framework 3,5|Alle Betriebssysteme|Unicode 4.1|  
|.NET Framework 4|Alle Betriebssysteme|Unicode 5.0|  
|.NET Framework 4.5|[!INCLUDE[win7](../../../includes/win7-md.md)]|Unicode 5.0|  
|.NET Framework 4.5|[!INCLUDE[win8](../../../includes/win8-md.md)]|Unicode 6.0|  
  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] sind der Zeichenfolgenvergleich und die Sortierung vom Betriebssystem abhängig.[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] unter [!INCLUDE[win7](../../../includes/win7-md.md)] ruft Daten aus eigenen Tabellen ab, die Unicode 5.0 implementieren.[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] unter [!INCLUDE[win8](../../../includes/win8-md.md)] ruft Daten aus den Betriebssystemtabellen ab, die Unicode 6.0 implementieren. Wenn Sie kulturabhängige sortierte Daten serialisieren, können mit der <xref:System.Globalization.SortVersion>\-Klasse bestimmen, wann die serialisierten Daten sortiert werden müssen, damit sie mit .NET Framework und der Sortierreihenfolge des Betriebssystems konsistent sind. Ein Beispiel finden Sie im Thema zur <xref:System.Globalization.SortVersion>\-Klasse.  
  
 Wenn Ihre App umfangreiche kulturspezifische Sortierungen von Zeichenfolgendaten ausführt, können Sie Zeichenfolgen mit der <xref:System.Globalization.SortKey>\-Klasse vergleichen. Ein Sortierschlüssel spiegelt die kulturspezifischen Sortierungsgewichtungen wider, einschließlich alphabetischer, Groß\-\/Kleinschreibungs\- sowie diakritischer Gewichtungen einer bestimmten Zeichenfolge. Da Vergleiche mit Sortierschlüsseln binär sind, werden diese schneller ausgeführt als Vergleiche unter impliziter oder expliziter Verwendung eines <xref:System.Globalization.CompareInfo>\-Objekts. Sie erstellen einen kulturabhängigen Sortierschlüssel für eine bestimmte Zeichenfolge, indem Sie die Zeichenfolge an die <xref:System.Globalization.CompareInfo.GetSortKey%2A?displayProperty=fullName>\-Methode übergeben.  
  
 Das folgende Beispiel ähnelt dem vorherigen Beispiel. Anstatt jedoch die <xref:System.Array.Sort%28System.Array%29?displayProperty=fullName>\-Methode aufzurufen, die die <xref:System.Globalization.CompareInfo.Compare%2A?displayProperty=fullName>\-Methode implizit aufruft, wird eine <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName>\-Implementierung definiert, die Sortierschlüssel vergleicht, welche dann instanziiert und an die [Array.Sort\<T\>\(T\<xref:System.Array.Sort%60%601%28%60%600%5B%5D%2CSystem.Collections.Generic.IComparer%7B%60%600%7D%29?displayProperty=fullName>\-Methode übergeben werden.  
  
 [!code-csharp[Conceptual.Globalization#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/sortkey1.cs#15)]
 [!code-vb[Conceptual.Globalization#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/sortkey1.vb#15)]  
  
<a name="Strings_Concat"></a>   
### Zeichenfolgenverkettung vermeiden  
 Vermeiden Sie, soweit möglich, die Verwendung zusammengesetzter Zeichenfolgen, die zur Laufzeit aus verketteten Ausdrücken erstellt werden. Zusammengesetzte Zeichenfolgen sind schwer zu lokalisieren, da sie häufig eine grammatische Reihenfolge in der Originalsprache der App voraussetzen, die nicht für andere lokalisierte Sprachen gilt.  
  
<a name="DatesAndTimes"></a>   
## Arbeiten mit Datumsangaben und Zeiten  
 Wie Sie Datums\- und Uhrzeitwerte behandeln, ist davon abhängig, ob diese auf der Benutzeroberfläche angezeigt oder beibehalten werden. In diesem Abschnitt werden beide Nutzungsarten behandelt. Außerdem wird erläutert, wie Sie Zeitzonenunterschiede und arithmetische Operationen beim Arbeiten mit Daten\- und Uhrzeitwerten behandeln können.  
  
<a name="DatesAndTimes_Display"></a>   
### Anzeigen von Datums\- und Zeitangaben  
 Wenn Datumsangaben und Uhrzeiten auf der Benutzeroberfläche angezeigt werden, sollten Sie normalerweise die Formatierungskonventionen der Kultur des Benutzers verwenden, die durch die <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>\-Eigenschaft und das von der <xref:System.Globalization.DateTimeFormatInfo>\-Eigenschaft zurückgegebene `CultureInfo.CurrentCulture.DateTimeFormat`\-Objekt definiert wird. Die Formatierungskonventionen der aktuellen Kultur werden automatisch verwendet, wenn Sie ein Datum mit einer der folgenden Methoden formatieren:  
  
-   Die parameterlose <xref:System.DateTime.ToString?displayProperty=fullName>\-Methode  
  
-   Die <xref:System.DateTime.ToString%28System.String%29?displayProperty=fullName>\-Methode, die eine Formatzeichenfolge enthält  
  
-   Die parameterlose <xref:System.DateTimeOffset.ToString?displayProperty=fullName>\-Methode  
  
-   Die <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=fullName>\-Methode, die eine Formatzeichenfolge enthält  
  
-   Die Funktion der [kombinierten Formatierung](../../../docs/standard/base-types/composite-formatting.md) bei der Verwendung mit Datumsangaben  
  
 Im folgenden Beispiel werden Daten zum Sonnenaufgang und Sonnenuntergang für den 11. Oktober 2012 angezeigt. Die aktuelle Kultur wird zuerst auf Kroatisch \(Kroatien\) und dann auf Englisch \(Großbritannien\) festgelegt. In beiden Fällen werden die Datums\- und Uhrzeitangaben im entsprechenden Format für die jeweilige Kultur angezeigt.  
  
 [!code-csharp[Conceptual.Globalization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates1.cs#2)]
 [!code-vb[Conceptual.Globalization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates1.vb#2)]  
  
<a name="DatesAndTimes_Persist"></a>   
### Beibehalten von Datums\- und Zeitangaben  
 Sie sollten Datums\- und Uhrzeitangaben niemals in einem Format beibehalten, das je nach Kultur variieren kann. Dies ist ein häufiger Programmierfehler, der zu beschädigten Daten oder einer Laufzeitausnahme führt. Im folgenden Beispiel werden zwei Datumsangaben, der 9. Januar 2013 und der 18. August 2013, unter Verwendung der Formatierungskonventionen der Kultur Englisch \(USA\) als Zeichenfolgen serialisiert. Wenn die Daten mit den Konventionen der Kultur Englisch \(USA\) abgerufen und analysiert werden, können sie erfolgreich wiederhergestellt werden. Wenn sie jedoch mit den Konventionen der Kultur Englisch \(Großbritannien\) abgerufen und analysiert werden, wird das erste Datum fälschlicherweise als 1. September interpretiert, und das zweite kann nicht analysiert werden, da der Gregorianische Kalender keinen 18. Monat aufweist.  
  
 [!code-csharp[Conceptual.Globalization#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates2.cs#3)]
 [!code-vb[Conceptual.Globalization#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates2.vb#3)]  
  
 Sie können dieses Problem auf drei Arten vermeiden:  
  
-   Serialisieren Sie Datum und Uhrzeit im Binärformat anstatt als Zeichenfolge.  
  
-   Speichern und analysieren Sie die Zeichenfolgendarstellung von Datum und Uhrzeit, indem Sie eine benutzerdefinierte Formatzeichenfolge verwenden, die von der Kultur des Benutzers unabhängig ist.  
  
-   Speichern Sie die Zeichenfolge, indem Sie die Formatierungskonventionen der invarianten Kultur verwenden.  
  
 Der letzte Ansatz wird anhand des folgenden Beispiels veranschaulicht. Dabei werden die Formatierungskonventionen der invarianten Kultur verwendet, die von der statischen <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>\-Eigenschaft zurückgegeben wird.  
  
 [!code-csharp[Conceptual.Globalization#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates3.cs#4)]
 [!code-vb[Conceptual.Globalization#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates3.vb#4)]  
  
<a name="DatesAndTimes_TimeZones"></a>   
### Serialisierung und Unterstützung von Zeitzonen  
 Ein Datums\- und Uhrzeitwert kann über mehrere Interpretationen verfügen, von der allgemeinen Uhrzeit \("Die Läden öffnen am 2. Januar 2013 um 9:00 Uhr"\) bis zu einem bestimmten Zeitpunkt \("Geburtsdatum: 2. Januar 2013 6:32:00 Uhr"\). Wenn ein Zeitwert einen bestimmten Zeitpunkt darstellt und aus einem serialisierten Wert wiederhergestellt wird, sollten Sie sicherstellen, dass er den gleichen Zeitpunkt unabhängig vom geografischen Ort oder der Zeitzone des Benutzers repräsentiert.  
  
 Dieses Problem wird anhand des folgenden Beispiels veranschaulicht. Ein einzelner lokaler Datums\- und Uhrzeitwert wird als Zeichenfolge in drei [Standardformaten](../../../docs/standard/base-types/standard-date-and-time-format-strings.md) \("G" für generelles Datum, lange Zeit, "s" für sortierbares Datum\/Uhrzeit und "o" für Roundtrip\-Datum\/\-Uhrzeit\) sowie im Binärformat gespeichert.  
  
 [!code-csharp[Conceptual.Globalization#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates4.cs#10)]
 [!code-vb[Conceptual.Globalization#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates4.vb#10)]  
  
 Wenn die Daten auf einem System in der gleichen Zeitzone wiederhergestellt werden, in der sie auch serialisiert wurden, spiegeln die deserialisierten Datums\- und Uhrzeitwerte den ursprünglichen Wert wider, wie die Ausgabe zeigt:  
  
```  
  
'3/30/2013 6:00:00 PM' --> 3/30/2013 6:00:00 PM Unspecified  
'2013-03-30T18:00:00' --> 3/30/2013 6:00:00 PM Unspecified  
'2013-03-30T18:00:00.0000000-07:00' --> 3/30/2013 6:00:00 PM Local  
  
3/30/2013 6:00:00 PM Local  
  
```  
  
 Wenn Sie die Daten jedoch auf einem System in einer anderen Zeitzone wiederherstellen, behält nur der Datums\- und Uhrzeitwert, der mit der Standardformatzeichenfolge "o" \(Roundtrip\) formatiert wurde, die Zeitzoneninformationen bei und stellt daher den gleichen Zeitpunkt dar. Wenn die Datums\- und Uhrzeitdaten auf einem System in der Zeitzone Romanische Normalzeit wiederhergestellt werden, lautet die Ausgabe wie folgt:  
  
```  
  
'3/30/2013 6:00:00 PM' --> 3/30/2013 6:00:00 PM Unspecified  
'2013-03-30T18:00:00' --> 3/30/2013 6:00:00 PM Unspecified  
'2013-03-30T18:00:00.0000000-07:00' --> 3/31/2013 3:00:00 AM Local  
  
3/30/2013 6:00:00 PM Local  
  
```  
  
 Um einen Datums\- und Uhrzeitwert exakt widerzuspiegeln, der einen einzigen Zeitpunkt unabhängig von der Zeitzone des Systems darstellt, auf dem die Daten deserialisiert werden, können Sie einen der folgenden Schritte ausführen:  
  
-   Speichern Sie den Wert als Zeichenfolge, indem Sie die Standardformatzeichenfolge "o" \(Roundtrip\) verwenden. Deserialisieren Sie ihn anschließend auf dem Zielsystem.  
  
-   Konvertieren Sie ihn in UTC, und speichern Sie ihn als Zeichenfolge, indem Sie die Standardformatzeichenfolge "r" \(RFC1123 \) verwenden. Deserialisieren Sie ihn anschließend auf dem Zielsystem, und konvertieren Sie ihn in die Ortszeit.  
  
-   Konvertieren Sie ihn in UTC, und speichern Sie ihn als Zeichenfolge, indem Sie die Standardformatzeichenfolge "u" \(universell sortierbar\) verwenden. Deserialisieren Sie ihn anschließend auf dem Zielsystem, und konvertieren Sie ihn in die Ortszeit.  
  
-   Konvertieren Sie ihn in UTC, und speichern Sie ihn im Binärformat. Deserialisieren Sie ihn anschließend auf dem Zielsystem, und konvertieren Sie ihn in die Ortszeit.  
  
 Das folgende Beispiel veranschaulicht die einzelnen Techniken:  
  
 [!code-csharp[Conceptual.Globalization#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates8.cs#11)]
 [!code-vb[Conceptual.Globalization#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates8.vb#11)]  
  
 Wenn die Daten auf einem System in der Zeitzone Pazifik Normalzeit serialisiert und auf einem System in der Zeitzone Romanische Normalzeit deserialisiert werden, lautet die Ausgabe wie folgt:  
  
```  
  
'2013-03-30T18:00:00.0000000-07:00' --> 3/31/2013 3:00:00 AM Local  
'Sun, 31 Mar 2013 01:00:00 GMT' --> 3/31/2013 3:00:00 AM Local  
'2013-03-31 01:00:00Z' --> 3/31/2013 3:00:00 AM Local  
  
3/31/2013 3:00:00 AM Local  
  
```  
  
 Weitere Informationen finden Sie unter [Konvertieren von Uhrzeiten zwischen Zeitzonen](../../../docs/standard/datetime/converting-between-time-zones.md).  
  
<a name="DatesAndTimes_Arithmetic"></a>   
### Ausführen von arithmetischen Datums\- und Uhrzeitoperationen  
 Der <xref:System.DateTime>\- und der <xref:System.DateTimeOffset>\-Typ unterstützen arithmetische Operationen. Sie können die Differenz zwischen zwei Datumswerten berechnen oder bestimmte Zeitintervalle zu einem Datumswert addieren oder davon subtrahieren. Jedoch werden bei arithmetischen Operationen für Datums\- und Uhrzeitwerte keine Zeitzonen oder Regeln zur Anpassung der Zeitzone berücksichtigt. Daher kann eine Datums\- und Uhrzeitarithmetik für Werte, die Zeitpunkte darstellen, fehlerhafte Ergebnisse zurückgeben.  
  
 Beispielsweise erfolgt die Umstellung von der pazifischen Normalzeit auf die pazifische Sommerzeit am zweiten Sonntag im März. Im Jahr 2013 ist dies der 10. März. Wenn Sie, wie im nachfolgenden Beispiel, auf einem System in der Zeitzone „Pazifik Normalzeit“ das Datum und die Uhrzeit für einen Zeitpunkt 48 Stunden nach dem 9. März 2013, 10:30 Uhr berechnen, wird als Ergebnis 11. März 2013, 10:30 Uhr angegeben, d.h. die Zeitumstellung wird nicht berücksichtigt.  
  
 [!code-csharp[Conceptual.Globalization#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates5.cs#8)]
 [!code-vb[Conceptual.Globalization#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates5.vb#8)]  
  
 Um sicherzustellen, dass eine arithmetische Operation für Datums\- und Uhrzeitwerte akkurate Ergebnisse liefert, führen Sie folgende Schritte aus:  
  
1.  Konvertieren Sie die Zeit in der Quellzeitzone in UTC.  
  
2.  Führen Sie die arithmetische Operation aus.  
  
3.  Wenn das Ergebnis ein Datums\- und Uhrzeitwert ist, konvertieren Sie diesen von UTC in die Uhrzeit der Quellzeitzone.  
  
 Das folgende Beispiel gleicht dem vorhergehenden bis auf die folgenden drei Schritte, um zum 9. März 2013 um 10:30 Uhr korrekt 48 Stunden zu addieren.  
  
 [!code-csharp[Conceptual.Globalization#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates6.cs#9)]
 [!code-vb[Conceptual.Globalization#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates6.vb#9)]  
  
 Weitere Informationen finden Sie unter [Durchführen arithmetischer Datums\- und Uhrzeitoperationen](../../../docs/standard/datetime/performing-arithmetic-operations.md).  
  
### Verwenden kulturabhängiger Namen für Datumselemente  
 Ihre App muss möglicherweise den Namen des Monats oder des Wochentags anzeigen. Hierzu wird normalerweise ein Code wie der folgende verwendet.  
  
 [!code-csharp[Conceptual.Globalization#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/monthname1.cs#19)]
 [!code-vb[Conceptual.Globalization#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/monthname1.vb#19)]  
  
 Allerdings gibt dieser Code immer die Namen der Wochentage auf Englisch zurück. Code, der den Namen des Monats extrahiert, ist oft noch weniger flexibel. Oft wird von einem Zwölf\-Monats\-Kalender mit Namen von Monaten in einer bestimmten Sprache ausgegangen.  
  
 Durch [benutzerdefinierte Formatzeichenfolgen für Datum und Uhrzeit](../../../docs/standard/base-types/custom-date-and-time-format-strings.md) oder die Eigenschaften des <xref:System.Globalization.DateTimeFormatInfo>\-Objekts können Zeichenfolgen, die die Namen von Wochentagen oder Monaten in der Kultur des Benutzers darstellen, leicht extrahiert werden, wie im folgenden Beispiel veranschaulicht wird. Die aktuelle Kultur wird in Französisch \(Frankreich\) geändert, und die Namen des Wochentags und des Monats werden für den 1. Juli 2013 angezeigt.  
  
 [!code-csharp[Conceptual.Globalization#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/monthname2.cs#20)]
 [!code-vb[Conceptual.Globalization#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/monthname2.vb#20)]  
  
<a name="Numbers"></a>   
## Arbeiten mit numerischen Werte  
 Die Behandlung von Zahlen ist davon abhängig, ob diese auf der Benutzeroberfläche angezeigt oder beibehalten werden. In diesem Abschnitt werden beide Nutzungsarten behandelt.  
  
> [!NOTE]
>  Bei Analyse\- und Formatierungsvorgängen erkennt .NET Framework nur die lateinischen Standardzeichen 0 bis 9 \(U\+0030 bis U\+0039\) als numerische Zeichen.  
  
<a name="Numbers_Display"></a>   
### Anzeigen von numerischen Werten  
 Wenn Zahlen auf der Benutzeroberfläche angezeigt werden, sollten Sie normalerweise die Formatierungskonventionen der Kultur des Benutzers verwenden, die durch die <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>\-Eigenschaft und das von der <xref:System.Globalization.NumberFormatInfo>\-Eigenschaft zurückgegebene `CultureInfo.CurrentCulture.NumberFormat`\-Objekt definiert wird. Die Formatierungskonventionen der aktuellen Kultur werden automatisch verwendet, wenn Sie ein Datum mit einer der folgenden Methoden formatieren:  
  
-   Die parameterlose `ToString`\-Methode eines die oft ausgegebene Befehlszeilen  numerischen Typs  
  
-   Die `ToString(String)`\-Methode eines die oft ausgegebene Befehlszeilen  numerischen Typs, der eine Formatzeichenfolge als Argument enthält  
  
-   Die Funktion der [kombinierten Formatierung](../../../docs/standard/base-types/composite-formatting.md) bei der Verwendung mit numerischen Werten  
  
 Im folgenden Beispiel wird die Durchschnittstemperatur pro Monat in Paris, Frankreich, angezeigt. Zuerst wird die aktuelle Kultur auf Französisch \(Frankreich\) festgelegt, bevor die Daten anzeigt werden. Anschließend wird die Kultur auf Englisch \(USA\) festgelegt. In beiden Fällen werden die Monatsnamen und Temperaturen im entsprechenden Format für die jeweilige Kultur angezeigt. Beachten Sie, dass die zwei Kulturen verschiedene Dezimaltrennzeichen beim Temperaturwert verwenden. Beachten Sie außerdem, dass im Beispiel die benutzerdefinierte Datums\- und Uhrzeitformatzeichenfolge "MMMM" verwendet wird, um den vollständigen Monatsnamen anzuzeigen, und dass in der Ergebniszeichenfolge ausreichend Platz für den Monatsnamen zugeordnet wird, indem die Länge des längsten Monatsnamens im <xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A?displayProperty=fullName>\-Array ermittelt wird.  
  
 [!code-csharp[Conceptual.Globalization#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/numbers1.cs#5)]
 [!code-vb[Conceptual.Globalization#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/numbers1.vb#5)]  
  
<a name="Numbers_Persist"></a>   
### Beibehalten von numerischen Werten  
 Numerische Daten sollten niemals in einem kulturabhängigen Format beibehalten werden. Dies ist ein häufiger Programmierfehler, der zu beschädigten Daten oder einer Laufzeitausnahme führt. Im folgenden Beispiel werden zehn zufällige Gleitkommazahlen generiert und anschließend unter Verwendung der Formatierungskonventionen der Kultur Englisch \(USA\) als Zeichenfolgen serialisiert. Wenn die Daten mit den Konventionen der Kultur Englisch \(USA\) abgerufen und analysiert werden, können sie erfolgreich wiederhergestellt werden. Wenn jedoch versucht wird, sie mit den Konventionen der Kultur Französisch \(Frankreich\) abzurufen und zu analysieren, kann keine der Zahlen analysiert werden, da die Kulturen unterschiedliche Dezimaltrennzeichen verwenden.  
  
 [!code-csharp[Conceptual.Globalization#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/numbers2.cs#6)]
 [!code-vb[Conceptual.Globalization#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/numbers2.vb#6)]  
  
 Um dieses Problem zu vermeiden, können Sie eine der folgenden Methoden verwenden:  
  
-   Speichern und analysieren Sie die Zeichenfolgendarstellung der Zahl, indem Sie eine benutzerdefinierte Formatzeichenfolge verwenden, die von der Kultur des Benutzers unabhängig ist.  
  
-   Speichern Sie die Zahl als Zeichenfolge, indem Sie die Formatierungskonventionen der invarianten Kultur verwenden, die von der <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>\-Eigenschaft zurückgegeben wird.  
  
-   Serialisieren Sie die Zahl im binären Format anstatt im Zeichenfolgenformat.  
  
 Der letzte Ansatz wird anhand des folgenden Beispiels veranschaulicht. Das Array aus <xref:System.Double>\-Werten wird serialisiert. Die Werte werden anschließend deserialisiert und mit den Formatierungskonventionen der Kulturen Englisch \(USA\) und Französisch \(Frankreich\) angezeigt.  
  
 [!code-csharp[Conceptual.Globalization#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/numbers3.cs#7)]
 [!code-vb[Conceptual.Globalization#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/numbers3.vb#7)]  
  
 Das Serialisieren von Währungen ist ein Sonderfall. Da ein Währungswert von der Währungseinheit abhängig ist, in der er ausgedrückt wird, ist es wenig sinnvoll, ihn als unabhängigen numerischen Wert zu behandeln. Wenn Sie jedoch einen Währungswert als formatierte Zeichenfolge speichern, die ein Währungssymbol enthält, kann er nicht auf einem System deserialisiert werden, dessen Standardkultur ein anderes Währungssymbol verwendet, wie im folgenden Beispiel gezeigt wird.  
  
 [!code-csharp[Conceptual.Globalization#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/currency1.cs#16)]
 [!code-vb[Conceptual.Globalization#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/currency1.vb#16)]  
  
 Stattdessen sollten Sie den numerischen Wert zusammen mit kulturellen Informationen wie dem Namen der Kultur serialisieren, sodass der Wert und sein Währungssymbol unabhängig von der aktuellen Kultur deserialisiert werden können. Im folgenden Beispiel wird dies erreicht, indem eine `CurrencyValue`\-Struktur mit zwei Membern definiert wird: der <xref:System.Decimal>\-Wert und der Name der Kultur, der der Wert angehört.  
  
 [!code-csharp[Conceptual.Globalization#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/currency2.cs#17)]
 [!code-vb[Conceptual.Globalization#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/currency2.vb#17)]  
  
<a name="Cultures"></a>   
## Arbeiten mit kulturspezifischen Einstellungen  
 In .NET Framework stellt die <xref:System.Globalization.CultureInfo>\-Klasse eine bestimmte Kultur oder Region dar. Einige zugehörige Eigenschaften geben Objekte zurück, die spezielle Informationen über Aspekte einer Kultur bereitstellen:  
  
-   Die <xref:System.Globalization.CultureInfo.CompareInfo%2A?displayProperty=fullName>\-Eigenschaft gibt ein <xref:System.Globalization.CompareInfo>\-Objekt zurück, das Informationen darüber enthält, wie in der Kultur Zeichenfolgen verglichen und sortiert werden.  
  
-   Die <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName>\-Eigenschaft gibt ein <xref:System.Globalization.DateTimeFormatInfo>\-Objekt zurück, das kulturspezifische Informationen bereitstellt, die beim Formatieren von Datums\- und Uhrzeitdaten verwendet werden.  
  
-   Die <xref:System.Globalization.CultureInfo.NumberFormat%2A?displayProperty=fullName>\-Eigenschaft gibt ein <xref:System.Globalization.NumberFormatInfo>\-Objekt zurück, das kulturspezifische Informationen bereitstellt, die beim Formatieren von numerischen Daten verwendet werden.  
  
-   Die <xref:System.Globalization.CultureInfo.TextInfo%2A?displayProperty=fullName>\-Eigenschaft gibt ein <xref:System.Globalization.TextInfo>\-Objekt zurück, das Informationen zum Schriftsystem der Kultur bereitstellt.  
  
 Treffen Sie generell keine Annahmen über die Werte von bestimmten <xref:System.Globalization.CultureInfo>\-Eigenschaften und deren verknüpfte Objekte. Stattdessen sollten Sie aus folgenden Gründen davon ausgehen, dass kulturspezifische Daten Änderungen unterliegen:  
  
-   Einzelne Eigenschaftswerte unterliegen im Laufe der Zeit Änderungen und Revisionen, da Daten korrigiert werden, bessere Daten verfügbar werden oder die kulturspezifischen Konventionen sich ändern.  
  
-   Einzelne Eigenschaftswerte können zwischen Versionen von .NET Framework oder Betriebssystemversionen variieren.  
  
-   .NET Framework unterstützt Ersatzkulturen. Dadurch ist es möglich, eine neue benutzerdefinierte Kultur zu definieren, die bestehende Standardkulturen ergänzt oder vollständig ersetzt.  
  
-   Der Benutzer kann kulturspezifische Einstellungen über die App **Region und Sprache** in der Systemsteuerung anpassen. Wenn Sie ein <xref:System.Globalization.CultureInfo>\-Objekt instanziieren, können Sie festlegen, ob es diese Benutzeranpassungen widergespiegelt, indem Sie den <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName>\-Konstruktor aufrufen. In der Regel sollten Sie bei Endbenutzer\-Apps die Benutzereinstellungen berücksichtigen, sodass der Benutzer die Daten in einem Format angezeigt bekommt, das er erwartet.  
  
## Siehe auch  
 [Globalisierung und Lokalisierung](../../../docs/standard/globalization-localization/index.md)   
 [Empfohlene Vorgehensweisen für die Verwendung von Zeichenfolgen](../../../docs/standard/base-types/best-practices-strings.md)