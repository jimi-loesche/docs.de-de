---
title: "Neues in Windows Workflow Foundation in .NET 4.5 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 195c43a8-e0a8-43d9-aead-d65a9e6751ec
caps.latest.revision: 32
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 32
---
# Neues in Windows Workflow Foundation in .NET 4.5
[!INCLUDE[wf](../../../includes/wf-md.md)] in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] verfügt über viele neue Funktionen wie neue Aktivitäten, Designer\-Funktionen und Modelle für die Workflowentwicklung.Viele, aber nicht alle der neuen mit [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] eingeführten Workflowfunktionen werden im neu gehosteten Workflow\-Designer unterstützt.[!INCLUDE[crabout](../../../includes/crabout-md.md)] zu den unterstützten neuen Funktionen finden Sie unter [Unterstützung für neue Workflow Foundation 4.5\-Funktionen im neu gehosteten Workflow\-Designer](../../../docs/framework/windows-workflow-foundation//wf-features-in-the-rehosted-workflow-designer.md).[!INCLUDE[crabout](../../../includes/crabout-md.md)] zum Migrieren von .NET 3.0 und .NET 3.5\-Workflowanwendungen, sodass sie die neueste Version verwenden, finden Sie unter [Migrationsanleitung](../../../docs/framework/windows-workflow-foundation//migration-guidance.md).Dieses Thema bietet eine Übersicht über die neuen Workflowfunktionen, die mit [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] eingeführt wurden.  
  
> [!WARNING]
>  Die neuen, in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] eingeführten [!INCLUDE[wf2](../../../includes/wf2-md.md)]\-Funktionen sind nicht für Projekte verfügbar, die frühere Versionen des Frameworks als Zielframework verwenden.Wenn ein Projekt, das [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] als Zielframework verwendet, auf eine frühere Frameworkversion verwiesen wird, treten mehrere Probleme auf.  
>   
>  -   C\#\-Ausdrücke werden im Designer durch die Meldung **Wert wurde in XAML festgelegt** ersetzt.  
> -   Viele Erstellungsfehler einschließlich des folgenden Fehlers treten auf.  
>   
>  **Das Dateiformat ist nicht mit dem aktuellen Zielframework kompatibel.Zum Konvertieren des Dateiformats müssen Sie die Datei explizit speichern.Diese Fehlermeldung wird nicht mehr angezeigt, wenn Sie die Datei speichern und erneut im Designer öffnen.**  
  
##  <a name="BKMK_Versioning"></a> Workflowversionsverwaltung  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] wurden neue Versionsverwaltungsfunktionen eingeführt, die auf der neuen <xref:System.Activities.WorkflowIdentity>\-Klasse basieren.<xref:System.Activities.WorkflowIdentity> bietet Anwendern von Workflowanwendungen einen Mechanismus, um ihrer Definition eine persistente Workflowinstanz zuzuordnen.  
  
