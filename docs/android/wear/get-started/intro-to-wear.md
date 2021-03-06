---
title: Введение в Android Wear
description: С появлением Google Android Wear вы больше не ограничены только телефоны и планшеты когда дело доходит до разработки отличных приложений для Android. Поддержка Android Wear Xamarin.Android позволяет вам выполнять C# кода на запястье! В этом введении предоставляет общий обзор Android Wear, описывает ее основные компоненты и предлагает обзор возможностей, доступных в Android Wear 2.0. Он перечисляет некоторые из наиболее популярных устройств Android Wear, а также предоставляет ссылки на важную документацию по Google Android Wear для дальнейшего изучения.
ms.prod: xamarin
ms.assetid: EAEF99F0-8FBE-47E4-8644-E7244CFAF464
ms.technology: xamarin-android
author: conceptdev
ms.author: crdun
ms.date: 03/01/2018
ms.openlocfilehash: a35cb82f4f6d20e91f45a782c73d3ef811947c3a
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61284251"
---
# <a name="introduction-to-android-wear"></a>Введение в Android Wear

_С появлением Google Android Wear вы больше не ограничены только телефоны и планшеты когда дело доходит до разработки отличных приложений для Android. Поддержка Android Wear Xamarin.Android позволяет вам выполнять C# кода на запястье! В этом введении предоставляет общий обзор Android Wear, описывает ее основные компоненты и предлагает обзор возможностей, доступных в Android Wear 2.0. Он перечисляет некоторые из наиболее популярных устройств Android Wear, а также предоставляет ссылки на важную документацию по Google Android Wear для дальнейшего изучения._


## <a name="overview"></a>Обзор

Android Wear работает на разнообразных устройствах, включая первого поколения 360 Motorola, смотреть G LG и шестеренки Samsung, Live. Также была отпущена второго поколения, включая 3 SmartWatch Sony, дополнительные возможности, включая встроенные GPS и воспроизведение музыки в автономном режиме. Для Android Wear 2.0 Google совместно с LG для двух новых watches: Спорт Watch LG и стиль LG контрольных значений.

![Устройства Android Wear 2.0](intro-to-wear-images/hero-image.png "устройств 2.0 Android Wear пример")

Поддерживают Xamarin.Android 5.0 и более поздних версий поддерживает Android Wear через наши Android 4.4W (API 20) и пакет NuGet, который добавляет дополнительные элементы управления износа конкретного пользовательского интерфейса. Xamarin.Android 5.0 и более поздние версии также включает функции для упаковка приложений одежды. Пакеты NuGet также доступны для Android 2.0, Wear, как описано далее в этом руководстве.


## <a name="android-wear-basics"></a>Основы Android Wear

Android Wear имеет парадигма интерфейс пользователя, которая отличается от портативных приложений Android. Первая группа износа приложений были разработаны для расширения вспомогательное портативные приложения, в некоторых способом, но, начиная с Android Wear 2.0, износа приложения можно использовать отдельно. При развертывании приложения одежды, он упаковывается дополнительного портативные приложения. Так как большинство Wear приложения зависят от дополнительного портативные приложения, они нужен способ взаимодействия с портативных приложений. В следующих разделах описываются эти сценарии использования и структуры самых важных особенностей Android Wear. 



### <a name="usage-scenarios"></a>Сценарии использования

Первая версия Android Wear сконцентрировала свое внимание на расширение текущего портативных приложений с помощью улучшенные уведомления и синхронизацию данных между портативные приложения и носимого приложения. Следовательно эти сценарии являются сравнительно легко реализовать.


#### <a name="wearable-notifications"></a>Уведомления с носимого

