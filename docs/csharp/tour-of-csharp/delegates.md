---
title: "C#-Delegaten – Überblick über C#"
description: "Hier lernen Sie späte Bindungen mit C#-Delegaten kennen."
keywords: ".NET, csharp, Delegat, Lambda, späte Bindung"
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 3cc27357-3ac2-43a1-aad0-86a77b88f884
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: bb304b2e5c762a44aab931b5e8f7fe9c99805eba
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---

# <a name="delegates"></a>Delegaten

Ein ***Delegattyp*** stellt Verweise auf Methoden mit einer bestimmten Parameterliste und dem Rückgabetyp dar. Delegate ermöglichen die Behandlung von Methoden als Entitäten, die Variablen zugewiesen und als Parameter übergeben werden können. Delegate ähneln dem Konzept von Funktionszeigern, die Sie in einigen anderen Sprachen finden. Im Gegensatz zu Funktionszeigern sind Delegate allerdings objektorientiert und typsicher.

Im folgenden Beispiel wird ein Delegattyp namens `Function` deklariert und verwendet.

[!code-csharp[DelegateExample](../../../samples/snippets/csharp/tour/delegates/Program.cs#L3-L37)]

Eine Instanz des Delegattyps `Function` kann auf jede Methode verweisen, die ein `double`-Argument und einen `double`-Wert akzeptiert. Die `Apply`-Methode wendet eine bestimmte Funktion auf die Elemente eines `double[]` an, wobei ein `double[]` mit den Ergebnissen zurückgegeben wird. In der `Main`-Methode wird `Apply` verwendet, um drei verschiedene Funktionen auf ein `double[]` anzuwenden.

Ein Delegat kann entweder auf eine statische Methode verweisen (z.B. `Square` oder `Math.Sin` im vorherigen Beispiel) oder eine Instanzmethode (z.B. `m.Multiply` im vorherigen Beispiel). Ein Delegat, der auf eine Instanzmethode verweist, verweist auch auf ein bestimmtes Objekt, und wenn die Instanzmethode durch den Delegaten aufgerufen wird, wird das Objekt `this` im Aufruf.

Delegaten können auch mit anonymen Funktionen erstellt werden, die dynamisch erstellte „Inlinemethoden“ sind. Anonyme Funktionen können die lokalen Variablen der umgebenden Methoden sehen. Folglich kann das obige Multiplikatorbeispiel ohne Verwendung einer Multiplikatorklasse leichter geschrieben werden:

[!code-csharp[LambdaExample](../../../samples/snippets/csharp/tour/delegates/Program.cs#L44-L44)]

Eine interessante und nützliche Eigenschaft eines Delegaten ist, dass er die Klasse der Methode, auf die er verweist, nicht kennt oder sie ignoriert; wichtig ist nur, dass die referenzierte Methode die gleichen Parameter und den gleichen Rückgabetyp hat wie der Delegat.

>[!div class="step-by-step"]
[Zurück](enums.md)
[Weiter](attributes.md)

