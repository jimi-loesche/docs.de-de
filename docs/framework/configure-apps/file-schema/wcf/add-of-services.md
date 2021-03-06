---
title: "&lt;add&gt; von &lt;services&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6bdc4590-aa9c-4ec8-9345-879d780cd141
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;add&gt; von &lt;services&gt;
Legt Einstellungen für eine Instanz von <xref:System.Workflow.Runtime.WorkflowRuntime> zum Hosten workflowbasierter [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)]\-Dienste fest.  Dieses Element ist vom Typ <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>.  
  
## Syntax  
  
```  
  
<workflowRuntime>  
   <services>  
      <add type="String"/>  
   </services>  
</workflowRuntime>  
```  
  
## Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### Attribute  
  
|Attribut|Beschreibung|  
|--------------|------------------|  
|Typ|Eine Zeichenfolge, die den durch die Assembly bezeichneten Typnamen des zu initialisierenden Diensts angibt.  Der angegebene Dienst muss bestimmten Regeln über die Signaturen ihrer Konstruktoren folgen.  Weitere Informationen finden Sie unter <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>.|  
  
### Untergeordnete Elemente  
 Keine  
  
### Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<Dienste\>](../../../../../docs/framework/configure-apps/file-schema/wcf/services-of-workflowruntime.md)|Eine Auflistung von Diensten, die dem <xref:System.Workflow.Runtime.WorkflowRuntime>\-Modul hinzugefügt werden.  Die Elemente sind vom Typ <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>.  Die in der Auflistung angegebenen Dienste werden vom Workflow\-Laufzeitmodul initialisiert und den Diensten hinzugefügt, wenn der entsprechende <xref:System.Workflow.Runtime.WorkflowRuntime>\-Konstruktor aufgerufen wird.  Aus diesem Grund müssen die in der Auflistung angegebenen Dienste bestimmte Regeln bezüglich der Signaturen ihrer Konstruktoren erfüllen.  Weitere Informationen finden Sie unter <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>.|  
  
## Hinweise  
 Der in diesem Element angegebene Dienst wird vom Workflow\-Lauftzeitmodul initialisiert und seinen Diensten hinzugefügt, wenn der entsprechende <xref:System.Workflow.Runtime.WorkflowRuntime>\-Konstruktor aufgerufen wird.  Deshalb muss der in der Auflistung angegebenen Dienst bestimmten Regeln über die Signaturen ihrer Konstruktoren folgen.  Weitere Informationen finden Sie unter <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>.  
  
## Beispiel  
  
```  
<serviceBehaviors>  
   <behavior name="ServiceBehavior">  
      <workflowRuntime name="WorkflowServiceHostRuntime"  
                       validateOnCreate="true"  
                       enablePerformanceCounters="true">  
         <services>  
             <add type="NetFx.Checkin.Scenario.WorkflowServices.WorkflowBasedServices.Common.TestPersistenceService.FilePersistenceService, NetFx.Checkin.Scenario.WorkflowServices.WorkflowBasedServices.Common"/>  
         </services>  
      </workflowRuntime>  
   </behavior>  
</serviceBehaviors>  
```  
  
## Siehe auch  
 <xref:System.ServiceModel.Configuration.WorkflowRuntimeElement>   
 <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>   
 <xref:System.Workflow.Runtime.WorkflowRuntime>   
 [Workflow Configuration Files](http://msdn.microsoft.com/de-de/ada4bb90-6c9d-4f3d-a9d0-b559bb0f9909)