---
title: "Transaktive Warteschlangen | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b1b011dd-5e0b-482c-9bb0-9d8727038f14
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Transaktive Warteschlangen
In diesem Beispiel wird veranschaulicht, wie Warteschlangen und Transaktionen in [!INCLUDE[wf](../../../../includes/wf-md.md)] integriert werden, um zuverlässige und skalierbare Dienste zu erstellen.Ein <xref:System.Activities.TransactionScope> wird im Clientworkflow verwendet, um Meldungen mithilfe der <xref:System.ServiceModel.NetMsmqBinding> an eine Warteschlange unter einer Transaktion zu senden.Ein <xref:System.ServiceModel.Activities.TransactedReceiveScope> wird auf dem Server verwendet, um Meldungen von der Warteschlange zu empfangen und den Zustand des Workflows unter der gleichen Transaktion zu aktualisieren.  
  
## Veranschaulicht  
 <xref:System.Activities.Statements.TransactionScope>, <xref:System.ServiceModel.Activities.TransactedReceiveScope>, <xref:System.ServiceModel.NetMsmqBinding>, <xref:System.ServiceModel.Activities.Receive> und inhaltsbasierte Korrelation.  
  
## Diskussion  
 Zur Veranschaulichung der in diesem Beispiel behandelten Funktionen wird ein `RewardsPoints`\-Workflowdienst erstellt, der die für ein bestimmtes Konto verdienten und verwendeten Punkte nachverfolgt.Der Client verwendet <xref:System.Activities.WorkflowInvoker>, um das Übermitteln unterschiedlicher Anforderungen an die Warteschlange zu simulieren.Zum Bereitstellen einer Meldung für eine Warteschlange unter einer Transaktion kann die <xref:System.ServiceModel.Activities.Send>\-Aktivität im <xref:System.Activities.Statements.TransactionScope.Body%2A> eines <xref:System.Activities.Statements.TransactionScope> platziert werden.In diesem Beispiel wird zuerst der Client und dann der Server ausgeführt, um zu veranschaulichen, wie in der Warteschlange befindliche Meldungen die Client\- und Serveranwendungen entkoppeln können.  
  
 Sobald der Client abgeschlossen wurde, wird der Dienst konfiguriert und gehostet.Sobald er geöffnet wird, fängt er an, die Meldungen zu verarbeiten, die bereits in der Warteschlange platziert wurden.Jede Meldung wird unter der gleichen Servertransaktion empfangen und verarbeitet.In diesem Beispiel ist die erste empfangene Meldung eine `CreateAccount`\-Anforderung, die die Instanz erstellt und die Inhaltskorrelation auf Grundlage des Kontonamens initialisiert, der als Teil der Anforderungsmeldung übergeben wurde.Zum Modellieren der Art des Dienstes, die Sie unter realen Bedingungen erwarten können, werden die folgenden beiden <xref:System.ServiceModel.Activities.TransactedReceiveScope>\-Aktivitäten, die die `AddPoints`\-Meldung und die `UsePoints`\-Meldung verarbeiten, in parallelen Verzweigungen in eine `while`\-Schleife eingefügt, damit diese Meldungen immer wieder in beliebiger Reihenfolge verarbeitet werden können.  
  
 <xref:System.Activities.Statements.TransactionScope> und <xref:System.ServiceModel.Activities.TransactedReceiveScope> weisen jeweils am Ende ihrer Bereiche einen impliziten Persistenzpunkt auf. Die Verwendung dieser Aktivitäten in [!INCLUDE[wf1](../../../../includes/wf1-md.md)] in Kombination mit Warteschlangen ist daher eine zuverlässige Möglichkeit, um den Workflow von einem konsistenten Zustand in den nächsten zu verschieben und gleichzeitig sicherzustellen, dass keine Meldungen verloren gehen.  
  
#### So richten Sie das Beispiel ein, erstellen es und führen es aus  
  
1.  Installieren und konfigurieren Sie MSMQ.Weitere Informationen finden Sie unter [Installieren von Message Queuing](http://go.microsoft.com/fwlink/?LinkId=178526).  
  
2.  Stellen Sie sicher, dass MSDTC ausgeführt wird, indem Sie den folgenden Befehl in einer Befehlszeile ausführen.`net start msdtc`  
  
3.  Kompilieren Sie das Projekt, und öffnen Sie die ausführbare Datei, oder öffnen Sie das Projekt in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)], und wählen Sie eine Startoption im Debugmenü aus.Zuerst wird die Warteschlange erstellt; anschließend wird der Client ausgeführt, und Meldungen werden an die Warteschlange übermittelt. Schließlich wird der Dienst gestartet, und die Meldungen werden verarbeitet.Zum Beenden des Programms drücken Sie die EINGABETASTE.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert.Überprüfen Sie das folgende \(standardmäßige\) Verzeichnis, bevor Sie fortfahren.  
>   
>  `<Installationslaufwerk>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation \(WCF\) and Windows Workflow Foundation \(WF\) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]\- und [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\-Beispiele herunterzuladen.Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Transactions\TransactedQueues`