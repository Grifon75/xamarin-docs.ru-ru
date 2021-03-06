---
title: Расширения платформы Xamarin.Essentials
description: Xamarin.Essentials предоставляет несколько методов расширения платформы при работе с такими типами платформы, как Rect, Size и Point.
ms.assetid: AB4D198A-4FD7-479E-8627-01F887A6D056
author: jamesmontemagno
ms.author: jamont
ms.date: 03/13/2019
ms.openlocfilehash: 740f6f4658c3e840f73261f554eb330ee02edb5d
ms.sourcegitcommit: 5d4e6677224971e2bc0268f405d192d0358c74b8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/21/2019
ms.locfileid: "58329069"
---
# <a name="xamarinessentials-platform-extensions"></a>Xamarin.Essentials: расширения платформы

Xamarin.Essentials предоставляет несколько методов расширения платформы при работе с такими типами платформы, как Rect, Size и Point. Это означает, что можно осуществлять преобразование между версией `System` этих типов для их конкретных типов в iOS, Android и UWP. 

## <a name="get-started"></a>Начало работы

[!include[](~/essentials/includes/get-started.md)]

## <a name="using-platform-extensions"></a>Использование расширений платформы

Добавьте в свой класс ссылку на Xamarin.Essentials:

```csharp
using Xamarin.Essentials;
```

Все расширения платформы могут вызываться только из проектов iOS, Android или UWP.

### <a name="point"></a>Точка

```csharp
var system = new System.Drawing.Point(x, y);

// Convert to CoreGraphics.CGPoint, Android.Graphics.Point, and Windows.Foundation.Point
var platform = system.ToPlatformSize();

// Back to System.Drawing.Size
var system2 = platform.ToSystemSize();
```

### <a name="size"></a>Размер

```csharp
var system = new System.Drawing.Size(width, height);

// Convert to CoreGraphics.CGSize, Android.Util.Size, and Windows.Foundation.Size
var platform = system.ToPlatformSize();

// Back to System.Drawing.Size
var system2 = platform.ToSystemSize();
```

### <a name="rectangle"></a>Прямоугольник

```csharp
var system = new System.Drawing.Rectangle(x, y, width, height);

// Convert to CoreGraphics.CGRect, Android.Graphics.Rect, and Windows.Foundation.Rect
var platform = system.ToPlatformSize();

// Back to System.Drawing.Size
var system2 = platform.ToSystemSize();
```

## <a name="api"></a>API

- [Исходный код преобразователей](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Types/PlatformExtensions)
- [Документация по API преобразователей точек](xref:Xamarin.Essentials.PointExtensions)
- [Документация по API преобразователей прямоугольника](xref:Xamarin.Essentials.RectangleExtensions)
- [Документация по API преобразователей размера](xref:Xamarin.Essentials.SizeExtensions)
