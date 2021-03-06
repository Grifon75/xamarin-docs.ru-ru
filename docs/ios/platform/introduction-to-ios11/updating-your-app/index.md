---
title: Обновление приложения до iOS 11
description: Этот документ содержит ссылки на различные руководства, описывающие новые возможности, доступные для разработчиков Xamarin.iOS с версией iOS 11. Например изменяет App Store обновления визуального проектирования, и обновляет значка приложения.
ms.prod: xamarin
ms.assetid: EC809504-9CF6-4949-B6EE-36384297E744
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 09/13/2016
ms.openlocfilehash: 3193f27c30080a4335abfe969acb3c8b33516469
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61386357"
---
# <a name="updating-your-app-to-ios-11"></a>Обновление приложения до iOS 11

В iOS 11 Apple представила архитектуру обновления, новые визуальные изменения и процесс обновленные iTunes Connect. В этом руководстве описано каждое из этих изменений, помогая обновлены для iOS 11 в приложении Xamarin.iOS.

## <a name="architecture-changesarchitecture-changesmd"></a>[Изменения архитектуры](architecture-changes.md)

Одно из самых существенных изменений, которые следует учитывать с iOS 11 будет вывод поддержки 32-разрядных приложений, как описано в [Apple](https://developer.apple.com/news/?id=06282017b) пресс-релизе.

Это руководство поможет выполнить обновление приложения для 64-разрядных систем.

## <a name="visual-design-updatesvisual-designmd"></a>[Обновления визуального проектирования](visual-design.md)

В iOS 11 Apple представила новые визуальные изменения, включая обновления для панели навигации, панель поиска и представления таблицы. Кроме были улучшены для обеспечения дополнительной гибкости поля и содержимое во весь экран. В этом руководстве рассматриваются эти изменения.

## <a name="app-store-changesapp-store-changesmd"></a>[Изменения магазина приложений](app-store-changes.md)

IOS App Store была полной переработки, который не только позволяет пользователям эффективно перемещаться в хранилище, но также позволяет вам, как разработчик, повышение уровня приложения для пользователей. Эти promotions включать обновления для покупки из приложений и обновлений на страницу продуктов. iOS 11 также добавляет обновления, касающиеся способ взаимодействия с пользователями, как добавить значок приложения и как опубликовать приложение для просмотра.

## <a name="app-icon-updates"></a>Обновляет значок приложения

> [!NOTE]
> Значки приложений теперь должно быть доставлено по _каталог активов_. 

Дополнительные сведения об использовании каталоги активов см. [значок App Store](~/ios/app-fundamentals/images-icons/app-store-icon.md) руководства. Для получения справки по миграции значки с Info.plist в каталог ресурсов, см. в разделе [переход с Info.plist на каталоги активов](~/ios/app-fundamentals/images-icons/app-icons.md) руководства.

Значок "обязательно" в каталоге ресурсов называется **App Store** и должны быть размером 1024 x 1024. В соответствии с требованиями Apple значок App Store в каталоге ресурсов не может быть прозрачным и не должен содержать альфа-канал.

![Приложение сохранять расположение значка в каталог ресурсов.](images/image1.png)

## <a name="related-links"></a>Связанные ссылки

- [Новые возможности в iOS 11 (Apple)](https://developer.apple.com/ios/)
- [Страница продукта обновленные App Store (Apple)](https://developer.apple.com/app-store/product-page/)
- [Обновление приложения для iOS 11 (WWDC) (видео)](https://developer.apple.com/videos/play/wwdc2017/204/)
