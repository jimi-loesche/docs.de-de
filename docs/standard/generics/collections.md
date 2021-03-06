---
title: "Generische Auflistungen in .NET Framework | Microsoft Docs"
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
  - "Generische Auflistungen [.NET Framework]"
  - "Generika [.NET Framework], Auflistungen"
ms.assetid: 5b646751-6ab7-465c-916c-b1a76aefa9f5
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Generische Auflistungen in .NET Framework
Dieses Thema enthält eine Übersicht über die generischen Auflistungsklassen und andere generischen Typen in .NET Framework.  
  
## Generische Auflistungen in .NET Framework  
 Die Klassenbibliothek von .NET Framework enthält eine Reihe generischer Auflistungsklassen im <xref:System.Collections.Generic>\- und im <xref:System.Collections.ObjectModel>\-Namespace.  Weitere Informationen zu diesen Klassen finden Sie unter [Häufig verwendete Auflistungstypen](../../../docs/standard/collections/commonly-used-collection-types.md).  
  
### System.Collections.Generic  
 Viele der generischen Auflistungstypen sind direkte Entsprechungen nicht generischer Typen.  <xref:System.Collections.Generic.Dictionary%602> ist eine generische Version von <xref:System.Collections.Hashtable>. Sie verwendet die generische Struktur <xref:System.Collections.Generic.KeyValuePair%602> für die Enumeration anstelle von <xref:System.Collections.DictionaryEntry>.  
  
 <xref:System.Collections.Generic.List%601> ist eine generische Version von <xref:System.Collections.ArrayList>.  Es gibt die generischen Klassen <xref:System.Collections.Generic.Queue%601> und <xref:System.Collections.Generic.Stack%601>, die nicht generischen Versionen entsprechen.  
  
 Es gibt generische und nicht generische Versionen von <xref:System.Collections.Generic.SortedList%602>.  Beide Versionen sind eine Mischung aus einem Wörterbuch und einer Liste.  Die generische <xref:System.Collections.Generic.SortedDictionary%602>\-Klasse ist ein reines Wörterbuch und hat keine nicht generische Entsprechung.  
  
 Die generische <xref:System.Collections.Generic.LinkedList%601>\-Klasse ist eine echte verknüpfte Liste.  Sie hat keine nicht generische Entsprechung.  
  
### System.Collections.ObjectModel  
 Die generische <xref:System.Collections.ObjectModel.Collection%601>\-Klasse stellt eine Basisklasse bereit, aus der Sie Ihre eigenen generischen Auflistungstypen ableiten können.  Die <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>\-Klasse bietet eine einfache Möglichkeit, eine schreibgeschützte Auflistung von jedem beliebigen Typ abzuleiten, der die generische <xref:System.Collections.Generic.IList%601>\-Schnittstelle implementiert.  Die generische <xref:System.Collections.ObjectModel.KeyedCollection%602>\-Klasse bietet eine Möglichkeit, Objekte zu speichern, die ihre eigenen Schlüssel enthalten.  
  
## Weitere generische Typen  
 Die generische <xref:System.Nullable%601>Struktur ermöglicht es Ihnen, die Werttypen so zu verwenden, als ob ihnen `null` zugewiesen werden könnte.  Dies kann nützlich sein, wenn Datenbankabfragen verwendet werden, für die möglicherweise Felder fehlen, die Werttypen enthalten.  Der generische Typparameter kann ein beliebiger Werttyp sein.  
  
> [!NOTE]
>  In C\# muss <xref:System.Nullable%601> nicht explizit verwendet werden, da die Sprache eine Syntax für NULL\-fähige Typen hat.  
  
 Die generische <xref:System.ArraySegment%601>\-Struktur bietet eine Möglichkeit, einen Bereich von Elementen in einem eindimensionalen nullbasierten Array eines beliebigen Typs abzugrenzen.  Der generische Typparameter ist der Typ der Elemente des Arrays.  
  
 Wird der generische <xref:System.EventHandler%601>\-Delegat verwendet, muss kein Delegattyp zum Behandeln von Ereignissen mehr deklariert werden, wenn das Ereignis dem von [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] verwendeten Muster für die Ereignisbehandlung folgt.  Angenommen, Sie haben die von <xref:System.EventArgs> abgeleitete `MyEventArgs`\-Klasse erstellt, um die Daten für das Ereignis zu speichern.  Sie können das Ereignis dann wie folgt deklarieren:  
  
 [!code-cpp[Conceptual.Generics.Overview#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Generics.Overview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source2.cs#7)]
 [!code-vb[Conceptual.Generics.Overview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source2.vb#7)]  
  
## Siehe auch  
 <xref:System.Collections.Generic?displayProperty=fullName>   
 <xref:System.Collections.ObjectModel?displayProperty=fullName>   
 [Generika](../../../docs/standard/generics/index.md)   
 [Generische Delegaten zum Bearbeiten von Arrays und Listen](../../../docs/standard/generics/delegates-for-manipulating-arrays-and-lists.md)   
 [Generische Schnittstellen](../../../docs/standard/generics/interfaces.md)