-   Entwickler, die das <xref:System.Activities.WorkflowApplication>\-Hosting verwenden, können mit <xref:System.Activities.WorkflowIdentity> das parallele Hosten mehrerer Versionen eines Workflows aktivieren.Persistente Workflowinstanzen können mit der neuen <xref:System.Activities.WorkflowApplicationInstance>\-Klasse geladen werden, und anschließend kann <xref:System.Activities.WorkflowApplicationInstance.DefinitionIdentity%2A> vom Host verwendet werden, um beim Instanziieren von <xref:System.Activities.WorkflowApplication> die richtige Version der Workflowdefinition bereitzustellen.Weitere Informationen finden Sie unter [Verwenden von WorkflowIdentity und Versionsverwaltung](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md) und [Vorgehensweise: Paralleles Hosten mehrerer Workflowversionen](../../../docs/framework/windows-workflow-foundation//how-to-host-multiple-versions-of-a-workflow-side-by-side.md).  
  
-   <xref:System.ServiceModel.WorkflowServiceHost> ist jetzt ein versionsübergreifender Host.Wenn eine neue Version eines Workflowdiensts bereitgestellt wird, werden neue Instanzen mithilfe des neuen Diensts erstellt, während vorhandene Instanzen mit der vorherigen Version abgeschlossen werden.Weitere Informationen finden Sie unter [Parallele Versionsverwaltung in WorkflowServiceHost](../../../docs/framework/wcf/feature-details/side-by-side-versioning-in-workflowservicehost.md).  
  
-   Dynamische Updates werden eingeführt, die einen Mechanismus zum Aktualisieren der Definition einer persistenten Workflowinstanz bereitstellen.Weitere Informationen finden Sie unter [Dynamisches Update](../../../docs/framework/windows-workflow-foundation//dynamic-update.md) und [Vorgehensweise: Aktualisieren der Definition einer ausgeführten Workflowinstanz](../../../docs/framework/windows-workflow-foundation//how-to-update-the-definition-of-a-running-workflow-instance.md).  
  
-   Ein SqlWorkflowInstanceStoreSchemaUpgrade.sql\-Datenbankskript wird bereitgestellt, um ein Upgrade für Persistenzdatenbanken auszuführen, die mit [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]\-Datenbankskripts erstellt wurden.Dieses Skript aktualisiert [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]\-Persistenzdatenbanken, um die neuen Versionsverwaltungsfunktionen zu unterstützen, die in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] eingeführt wurden.Den persistenten Workflowinstanzen in der Datenbank werden Standardversionswerte zugeordnet, und sie können an einer parallelen Ausführung und an dynamischen Updates beteiligt sein.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Aktualisieren von .NET Framework 4\-Persistenzdatenbanken zur Unterstützung der Workflowversionsverwaltung](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md#UpdatingWF4PersistenceDatabases).  
  
##  <a name="BKMK_NewActivities"></a> Aktivitäten  
 Die integrierte Aktivitätsbibliothek enthält neue Aktivitäten und neue Funktionen für vorhandene Aktivitäten.  
  
###  <a name="BKMK_NoPersistScope"></a> NoPersist\-Bereich  
 <xref:System.Activities.Statements.NoPersistScope> ist eine neue Containeraktivität, die verhindert, dass ein Workflow persistent gespeichert wird, wenn die untergeordneten Aktivitäten von NoPersistScopes ausgeführt werden.Dies ist in Szenarien hilfreich, in denen die persistente Speicherung des Workflows nicht angebracht ist, beispielsweise, wenn der Workflow computerspezifische Ressourcen wie Dateihandles verwendet, oder im Verlauf von Datenbanktransaktionen.Um zu vermeiden, dass die Persistenz während der Ausführung einer Aktivität auftritt, war früher eine benutzerdefinierte <xref:System.Activities.NativeActivity> erforderlich, die einen <xref:System.Activities.NoPersistHandle> verwendete.  
  
###  <a name="BKMK_NewFlowchartCapabilities"></a> Neue Flussdiagrammfunktionen  
 Flussdiagramme wurden für [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] überarbeitet und weisen die folgenden neuen Funktionen auf:  
  
-   Die `DisplayName`\-Eigenschaft einer <xref:System.Activities.Statements.FlowSwitch%601>\-Aktivität oder <xref:System.Activities.Statements.FlowDecision>\-Aktivität ist bearbeitbar.Auf diese Weise kann der Aktivitäts\-Designer mehr Informationen über den Zweck der Aktivität anzeigen.  
  
-   Flussdiagramme weisen eine neue Eigenschaft auf, die <xref:System.Activities.Statements.Flowchart.ValidateUnconnectedNodes%2A> genannt wird. Der Standardwert für diese Eigenschaft ist `False`.Wenn diese Eigenschaft auf `True` festgelegt ist, führen nicht verbundene Flussdiagrammknoten zu Validierungsfehlern.  
  
## Unterstützung für teilweise Vertrauenswürdigkeit  
 Workflows in [!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)] benötigen eine voll vertrauenswürdige Anwendungsdomäne.In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] können Workflows in einer teilweise vertrauenswürdigen Umgebung ausgeführt werden.In einer teilweise vertrauenswürdigen Umgebung können Komponenten von Drittanbietern eingesetzt werden, ohne ihnen vollen Zugriff auf die Ressourcen des Hosts zu gewähren.Mögliche Bedenken zum Ausführen von Workflows unter teilweiser Vertrauenswürdigkeit:  
  
