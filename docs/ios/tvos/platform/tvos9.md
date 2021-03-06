---
title: Введение в tvOS 9
description: В этой статье рассматриваются все новые и измененные API-интерфейсы и функции, доступные в tvOS 9 для разработчиков Xamarin.tvOS.
ms.prod: xamarin
ms.assetid: A7E738E1-9F94-489B-918F-7DF8F0810987
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 06/07/2016
ms.openlocfilehash: dda197f71b2a2ab3e0d61a838ab85d79b7a078c7
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61270350"
---
# <a name="introduction-to-tvos-9"></a>Введение в tvOS 9

_В этой статье рассматриваются все новые и измененные API-интерфейсы и функции, доступные в tvOS 9 для разработчиков Xamarin.tvOS._

Apple выпустила четвертого поколения оборудования Apple TV с модернизированный, удаленный с поддержкой сенсорного ввода, новый tvOS операционной системой (с учетом iOS 9).

В первый раз tvOS откроется на платформе Apple TV, которое разработчик, что позволяет создавать полнофункциональные приложения и публикуйте их через Store встроенных приложений Apple большом в процесс аналогичен опыт написания и освобождение приложений для iOS с помощью iTunes App Store.

Если вы знакомы с разработкой приложений Xamarin.iOS, вы увидите, переход на tvOS довольно прост. Большинство API-интерфейсов и компонентов совпадают, однако многие общие интерфейсы API недоступны (например, WebKit). Кроме того, работаете с удаленной Siri создает некоторые трудности разработки, которые отсутствуют в сенсорный экран на основе устройств iOS.

