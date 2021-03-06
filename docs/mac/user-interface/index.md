---
title: элементы управления интерфейса пользователя macOS в Xamarin.Mac
description: Этот документ содержит ссылки на руководства, описывающие различные элементы управления пользовательского интерфейса для разработчиков Xamarin.Mac. Связанное содержимое смотрит на windows, диалоговые окна, оповещения, меню, панелей инструментов, представления таблиц, представления структуры и многое другое.
ms.prod: xamarin
ms.assetid: 876B6EC2-E158-43F2-B9C9-03F54F3D2A49
ms.technology: xamarin-mac
author: lobrien
ms.author: laobri
ms.date: 03/27/2018
ms.openlocfilehash: a12553cf0b7b9584bb8ff7bc04ed326ad4a7ad2a
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61281601"
---
# <a name="macos-user-interface-controls-in-xamarinmac"></a>элементы управления интерфейса пользователя macOS в Xamarin.Mac

_Этой статье приведены ссылки на руководства, описывающие различные элементы управления пользовательского интерфейса macOS._

При работе с C# и .NET в приложении Xamarin.Mac, у вас есть доступ к тем же пользователем элементы управления интерфейса, работающий в *Objective-C* и *Xcode* does. Поскольку Xamarin.Mac напрямую интегрируется с Xcode, можно использовать конструктор _Interface Builder_ для создания и поддержания интерфейсов пользователя (или при необходимости создать их непосредственно в коде C#).

