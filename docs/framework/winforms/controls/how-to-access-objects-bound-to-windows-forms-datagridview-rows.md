---
title: "Gewusst wie: Aufrufen von Objekten, die an DataGridView-Zeilen in Windows Forms gebunden sind | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Datenblätter, Zugreifen auf gebundene Objekte"
  - "DataGridView-Steuerelement [Windows Forms], Zugreifen auf an Zeilen gebundene Objekte"
  - "Objektbindung, Zugreifen auf gebundene Objekte"
ms.assetid: 0e05748f-4403-4eb8-8b2f-b098108181b5
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Gewusst wie: Aufrufen von Objekten, die an DataGridView-Zeilen in Windows Forms gebunden sind
Manchmal ist es hilfreich, eine Tabelle mit Informationen anzuzeigen, die in einer Auflistung von Geschäftsobjekten gespeichert sind.  Beim Binden eines <xref:System.Windows.Forms.DataGridView>\-Steuerelements an eine solche Auflistung wird jede öffentliche Eigenschaft in einer eigenen Spalte angezeigt, es sei denn, die Eigenschaft wurde mit <xref:System.ComponentModel.BrowsableAttribute> als nicht durchsuchbar markiert.  Angenommen, eine Auflistung von `Customer`\-Objekten hätte Spalten wie **Name** und **Adresse**.  
  
 Wenn diese Objekte zusätzliche Informationen und Code enthalten, auf die Sie zugreifen möchten, können Sie dies über Zeilenobjekte erreichen.  Im folgenden Codebeispiel können Benutzer mehrere Zeilen auswählen und auf eine Schaltfläche klicken, um eine Rechnung an jeden der entsprechenden Kunden zu senden.  
  
### So greifen Sie auf zeilengebundene Objekte zu  
  
-   Verwenden Sie die <xref:System.Windows.Forms.DataGridViewRow.DataBoundItem%2A?displayProperty=fullName>\-Eigenschaft.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewObjectBinding#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/CS/datagridviewobjectbinding.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewObjectBinding#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/VB/datagridviewobjectbinding.vb#10)]  
  
## Beispiel  
 Das vollständige Codebeispiel beinhaltet eine einfache `Customer`\-Implementierung und bindet die <xref:System.Windows.Forms.DataGridView> an eine <xref:System.Collections.ArrayList>, die ein paar `Customer`\-Objekte enthält.  Der <xref:System.Windows.Forms.Control.Click>\-Ereignishandler der <xref:System.Windows.Forms.Button?displayProperty=fullName> muss über die Zeilen auf die `Customer`\-Objekte zugreifen, weil außerhalb des <xref:System.Windows.Forms.Form.Load?displayProperty=fullName>\-Ereignishandlers nicht auf die Kundenauflistung zugegriffen werden kann.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewObjectBinding#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/CS/datagridviewobjectbinding.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewObjectBinding#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/VB/datagridviewobjectbinding.vb#00)]  
  
## Kompilieren des Codes  
 Für dieses Beispiel benötigen Sie Folgendes:  
  
-   Verweise auf die Assemblys "System" und "System.Windows.Forms".  
  
 Informationen zum Erstellen dieses Beispiels über die Befehlszeile für [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] oder [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] finden Sie unter [Erstellen von der Befehlszeile aus](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) oder [Erstellen über die Befehlszeile mit csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  Sie können dieses Beispiel auch in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] erstellen, indem Sie den Code in ein neues Projekt einfügen.  Siehe auch [Gewusst wie: Kompilieren und Ausführen eines vollständigen Windows Forms\-Codebeispiels mit Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Siehe auch  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewRow>   
 <xref:System.Windows.Forms.DataGridViewRow.DataBoundItem%2A?displayProperty=fullName>   
 [Anzeigen von Daten im DataGridView\-Steuerelement in Windows Forms](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [Gewusst wie: Binden von Objekten an das DataGridView\-Steuerelement in Windows Forms](../../../../docs/framework/winforms/controls/how-to-bind-objects-to-windows-forms-datagridview-controls.md)