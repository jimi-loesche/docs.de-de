---
title: "Gewusst wie: Lesen aus einer Textdatei | Microsoft Docs"
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
  - "Datenstreams, Lesen von Text aus Dateien"
  - "E/A [.NET Framework], Lesen von Text aus Dateien"
  - "Lesen von Daten, Textdateien"
  - "Lesen von Textdateien"
  - "Streams, Lesen von Text aus Dateien"
ms.assetid: ed180baa-dfc6-4c69-a725-46e87edafb27
caps.latest.revision: 23
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 23
---
# Gewusst wie: Lesen aus einer Textdatei
In den folgenden Beispielen wird das synchrone und asynchrone Lesen aus einer Textdatei mithilfe von .NET für Desktop\-Apps veranschaulicht.  In beiden Beispielen geben Sie beim Erstellen der Instanz der <xref:System.IO.StreamReader>\-Klasse einen absoluten oder relativen Pfad zur Datei an.  In den folgenden Beispielen wird angenommen, dass sich eine Datei mit dem Namen "TestFile.txt" im gleichen Ordner wie die Anwendung befindet.  
  
 Diese Codebeispiele gelten nicht für die Entwicklung von Windows Store\-Apps, da die Windows\-Runtime verschiedene Streamtypen für Lese\- und Schreibvorgänge für Dateien bereitstellt.  Ein Beispiel für das Lesen von Text aus einer Datei im Kontext einer Windows Store\-App finden Sie unter [Schnellstart: Lesen und Schreiben einer Datei](http://msdn.microsoft.com/library/windows/apps/hh758325.aspx).  Weitere Beispiele zum Konvertieren zwischen .NET Framework\-Streams und Windows\-Runtime\-Streams finden Sie unter [Gewusst wie: Konvertieren zwischen .NET Framework\-Streams und Windows\-Runtime\-Streams](../../../docs/standard/io/how-to-convert-between-dotnet-streams-and-winrt-streams.md).  
  
## Beispiel  
 Das erste Beispiel veranschaulicht einen synchronen Lesevorgang in einer Konsolenanwendung an.  In diesem Beispiel wird die Textdatei mit einem Streamreader geöffnet, der Inhalt wird in eine Zeichenfolge kopiert, und die Zeichenfolge wird in der Konsole ausgegeben.  
  
 [!code-csharp[Conceptual.BasicIO.TextFiles#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source3.cs#3)]
 [!code-vb[Conceptual.BasicIO.TextFiles#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source3.vb#3)]  
  
## Beispiel  
 Das zweite Beispiel veranschaulicht einen asynchronen Lesevorgang in einer Windows Presentation Foundation \(WPF\)\-Anwendung.  
  
 [!code-csharp[Conceptual.BasicIO.TextFiles#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source6.cs#6)]
 [!code-vb[Conceptual.BasicIO.TextFiles#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source6.vb#6)]  
  
## Siehe auch  
 <xref:System.IO.StreamReader>   
 <xref:System.IO.File.OpenText%2A?displayProperty=fullName>   
 <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=fullName>   
 [Asynchrone Datei\-E\/A](../../../docs/standard/io/asynchrone-datei-e-a.md)   
 [NIB: How to: Create a Directory Listing](http://msdn.microsoft.com/de-de/4d2772b1-b991-4532-a8a6-6ef733277e69)   
 [Schnellstart: Lesen und Schreiben von Dateien](http://msdn.microsoft.com/library/windows/apps/hh758325.aspx)   
 [Gewusst wie: Konvertieren zwischen .NET Framework\-Streams und Windows\-Runtime\-Streams](../../../docs/standard/io/how-to-convert-between-dotnet-streams-and-winrt-streams.md)   
 [Gewusst wie: Lesen und Schreiben einer neu erstellten Datendatei](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)   
 [Gewusst wie: Öffnen und Anfügen an eine Protokolldatei](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)   
 [Gewusst wie: Schreiben von Text in eine Datei](../../../docs/standard/io/how-to-write-text-to-a-file.md)   
 [Gewusst wie: Lesen von Zeichen aus einer Zeichenfolge](../../../docs/standard/io/how-to-read-characters-from-a-string.md)   
 [Gewusst wie: Schreiben von Zeichen in eine Zeichenfolge](../../../docs/standard/io/how-to-write-characters-to-a-string.md)   
 [Datei\- und Stream\-E\/A](../../../docs/standard/io/index.md)