Перечисленных ниже руководствах подробные сведения о работе с элементами пользовательского интерфейса macOS в приложении Xamarin.Mac. Настоятельно рекомендуется работать через [Привет, Mac](~/mac/get-started/hello-mac.md) статьи, во-первых, в частности [введение в Xcode и конструкторе Interface Builder](~/mac/get-started/hello-mac.md#introduction-to-xcode-and-interface-builder) и [переменных экземпляров и действий](~/mac/get-started/hello-mac.md#outlets-and-actions) разделы, так как он рассматриваются основные понятия и методы, которые мы будем использовать в каждой статье.

Может потребоваться взгляните на [предоставление C# классы / методы Objective-c](~/mac/internals/how-it-works.md#exposing-c-classes--methods-to-objective-c) раздел [структуре Xamarin.Mac](~/mac/internals/how-it-works.md) документов, как он объясняет `Register` и `Export` атрибуты, используемые для передачи классов C# в службе Objective-C объекты и элементы пользовательского интерфейса.

## <a name="windowsmacuser-interfacewindowmd"></a>[Windows](~/mac/user-interface/window.md)

В этой статье рассматривается работа с окнами и панелями в приложении Xamarin.Mac. Он охватывает, создании и обслуживании окон и панелей в Xcode и конструктор Interface Builder, загрузка windows и панелей из .storyboard или .xib файлов, с помощью windows и реагирование на окна в коде C#.

## <a name="dialogsmacuser-interfacedialogmd"></a>[Диалоговые окна](~/mac/user-interface/dialog.md)

В этой статье рассматривается работа с диалоговыми и модальными окнами в приложении Xamarin.Mac. Он о создании и обслуживании модальных окон в Xcode и конструкторе Interface Builder, работа со стандартными диалоговыми окнами, отображение и реагирование на окна в коде C#.

## <a name="alertsmacuser-interfacealertmd"></a>[Оповещения](~/mac/user-interface/alert.md)

В этой статье рассматривается работа с оповещениями в приложении Xamarin.Mac. Он охватывает Создание и отображение оповещений из кода C# и реагирование на оповещения.

## <a name="menusmacuser-interfacemenumd"></a>[Меню](~/mac/user-interface/menu.md)

Меню используются в различных частях пользовательского интерфейса приложения Mac; приложения в главном меню в верхней части экрана, чтобы всплывающих меню и контекстные меню, которые могут находиться в любом месте окна. Меню — неотъемлемая часть пользовательского интерфейса приложений Mac. В этой статье рассматривается работа с меню Cocoa в приложении Xamarin.Mac.

## <a name="standard-controlsmacuser-interfacestandard-controlsmd"></a>[Стандартные элементы управления](~/mac/user-interface/standard-controls.md)

Работа с стандартных элементов управления AppKit, таких как кнопки, метки, текстовые поля, флажки и Сегментированные элементы управления в приложении Xamarin.Mac. В этом руководстве описывается добавление пользовательского интерфейса в конструктора Interface Builder, написанному для кода с помощью переменных экземпляров и действий и работа с элементами управления AppKit в коде C#.

## <a name="toolbarsmacuser-interfacetoolbarmd"></a>[Панели инструментов](~/mac/user-interface/toolbar.md)

В этой статье рассматривается работа с панелями инструментов в приложении Xamarin.Mac. Он о создании и обслуживании панелей инструментов в Xcode и конструктор Interface Builder, предоставлении элементов панели инструментов в код с помощью переменных экземпляров и действий, включении и отключении элементов панелей инструментов и реагировании на элементы панели инструментов в коде C#.

## <a name="table-viewsmacuser-interfacetable-viewmd"></a>[Представления таблиц](~/mac/user-interface/table-view.md)

В этой статье рассматривается работа с представлениями таблиц в приложении Xamarin.Mac. Он о создании и обслуживании представлений таблиц в Xcode и конструктор Interface Builder, как предоставлять таблицы представления элементов в коде с помощью переменных экземпляров и действий, заполнении представлений таблиц и реагирование на элементы представлений таблиц в коде C#.

## <a name="outline-viewsmacuser-interfaceoutline-viewmd"></a>[Представления структуры](~/mac/user-interface/outline-view.md)

В этой статье рассматривается работа с представлениями структур в приложении Xamarin.Mac. Он о создании и обслуживании представлений структур в Xcode и конструктор Interface Builder, как предоставить представление структуры элементов в коде с помощью переменных экземпляров и действий, заполнении представления структуры и реагирование на структуры Просмотр элементов в коде C#.

## <a name="source-listsmacuser-interfacesource-listmd"></a>[Списки источников](~/mac/user-interface/source-list.md)

В этой статье рассматривается работа с списки-источники в приложении Xamarin.Mac. Здесь рассматривается создание и обслуживание списки-источники в Xcode и конструктор Interface Builder, предоставлении элементов списков источников в код с помощью переменных экземпляров и действий, заполнении списки-источники и отвечать на элементы списков источников в коде C#.

## <a name="collection-viewsmacuser-interfacecollection-viewmd"></a>[Представления коллекций](~/mac/user-interface/collection-view.md)

В этой статье рассматривается работа с представлениями коллекции в приложении Xamarin.Mac. Он о создании и обслуживании представлений коллекций в Xcode и конструктор Interface Builder, как предоставлять представления коллекции элементов в коде с помощью переменных экземпляров и действий, заполнении представлений коллекций и отвечать на запросы к представлениям коллекции в коде C#.

## <a name="creating-custom-controlsmacuser-interfacecustom-controlsmd"></a>[Создание пользовательских элементов управления](~/mac/user-interface/custom-controls.md)

В этой статье описано, как создавать пользовательские элементы управления интерфейса (путем наследования от `NSControl`), рисование пользовательского интерфейса для элемента управления и создания настраиваемых действий, которые могут использоваться с помощью конструктора Interface Builder.

## <a name="mac-samples-gallery"></a>Коллекции примеров Mac

Кроме того, рекомендуется рассмотреть [коллекции примеров Mac](https://developer.xamarin.com/samples/mac/all/). Он включает в себя множество готовых к использованию кода, которые помогут вам быстро приступить к работе проект Xamarin.Mac.

## <a name="related-links"></a>Связанные ссылки

- [Рекомендации по созданию пользовательских интерфейсов в macOS](https://developer.apple.com/macos/human-interface-guidelines/overview/themes/)