В этом руководстве будет дается введение в все новые и измененные API-интерфейсы и функции, доступные в tvOS 9 для разработчиков Xamarin.tvOS. Дополнительные сведения о tvOS, см. в разделе Apple [разработка для новой Apple TV](https://developer.apple.com/tvos/) документации.

<a name="Supported-and-Unsupported-Capabilities" />

## <a name="supported-and-unsupported-capabilities"></a>Поддерживаемые и неподдерживаемые возможности

приложения tvOS, работающие на Apple TV следующие поддерживаемые возможности и функции:

 - Группы приложений
 - Фоновые режимы
 - Защита данных
 - Game Center
 - Игровые устройства управления
 - iCloud
 - Покупки из приложений
 - Обмен связками ключей

Не поддерживаются следующие функции и возможности:

 - Apple Pay
 - "Песочница" приложений
 - Связанные домены
 - HealthKit
 - HomeKit
 - Звук между приложениями
 - Карты
 - Личная VPN
 - Push-уведомления
 - Wallet
 - Конфигурация беспроводных периферийных устройств

См. наш [сборки поддерживается](~/ios/tvos/internals/assemblies.md) и [поддерживаемых платформ](~/ios/tvos/internals/frameworks.md) Дополнительные сведения см.

<a name="Apple-TV-Hardware" />

## <a name="apple-tv-hardware"></a>Apple TV оборудования

Новый Apple TV имеет следующие характеристики оборудования:

 - 64-разрядный процессор A8
 - 32 или 64 ГБ хранилища
 - 2 ГБ ОЗУ
 - 10/100 Мбит/с Ethernet
 - 802.11a/b/g/n/ac Wi-Fi
 - разрешение 1080p
 - HDMI
 - USB-порт C (для разработчиков и только для диагностики использования)
 - Новый Siri Remote или Apple TV удаленный (в зависимости от региона)

### <a name="siri-remote"></a>Siri Remote

На основе региона, предоставленный Apple TV удаленного будут поступать в либо одной конфигурации. Siri Remote или Apple TV удаленным.

Удаленное Siri в настоящее время доступна в следующих странах:

 - Австралия
 - Канада
 - Франция
 - Германия
 - Япония
 - Испания
 - Великобритания
 - США

Все остальные страны, получите Apple TV удаленного замены кнопки Siri на кнопку поиска, которая появляется на экране поиска по умолчанию с помощью ввода текста для поиска:

[![](tvos9-images/remote02.png "Siri Remote")](tvos9-images/remote02.png#lightbox)

Дополнительные сведения см. в разделе наших [контроллеры Siri Remote и контроллеры Bluetooth](~/ios/tvos/platform/remote-bluetooth.md) документации.

<a name="Apple-TV-Provisioning" />

## <a name="apple-tv-provisioning"></a>Подготовка Apple TV

Так же, как разработка приложений для iOS, новый tvOS потребуются нужный профиль подготовки для разработки и распространения, на основе членства в группах и удостоверений подписывания, уже определенными в Apple.

Правильной подготовки также необходим для доступа к функциям tvOS, такими как iCloud KVS и CloudKit данных хранилища. См. наш [ресурсы и хранилище данных](~/ios/tvos/app-fundamentals/resources-data-storage.md) информацию о поддержке iCloud в своих приложениях Xamarin.tvOS.

Профили подготовки создаются и устанавливаются так же, как работа с приложениями Xamarin.iOS. Таким образом, см. в разделе iOS [подготовки устройств](~/ios/get-started/installation/device-provisioning/index.md) документации для получения дополнительных сведений.

<a name="Apple-TV-Apps" />

## <a name="apple-tv-apps"></a>Apple ТВ-приложений

Новое оборудование Apple TV и tvOS 9 поддерживает два типа приложений: традиционные и между клиентом и сервером приложений.

<a name="Traditional-Apps" />

### <a name="traditional-apps"></a>Традиционные приложения

Традиционные приложения приобретенных у Apple TV App Store и устанавливаются непосредственно на устройстве. Эти приложения может быть играм, служебных программ или приложений мультимедиа, разработанных с помощью платформы и методики, как приложения Xamarin.iOS.

Приложения Apple TV максимальный размер 200 МБ и можно загрузить дополнительные 2 ГБ содержимого с помощью ресурсы по запросу. См. в нашем [ресурсы и хранилище данных](~/ios/tvos/app-fundamentals/resources-data-storage.md) Дополнительные сведения.

См. в разделе наших [по Tvos краткое руководство по](~/ios/tvos/get-started/hello-tvos.md) познакомиться со средствами и понятия, необходимые для разработки приложений tvOS с помощью Xamarin.tvOS.

<a name="Summary" />

### <a name="client-server-apps"></a>Между клиентом и сервером приложений

Помимо установленных традиционных приложений Apple TV упрощает создание потоковая передача клиент сервер веб-приложений с помощью веб-технологии (HTTPS, XML и JavaScript). Будет разработки пользовательского интерфейса с помощью языка разметки TVML компании Apple и использовать JavaScript для определения поведения приложения, с помощью TVMLKit.

Дополнительные сведения см. в разделе Apple [Apple TV описание языка разметки](https://developer.apple.com/library/prerelease/tvos/documentation/LanguagesUtilities/Conceptual/ATV_Template_Guide/index.html#//apple_ref/doc/uid/TP40015064), [ссылка на платформу TVJS](https://developer.apple.com/library/prerelease/tvos/documentation/TVMLJS/Reference/TVJSFrameworkReference/index.html#//apple_ref/doc/uid/TP40016076), [ссылка на платформу TVMLKit](https://developer.apple.com/library/prerelease/tvos/documentation/TVMLKit/Reference/TVMLKit_Collection/index.html#//apple_ref/doc/uid/TP40016429), [о HTTP Live Streaming](https://developer.apple.com/library/prerelease/tvos/referencelibrary/GettingStarted/AboutHTTPLiveStreaming/about/about.html#//apple_ref/doc/uid/TP40013978) и [HLS разработки спецификации для Apple TV](https://developer.apple.com/services-account/download?path=/Documentation/HLS_Authoring_Specification_for_Apple_TV/HLS_Authoring_Specification_for_Apple_TV.pdf) документации.

<a name="User-Interface-Challenges" />

## <a name="user-interface-challenges"></a>Проблемы интерфейса пользователя

В отличие от iOS или OS X Apple TV не поддерживает сенсорный экран или мыши, которые позволяют пользователю напрямую, выберите и взаимодействовать с приложения или его содержимого. Вместо этого они пользователя новых удаленных Siri или контроллере Bluetooth игры для перехода интерфейса пользователя приложения. Дополнительные сведения см. в разделе наших [контроллеры Siri Remote и контроллеры Bluetooth](~/ios/tvos/platform/remote-bluetooth.md) документации.

Кроме того эффективность работы пользователя значительно отличается от операций ввода-вывода или приложений Mac, как правило, один взаимодействия с пользователями. С помощью Apple TV пользовательские интерфейсы обычно более социальную природу, где несколько человек может располагаться на диване, взаимодействие с одним приложением или друг от друга. Чтобы разработать успешный приложения Apple TV систему (новое приложение или подключаете существующую), эти изменения необходимо принимать во внимание. 

<a name="Summary" />

### <a name="working-with-focus-and-parallax-images"></a>Работа с концентрацией и фокусировки образов

Как уже говорилось, пользователей приложения Xamarin.tvOS не будут взаимодействовать с его интерфейсом непосредственно как с помощью iOS они tap изображения на экране устройства, но косвенно из двух зала, с помощью удаленного Siri. Для представления и управления взаимодействием с пользователем, Apple TV использует модель на основе фокуса. 

При изменении фокуса элегантной анимации и эффектов (например, в образах эффекта фокусировки) используются для четкого определения элемент пользовательского интерфейса, который в данный момент имеет фокус.

Если пользователь делает жест медленно, циклические на удаленном Siri, элемент с фокусом ввода будет sway в режиме реального времени, в ответ на это перемещение. По мере sway оформленный sheen применяется к своего изображения, делая области отображаются в разметке. После заданного периода бездействия любое содержимое в фокусе out затемняется и фокуса элемента будет увеличиваться еще больше.

Дополнительные сведения см. в разделе наших [работа с навигацией и фокусом](~/ios/tvos/app-fundamentals/navigation-focus.md) и [работа со значками и изображениями](~/ios/tvos/app-fundamentals/icons-images.md) документации.

<a name="The-Home-Screen" />

### <a name="the-home-screen"></a>Начальный экран

На экране Apple TV Главная показаны все приложения, которые устанавливаются и предоставляет способ доступа к персональных настроек пользователя:

[![](tvos9-images/home01.png "Начальный экран")](tvos9-images/home01.png#lightbox)

Пользователь переходит сетку значки приложений с помощью сенсорных жестов в Siri удаленного доступа с помощью фокус, чтобы выбрать приложение и запустите его. Значок приложения — это первого вероятность впечатление отличный потенциальных пользователей и должно передавать цель вашего приложения с первого взгляда.

Каждое приложение необходимо указать небольших и больших версию значка приложения. Мелкий значок будет использоваться на экране Apple TV Главная при установке приложения. Большой версии используется App Store. Крупный значок приложения должна имитировать внешний вид версии мелкого значка.

Дополнительные сведения см. в разделе наших [работа со значками и изображениями](~/ios/tvos/app-fundamentals/icons-images.md) документации.

<a name="The-Top-Shelf" />

### <a name="the-top-shelf"></a>Верхняя Полка

Если пользователь разместил Xamarin.tvOS приложения в верхней строке на экране Apple TV Главная, при выборе пользователем приложения будет отображаться большое изображение для верхней панели. Этот образ следует ознакомиться с функциями приложения или приведены прямые ссылки на его содержимое.

[![](tvos9-images/topshelf01.png "Верхняя Полка")](tvos9-images/topshelf01.png#lightbox)

Изображение для верхней панели, либо может быть представлен в виде один статический `.png` или `.lsr` файл или его можно создать динамически во время выполнения как одна строка, способному получать фокус элементов.

Вместо отображения статических основное изображение, оно может содержать динамическая строка или элементы, способному получать фокус или динамический набор прокрутки ленты. Оба эти динамические стиля позволяют выделить содержимое, предоставляемое с приложения или переход в его наиболее часто используемых функций.

Дополнительные сведения см. в разделе наших [работа со значками и изображениями](~/ios/tvos/app-fundamentals/icons-images.md) документации и Apple [ссылка на платформу TVServices](https://developer.apple.com/library/prerelease/tvos/documentation/TVServices/Reference/TVServices_Ref/index.html#//apple_ref/doc/uid/TP40016412) Дополнительные сведения о добавлении расширение полки верхней в приложение для предоставления динамическое содержимое полки верхней.






## <a name="related-links"></a>Связанные ссылки

- [Примеры tvOS](https://developer.xamarin.com/samples/tvos/all/)
- [tvOS](https://developer.apple.com/tvos/)
- [Человека направляющие интерфейса tvOS](https://developer.apple.com/tvos/human-interface-guidelines/)
- [Приложение руководство по программированию для tvOS](https://developer.apple.com/library/prerelease/tvos/documentation/General/Conceptual/AppleTV_PG/)
- [Создание приложений для tvOS с помощью Xamarin (видео)](https://university.xamarin.com/lightninglectures/tvos-with-xamarin)
