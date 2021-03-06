---
title: "Zugreifen auf Frames im verwalteten HTML-Dokumentobjektmodell | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "DOM, Zugreifen auf Rahmen in verwaltetem HTML-DOM"
  - "Rahmen, Aufrufen"
  - "HTML-DOM, Verwaltet"
  - "HTML, DOM"
  - "HTML, Verwaltet"
  - "Verwaltetes HTML-DOM"
ms.assetid: cdeeaa22-0be4-4bbf-9a75-4ddc79199f8d
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Zugreifen auf Frames im verwalteten HTML-Dokumentobjektmodell
Einige HTML\-Dokumente bestehen aus *Frames* oder Fenstern, die eigene HTML\-Dokumente enthalten können.  Mit Frames ist es ganz einfach, HTML\-Seiten zu erstellen, auf denen ein oder mehrere Teile statisch bleiben, wie die Navigationsleiste, während sich der Inhalt der anderen Frames permanent ändert.  
  
 HTML\-Autoren können Frames in einer von zwei Weisen erstellen:  
  
-   Unter Verwendung der Tags `FRAMESET` und `FRAME`, womit feste Fenster erstellt werden,  
  
 \- oder \-  
  
-   mithilfe des Tags `IFRAME`, mit dem ein unverankertes Fenster erstellt wird, das zur Laufzeit neu positioniert werden kann.  
  
1.  Da Frames HTML\-Dokumente enthalten, werden sie im DOM \(Document Object Model\) sowohl als Fensterelemente als auch als Frameelemente dargestellt.  
  
2.  Wenn Sie mit der Frames\-Auflistung von <xref:System.Windows.Forms.HtmlWindow> auf ein `FRAME`\- oder `IFRAME`\-Tag zugreifen, rufen Sie ein Fensterelement ab, das dem Frame entspricht.  Dies repräsentiert alle dynamischen Eigenschaften des Frames, wie die aktuelle URL, das Dokument und die Größe.  
  
3.  Wenn Sie über die <xref:System.Windows.Forms.HtmlWindow.WindowFrameElement%2A>\-Eigenschaft von <xref:System.Windows.Forms.HtmlWindow>, die <xref:System.Windows.Forms.HtmlElement.Children%2A>\-Auflistung oder mit Methoden wie <xref:System.Windows.Forms.HtmlElementCollection.GetElementsByName%2A> oder <xref:System.Windows.Forms.HtmlDocument.GetElementById%2A> auf ein `FRAME`\- oder `IFRAME`\-Tag zugreifen, rufen Sie das Frameelement ab.  Dies repräsentiert die statischen Eigenschaften des Frames, einschließlich der URL, die in der ursprünglichen HTML\-Datei angegeben wurde.  
  
## Frames und Sicherheit  
 Der Zugriff auf Frames wird verkompliziert von der Tatsache, dass das verwaltete HTML\-DOM eine Sicherheitsmaßnahme implementiert, die als *frameübergreifende Scripting\-Sicherheit* bezeichnet wird.  Wenn ein Dokument ein `FRAMESET` mit zwei oder mehr `FRAME`s in unterschiedlichen Domänen enthält, können diese `FRAME`s nicht miteinander interagieren.  Anders ausgedrückt, ein `FRAME`, in dem Inhalte von Ihrer Website angezeigt werden, kann nicht auf Informationen in einem `FRAME` zugreifen, der sich auf einer Drittanbieterwebsite wie http:\/\/www.adatum.com\/ befindet.  Diese Sicherheitsmaßnahme wird auf der Ebene der <xref:System.Windows.Forms.HtmlWindow>\-Klasse implementiert.  Sie können allgemeine Informationen zu einem `FRAME` abrufen, der Informationen von einer anderen Website hostet, wie dessen URL, sind aber nicht in der Lage, auf dessen <xref:System.Windows.Forms.HtmlWindow.Document%2A> zuzugreifen oder die Größe oder den Speicherort des Host\-`FRAME`s oder \-`IFRAME`s zu ändern.  
  
 Diese Regel gilt auch für Fenster, die sie mit den Methoden <xref:System.Windows.Forms.HtmlWindow.Open%2A> und <xref:System.Windows.Forms.HtmlWindow.OpenNew%2A> öffnen.  Wenn sich das von Ihnen geöffnete Fenster in einer anderen Domäne als die Seite befindet, die im <xref:System.Windows.Forms.WebBrowser>\-Steuerelement gehostet wird, können Sie dieses Fenster nicht verschieben und dessen Inhalt nicht überprüfen.  Diese Einschränkungen gelten auch, wenn Sie ein <xref:System.Windows.Forms.WebBrowser>\-Steuerelement zum Anzeigen einer Website verwenden, die sich von der Website unterscheidet, die zum Bereitstellen Ihrer Windows Forms\-basierten Anwendung verwendet wird.  Wenn Sie die [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)]\-Bereitstellungstechnologie zum Installieren Ihrer Website auf Website A und dann <xref:System.Windows.Forms.WebBrowser> zum Anzeigen von Website B verwenden, können Sie auf die Daten von Website B nicht zugreifen.  
  
 Weitere Informationen zum websiteübergreifenden Scripting finden Sie unter [Informationen zum frameübergreifenden Scripting und zur Sicherheit](http://msdn.microsoft.com/library/ms533028.aspx).  
  
## Siehe auch  
 [FRAME\-Element &#124; frame\-Objekt](http://msdn.microsoft.com/library/ms535250.aspx)   
 [Verwenden des verwalteten HTML\-Dokumentobjektmodells](../../../../docs/framework/winforms/controls/using-the-managed-html-document-object-model.md)