Для поддержки Android Wear проще всего использовать преимущества общего характера уведомлений между монитора и носимого устройством. С помощью API-Интерфейс уведомлений v4 поддержки и `WearableExtender` класса (в [библиотека Xamarin Android поддерживают](https://www.nuget.org/packages/Xamarin.Android.Support.v4/)), можно воспользоваться собственные функции платформы, такие как карточки стилей папки "Входящие" или голоса. [RecipeAssistant](https://developer.xamarin.com/samples/monodroid/wear/RecipeAssistant/) пример содержит пример кода, демонстрирующий способы отправки список уведомлений на устройство Android Wear. 



#### <a name="companion-applications"></a>Помощник по поиску приложений

Другая стратегия — создать приложение, выполняющееся в собственном коде, на устройстве с носимого и пары с дополнительного портативные приложения. Хорошим примером этого подхода является [тест](https://developer.xamarin.com/samples/monodroid/wear/Quiz/) пример приложения, который показывает, как создать тест, который выполняется на карманном устройстве и задает вопросы викторины носимого устройства. 



### <a name="user-interface"></a>Пользовательский интерфейс

Первичная Навигация шаблон износа представляет собой ряд карточек, располагаются вертикально. Каждый из этих карточек могут иметь связанные действия, которые, располагаются в той же строке. `GridViewPager` Класс предоставляет следующие функциональные возможности; следует адаптера совпадает с концепцией `ListView`. Обычно выполняется связывание `GridViewPager` с `FragmentGridPagerAdaptor` (или `GridPagerAdaptor`), позволяет представлять каждой строки и столбца ячейки, как `Fragment`: 

[![Wear навигации](intro-to-wear-images/2d-picker-sml.png "Wear навигации")](intro-to-wear-images/2d-picker.png#lightbox)

Wear также делает использование кнопок действия, которые состоят из большой цветной круг с небольшой описание текст под ним (как это показано выше).  [GridViewPager](https://developer.xamarin.com/samples/monodroid/wear/GridViewPager/) образце показано, как использовать `GridViewPager` и `GridPagerAdapter` в приложении одежды.

Android Wear 2.0 добавляет панель навигации, панель действий и кнопок действий встроенный пользовательский интерфейс одежды. Дополнительные сведения об элементах пользовательского интерфейса Android Wear 2.0, см. в разделе Android [составляющие](https://www.google.com/design/spec-wear/system-overview/anatomy.html) раздела. 



### <a name="communications"></a>Взаимодействие

Android Wear обеспечивает два различных интерфейсов API, облегчает взаимодействие между носимого приложениями и приложениями handheld companion связи: 

**API данных** &ndash; этот API аналогичен синхронизированное хранилище данных между устройством носимого и карманное устройство. Android отвечает за распространение изменений между носимого и карманных ПК, когда он является оптимальным для этого. Когда переносной выходит за пределы диапазона, он помещает в очередь синхронизации на более позднее время. Главная точка входа для этого API является `WearableClass.DataApi`. Дополнительные сведения об этом API см. в разделе Android [синхронизации элементов данных](https://developer.android.com/training/wearables/data-layer/data-items.html) раздела. 

**Сообщения API** &ndash; этот API позволяет использовать путь нижнего уровня связи: небольшой объем полезных данных отправляется односторонняя связь без синхронизации между приложениями карманные и носимого.
Главная точка входа для этого API является `WearableClass.MessageApi`.
Дополнительные сведения об этом API см. в разделе Android [отправка и получение сообщений](https://developer.android.com/training/wearables/data-layer/messages.html) раздела.

Вы можете регистрировать обратные вызовы для получения этих сообщений через каждый из интерфейсов API прослушивателя, или в качестве альтернативы реализовать службу в приложение, которое является производным от `WearableListenerService`.
Эта служба будет автоматически создан Android Wear.
[FindMyPhone](https://developer.xamarin.com/samples/monodroid/wear/FindMyPhoneSample/) примере демонстрируются способы реализации `WearableListenerService`.



### <a name="deployment"></a>Развертывание

Каждое носимого приложение развертывается с помощью свой собственный файл APK, внедренным в основное приложение APK. Это упаковка обрабатывается автоматически в Xamarin.Android 5.0 и более поздних версий, но необходимо выполнить вручную для версий Xamarin.Android, предшествующих версии 5.0. 
[Работа с упаковкой](~/android/wear/deploy-test/packaging.md) Описание развертывания более подробно. 



## <a name="going-further"></a>Продвигаясь дальше 

Лучший способ ознакомиться с Android Wear — сборка и тестирование приложения. В следующем списке приведены заказа на материалы помогут вам быстро приступить к работе:

1.  [Установка и настройка](~/android/wear/get-started/installation.md) приведены подробные инструкции по установке и настройке среды разработки для создания приложений Xamarin.Android одежды. 

2.  После установки необходимых пакетов и настроены в эмуляторе или на устройстве, см. в разделе [Wear Hello,](~/android/wear/get-started/hello-wear.md) пошаговые инструкции, поясняющие, как создать небольшой проект Android Wear этой кнопки дескрипторы щелкает и отображает Щелкните счетчик на устройстве Android Wear. 

3.  [Развертывание и тестирование](~/android/wear/deploy-test/index.md) содержатся более подробные сведения о настройке и развертывании в эмуляторах и устройствах, включая инструкции для развертывания приложения на устройстве Android Wear через Bluetooth.

4.  [Работа с размерами экрана](~/android/wear/screen-sizes.md) объясняется, как для предварительного просмотра и оптимизировать пользовательский интерфейс для различных размеров экрана, на устройствах одежды. 

5.  [Работа с упаковкой](~/android/wear/deploy-test/packaging.md) описаны действия по вручную упаковка приложений одежды для распространения в Google Play.

После создания первого приложения одежды, может потребоваться выполнить сборку пользовательского оформлений для Android Wear. 
[Создание оформлений](~/android/wear/platform/creating-a-watchface.md) предоставляет пошаговые инструкции и примеры кода для разработки является урезанным работу службы цифровых watch лиц, следуют дополнительные код, который дополняет его на циферблате стиле аналог для языка с помощью дополнительных функций. 



## <a name="android-wear-20"></a>Android Wear 2.0

Android Wear 2.0 дает ряд новых функций и возможностей, таких как *сложности*, криволинейные макеты, навигации и действие лотков и развернутом уведомлении. Кроме того Wear 2.0 позволяет создавать автономные приложения, которые работают независимо от портативных приложений. Новый *жесты запястья* возможность позволяет использовать только одной взаимодействия с вашим приложением. В следующих разделах, выделите эти функции и предоставляют ссылки, которые помогут вам приступить к работе с ними в приложении.



### <a name="install-wear-20-packages"></a>Установка Wear 2.0 пакетов

Чтобы создать приложение Wear 2.0 с помощью Xamarin.Android, необходимо добавить **версии 2.0 Xamarin.Android.Wear** пакета в проект (щелкните **вкладки просмотра**):

[![Версии 2.0 Xamarin.Android.Wear](intro-to-wear-images/wear-nuget-2.0-sml.png "установить пакет NuGet версии 2.0 Xamarin.Android.Wear")](intro-to-wear-images/wear-nuget-2.0.png#lightbox)

Этот пакет NuGet содержит привязки для библиотеки Android Носимого поддержки и совместимости Wear.

В дополнение к **Xamarin.Android.Wear**, мы рекомендуем установить **Xamarin.GooglePlayServices.Wearable** NuGet: 

[![Xamarin.GooglePlayServices.Wearable](intro-to-wear-images/gpsw-nuget-sml.png "установить Xamarin.GooglePlayServices.Wearable NuGet")](intro-to-wear-images/gpsw-nuget.png#lightbox)


### <a name="key-features-of-wear-20"></a>Ключевые функции Wear 2.0

Android Wear 2.0 является осуществить грандиозное обновление для Android Wear с момента его первого запуска в 2014 г. В следующих разделах рассматриваются основные функции Android Wear 2.0, и приводятся ссылки, чтобы помочь вам приступить к использованию этих новых функций в приложении. 


#### <a name="complications"></a>Усложнения

*Сложности* являются небольшой watch лиц мини-приложения, которые можно использовать с первого взгляда без необходимости проведения пальцем на циферблате. Сложности, аналогичны рабочим столом мини-приложений; они отображают сведения, такие как погода, батареи, событиями календаря и статистики пригодности приложений: 

![Пример сложности](intro-to-wear-images/complications.png "пример сложностей")

Дополнительные сведения о сложности, см. в разделе Android [сложности лиц Watch](https://developer.android.com/wear/preview/features/complications.html) раздела. 



#### <a name="navigation-and-action-drawers"></a>Навигация и ящики действие 

Два новых лотков включаются в Wear 2.0. *Панель навигации*, который отображается в верхней части экрана, позволяет пользователям перемещаться между представлениями приложения (как указано в нижнем левом изображении). *Панель действий*, который отображается в нижней части экрана (как показано в правой части), позволяет пользователям выбрать из списка действий. 

![Навигация и ящики действие](intro-to-wear-images/drawers.png "навигации и ящики действие")

Дополнительные сведения об этих двух новых интерактивных лотков, см. в разделе Android [Wear навигации и действий](https://developer.android.com/wear/preview/features/ui-nav-actions.html) раздела. 



#### <a name="curved-layouts"></a>Макеты кривой 

Износа 2.0 появились новые возможности для отображения кривой макеты на устройствах round одежды. В частности, новые `WearableRecyclerView` класс оптимизирован для отображения списка элементов по вертикали на вывод разделов, round: 

![Пример макета Curved](intro-to-wear-images/curved-layout.png "пример криволинейные макета")

`WearableRecyclerView` расширяет `RecyclerView` класс для поддержки изогнутой макеты и циклическая жесты прокрутки. Дополнительные сведения см. в разделе Android [WearableRecyclerView](https://developer.android.com/reference/android/support/wearable/view/WearableRecyclerView.html) документации по API. 



#### <a name="standalone-apps"></a>Автономные приложения 

Приложения Android Wear 2.0 можно работать независимо от портативных приложений. Это означает, что, например, умные часы могут продолжать предлагают полный набор функций, даже если карманное устройство-компаньон выключен или далеко от носимого устройства. Дополнительные сведения об этой функции см. в разделе Android [автономные приложения](https://developer.android.com/wear/preview/features/standalone-apps.html) раздела.



#### <a name="wrist-gestures"></a>Жесты запястья 

Жесты запястья позволяют пользователям взаимодействовать с вашим приложением без использования сенсорный экран &ndash; пользователи могли отвечать на приложение с одной стороны. Поддерживаются два запястья жестов: 

-   Штрих, направленный запястья out
-   Запястья штрих, направленный в

Дополнительные сведения см. в разделе Android [жесты запястья](https://developer.android.com/wear/preview/features/gestures.html) раздела. 


Существует множество функций дополнительные Wear 2.0, таких как встроенные действия, смарт-ответа, удаленного ввода, развернутом уведомлении и новый промежуточный режим уведомлений. Дополнительные сведения о новых возможностях Wear 2.0 см. в разделе Android [Обзор API](https://developer.android.com/wear/preview/api-overview.html). 



## <a name="devices"></a>Устройства

Ниже приведены некоторые примеры устройств с ОС Android Wear.

* [Motorola 360](https://moto360.motorola.com/)
* [LG G Watch](http://www.lg.com/us/smart-watches/lg-W100-g-watch)
* [LG G Watch R](http://www.lg.com/us/smartwatch/g-watch-r)
* [Samsung Gear Live](http://www.samsung.com/global/microsite/gear/gearlive_design.html)
* [Sony SmartWatch 3](http://www.sonymobile.com/global-en/products/smartwear/smartwatch-3-swr50/)
* [ASUS ZenWatch](http://www.asus.com/us/Phones/ASUS_ZenWatch_WI500Q/)



## <a name="further-reading"></a>Дополнительные сведения

Ознакомьтесь с документацией Android Wear Google:

* [Об Android Wear](http://www.android.com/wear/)
* [Проектирование приложений для Android Wear](https://developer.android.com/design/wear/index.html)
* [Библиотека Android.support.wearable ](https://developer.android.com/reference/android/support/wearable/view/package-summary.html)
* [Android Wear 2.0](https://developer.android.com/wear/preview/index.html)



## <a name="summary"></a>Сводка

В этом введении ознакомились с обзором Android Wear. Оно описано основные возможности Android Wear и включено с обзором функций, реализованных в Android Wear 2.0. Он предоставляет ссылки на essential чтения, чтобы помочь разработчикам приступить к работе с разработкой приложений Xamarin.Android износа и его в списке примеры некоторых устройств Android Wear сейчас на рынке.


## <a name="related-links"></a>Связанные ссылки

- [Установка и настройка](~/android/wear/get-started/installation.md)
- [Начало работы](~/android/wear/get-started/index.md)