1.  Das Verwenden älterer, in der <xref:System.Activities.Statements.Interop>\-Aktivität enthaltener Komponenten \(einschließlich Regeln\) wird unter teilweiser Vertrauenswürdigkeit nicht unterstützt.  
  
2.  Das Ausführen von Workflows unter teilweiser Vertrauenswürdigkeit in <xref:System.ServiceModel.WorkflowServiceHost> wird nicht unterstützt.  
  
3.  Persistente Ausnahmen in einem teilweise vertrauenswürdigen Szenario stellen ein Sicherheitsrisiko dar.Um die Persistenz von Ausnahmen zu deaktivieren, muss dem Projekt eine Erweiterung des Typs <xref:System.Activities.ExceptionPersistenceExtension> hinzugefügt werden.Im folgenden Codebeispiel wird die Implementierung dieses Typs veranschaulicht.  
  
    ```  
    public class ExceptionPersistenceExtension   
    {  
        public ExceptionPersistenceExtension()   
        {   
            this.PersistExceptions = false;   
        }   
        public bool PersistExceptions { get; set; }   
    }  
  
    ```  
  
     Wenn Ausnahmen nicht serialisiert werden müssen, stellen Sie sicher, dass Ausnahmen in <xref:System.Activities.Statements.NoPersistScope> verwendet werden.  
  
