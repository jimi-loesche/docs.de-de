---
title: Zugriff auf Attribute mit Reflektion (Visual Basic) | Microsoft-Dokumentation
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: c56e41da-5433-464f-a7bf-2a722e78bc9f
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4763eccc5d1a6bdf3e89c1c4d825d5ff5c6caa3e
ms.lasthandoff: 03/13/2017

---
# <a name="accessing-attributes-by-using-reflection-visual-basic"></a>Zugriff auf Attribute mit Reflektion (Visual Basic)
Die Tatsache, dass Sie benutzerdefinierte Attribute definieren und platzieren Sie diese in Ihrem Quellcode können wäre von geringem Wert ohne eine Möglichkeit zum Abrufen von Informationen und darauf reagieren. Mithilfe der Reflektion können Sie die Informationen abrufen, die mit benutzerdefinierten Attributen definiert wurde. Die wichtigste Methode ist `GetCustomAttributes`, die ein Array von Objekten, die die Laufzeit-Entsprechungen der Source CodeAttribute zurückgibt. Diese Methode hat mehrere überlastete Versionen. Weitere Informationen finden Sie unter <xref:System.Attribute>.</xref:System.Attribute>  
  
 Ein Attributspezifikation, wie z. B.:  
  
```vb  
<Author("P. Ackerman", Version:=1.1)>   
Class SampleClass  
    ' P. Ackerman's code goes here...  
End Class  
```  
  
 ist dieses Konzept entspricht:  
  
```vb  
Dim anonymousAuthorObject As Author = New Author("P. Ackerman")  
anonymousAuthorObject.version = 1.1  
```  
  
 Der Code wird jedoch nicht ausgeführt, bis `SampleClass` Attribute abgefragt werden. Aufrufen von `GetCustomAttributes` auf `SampleClass` bewirkt, dass ein `Author` Objekt erstellt und initialisiert, wie oben beschrieben. Wenn die Klasse andere Attribute verfügt, werden andere Attributobjekte auf ähnliche Weise erstellt. `GetCustomAttributes`Gibt die `Author` -Objekt und alle weiteren Attributobjekte in einem Array. Sie können dann dieses Array durchlaufen zu ermitteln Sie, welche Attribute basierend auf dem Typ der jedes Element angewendet wurden, und extrahieren Sie Informationen aus den Attributobjekten.  
  
## <a name="example"></a>Beispiel  
 Hier ist ein vollständiges Beispiel. Ein benutzerdefiniertes Attribut definiert, auf mehrere Entitäten angewendet und mittels Reflektion abgerufen.  
  
```vb  
' Multiuse attribute  
<System.AttributeUsage(System.AttributeTargets.Class Or   
                       System.AttributeTargets.Struct,   
                       AllowMultiple:=True)>   
Public Class Author  
    Inherits System.Attribute  
    Private name As String  
    Public version As Double  
    Sub New(ByVal authorName As String)  
        name = authorName  
  
        ' Default value  
        version = 1.0  
    End Sub  
  
    Function GetName() As String  
        Return name  
    End Function          
End Class  
  
' Class with the Author attribute  
<Author("P. Ackerman")>   
Public Class FirstClass  
End Class  
  
' Class without the Author attribute  
Public Class SecondClass  
End Class  
  
' Class with multiple Author attributes.  
<Author("P. Ackerman"), Author("R. Koch", Version:=2.0)>   
Public Class ThirdClass  
End Class  
  
Class TestAuthorAttribute  
    Sub Main()  
        PrintAuthorInfo(GetType(FirstClass))  
        PrintAuthorInfo(GetType(SecondClass))  
        PrintAuthorInfo(GetType(ThirdClass))  
    End Sub  
  
    Private Shared Sub PrintAuthorInfo(ByVal t As System.Type)  
        System.Console.WriteLine("Author information for {0}", t)  
  
        ' Using reflection  
        Dim attrs() As System.Attribute = System.Attribute.GetCustomAttributes(t)  
  
        ' Displaying output  
        For Each attr In attrs  
            Dim a As Author = CType(attr, Author)  
            System.Console.WriteLine("   {0}, version {1:f}", a.GetName(), a.version)  
        Next              
    End Sub  
  
    ' Output:  
    '   Author information for FirstClass  
    '     P. Ackerman, version 1.00  
    ' Author information for SecondClass  
    ' Author information for ThirdClass  
    '  R. Koch, version 2.00  
    '  P. Ackerman, version 1.00  
  
End Class  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Reflection></xref:System.Reflection>   
 <xref:System.Attribute></xref:System.Attribute>   
 [Visual Basic-Programmierhandbuch](../../../../visual-basic/programming-guide/index.md)   
 [Abrufen von Informationen aus Attributen](http://msdn.microsoft.com/library/37dfe4e3-7da0-48b6-a3d9-398981524e1c)   
 [Reflektion (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)   
 [Attribute (Visual Basic)](../../../../visual-basic/language-reference/attributes.md)   
 [Erstellen von benutzerdefinierten Attributen (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/creating-custom-attributes.md)
