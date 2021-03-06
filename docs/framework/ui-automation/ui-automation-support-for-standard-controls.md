---
title: "UI Automation Support for Standard Controls | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "controls, UI Automation support for"
  - "UI Automation, support for standard controls"
ms.assetid: 3770ea8a-2655-4add-9c59-fe0610ad5084
caps.latest.revision: 11
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 10
---
# UI Automation Support for Standard Controls
> [!NOTE]
>  Diese Dokumentation ist für .NET Framework\-Entwickler vorgesehen, die die verwalteten [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Klassen verwenden möchten, die im <xref:System.Windows.Automation>\-Namespace definiert sind. Aktuelle Informationen zur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] finden Sie auf der Seite zur [Windows\-Automatisierungs\-API: UI\-Automatisierung](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Dieses Thema enthält Informationen zur [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]\-Unterstützung für Standardsteuerelemente in Anwendungen für die Frameworks [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] und [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Windows_Presentation_Foundation_Controls"></a>   
## WPF\-Steuerelemente \(Windows Presentation Foundation\)  
 Alle [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]\-Steuerelemente, die Informationen enthalten oder Benutzerinteraktionen unterstützen, verfügen über eine vollständige systemeigene Unterstützung für [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. Andere Elemente \(wie Bereiche\) sind für [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] nicht sichtbar.  
  
<a name="Win32_Controls"></a>   
## Win32\-Steuerelemente  
 Die meisten [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)]\-Steuerelemente werden über clientseitige Anbieter in „UIAutomationClientsideProviders.dll“ für [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] verfügbar gemacht. Diese Assembly wird automatisch für die Verwendung mit Benutzeroberflächenautomatisierungs\-Clientanwendungen registriert.  
  
 Vollständige Unterstützung gibt es nur für Steuerelemente von Version 6 von „ComCtrl32.dll“ \(ab [!INCLUDE[TLA#tla_winxp](../../../includes/tlasharptla-winxp-md.md)] verfügbar\).  
  
 Die folgenden Steuerelemente werden unterstützt:  
  
|Klassenname|Steuerelementtyp|  
|-----------------|----------------------|  
|Schaltfläche|Schaltfläche|  
|Schaltfläche|RadioButton|  
|Schaltfläche|Gruppieren|  
|Schaltfläche|CheckBox|  
|Schaltfläche|Link|  
|Schaltfläche|SplitButton|  
|Schaltfläche|CheckBox|  
|ComboBoxEx32|ComboBox|  
|ComboBox|ComboBox|  
|Bearbeiten|Dokument|  
|Bearbeiten|Bearbeiten|  
|SysLink|Link|  
|Statisch|Text|  
|Statisch|Bild|  
|SysIPAddress32|Benutzerdefiniert|  
|SysHeader32|Header\/HeaderItem|  
|SysListView32|DataGrid|  
|SysListView32|Liste|  
|ListBox|Liste|  
|ListBox|ListItem|  
|\#32768|Menü|  
|\#32768|MenuItem|  
|msctls\_progress32|ProgressBar|  
|RichEdit|Dokument. Siehe Hinweis.|  
|RichEdit20A|Dokument|  
|RichEdit20W|Dokument|  
|RichEdit50W|Dokument|  
|ScrollBar|Slider|  
|msctls\_trackbar32|Slider|  
|msctls\_updown32|Spinner|  
|msctls\_statusbar32|StatusBar|  
|SysTabControl32|Registerkarte|  
|SysTabControl32|TabItem|  
|ToolbarWindow32|ToolBar|  
|ToolbarWindow32|MenuItem|  
|ToolbarWindow32|Schaltfläche|  
|ToolbarWindow32|CheckBox|  
|ToolbarWindow32|RadioButton|  
|ToolbarWindow32|Trennzeichen|  
|tooltips\_class32|QuickInfo|  
|\#32774|QuickInfo|  
|ReBarWindow32|Symbolleiste|  
|SysTreeView32|Struktur|  
|SysTreeView32|TreeItem|  
  
 **Hinweis** Das RichEdit\-Steuerelement wird nur für mit [!INCLUDE[TLA#tla_winvista](../../../includes/tlasharptla-winvista-md.md)] ausgelieferte Versionen unterstützt \(in „RichEd20.dll“ ab Version 3.1 und „MsftEdit.dll“ ab Version 4.1\).  
  
 Die folgenden Steuerelemente werden nicht unterstützt:  
  
|Klassenname|Steuerelementtyp|  
|-----------------|----------------------|  
|SysAnimate32|Bild|  
|SysPager|Spinner|  
|SysDateTimePick32|Benutzerdefiniert|  
|SysMonthCal32|Kalender|  
|MS\_WINNOTE|Tooltip|  
|VBBubble|Tooltip|  
|ScrollBar \(wenn als eigenständiges Steuerelement verwendet\)|Slider|  
|SuperGrid|Benutzerdefiniert|  
  
<a name="Windows_Forms_Controls"></a>   
## Windows Forms\-Steuerelemente  
 [!INCLUDE[TLA2#tla_winforms](../../../includes/tla2sharptla-winforms-md.md)]\-Steuerelemente werden über clientseitige Anbieter in „UIAutomationClientsideProviders.dll“ für [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] verfügbar gemacht. Diese Assembly wird automatisch für die Verwendung mit Benutzeroberflächenautomatisierungs\-Clientanwendungen registriert.  
  
 [!INCLUDE[TLA2#tla_winforms](../../../includes/tla2sharptla-winforms-md.md)]\-Steuerelemente, die verwaltete Wrapper für allgemeine [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)]\-Steuerelemente sind, werden von [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] in der Regel unterstützt. Die folgenden Steuerelemente werden unterstützt:  
  
|Klassenname|  
|-----------------|  
|Schaltfläche|  
|CheckBox|  
|CheckedListBox|  
|ColorDialog|  
|ComboBox|  
|FolderBrowser|  
|FontDialog|  
|GroupBox|  
|HscrollBar|  
|ImageList|  
|Bezeichnung|  
|ListBox|  
|ListView|  
|MainMenu\/ContextMenu|  
|MonthCalendar|  
|NotifyIcon|  
|OpenFileDialog|  
|PageSetupDialog|  
|PrintDialog|  
|ProgressBar|  
|RadioButton|  
|RichTextBox|  
|SaveFileDialog|  
|ScrollableControl|  
|SoundPlayer|  
|StatusBar|  
|TabControl\/TabPage|  
|TextBox|  
|Zeitgeber|  
|Symbolleiste|  
|QuickInfo|  
|TrackBar|  
|TreeView|  
|VscrollBar|  
|Webbrowser|  
  
 Die folgenden Steuerelemente sind für [!INCLUDE[TLA#tla_aa](../../../includes/tlasharptla-aa-md.md)] nur über ihre Unterstützung für [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] verfügbar. Möglicherweise sind nicht alle Funktionen verfügbar.  
  
|Steuerelementname|  
|-----------------------|  
|BindingSource|  
|DataGrid|  
|DataGridView|  
|DataNavigator|  
|DomainUpDown|  
|ErrorProvider|  
|FlowLayoutPanel|  
|Formular|  
|LinkLabel|  
|HelpProvider|  
|MaskedTextBox|  
|MenuStrip\/ContextMenuStrip|  
|NumericUpDown|  
|Bereich|  
|PictureBox|  
|PrintDocument|  
|PrintPreview\-Control|  
|PrintPreview\-Dialog|  
|PropertyGrid|  
|UserControl|  
|ToolStrip|  
|TableLayoutPanel|  
|SplitContainer\/SplitterPanel|  
|Aufteilung|  
|RaftingContainer|  
|StatusStrip|  
  
## Siehe auch  
 [UI Automation Control Types](../../../docs/framework/ui-automation/ui-automation-control-types.md)