4.  Aktivitätsautoren sollten <xref:System.Activities.Activity.CacheMetadata%2A> überschreiben, damit während der Workflowlaufzeit nicht automatisch eine Reflektion für den Typ ausgeführt wird.Argumente und untergeordnete Aktivitäten dürfen nicht NULL sein, und <xref:System.Activities.ActivityMetadata.Bind%2A> muss explizit aufgerufen werden.Weitere Informationen zum Überschreiben von <xref:System.Activities.Activity.CacheMetadata%2A> finden Sie unter [Verfügbarmachen von Daten mit CacheMetadata](../../../docs/framework/windows-workflow-foundation//exposing-data-with-cachemetadata.md).Außerdem müssen Instanzen von Argumenten, die den Typ `internal` oder **private** aufweisen, explizit in <xref:System.Activities.Activity.CacheMetadata%2A> erstellt werden, um eine Erstellung mittels Reflektion zu vermeiden.  
  
5.  Die Typen verwenden nicht <xref:System.Runtime.Serialization.ISerializable> oder <xref:System.SerializableAttribute> für die Serialisierung. Die zu serialisierenden Typen müssen <xref:System.Runtime.DataContractSerializer> unterstützen.  
  
6.  Ausdrücke, die <xref:System.Activities.Expressions.LambdaValue%601> verwenden, setzen <xref:System.Security.Permissions.ReflectionPermissionAttribute.RestrictedMemberAccess%2A> voraus und funktionieren deshalb nicht unter teilweiser Vertrauenswürdigkeit.Bei Workflows, die <xref:System.Activities.Expressions.LambdaValue%601> verwenden, sollten diese Ausdrücke durch Aktivitäten ersetzt werden, die von <xref:System.Activities.CodeActivity%601> abgeleitet sind..  
  
7.  Ausdrücke können nicht mit <xref:System.Activities.XamlIntegration.WorkflowExpressionCompiler> oder dem von Visual Basic gehosteten Compiler für teilweise Vertrauenswürdigkeit kompiliert werden, zuvor kompilierte Ausdrücke können jedoch ausgeführt werden.  
  
8.  Eine einzelne Assembly, die [Transparenz der Ebene 2](http://aka.ms/Level2Transparency) verwendet, kann nicht in [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)], [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] mit voller Vertrauenswürdigkeit und in [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] mit teilweiser Vertrauenswürdigkeit verwendet werden.  
  
##  <a name="BKMK_NewDesignerCapabilites"></a> Neue Designer\-Funktionen  
  
###  <a name="BKMK_DesignerSearch"></a> Designer\-Suche  
 Um größere Workflows überschaubarer zu halten, können sie jetzt nach Schlüsselwort durchsucht werden.Diese Funktion ist nur in [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)], nicht aber in einem neu gehosteten Designer verfügbar.Es gibt zwei Arten von Suchen:  
  
-   Schnellsuche: wird entweder mit **STRG\+F**, **Bearbeiten**, **Suchen und Ersetzen** oder **Schnellsuche** initiiert.  
  
-   In Dateien suchen: wird entweder mit **STRG\+UMSCHALT\+F**, **Bearbeiten**, **Suchen und Ersetzen** oder **In Dateien suchen** initiiert.  
  
 Beachten Sie, dass der Ersetzungsvorgang nicht unterstützt wird.  
  
####  <a name="BKMK_QuickFind"></a> Schnellsuche  
 Schlüsselwörter, die in den Workflows gesucht werden, entsprechen den folgenden Designerelementen:  
  
-   Eigenschaften von <xref:System.Activities.Activity>\-Objekten, <xref:System.Activities.Statements.FlowNode>\-Objekten, <xref:System.Activities.Statements.State>\-Objekten, <xref:System.Activities.Statements.Transition>\-Objekten und anderen benutzerdefinierten Flusssteuerungselementen.  
  
-   Variablen  
  
-   Argumente  
  
-   Ausdrücke  
  
 Die Schnellsuche wird in der <xref:System.Activities.Presentation.Model.Modelitem>\-Struktur des Designers ausgeführt.Die Schnellsuche findet keine Namespaces, die in die Workflowdefinition importiert wurden.  
  
####  <a name="BKMK_FindInFiles"></a> Suchen in Dateien  
 Schlüsselwörter, die in den Workflows gesucht werden, stimmen mit dem tatsächlichen Inhalt der Workflowdateien überein.Die Suchergebnisse werden im Visual Studio\-Ansichtsbereich **Suchergebnisse** angezeigt.Durch Doppelklicken auf das Ergebniselement navigieren Sie im Workflow\-Designer zur Aktivität, in der die Übereinstimmung enthalten ist.  
  
###  <a name="BKMK_VariableDeleteContextMenu"></a> Löschen von Kontextmenüelementen im Variablen\- und Argument\-Designer  
 In [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] konnten Variablen und Argumente nur im Designer und mithilfe der Tastatur gelöscht werden.Ab [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] können Variablen und Argumente mithilfe des Kontextmenüs gelöscht werden.  
  
 Das folgende Bildschirmfoto zeigt das Kontextmenü des Variablen\- und Argument\-Designers.  
  
 ![Kontextmenü des Variablen&#45; und Argument&#45;Designers](../../../docs/framework/windows-workflow-foundation//media/designercontextmenu.png "DesignerContextMenu")  
  
###  <a name="BKMK_AutoSurround"></a> Automatisches Umschließen mit Sequenz  
 Da ein Workflow oder bestimmte Containeraktivitäten \(z. B. <xref:System.Activities.Statements.NoPersistScope>\) nur eine einzelne Textkörperaktivität enthalten können, musste der Entwickler zum Hinzufügen einer zweiten Aktivität die erste Aktivität löschen, eine <xref:System.Activities.Statements.Sequence>\-Aktivität hinzufügen und der Sequenzaktivität dann beide Aktivitäten hinzufügen.Wenn der Designer\-Oberfläche ab [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] eine zweite Aktivität hinzugefügt wird, wird automatisch eine `Sequence`\-Aktivität erstellt, um beide Aktivitäten zu umschließen.  
  
 Die folgende Bildschirmaufnahme zeigt eine `WriteLine`\-Aktivität in `Body` von `NoPersistScope`.  
  
 ![Automatisches Umschließen des Ablageorts](../../../docs/framework/windows-workflow-foundation//media/autosurround1.png "AutoSurround1")  
  
 Die folgende Bildschirmaufnahme zeigt die automatisch erstellte `Sequence`\-Aktivität in `Body`, wenn eine zweite `WriteLine`\-Komponente unterhalb der ersten abgelegt wird.  
  
 ![Automatisch erstellte Sequenzaktivität](../../../docs/framework/windows-workflow-foundation//media/autosurround2.png "AutoSurround2")  
  
###  <a name="BKMK_PanMode"></a> Schwenkmodus  
 Um in einem umfangreichen Workflow einfacher im Designer zu navigieren, kann der Schwenkmodus aktiviert werden, der es dem Entwickler ermöglicht, den sichtbaren Teil des Workflows durch Klicken und Ziehen zu verschieben, anstatt die Bildlaufleisten zu verwenden.Die Schaltfläche zum Aktivieren des Schwenkmodus befindet sich in der rechten unteren Ecke des Designers.  
  
 Das folgende Bildschirmfoto zeigt die Schaltfläche zum Schwenken, die sich in der unteren rechten Ecke des Workflow\-Designers befindet.  
  
 ![Schaltfläche "Schwenken" im Workflow Designer](../../../docs/framework/windows-workflow-foundation//media/panbutton.png "PanButton")  
  
 Die mittlere Maustaste oder die LEERTASTE kann ebenfalls verwendet werden, um den Workflow\-Designer zu schwenken.  
  
###  <a name="BKMK_MultiSelect"></a> Mehrfachauswahl  
 Mehrere Aktivitäten können gleichzeitig ausgewählt werden, indem Sie entweder ein Rechteck darum ziehen \(wenn der Schwenkmodus nicht aktiviert ist\), oder indem Sie die STRG\-TASTE gedrückt halten und nacheinander auf die gewünschten Aktivitäten klicken.  
  
 Mehrere ausgewählte Aktivitäten können auch im Designer gezogen und abgelegt und über das Kontextmenü bearbeitet werden.  
  
###  <a name="BKMK_DocumentOutline"></a> Gliederungsansicht der Workflowelemente  
 Um das Navigieren in hierarchischen Workflows zu erleichtern, werden die Komponenten eines Workflows in einer strukturähnlichen Gliederungsansicht angezeigt.Die Gliederung wird in der Ansicht **Dokumentgliederung** angezeigt.Um diese Ansicht zu öffnen, wählen Sie in der oberen Menüleiste **Ansicht**, **Weitere Fenster**, **Dokumentgliederung**, oder drücken Sie STRG\+W\+U.Wenn Sie auf einen Knoten in der Gliederungsansicht klicken, wechseln Sie automatisch zur entsprechenden Aktivität im Workflow\-Designer, und die Gliederungsansicht wird aktualisiert, um die im Designer ausgewählten Aktivitäten anzuzeigen.  
  
 Das folgende Bildschirmfoto des abgeschlossenen Workflows aus [Lernprogramm 'Erste Schritte'](../../../docs/framework/windows-workflow-foundation//getting-started-tutorial.md) zeigt die Gliederungsansicht mit einem sequenziellen Workflow.  
  
 ![Gliederungsansicht im Workflow Designer](../../../docs/framework/windows-workflow-foundation//media/outlineviewinworkflowdesigner.jpg "OutlineViewinWorkflowDesigner")  
  
###  <a name="BKMK_CSharpExpressions"></a> C\#\-Ausdrücke  
 Vor [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] konnten alle Ausdrücke in Workflows nur in Visual Basic geschrieben werden.In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] werden Visual Basic\-Ausdrücke nur für Projekte verwendet, die mit Visual Basic erstellt wurden.Visual C\#\-Projekte verwenden jetzt die Programmiersprache C\# für Ausdrücke.Ein voll funktionaler C\#\-Ausdrucks\-Editor wird mit Funktionen wie IntelliSense und der Hervorhebung grammatikalischer Fehler bereitgestellt.Die in früheren Versionen erstellten C\#\-Workflowprojekte, die Visual Basic\-Ausdrücke verwenden, sind weiterhin funktionsfähig.  
  
 C\#\-Ausdrücke werden zur Entwurfszeit validiert.Fehler in C\#\-Ausdrücken werden mit einer roten wellenförmigen Unterstreichung gekennzeichnet.  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)] zu C\#\-Ausdrücken finden Sie unter [C\#\-Ausdrücke](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md).  
  
###  <a name="BKMK_Visibility"></a> Bessere Kontrolle über die Sichtbarkeit der Shellleiste und Headerelemente  
 In einem neu gehosteten Designer sind einige standardmäßigen Benutzeroberflächen\-Steuerelemente für einen bestimmten Workflow möglicherweise bedeutungslos und deaktiviert.In [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] wird diese Anpassung nur von der Shellleiste im unteren Bereich des Designers unterstützt.In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] kann die Sichtbarkeit der Shellheaderelemente am oberen Rand des Designers angepasst werden, indem <xref:System.Activities.Presentation.View.DesignerView.WorkflowShellHeaderItemsVisibility%2A> mit dem entsprechenden <xref:System.Activities.Presentation.View.ShellHeaderItemsVisibility>\-Wert festgelegt wird.  
  
###  <a name="BKMK_AutoConnect"></a> Automatisches Verbinden und Einfügen in Flussdiagramm\- und Zustandsautomatworkflows  
 In [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] mussten Verbindungen zwischen Knoten in einem Flussdiagramm\-Workflow manuell hinzugefügt werden.In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] weisen Flussdiagramm\- und Zustandsautomatknoten Punkte für die automatische Verbindung auf, die sichtbar werden, wenn eine Aktivität aus der Toolbox auf die Designeroberfläche gezogen wird.Durch Ablegen einer Aktivität auf einem dieser Punkte wird die Aktivität automatisch zusammen mit der erforderlichen Verbindung hinzugefügt.  
  
 Das folgende Bildschirmfoto zeigt die Anfügepunkte, die sichtbar werden, wenn eine Aktivität aus der Toolbox gezogen wird.  
  
 ![Startpunkt eines Flussdiagramms mit automatisch verbundenen Punkten](../../../docs/framework/windows-workflow-foundation//media/autoconnect1.png "Autoconnect1")  
  
 Aktivitäten können auch auf Verbindungen zwischen Flussdiagrammknoten und \-zuständen gezogen werden, um den Knoten automatisch zwischen zwei anderen Knoten einzufügen.Das folgende Bildschirmfoto zeigt die hervorgehobene Verbindungslinie, auf die Aktivitäten aus der Toolbox gezogen und abgelegt werden können.  
  
 ![AutoEinfügen&#45;Handle zum Ablegen von Aktivitäten](../../../docs/framework/windows-workflow-foundation//media/autoinsert.png "Autoinsert")  
  
###  <a name="BKMK_Annotations"></a> Designer\-Anmerkungen  
 Zur einfacheren Entwicklung größerer Workflows unterstützt der Designer jetzt das Hinzufügen von Anmerkungen, um den Entwurfsprozess nachzuverfolgen.Aktivitäten, Zustände, Flussdiagrammknoten, Variablen und Argumente können mit Anmerkungen versehen werden.Das folgende Bildschirmfoto zeigt das Kontextmenü, das verwendet wird, um dem Designer Anmerkungen hinzuzufügen.  
  
 ![Kontextmenü der Anmerkung](../../../docs/framework/windows-workflow-foundation//media/annotationdialog.png "annotationdialog")  
  
### Debugzustände  
 In [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] konnten Nicht\-Aktivitätselemente keine Debughaltepunkte unterstützen, da sie keine Ausführungseinheiten bildeten.Diese Version stellt einen Mechanismus bereit, um <xref:System.Activities.Statements.State>\-Objekten Haltepunkte hinzuzufügen.Wenn ein Haltepunkt für <xref:System.Activities.Statements.State> festgelegt wird, wird die Ausführung unterbrochen, wenn vor der Planung der Eintragsaktivitäten oder Trigger ein Zustandsübergang stattfindet.  
  
###  <a name="BKMK_ActivityDelegates"></a> Definieren und Nutzen von ActivityDelegate\-Objekten im Designer  
 Aktivitäten in [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] verwendeten <xref:System.Activities.ActivityDelegate>\-Objekte, um Ausführungspunkte verfügbar zu machen, in denen andere Teile des Workflows mit der Ausführung eines Workflows interagieren konnten. Zur Verwendung dieser Ausführungspunkte war normalerweise jedoch beträchtlicher Code erforderlich.In dieser Version können Entwickler die Aktivitätsdelegaten mit dem Workflow\-Designer definieren und nutzen.Weitere Informationen finden Sie unter [Vorgehensweise: Definieren und Verarbeiten von Aktivitätsdelegaten im Workflow\-Designer](../Topic/How%20to:%20Define%20and%20consume%20activity%20delegates%20in%20the%20Workflow%20Designer.md).  
  
###  <a name="BKMK_BuildTimeValidation"></a> Validierung zur Buildzeit  
 In [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] galten Workflowvalidierungsfehler während der Erstellung eines Workflowprojekts nicht als Erstellungsfehler.Das bedeutete, dass das Erstellen eines Workflowprojekts erfolgreich gewesen sein konnte, obwohl Workflowvalidierungsfehler auftraten.In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] bewirken Workflowvalidierungsfehler, dass die Erstellung fehlschlägt.  
  
###  <a name="BKMK_DesignTimeValidation"></a> Hintergrundvalidierung zur Entwurfszeit  
 In [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] wurde die Workflowvalidierung als Vordergrundprozess ausgeführt, was bei komplexen oder zeitaufwändigen Validierungsprozessen dazu führen konnte, dass die Benutzeroberfläche hängen blieb.Da die Workflowvalidierung nun in einem Hintergrundthread stattfindet, wird die Benutzeroberfläche nicht blockiert.  
  
###  <a name="BKMK_ViewState"></a> Der Ansichtszustand wird an einem separaten Ort in XAML\-Dateien gespeichert  
 In [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] werden die Ansichtszustandsinformationen für einen Workflow an vielen verschiedenen Orten in der XAML\-Datei gespeichert.Dies ist für Entwickler, die XAML direkt lesen oder Code zum Entfernen von Ansichtszustandsinformationen schreiben möchten, ungünstig.In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] werden die Ansichtszustandsinformationen in der XAML\-Datei als separates Element in der XAML\-Datei serialisiert. Entwickler können die Ansichtszustandsinformationen einer Aktivität leicht auffinden und bearbeiten oder den Ansichtszustand vollständig entfernen.  
  
###  <a name="BKMK_ExpressionExtensibility"></a> Erweiterbarkeit von Ausdrücken  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] haben Entwickler die Möglichkeit, eigene Ausdrücke zu erstellen und eine Umgebung zum Erstellen von Ausdrücken zu nutzen, die als Plug\-In für den Workflow\-Designer verfügbar ist.  
  
###  <a name="BKMK_BackwardCompatRehostedDesigner"></a> Opt\-In für Workflow 4.5\-Funktionen im neu gehosteten Designer  
 Um die Abwärtskompatibilität zu gewährleisten, werden einige neue Funktionen in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] im neu gehosteten Designer standardmäßig nicht aktiviert.Dadurch wird sichergestellt, dass vorhandene Anwendungen, die den neu gehosteten Designer verwenden, nicht beeinträchtigt werden, indem ein Update auf die neueste Version ausgeführt wird.Um neue Funktionen im neu gehosteten Designer zu aktivieren, legen Sie entweder <xref:System.Activities.Presentation.DesignerConfigurationService.TargetFrameworkName%2A> auf ".NET Framework 4.5" oder einzelne Member von <xref:System.Activities.Presentation.DesignerConfigurationService> fest, um einzelne Funktionen zu aktivieren.  
  
##  <a name="BKMK_NewWFModels"></a> Neue Modelle für die Workflowentwicklung  
 Zusätzlich zu den Entwicklungsmodellen für sequenzielle oder Flussdiagramm\-Workflows umfasst diese Version Zustandsautomatworkflows und Vertrag zuerst\-Workflowdienste.  
  
###  <a name="BKMK_StateMachine"></a> Zustandsautomatworkflows  
 Zustandsautomatworkflows wurden als Teil von .NET Framework 4, Version 4.0.1, im [Microsoft .NET Framework 4 Plattform Update 1](http://go.microsoft.com/fwlink/?LinkID=215092) eingeführt.Dieses Update umfasste verschiedene neue Klassen und Aktivitäten, die es den Entwicklern ermöglichten, Zustandsautomatworkflows zu erstellen.Diese Klassen und Aktivitäten wurden für [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] aktualisiert.Updates umfassen:  
  
1.  Festlegen von Haltepunkten für Zustände  
  
2.  Kopieren und Einfügen von Übergängen im Workflow\-Designer  
  
3.  Designerunterstützung für das Erstellen von freigegebenen Triggerübergängen  
  
4.  Aktivitäten, die zum Erstellen von Zustandsautomatworkflows verwendet werden, darunter: <xref:System.Activities.Statements.StateMachine>, <xref:System.Activities.Statements.State> und <xref:System.Activities.Statements.Transition>  
  
 Das folgende Bildschirmfoto zeigt den abgeschlossenen Zustandsautomatworkflow aus [Lernprogramm 'Erste Schritte'](../../../docs/framework/windows-workflow-foundation//getting-started-tutorial.md), Schritt [Gewusst wie: Erstellen eines Zustandsautomatenworkflows](../../../docs/framework/windows-workflow-foundation//how-to-create-a-state-machine-workflow.md).  
  
 ![Abgeschlossener Zustandsautomatworkflow](../../../docs/framework/windows-workflow-foundation//media/wfstatemachinegettingstartedtutorialcomplete.JPG "WFStateMachineGettingStartedTutorialComplete")  
  
 Weitere Informationen zum Erstellen von Zustandsautomatworkflows finden Sie unter [Zustandsautomatworkflows](../../../docs/framework/windows-workflow-foundation//state-machine-workflows.md).  
  
###  <a name="BKMK_ContractFirst"></a> Vertrag zuerst\-Workflowentwicklung  
 Das Tool für die Vertrag zuerst\-Workflowentwicklung ermöglicht es dem Entwickler, einen Vertrag zuerst im Code zu entwerfen und dann mit wenigen Klicks in [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] automatisch eine Aktivitätsvorlage in der Toolbox zu generieren, die jeden Vorgang darstellt.Diese Aktivitäten werden dann verwendet, um einen Workflow zu erstellen, der die vom Vertrag definierten Vorgänge implementiert.Der Workflow\-Designer überprüft den Workflowdienst, um sicherzustellen, dass diese Vorgänge implementiert wurden und dass die Signatur des Workflows mit der Vertragssignatur übereinstimmt.Der Entwickler kann einen Workflowdienst auch einer Auflistung implementierter Verträge zuordnen.Weitere Informationen zur Entwicklung von Vertrag zuerst\-Workflowdiensten finden Sie unter [Vorgehensweise: Erstellen eines Workflowdiensts zum Verarbeiten eines vorhandenen Dienstvertrags](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow-service-that-consumes-an-existing-service-contract.md).