---
title: 'Xamarin.Essentials: VersionTracking'
description: Класс VersionTracking в Xamarin.Essentials позволяет проверить версию и номера сборки приложений, а также просмотреть дополнительные сведения, например, запущено ли приложение впервые или получение сведений о предыдущей сборке для текущей версии и многое другое.
ms.assetid: 670C7E8A-E882-4AC0-97D2-A53D90ADD6A3
author: jamesmontemagno
ms.author: jamont
ms.date: 11/04/2018
ms.openlocfilehash: 7d3877577523ed17c78fd5d2ad02923bd3d821e2
ms.sourcegitcommit: 01f93a34b466f8d4043cef68fab9b35cd8decee6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2018
ms.locfileid: "52898843"
---
# <a name="xamarinessentials-version-tracking"></a>Xamarin.Essentials: VersionTracking

Класс **VersionTracking** позволяет проверить версию и номера сборки приложений, а также просмотреть дополнительные сведения, например, запущено ли приложение впервые или получение сведений о предыдущей сборке для текущей версии и многое другое.

## <a name="get-started"></a>Начало работы

[!include[](~/essentials/includes/get-started.md)]

## <a name="using-version-tracking"></a>Использование VersionTracking

Добавьте в свой класс ссылку на Xamarin.Essentials:

```csharp
using Xamarin.Essentials;
```

При первом использовании класса **VersionTracking** он начнет отслеживание текущей версии. Необходимо вызывать `Track` заранее только при каждой загрузке приложения, чтобы убедиться, что сведения о текущей версии отслеживаются.

```csharp
VersionTracking.Track();
```

После первоначального вызова `Track` сведения о версии можно считывать:

```csharp

// First time ever launched application
var firstLaunch = VersionTracking.IsFirstLaunchEver;

// First time launching current version
var firstLaunchCurrent = VersionTracking.IsFirstLaunchForCurrentVersion;

// First time launching current build
var firstLaunchBuild = VersionTracking.IsFirstLaunchForCurrentBuild;

// Current app version (2.0.0)
var currentVersion = VersionTracking.CurrentVersion;

// Current build (2)
var currentBuild = VersionTracking.CurrentBuild;

// Previous app version (1.0.0)
var previousVersion = VersionTracking.PreviousVersion;

// Previous app build (1)
var previousBuild = VersionTracking.PreviousBuild;

// First version of app installed (1.0.0)
var firstVersion = VersionTracking.FirstInstalledVersion;

// First build of app installed (1)
var firstBuild = VersionTracking.FirstInstalledBuild;

// List of versions installed (1.0.0, 2.0.0)
var versionHistory = VersionTracking.VersionHistory;

// List of builds installed (1, 2)
var buildHistory = VersionTracking.BuildHistory;
```

## <a name="platform-implementation-specifics"></a>Особенности реализации для платформ

Все сведения о версии сохраняются с помощью API [параметров](preferences.md) в Xamarin.Essentials с именем файла **[YOUR-APP-PACKAGE-ID].xamarinessentials.versiontracking**. Режим сохранения данных соответствует описанному в документации о [параметрах](preferences.md#persistence).

## <a name="api"></a>API

- [Исходный код для отслеживания версий](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/VersionTracking)
- [Документация по API отслеживания версий](xref:Xamarin.Essentials.VersionTracking)
