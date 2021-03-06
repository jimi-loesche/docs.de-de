---
title: "Beobachterentwurfsmuster | Microsoft Docs"
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
  - "IObservable(Of T)-Schnittstelle"
  - "IObservable<T>-Schnittstelle"
  - "IObserver(Of T)-Schnittstelle"
  - "IObserver<T>-Schnittstelle"
  - "Beobachterentwurfsmuster [.NET Framework]"
ms.assetid: 3680171f-f522-453c-aa4a-54f755a78f88
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Beobachterentwurfsmuster
Mit dem Entwurfsmuster "Beobachter" kann sich ein Abonnent bei einem Anbieter registrieren und Benachrichtigungen von diesem empfangen.  Es ist für jedes Szenario geeignet, das pushbasierte Benachrichtigungen erfordert.  Das Muster definiert einen *Anbieter* \(auch als *Antragssteller* oder *Observable* bezeichnet\) und keinen, einen oder mehrere *Beobachter*.  Beobachter registrieren sich beim Anbieter, und sobald eine vordefinierte Bedingung, ein Ereignis oder eine Statusänderung stattfindet, benachrichtigt der Anbieter automatisch alle Beobachter, indem er eine ihrer Methoden aufruft.  In diesem Methodenaufruf kann der Anbieter den Beobachtern auch aktuelle Statusinformationen bereitstellen.  In .NET Framework wird das Entwurfsmuster "Beobachter" angewendet, indem die generischen Schnittstellen <xref:System.IObservable%601?displayProperty=fullName> und <xref:System.IObserver%601?displayProperty=fullName> implementiert werden.  Der generische Typparameter stellt den Typ dar, der Benachrichtigungsinformationen bereitstellt.  
  
## Anwenden des Musters  
 Das Entwurfsmuster "Beobachter" ist für verteilte pushbasierte Benachrichtigungen geeignet, da es eine saubere Trennung zwischen zwei verschiedenen Komponenten bzw. Anwendungsebenen erlaubt, z. B. zwischen einer Datenquellenebene \(Geschäftslogik\) und einer Benutzeroberflächenebene \(Anzeige\).  Das Muster kann immer dann implementiert werden, wenn ein Anbieter Rückrufe verwendet, um seinen Clients aktuelle Informationen bereitzustellen.  
  
 Für eine Implementierung des Musters wird Folgendes benötigt:  
  
-   Ein Anbieter oder Antragsteller, der das Objekt darstellt, das Benachrichtigungen an die Beobachter sendet.  Ein Anbieter ist eine Klasse oder eine Struktur, die die <xref:System.IObservable%601>\-Schnittstelle implementiert.  Der Anbieter muss eine einzelne <xref:System.IObservable%601.Subscribe%2A?displayProperty=fullName>\-Methode implementieren, die von Beobachtern aufgerufen wird, die Benachrichtigungen vom Anbieter erhalten möchten.  
  
-   Ein Beobachter, bei dem es sich um ein Objekt handelt, das Benachrichtigungen von einem Anbieter empfängt.  Ein Beobachter ist eine Klasse oder eine Struktur, die die <xref:System.IObserver%601>\-Schnittstelle implementiert.  Der Beobachter muss drei Methoden implementieren, die alle vom Anbieter aufgerufen werden:  
  
    -   <xref:System.IObserver%601.OnNext%2A?displayProperty=fullName>, die dem Beobachter neue oder aktuelle Informationen bereitstellt.  
  
    -   <xref:System.IObserver%601.OnError%2A?displayProperty=fullName>, die den Beobachter informiert, dass ein Fehler aufgetreten ist.  
  
    -   <xref:System.IObserver%601.OnCompleted%2A?displayProperty=fullName>, die angibt, dass der Anbieter das Senden von Benachrichtigungen abgeschlossen hat.  
  
-   Ein Mechanismus, mit dem der Anbieter Beobachter verwalten kann.  In der Regel verwendet der Anbieter ein Containerobjekt, z. B. ein <xref:System.Collections.Generic.List%601?displayProperty=fullName>\-Objekt, um Verweise auf die <xref:System.IObserver%601>\-Implementierungen zu speichern, die Benachrichtigungen abonniert haben.  Durch das Verwenden eines Speichercontainers zu diesem Zweck kann der Anbieter eine beliebige Anzahl von Beobachtern behandeln.  Die Reihenfolge, in der Beobachter Benachrichtigungen empfangen, ist nicht definiert. Der Anbieter kann die Methode zum Bestimmen der Reihenfolge frei wählen.  
  
-   Eine <xref:System.IDisposable>\-Implementierung, die es dem Anbieter ermöglicht, Beobachter zu entfernen, wenn die Benachrichtigungen abgeschlossen wurden.  Beobachter erhalten einen Verweis auf die <xref:System.IDisposable>\-Implementierung der <xref:System.IObservable%601.Subscribe%2A>\-Methode, sodass sie die <xref:System.IDisposable.Dispose%2A?displayProperty=fullName>\-Methode ebenfalls aufrufen können, um das Abonnement zu kündigen, bevor der Anbieter das Senden von Benachrichtigungen abgeschlossen hat.  
  
