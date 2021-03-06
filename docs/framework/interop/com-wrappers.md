---
title: "COM Wrappers | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "wrapper classes"
  - "COM interop, COM wrappers"
  - "COM wrappers"
  - "COM, wrappers"
  - "interoperation with unmanaged code, COM wrappers"
  - "COM callable wrappers"
ms.assetid: e56c485b-6b67-4345-8e66-fd21835a6092
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# COM Wrappers
Модель объектов COM отличается от модели .NET Framework по нескольким важным пунктам:  
  
-   Клиенты COM\-объектов должны управлять этими объектами в течение всего времени их существования, а среда CLR самостоятельно управляет объектами в течение всего времени их существования в этой среде.  
  
-   Клиенты COM\-объектов определяют доступность службы по тому, получат ли они указатель интерфейса, запросив интерфейс, предоставляющий соответствующую службу, или нет.  Клиенты объектов .NET могут получить описание функциональных возможностей объекта с помощью отражения.  
  
-   Объекты .NET размещаются в памяти, управляемой средой выполнения .NET Framework.  Среда выполнения может перемещать объекты внутри памяти с целью оптимизации производительности и обновлять все ссылки на перемещаемые объекты.  Неуправляемые клиенты, получив указатель на объект, считают, что данный объект все время находится в одном и том же месте.  У этих клиентов отсутствует механизм работы с объектом, не имеющим постоянного местоположения.  
  
 Чтобы преодолеть указанные отличия, среда выполнения содержит классы оболочек, которые заставляют как управляемые, так и неуправляемые клиенты полагать, что они вызывают объекты в своих собственных средах.  Когда управляющий клиент вызывает метод для COM\-объекта, среда выполнения создает [вызываемую оболочку времени выполнения](../../../docs/framework/interop/runtime-callable-wrapper.md).  Вызываемые оболочки времени выполнения помимо других функций абстрагируют различия между ссылочными механизмами управляемых и неуправляемых объектов.  Среда выполнения также создает [вызываемую оболочку COM](../../../docs/framework/interop/com-callable-wrapper.md) для обращения процесса, позволяя COM\-клиенту легко вызвать метод в объекте .NET.  Как показано на следующем рисунке, вызывающий код определяет класс оболочек, создаваемый средой выполнения.  
  
 ![Общие сведения об оболочках COM](../../../docs/framework/interop/media/bidirectional.gif "bidirectional")  
Общие сведения об оболочках COM  
  
 В большинстве случаев стандартная вызываемая оболочка времени выполнения или вызываемая оболочка COM, созданная средой выполнения, обеспечивает соответствующий маршалинг вызовов, пересекающих границу между средами COM и .NET Framework.  Использование пользовательских атрибутов позволяет настроить способ представления средой выполнения управляемого и неуправляемого кода.  
  
## См. также  
 [Advanced COM Interoperability](http://msdn.microsoft.com/ru-ru/3ada36e5-2390-4d70-b490-6ad8de92f2fb)   
 [Runtime Callable Wrapper](../../../docs/framework/interop/runtime-callable-wrapper.md)   
 [COM Callable Wrapper](../../../docs/framework/interop/com-callable-wrapper.md)   
 [Customizing Standard Wrappers](http://msdn.microsoft.com/ru-ru/c40d089b-6a3c-41b5-a20d-d760c215e49d)   
 [How to: Customize Runtime Callable Wrappers](http://msdn.microsoft.com/ru-ru/4a4bb3da-4d60-4517-99f2-78d46a681732)