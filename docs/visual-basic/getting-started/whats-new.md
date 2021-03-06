---
title: Neues in Visual Basic
ms.date: 2017-04-27
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- VB.StartPage.WhatsNew
dev_langs:
- VB
helpviewer_keywords:
- new features, Visual Basic
- what's new [Visual Basic]
- Visual Basic, what's new
ms.assetid: d7e97396-7f42-4873-a81c-4ebcc4b6ca02
caps.latest.revision: 145
author: rpetrusha
ms.author: ronpet
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0a9379d5dd2d1c6b3ed6820e350c19fb346ac84c
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="whats-new-for-visual-basic"></a>Neues in Visual Basic

In diesem Thema sind die Namen der wichtigsten Funktionen für jede Version von Visual Basic mit ausführlichen Beschreibungen der neuen und verbesserten Funktionen in der neuesten Version der Sprache aufgelistet.
  
## <a name="current-version"></a>Aktuelle Version

Visual Basic/Visual Studio .NET 2017   
Informationen zu neuen Funktionen finden Sie unter [Visual Basic 2017](#visual-basic-2017)

## <a name="previous-versions"></a>Frühere Versionen

Visual Basic / Visual Studio .NET 2015   
Informationen zu neuen Funktionen finden Sie unter [Visual Basic 14](#visual-basic-14)

Visual Basic / Visual Studio .NET 2013  
Technologievorschau von .NET Compiler Platform („Roslyn“)

Visual Basic / Visual Studio .NET 2012   
Die Schlüsselwörter `Async` und `await`, Iteratoren, Aufruferinformationsattribute

Visual Basic, Visual Studio .NET 2010   
Automatisch implementierte Eigenschaften, Auflistungsinitialisierer, implizite Zeilenfortsetzung, dynamische, generische Ko-/Kontravarianz, Zugriff auf globalen Namespace

Visual Basic / Visual Studio .NET 2008   
Language Integrated Query (LINQ), XML-Literale, lokaler Typrückschluss, Objektinitialisierer, anonyme Typen, Erweiterungsmethoden, lokaler `var`-Typrückschluss, Lambda-Ausdrücke, `if`-Operator, partielle Methoden, auf NULL festlegbare Werttypen  

Visual Basic / Visual Studio .NET 2005   
Der `My`-Typ und Hilfstypen (Zugriff auf App, Computer, Dateisystem, Netzwerk)

Visual Basic / Visual Studio .NET 2003   
Bitschiebeoperatoren, Deklaration von Schleifenvariablen

Visual Basic / Visual Studio .NET 2002   
Die erste Version von Visual Basic .NET

## <a name="visual-basic-2017"></a>Visual Basic 2017

[Tupel](../programming-guide/language-features/data-types/tuples.md)

Tupel sind einfache Datenstrukturen, die am häufigsten für die Rückgabe von mehreren Werten aus einem einzelnen Methodenaufruf verwendet werden. Für gewöhnlich müssen Sie eine der folgenden Aktionen durchführen, um mehrere Werte aus einer Methode zurückzugeben:

- die Definition eines benutzerdefinierten Typs (eine `Class` oder eine `Structure`). Dabei handelt es sich um eine schwierige Lösung.

- die Definition von mindestens einem `ByRef`-Parameter zusätzlich zur Rückgabe eines Werts aus der Methode
 
Die Unterstützung für Tupel von Visual Basic erlaubt Ihnen die schnelle Definition von Tupeln, die optionale Zuweisung von semantischen Namen an deren Werte und das schnelle Abrufen dieser Werte. In folgendem Beispiel wird ein Aufruf der <xref:System.Int32.TryParse%2A>-Methode umschlossen und ein Tupel zurückgegeben.

[!code-vb[Tuple](../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#2)]

Anschließend können Sie die Methode aufrufen und das zurückgegebene Tupel mit Code wie dem folgenden behandeln.

[!code-vb[ReturnTuple](../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#3)] 

**Binäre Literale und Zahlentrennzeichen**

Sie können ein binäres Literal definieren, indem Sie die Präfixe `&B` oder `&b` verwenden. Zusätzlich können Sie einen Unterstrich (`_`) als Zahlentrennzeichen verwenden, um die Lesbarkeit zu verbessern. In folgendem Beispiel werden Funktionen sowohl verwendet, um einen `Byte`-Wert zuzuweisen, als auch um ihn als Dezimal-, Hexadezimal- und binäre Zahl anzuzeigen.

[!code-vb[Binär](../../../samples/snippets/visualbasic/getting-started/bin-example.vb#1)]

Weitere Informationen finden Sie im Abschnitt „Zuweisung von Literalen“ der Datentypen [Byte](../language-reference/data-types/byte-data-type.md#literal-assignments), [Integer](../language-reference/data-types/integer-data-type.md#literal-assignments), [Long](../language-reference/data-types/long-data-type.md#literal-assignments), [Short](../language-reference/data-types/short-data-type.md#literal-assignments), [SByte](../language-reference/data-types/sbyte-data-type.md#literal-assignments), [UInteger](../language-reference/data-types/uinteger-data-type.md#literal-assignments), [ULong](../language-reference/data-types/ulong-data-type.md#literal-assignments) und [UShort](../language-reference/data-types/ushort-data-type.md#literal-assignments).

**Unterstützung für Verweisrückgabewerte von C#**

Ab C# 7 unterstützt C# Verweisrückgabewerte. Das heißt, wenn die aufrufende Methode einen von einem Verweis zurückgegebenen Wert erhält, kann sie den Wert des Verweises ändern. In Visual Basic können Sie keine Methoden mit Verweisrückgabewerten erstellen. Allerdings können Sie Verweisrückgabewerte verarbeiten und modifizieren.

Die folgende in C# geschriebene `Sentence`-Klasse enthält z.B eine `FindNext`-Methode, die nach dem nächsten Wort in einer Sequenz sucht, die mit einer angegebenen Teilzeichenfolge beginnt. Die Zeichenfolge wird als Verweisrückgabewert zurückgegeben, und eine vom Verweis an die Methode übergebene `Boolean`-Variable gibt an, ob die Suche Erfolg hatte. Das bedeutet, dass der Aufrufer nicht nur den Rückgabewert lesen sondern auch modifizieren kann. Diese Modifizierung wird in der `Sentence`-Klasse widergespiegelt.

[!code-csharp[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-returns.cs)]

Sie können das in der Sequenz gefundene Wort in seiner einfachsten Form mit Code wie dem folgenden modifizieren. Beachten Sie, dass Sie nicht der Methode sondern dem Ausdruck, den die Methode zurückgibt, einen Wert zuweisen. Dabei handelt es sich um den Verweisrückgabewert.

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-return.vb#1)]

Bei diesem Code besteht jedoch das Problem, dass die Methode das erste Wort zurückgibt, wenn keine Übereinstimmung gefunden wurde. Da in dem Beispiel nicht der Wert des `Boolean`-Arguments untersucht wird, um festzustellen, ob eine Übereinstimmung gefunden wurde, wird das erste Wort modifiziert, wenn es keine Übereinstimmung gibt. In folgendem Beispiel wird dies korrigiert, indem das erste Wort durch sich selbst ersetzt wird, wenn es keine Übereinstimmung gibt.

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-return.vb#2)]

Eine sinnvollere Lösung ist das Verwenden einer Hilfsmethode, an die der Verweisrückgabewert vom Verweis übergeben wird. Die Hilfsmethode kann dann das an sie vom Verweis übergebene Argument modifizieren. In folgendem Beispiel wird dies getan.

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-return-helper.vb#1)]

Weitere Informationen finden Sie unter [Verweisrückgabewerte](../programming-guide/language-features/procedures/ref-return-values.md).

## <a name="visual-basic-14"></a>Visual Basic 14

[nameof](../../csharp/language-reference/keywords/nameof.md)  
 Sie können den nicht qualifizierten Zeichenfolgennamen eines Typs oder Members zur Verwendung in einer Fehlermeldung ohne Hartcodierung einer Zeichenfolge abrufen.  Dadurch bleibt der Code bei der Umgestaltung korrekt.  Diese Funktion eignet sich auch zum Einbinden von MVC-Links (Model-View-Controller) und das Auslösen von Ereignissen durch geänderte Eigenschaften.  
  
[Zeichenfolgeninterpolation](../../csharp/language-reference/keywords/interpolated-strings.md)  
 Sie können Ausdrücke für die Zeichenfolgeninterpolierung zum Erstellen von Zeichenfolgen verwenden.  Ein Ausdruck für eine interpolierte Zeichenfolge sieht wie eine Vorlagenzeichenfolge aus, die Ausdrücke enthält.  Eine interpolierte Zeichenfolge ist in Bezug auf die Argumente leichter zu verstehen als eine [Zusammengesetzte Formatierung](../../standard/base-types/composite-format.md).  
  
[Memberzugriff und Indizierung mit NULL-Bedingung](../../csharp/language-reference/operators/null-conditional-operators.md)  
Sie können eine Prüfung auf null auf sehr einfache syntaktische Weise vornehmen, bevor Sie eine Operation für den Memberzugriff (`?.`) oder die Indizierung (`?[]`) ausführen.  Mithilfe dieser Operatoren müssen Sie für die Prüfung auf null weniger Code schreiben, insbesondere beim tieferen Eindringen in Datenstrukturen.  Wenn der linke Operand oder Objektverweis NULL ist, geben die Operationen NULL zurück.  
  
[Multi-line String Literals (Mehrzeilige Zeichenfolgenliterale)](../../visual-basic/programming-guide/language-features/strings/string-basics.md)  
 Zeichenfolgenliterale können Zeilenumbruchsequenzen enthalten.  Sie müssen nicht mehr die alte Problemumgehung mit `<xml><![CDATA[...text with newlines...]]></xml>.Value` verwenden.  
  
Kommentare  
Sie können Kommentare nach impliziten Zeilenfortsetzungen, innerhalb von Initialisierungsausdrücken und zwischen LINQ-Ausdrücken einfügen.  
  
 Intelligentere Auflösung vollqualifizierter Namen  
 Bei Code wie `Threading.Thread.Sleep(1000)` suchte Visual Basic bisher den Namespace "Threading", stellte fest, dass dieser mit "System.Threading" und "System.Windows.Threading" mehrdeutig war und meldete dann einen Fehler.  Nun berücksichtigt Visual Basic die beiden möglichen Namespaces gemeinsam.  Wenn Sie die Vervollständigungsliste anzeigen, listet der Visual Studio-Editor Member beider Typen in der Vervollständigungsliste auf.  
  
 Datumsliterale mit Jahresangabe am Anfang  
 Datumsliterale im Format jjjj-mm-tt sind möglich, z. B. `#2015-03-17 16:10 PM#`.  
  
 Schreibgeschützte Schnittstelleneigenschaften  
 Sie können mithilfe einer Readwrite-Eigenschaft schreibgeschützte Schnittstelleneigenschaften implementieren.  Die Schnittstelle garantiert Mindestfunktionalität und hindert eine Implementierungsklasse nicht daran, die Festlegung der Eigenschaft zuzulassen.  
  
 [TypeOf \<expr> IsNot \<type>](../../visual-basic/language-reference/operators/typeof-operator.md)  
 Zur besseren Lesbarkeit des Codes können Sie nun `TypeOf` mit `IsNot` verwenden.  
  
 [#Disable Warning\<<ID> und #Enable Warning \<<ID>](../../visual-basic/language-reference/directives/directives.md)  
 Sie können bestimmte Warnungen für Bereiche innerhalb einer Quelldatei deaktivieren und aktivieren.  
  
 Verbesserungen bei XML-Dokumentationskommentaren  
 Beim Schreiben von Dokumentationskommentaren steht intelligente Editor- und Buildunterstützung zum Überprüfen von Parameternamen, ordnungsgemäßer Handhabung von `crefs` (Generika, Operatoren usw.), Farben und Umgestaltung bereit.  
  
 [Partial Module and Interface Definitions (Partielle Modul- und Schnittstellendefinitionen)](../../visual-basic/language-reference/modifiers/partial.md)  
 Zusätzlich zu Klassen und Strukturen können Sie partielle Module und Schnittstellen deklarieren.  
  
 [Partial Module and Interface Definitions (#Region-Direktiven in Methodentexten)](../../visual-basic/language-reference/directives/region-directive.md)  
 Sie können die Begrenzer #Region...#End Region an einer beliebigen Stelle in einer Datei, innerhalb von Funktionen und sogar Funktionsrümpfe übergreifend einfügen.  
  
 [Overrides Definitions are Implicitly Overloads (Überschreibungsdefinitionen sind implizite Überladungen)](../../visual-basic/language-reference/modifiers/overrides.md)  
 Wenn Sie den `Overrides`-Modifizierer zu einer Definition hinzufügen, fügt der Compiler implizit `Overloads` hinzu, sodass Sie in allgemeinen Fällen weniger Code eingeben können.  
  
 CObj in Attributargumenten zulässig  
 Der Compiler gab gewöhnlich eine Fehlermeldung aus, dass CObj(...) bei Verwendung in Attributkonstruktionen keine Konstante war.  
  
 Deklarieren und Verwenden mehrdeutiger Methoden von unterschiedlichen Schnittstellen  
 Zuvor führte der folgende Code zu Fehlern, die Sie daran hinderten, `IMock` zu deklarieren oder `GetDetails` aufzurufen (wenn diese in C# deklariert waren):  
  
```vb  
Interface ICustomer  
  Sub GetDetails(x As Integer)  
End Interface  
  
Interface ITime  
  Sub GetDetails(x As String)  
End Interface  
  
Interface IMock : Inherits ICustomer, ITime  
  Overloads Sub GetDetails(x As Char)  
End Interface  
  
Interface IMock2 : Inherits ICustomer, ITime  
End Interface  
```  
  
 Nun verwendet der Compiler normale Regeln zur Überladungsauflösung, um die am besten geeignete `GetDetails`-Methode zum Aufrufen auszuwählen, und Sie können Schnittstellenbeziehungen in Visual Basic deklarieren, wie sie im Beispiel gezeigt sind.  
  
## <a name="see-also"></a>Siehe auch  
 [Neues in Visual Studio 2017](/visualstudio/ide/whats-new-in-visual-studio)