-   Ein Objekt, das die Daten enthält, die vom Anbieter an die Beobachter gesendet werden.  Der Typ des Objekts entspricht dem generischen Typparameter der Schnittstellen <xref:System.IObservable%601> und <xref:System.IObserver%601>.  Obwohl dieses Objekt vom selben Typ sein kann wie die <xref:System.IObservable%601>\-Implementierung, handelt es sich in den meisten Fällen um einen separaten Typ.  
  
> [!NOTE]
>  Zusätzlich zum Implementieren des Entwurfsmusters "Beobachter" sind Sie ggf. an einer ausführlichen Untersuchung von Bibliotheken interessiert, die mithilfe der Schnittstellen <xref:System.IObservable%601> und <xref:System.IObserver%601> erstellt werden.  Beispielsweise bestehen [Reagierende Erweiterungen für .NET \(Rx\)](http://go.microsoft.com/fwlink/?LinkId=186345) aus einem Satz von Erweiterungsmethoden und LINQ\-Standardsequenzoperatoren, um die asynchrone Programmierung zu unterstützen.  
  
## Implementieren des Musters  
 Im folgenden Beispiel wird das Entwurfsmuster "Beobachter" verwendet, um ein Informationssystem für die Flughafengepäckausgabe zu implementieren.  Eine `BaggageInfo`\-Klasse stellt Informationen über ankommende Flüge und über die Laufbänder bereit, von denen das Gepäck der einzelnen Flüge abgeholt werden kann.  Dies wird im folgenden Beispiel gezeigt.  
  
 [!code-csharp[Conceptual.ObserverDesignPattern#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/provider.cs#1)]
 [!code-vb[Conceptual.ObserverDesignPattern#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/provider.vb#1)]  
  
 Eine `BaggageHandler`\-Klasse ist für den Empfang von Informationen über ankommende Flüge und die Gepäckausgabebänder verantwortlich.  Intern werden zwei Auflistungen verwaltet:  
  
-   `observers` \- Eine Auflistung der Clients, die aktualisierte Informationen erhalten.  
  
-   `flights` \- Eine Auflistung der Flüge und zugewiesenen Laufbänder.  
  
 Beide Auflistungen werden von generischen <xref:System.Collections.Generic.List%601>\-Objekten dargestellt, die im `BaggageHandler`\-Klassenkonstruktor instanziiert werden.  Der Quellcode für die `BaggageHandler`\-Klasse wird im folgenden Beispiel gezeigt.  
  
 [!code-csharp[Conceptual.ObserverDesignPattern#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/provider.cs#2)]
 [!code-vb[Conceptual.ObserverDesignPattern#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/provider.vb#2)]  
  
 Clients, die aktualisierte Informationen erhalten möchten, rufen die `BaggageHandler.Subscribe`\-Methode auf.  Wenn sich der Client zuvor noch nicht für Benachrichtigungen registriert hat, wird der `observers`\-Auflistung ein Verweis auf die <xref:System.IObserver%601>\-Implementierung des Clients hinzugefügt.  
  
 Die überladene `BaggageHandler.BaggageStatus`\-Methode kann aufgerufen werden, um anzugeben, dass Gepäck aus einem Flug entweder entladen oder nicht mehr entladen wird.  Im ersten Fall wird der Methode eine Flugnummer, der Flughafen, von dem der Flug gestartet ist, und das Laufband übergeben, auf dem das Gepäck entladen wird.  Im zweiten Fall wird der Methode nur eine Flugnummer übergeben.  Für Gepäck, das entladen wird, überprüft die Methode, ob die `BaggageInfo`\-Informationen, die an die Methode übergeben wurden, in der `flights`\-Auflistung vorhanden sind.  Ist dies nicht der Fall, fügt die Methode die Informationen hinzu und ruft die `OnNext`\-Methode aller Beobachter auf.  Für Flüge, deren Gepäck nicht mehr entladen wird, überprüft die Methode, ob Informationen zu diesem Flug in der `flights`\-Auflistung gespeichert sind.  Wenn dies der Fall ist, ruft die Methode die `OnNext`\-Methode jedes Beobachters auf und entfernt das `BaggageInfo`\-Objekt aus der `flights`\-Auflistung.  
  
 Wenn der letzte Flug des Tages gelandet ist und sein Gepäck verarbeitet wurde, wird die `BaggageHandler.LastBaggageClaimed`\-Methode aufgerufen.  Diese Methode ruft die `OnCompleted`\-Methode jedes Beobachters auf, um anzuzeigen, dass alle Benachrichtigungen abgeschlossen wurden, und löscht dann die `observers`\-Auflistung.  
  
 Die <xref:System.IObservable%601.Subscribe%2A>\-Methode des Anbieters gibt eine <xref:System.IDisposable>\-Implementierung zurück, mit der die Beobachter den Empfang von Benachrichtigungen beenden können, bevor die <xref:System.IObserver%601.OnCompleted%2A>\-Methode aufgerufen wird.  Der Quellcode für die `Unsubscriber(Of BaggageInfo)`\-Klasse wird im folgenden Beispiel gezeigt.  Wenn die Klasse in der `BaggageHandler.Subscribe`\-Methode instanziiert wird, werden ein Verweis auf die `observers`\-Auflistung und ein Verweis auf den Beobachter übergeben, der der Auflistung hinzugefügt wird.  Diese Verweise werden lokalen Variablen zugewiesen.  Wenn die `Dispose`\-Methode des Objekts aufgerufen wird, überprüft sie, ob der Beobachter noch in der `observers`\-Auflistung vorhanden ist, und entfernt in diesem Fall den Beobachter.  
  
 [!code-csharp[Conceptual.ObserverDesignPattern#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/provider.cs#3)]
 [!code-vb[Conceptual.ObserverDesignPattern#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/provider.vb#3)]  
  
 Im folgenden Beispiel wird eine <xref:System.IObserver%601>\-Implementierung mit dem Namen `ArrivalsMonitor` gezeigt. Dies ist eine Basisklasse, die Informationen für die Gepäckausgabe anzeigt.  Die Informationen werden alphabetisch nach dem Namen der Stadt sortiert, aus der der Flug kam.  Die Methoden von `ArrivalsMonitor` werden als `overridable` \(Visual Basic\) bzw. als `virtual` \(C\#\) gekennzeichnet, damit sie alle durch eine abgeleitete Klasse überschrieben werden können.  
  
 [!code-csharp[Conceptual.ObserverDesignPattern#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/observer.cs#4)]
 [!code-vb[Conceptual.ObserverDesignPattern#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/observer.vb#4)]  
  
 Die`ArrivalsMonitor`\-Klasse beinhaltet die `Subscribe`\-Methode und die `Unsubscribe`\-Methode.  Mit der `Subscribe`\-Methode kann die Klasse die <xref:System.IDisposable>\-Implementierung, die beim Aufruf von <xref:System.IObservable%601.Subscribe%2A> zurückgegeben wurde, in einer privaten Variablen speichern.  Mit der `Unsubscribe`\-Methode kann die Klasse den Empfang von Benachrichtigungen kündigen, indem die <xref:System.IDisposable.Dispose%2A>\-Implementierung des Anbieters aufgerufen wird.  `ArrivalsMonitor` stellt ebenfalls Implementierungen der Methoden <xref:System.IObserver%601.OnNext%2A>, <xref:System.IObserver%601.OnError%2A> und <xref:System.IObserver%601.OnCompleted%2A> bereit.  Nur die <xref:System.IObserver%601.OnNext%2A>\-Implementierung enthält eine signifikante Menge an Code.  Die Methode arbeitet mit einem privaten, sortierten, generischen <xref:System.Collections.Generic.List%601>\-Objekt, in dem Informationen über die Herkunftsflugplätze der ankommenden Flüge und über die Laufbänder verwaltet werden, auf denen das Gepäck bereitgestellt wird.  Wenn die `BaggageHandler`\-Klasse einen neuen ankommenden Flug meldet, fügt die <xref:System.IObserver%601.OnNext%2A>\-Methodenimplementierung der Liste Informationen über diesen Flug hinzu.  Wenn die `BaggageHandler`\-Klasse meldet, dass das Gepäck des Fluges entladen wurde, entfernt die <xref:System.IObserver%601.OnNext%2A>\-Methode diesen Flug aus der Liste.  Bei jeder Änderung wird die Liste sortiert und an der Konsole angezeigt.  
  
 Das folgende Beispiel enthält den Einstiegspunkt der Anwendung, die die `BaggageHandler`\-Klasse und zwei Instanzen der `ArrivalsMonitor`\-Klasse instanziiert und die `BaggageHandler.BaggageStatus`\-Methode verwendet, um Informationen über ankommende Flüge hinzuzufügen und zu entfernen.  In jedem Fall empfangen die Beobachter Updates und zeigen ordnungsgemäß Informationen zur Gepäckausgabe an.  
  
 [!code-csharp[Conceptual.ObserverDesignPattern#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/program.cs#5)]
 [!code-vb[Conceptual.ObserverDesignPattern#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/module1.vb#5)]  
  
## Verwandte Themen  
  
|Titel|Beschreibung|  
|-----------|------------------|  
|[Empfohlene Vorgehensweisen für Beobachterentwurfsmuster](../../../docs/standard/events/observer-design-pattern-best-practices.md)|Beschreibt bewährte Methoden für die Entwicklung von Anwendungen, die das Entwurfsmuster "Beobachter" implementieren.|  
|[Gewusst wie: Implementieren eines Anbieters](../../../docs/standard/events/how-to-implement-a-provider.md)|Enthält die schrittweise Implementierung eines Anbieters für eine Anwendung zur Temperaturüberwachung.|  
|[Gewusst wie: Implementieren eines Observers](../../../docs/standard/events/how-to-implement-an-observer.md)|Enthält die schrittweise Implementierung eines Beobachters für eine Anwendung zur Temperaturüberwachung.|