---
title: await (C#-Referenz)
ms.date: 2017-05-22
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- await_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- await keyword [C#]
- await [C#]
ms.assetid: 50725c24-ac76-4ca7-bca1-dd57642ffedb
caps.latest.revision: 36
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
ms.openlocfilehash: 28be25d2f467ea5df4de50516bfa03347c77081e
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="await-c-reference"></a>await (C#-Referenz)
Der Operator `await` wird auf eine Aufgabe in einer asynchronen Methode angewendet, um einen Unterbrechungspunkt in die Ausführung der Methode einzufügen, bis die Aufgabe abgeschlossen ist. Die Aufgabe stellt derzeit ausgeführte Arbeit dar.  
  
`await` kann nur in einer asynchronen Methode verwendet werden, die vom Schlüsselwort [async](../../../csharp/language-reference/keywords/async.md) verändert wird. Eine solche mit dem `async`-Modifizierer definierte Methode, die in der Regel mindestens einen `await`-Ausdruck enthält, wird als *asynchrone Methode* bezeichnet.  
  
> [!NOTE]
>  Die Schlüsselwörter `async` und `await` wurden in C# 5 eingeführt. Eine Einführung in die asynchrone Programmierung finden Sie unter [Asynchronous Programming with async and await (Asynchrone Programmierung mit „async“ und „await“)](../../../csharp/programming-guide/concepts/async/index.md).  
  
In der Regel wird die Aufgabe, auf die Sie den Operator `await` anwenden, von einem Aufruf einer Methode zurückgegeben, die das [aufgabenbasierte asynchrone Muster](../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md) implementiert. Dazu zählen Methoden, die die Objekte <xref:System.Threading.Tasks.Task>, <xref:System.Threading.Tasks.Task%601> und `System.Threading.Tasks.ValueType<TResult>` zurückgeben.  

  
 Im folgenden Beispiel gibt die <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A?displayProperty=fullName>-Methode ein `Task<byte[]>`-Objekt zurück. Diese Aufgabe enthält das Versprechen, das tatsächliche Bytearray zu erzeugen, wenn die Aufgabe abgeschlossen ist. Der `await`-Operator hält die Ausführung an, bis die Arbeit der Methode <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> abgeschlossen ist. In der Zwischenzeit wird die Steuerung wieder an den Aufrufer von `GetPageSizeAsync` übergeben. Wenn der Task die Ausführung beendet, wird der `await`-Ausdruck zu einem Bytearray ausgewertet.  

[!code-cs[await-Beispiel](../../../../samples/snippets/csharp/language-reference/keywords/await/await1.cs)]  

> [!IMPORTANT]
>  Das vollständige Beispiel finden Sie unter [Exemplarische Vorgehensweise: Zugreifen auf das Web mit Async und Await](../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md). Sie können das Beispiel aus den [Codebeispielen für Entwickler](http://go.microsoft.com/fwlink/?LinkID=255191&clcid=0x409) der Microsoft-Website herunterladen. Das Beispiel befindet sich im AsyncWalkthrough_HttpClient-Projekt.  
  
Wenn `await` auf das Ergebnis eines Methodenaufrufs angewendet wird, der `Task<TResult>` zurückgibt, ist der Typ des `await`-Ausdrucks `TResult`, wie im vorherigen Beispiel gezeigt. Wenn `await` auf das Ergebnis eines Methodenaufrufs angewendet wird, der `Task` zurückgibt, ist der Typ des `await`-Ausdrucks `void`. Der Unterschied wird im folgenden Beispiel veranschaulicht.  
  
```csharp  
// await keyword used with a method that returns a Task<TResult>.  
TResult result = await AsyncMethodThatReturnsTaskTResult();  
  
// await keyword used with a method that returns a Task.  
await AsyncMethodThatReturnsTask();  

// await keyword used with a method that returns a ValueTask<TResult>.
TResult result = await AsyncMethodThatReturnsValueTaskTResult();
```  
  
Ein `await`-Ausdruck blockiert nicht den Thread, auf dem er ausgeführt wird. Stattdessen bewirkt er, dass der Compiler den Rest der asynchronen Methode als Fortsetzung der erwarteten Aufgabe registriert. Die Steuerung wird dann wieder an den Aufrufer der Async-Methode übergeben. Wenn die Aufgabe abgeschlossen ist, löst sie ihre Fortsetzung aus, und die Ausführung der asynchronen Methode wird da fortgesetzt, wo sie angehalten wurde.  
  
Ein `await`-Ausdruck kann nur in seiner einschließenden Methode, einem Lambdaausdruck oder einer anonymen Methode auftreten, die durch einen `async`-Modifizierer gekennzeichnet sein muss. Der Begriff *await* dient nur in diesem Kontext als Schlüsselwort. In anderen Kontexten wird er als Bezeichner interpretiert. Innerhalb der Methode, des Lambdaausdrucks oder der anonymen Methode kann ein `await`-Ausdruck nicht im Textteil einer synchronen Funktion, einem Abfrageausdruck, im Block einer [lock-Anweisung](../../../csharp/language-reference/keywords/lock-statement.md) oder in einem [unsicheren](../../../csharp/language-reference/keywords/unsafe.md) Kontext auftreten.  
  
## <a name="exceptions"></a>Ausnahmen  
Die meisten asynchronen Methoden geben einen <xref:System.Threading.Tasks.Task> oder <xref:System.Threading.Tasks.Task%601> zurück. Die Eigenschaften der zurückgegebenen Aufgabe enthalten Informationen über den Status und Verlauf, z. B. ob die Aufgabe abgeschlossen ist, ob die asynchrone Methode eine Ausnahme verursacht hat oder abgebrochen wurde, und was das Endergebnis ist. Der Operator `await` greift auf diese Eigenschaften zu, indem er Methoden auf dem von der `GetAwaiter`-Methode zurückgegebenen Objekt aufruft.  
  
Wenn Sie auf eine asynchrone Methode warten, die eine Aufgabe zurückgibt und eine Ausnahme verursacht, löst der Operator `await` die Ausnahme erneut aus.  
  
Wenn Sie auf eine asynchrone Methode warten, die eine Aufgabe zurückgibt und abgebrochen wird, löst der Operator `await` erneut eine <xref:System.OperationCanceledException> aus.  
  
Eine einzelne Aufgabe, die einen Fehlerzustand aufweist, kann verschiedene Ausnahmen auslösen. Beispielsweise kann die Aufgabe das Ergebnis eines Aufrufs an <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> sein. Wenn Sie auf eine solche Aufgabe warten, löst die await-Operation nur eine der Ausnahmen erneut aus. Sie können jedoch nicht vorhersagen, welche der Ausnahmen erneut ausgelöst wird.  
  
Beispiele für die Fehlerbehandlung in asynchronen Methoden finden Sie unter [try-catch](../../../csharp/language-reference/keywords/try-catch.md).  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird die Gesamtzahl der Zeichen auf den Seiten zurückgegeben, deren URLs als Befehlszeilenargumente übergeben werden. Im Beispiel wird die Methode `GetPageLengthsAsync` aufgerufen, die mit dem Schlüsselwort `async` gekennzeichnet ist. Die Methode `GetPageLengthsAsync` verwendet wiederum das Schlüsselwort `await`, um auf Aufrufe der Methode <xref:System.Net.Http.HttpClient.GetStringAsync%2A?displayProperty=fullName> zu warten.  

[!code-cs[await-Beispiel](../../../../samples/snippets/csharp/language-reference/keywords/await/await2.cs)]  

Da die Verwendung von `async` und `await` an einem Anwendungseinstiegspunkt nicht unterstützt wird, kann das `async`-Attribut nicht auf die `Main`-Methode angewendet werden und es kann auch nicht auf den Methodenaufruf `GetPageLengthsAsync` gewartet werden. Es kann sichergestellt werden, dass die `Main`-Methode auf den Abschluss des asynchronen Vorgangs wartet, indem der Wert der Eigenschaft <xref:System.Threading.Tasks.Task%601.Result?displayProperty=fullName> abgerufen wird. Bei Aufgaben, die keinen Wert zurückgeben, wird die Methode <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=fullName> aufgerufen. 

## <a name="see-also"></a>Siehe auch  
[Asynchrone Programmierung mit Async und Await](../../../csharp/programming-guide/concepts/async/index.md)   
[Exemplarische Vorgehensweise: Zugreifen auf das Web mit Async und Await](../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
[async](../../../csharp/language-reference/keywords/async.md)

