---
title: Обработка сенсорного ввода в приложениях Xamarin.iOS
description: Этот документ содержит ссылки на руководства, описывающие способы работы с сенсорного ввода, мультисенсорный ввод, жесты и 3D Touch в приложении Xamarin.iOS.
ms.prod: xamarin
ms.assetid: E3904713-6018-4755-A315-EB045DFB3500
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 01/23/2017
ms.openlocfilehash: 5aabc3a3c2ffbcffc0e12379989f7eb43b03a902
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61399295"
---
# <a name="handling-touch-in-xamarinios-apps"></a>Обработка сенсорного ввода в приложениях Xamarin.iOS

Как и другие мобильные платформы iOS имеет ряд способов обработки сенсорного ввода. Может поддерживать мультисенсорные — много точек контакта на экране и сложные жестов. В этом руководстве представлены некоторые основные понятия, а также particularities реализации касания и жестов в iOS.

iOS инкапсулирует сенсорные данные в `UITouch` класс, который будет предоставляться доступ для приложений с помощью ряда `UIResponder` методы. Приложения можно переопределить эти методы в подклассах класса `UIView` и `UIViewController`, из которых являются производными от `UIResponder`.

Кроме фиксирования сенсорные данные, iOS предоставляет средства для интерпретации шаблоны штрихи в жестов. Эти средства распознавания жестов в свою очередь может использоваться для интерпретации команд конкретного приложения, таких как поворот изображения или укажите директиву страницы. iOS предоставляет широкий набор классов для обработки распространенных жесты минимальное требует добавления кода.

Выбор между штрихи и средства распознавания жестов может быть запутанным. Данное руководство рекомендует, как правило, предпочтение следует уделять распознавателей жестов. Средства распознавания жестов, реализуются как дискретные классы, которые предоставляют больше разделения проблем и улучшенную инкапсуляцию. Это упрощает для совместного использования логики между различными представлениями, сводя к минимуму объем кода, написанного.

Однако бывают случаи, когда необходимо использовать обработку низкоуровневых сенсорного ввода и даже отслеживания нескольких пальцев, например, для создания программы finger-paint.

## <a name="sections"></a>Разделы

-  [Сенсорные технологии в iOS](touch-in-ios.md)
-  [Пошаговое руководство: использование сенсорного ввода в iOS](ios-touch-walkthrough.md)
-  [Мультисенсорное отслеживание](touch-tracking.md)

Данное руководство служит краткое описание сенсорного ввода в iOS. Дополнительные сведения об использовании в iOS 3D Touch и обратной связи Haptic которого были введены в iOS 9 и 10 соответственно см. в конкретных приведенных ниже руководствах:

* [Трехмерные сенсорные технологии](~/ios/platform/3d-touch.md)
* [Обеспечение обратной связи Haptic](~/ios/user-interface/ios-ui/haptic-feedback.md)

## <a name="related-links"></a>Связанные ссылки

- [iOS Touch запустить (пример)](https://developer.xamarin.com/samples/monotouch/ApplicationFundamentals/Touch_start)
- [iOS Touch окончательный (пример)](https://developer.xamarin.com/samples/monotouch/ApplicationFundamentals/Touch_final)
- [FingerPaint (пример)](https://developer.xamarin.com/samples/monotouch/ApplicationFundamentals/FingerPaint)
