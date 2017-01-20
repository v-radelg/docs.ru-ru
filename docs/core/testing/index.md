---
title: "Модульное тестирование в .NET Core"
description: "Модульное тестирование в .NET Core"
keywords: .NET, .NET Core
author: ardalis
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 815ac74c-4bd9-4a94-a87c-78288b27c0e2
translationtype: Human Translation
ms.sourcegitcommit: 352d4a1fe96b701ebf9e0d60d006cfb9ed77977c
ms.openlocfilehash: e7cc50bd4ab9e5ef008639f70d9e827b349d5b3e

---

# <a name="unit-testing-in-net-core"></a>Модульное тестирование в .NET Core

Авторы: [Стив Смит](http://ardalis.com) (Steve Smith) и [Билл Вагнер](https://github.com/BillWagner) (Bill Wagner)

При разработке платформы .NET Core учитывались возможности тестирования, поэтому создавать модульные тесты для приложений стало еще проще. В этой статье вкратце рассматриваются модульные тесты (и то, чем они отличаются от других типов тестов).
В связанных ресурсах демонстрируется, как добавить тестовый проект в решение и как затем выполнять модульные тесты с помощью командной строки или Visual Studio.

## <a name="getting-started-with-testing"></a>Приступая к тестированию
 
Наличие набора автоматических тестов — один из лучших способов обеспечить работу приложения именно так, как она задумывалась разработчиками. Существует множество различных типов тестов для приложений, включая тесты интеграции, веб-тесты, нагрузочные тесты и т. д. На самом низком уровне применяются модульные тесты, которые проверяют отдельные компоненты или методы программного обеспечения. Модульные тесты должны применяться только к коду, находящемуся под контролем разработчика, но не к компонентам инфраструктуры, таким как базы данных, файловые системы или сетевые ресурсы. Модульные тесты можно создавать в рамках [разработки на основе тестирования (TDD)](http://deviq.com/test-driven-development/) или добавлять в существующий код для проверки его правильности. В любом случае они должны быть небольшими, иметь понятные имена и выполняться быстро, так как в идеале у вас должна быть возможность выполнить сотни таких тестов перед публикацией изменений в репозитории общего кода проекта.

> [!NOTE]
> У разработчиков часто возникают проблемы с тем, чтобы придумать подходящие имена для тестовых классов и методов. В качестве отправной точки команда разработчиков ASP.NET следует [этим соглашениям](https://github.com/aspnet/Home/wiki/Engineering-guidelines#unit-tests-and-functional-tests).

При создании модульных тестов будьте внимательны, чтобы случайно не добавить зависимости от инфраструктуры. Из-за них тесты, как правило, выполняются медленнее и менее стабильно и их следует зарезервировать для тестов интеграции. Чтобы избежать скрытых зависимостей в коде приложения, следуйте [принципу явных зависимостей](http://deviq.com/explicit-dependencies-principle/) и используйте [внедрение зависимостей](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection) для запроса зависимостей из платформы. Кроме того, можно выделить модульные тесты в отдельный проект, изолировав их от тестов интеграции, чтобы гарантировать отсутствие в этом проекте ссылок на пакеты инфраструктуры или зависимостей от них.

Дополнительные сведения о модульном тестировании в проектах .NET Core:

Воспользуйтесь этим [пошаговым руководством по созданию модульных тестов с помощью xUnit и CLI .NET](unit-testing-with-dotnet-test.md).

Команда разработчиков XUnit написала учебник, в котором показано ,как [использовать xUnit с помощью .NET Core и Visual Studio](http://xunit.github.io/docs/getting-started-dotnet-core.html).



<!--HONumber=Nov16_HO3-->

