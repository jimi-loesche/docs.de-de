---
title: COM-Beispielklasse (C#-Programmierhandbuch)
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- examples [C#], COM classes
- COM, exposing Visual C# objects to
ms.assetid: 6504dea9-ad1c-4993-a794-830fec5270af
caps.latest.revision: 17
author: BillWagner
ms.author: wiwagn
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
ms.openlocfilehash: a759a7dcd211207c8740dd99d592daa509ddec47
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="example-com-class-c-programming-guide"></a>COM-Beispielklasse (C#-Programmierhandbuch)
Das Folgende ist ein Beispiel für eine Klasse, die Sie als COM-Objekt offenlegen würden. Nachdem dieser Code in eine CS-Datei platziert und Ihrem Projekt hinzugefügt wurde, legen Sie die Eigenschaft **für COM-Interop registrieren** auf **TRUE** fest. Weitere Informationen finden Sie unter [Vorgehensweise: Registrieren einer Komponente für COM-Interop](http://msdn.microsoft.com/en-us/4de7d474-56e8-4027-994d-d47ca4725c5e).  
  
 Das Verfügbarmachen von Visual C#-Objekten für COM erfordert die Deklaration einer Klassenschnittstelle, einer Ereignisschnittstelle (wenn dies erforderlich ist) und die Klasse selbst. Klassenmember müssen diesen Regeln folgen, um für COM sichtbar zu sein:  
  
-   Die Klasse muss öffentlich sein.  
  
-   Eigenschaften, Methoden und Ereignisse müssen öffentlich sein.  
  
-   Eigenschaften und Methoden müssen auf der Klassenschnittstelle deklariert werden.  
  
-   Ereignisse müssen in der Ereignisschnittstelle deklariert werden.  
  
 Andere öffentliche Member in der Klasse, die nicht in diesen Schnittstellen deklariert sind, werden für COM nicht sichtbar sein, aber für andere .NET Framework-Objekte werden sie sichtbar sein.  
  
 Um Eigenschaften und Methoden für COM verfügbar zu machen, müssen Sie diese auf der Klassenschnittstelle deklarieren, sie mit einem `DispId`-Attribut markieren und sie in der Klasse implementieren. Die Reihenfolge, in der die Elemente in der Schnittstelle deklariert werden, ist die für die COM-Vtable verwendete Reihenfolge.  
  
 Um Ereignisse aus Ihrer Klasse verfügbar zu machen, müssen Sie diese auf der Ereignisschnittstelle deklarieren und sie mit einem `DispId`-Attribut markieren. Die Klasse sollte diese Schnittstelle nicht implementieren.  
  
 Die Klasse implementiert die Klassenschnittstelle. Es kann mehr als eine Schnittstelle implementieren, aber die erste Implementierung ist die Standard-Klassenschnittstelle. Implementieren Sie die Methoden und Eigenschaften hier, die Sie für COM verfügbar gemacht haben. Sie müssen als öffentlich markiert sein und den Deklarationen in der Klassenschnittstelle entsprechen. Deklarieren Sie außerdem die von der Klasse hier ausgelösten Ereignisse. Sie müssen als öffentlich markiert sein und den Deklarationen in der Klassenschnittstelle entsprechen.  
  
## <a name="example"></a>Beispiel  
 [!code-cs[csProgGuideInterop#8](../../../csharp/programming-guide/interop/codesnippet/CSharp/example-com-class_1.cs)]  
  
## <a name="see-also"></a>Siehe auch  
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [Interoperabilität](../../../csharp/programming-guide/interop/index.md)   
 [Seite „Erstellen“, Projekt-Designer (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp)

