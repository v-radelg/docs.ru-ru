---
title: Expression Trees
description: Expression Trees
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: aceb4719-0d5a-4b19-b01f-b51063bcc54f
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e6ec60b6cdbe29def719f7970dad15fad65902e7
ms.lasthandoff: 03/13/2017

---

# <a name="expression-trees"></a>Expression Trees

Если вы использовали LINQ, то у вас есть опыт работы с полнофункциональной библиотекой, в которой типы `Func` являются частью набора API. (Если вы не работали с LINQ, то перед чтением этого раздела рекомендуем ознакомиться с учебниками по [LINQ](linq/index.md) и [лямбда-выражениям](lambda-expressions.md).) *Деревья выражений* обеспечивают более широкие возможности взаимодействия с аргументами, являющимися функциями.

Аргументы функции применяются (как правило, с помощью лямбда-выражений) при создании запросов LINQ. В типичном запросе LINQ аргументы функции преобразуются в делегат, создаваемый компилятором. 

Если требуются более широкие возможности взаимодействия, необходимо использовать *деревья выражений*.
Деревья выражений представляют код в виде структуры, которую можно анализировать, изменять или выполнять. Это дает возможность управлять кодом во время выполнения. Вы можете написать код, который анализирует выполняющиеся алгоритмы или добавляет новые возможности. В более сложных сценариях вы можете изменять выполняющиеся алгоритмы и даже преобразовывать выражения C# в иную форму для выполнения в другой среде.

Вероятно, вы уже писали код, в котором используются деревья выражений. Интерфейсы API LINQ платформы Entity Framework принимают деревья выражений в качестве аргументов для модели выражений запросов LINQ.
Это позволяет платформе [Entity Framework](http://docs.efproject.net/en/latest/) преобразовывать запросы, написанные на C#, в код SQL, который выполняется в ядре СУБД. Другим примером является [Moq](https://github.com/Moq/moq) — популярная платформа прототипирования для .NET.

В дальнейших разделах этого учебника описывается, что представляют собой деревья выражений, рассматриваются поддерживающие их классы платформы и демонстрируются способы работы с деревьями выражений. Вы узнаете, как считывать деревья выражений, как создавать их, а также как создавать модифицированные деревья выражений и выполнять код, представленный деревьями выражений. После ознакомления с учебником вы будете готовы к использованию этих структур для создания эффективных адаптивных алгоритмов.
<style type="text/css"> ol { list-style-type: upper-roman; } </style>
1. [Описание деревьев выражений](expression-trees-explained.md)

    Understand the structure and concepts behind *Expression Trees*.
    
2. [Типы платформ, поддерживающие деревья выражений](expression-classes.md)
    
    Сведения о структурах и классах, которые служат для определения деревьев выражений и управления ими.
    
3. [Выполнение выражений](expression-trees-execution.md)

    Сведения о том, как преобразовать дерево выражения, представленное как лямбда-выражение, в делегат и как выполнить полученный делегат.

4. [Интерпретация выражений](expression-trees-interpreting.md)

    Сведения об обходе и анализе *деревьев выражений* для получения представления о том, какой код они представляют.

5. [Построение выражений](expression-trees-building.md)

    Сведения о построении узлов для дерева выражения и сборке деревьев выражений.

6. [Преобразование выражений](expression-trees-translating.md)

    Сведения о создании измененной копии дерева выражения или преобразовании дерева выражения в другой формат.

7. [Заключение](expression-trees-summary.md)

    Сводные сведения о деревьях выражений.
    
