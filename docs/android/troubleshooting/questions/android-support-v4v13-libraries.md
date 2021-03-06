---
title: Оптимизированные пакеты NuGet поддержки Android v4 и v13 в Xamarin
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: FE66A82A-6C05-4646-BC52-E806F5DC606C
ms.technology: xamarin-android
author: conceptdev
ms.author: crdun
ms.date: 03/09/2018
ms.openlocfilehash: a990d933c258812b2b3d3374fb6435af06f729ea
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61227056"
---
# <a name="smarter-xamarin-android-support-v4--v13-nuget-packages"></a>Оптимизированные пакеты NuGet поддержки Android v4 и v13 в Xamarin

## <a name="about-the-android-support-libraries"></a>О вспомогательные библиотеки Android

Google создала библиотек поддержки для предоставления новых функций для более старых версиях Android. В общем случае библиотеки поддержки приведены номера версии в их имя, являющееся низкий уровень API Android они совместимы с (например: Поддержка v4 может использоваться только в API уровня 4 и более поздних версий. Дополнительные сведения в этом [обсуждении Stack Overflow](https://stackoverflow.com/questions/9926403/android-support-package-compatibility-library-use-v4-or-v13)). 

Два из библиотеки поддержки: `Support-v4` и `Support-v13` не может использоваться вместе в одном приложении, то есть они являются взаимоисключающими. Это обусловлено `Support-v13` фактически содержит все типы и реализации `Support-v4`. При попытке ссылаться как на том же проекте будут возникать ошибки повторяющийся тип.

## <a name="problems-with-referencing"></a>Проблемы со ссылками на

Так как `Support-v4` стала настолько популярной, много сторонних библиотек теперь от нее зависят. Их можно выбрать для зависящих от поддержки v13, вместо этого, но более часто зависят от _v4_ с момента, позволяет все приложения, с помощью этих сторонних библиотек поддерживает API уровней, вплоть до 4.

Если библиотека стороннего производителя Xamarin 3-й день ссылается на `Xamarin.Android.Support.v4.dll` привязка к `Support-v4`, любое приложение, которое использует эту библиотеку также необходима ссылка `Xamarin.Android.Support.v4.dll`. Это становится проблемой, когда то же приложение также хочет использовать некоторые функции из `Xamarin.Android.Support.v13.dll` привязка к `Support-v13`. Если вы ссылаетесь обе привязки, то возникают ошибки повторяющийся тип.

## <a name="type-forwarded-v4-binding-assembly"></a>Переадресация типа v4 привязки сборки

Чтобы обойти эту проблему, мы создали специальный `Xamarin.Android.Support.v4.dll` сборки, который не имеет реализации, но просто `[assembly: TypeForwardedTo (..)]` атрибуты, которые пересылают все `Support-v4` типы для реализации в `Xamarin.Android.Support.v13.dll` сборки.

Это означает, что разработчик может ссылаться на это _Переадресация типа_ сборки в свои приложения, которое будет удовлетворять ссылку `Xamarin.Android.Support.v4.dll` по любой библиотеки сторонних производителей, по-прежнему предоставляя `Xamarin.Android.Support.v13.dll` для использования в приложении.

## <a name="nuget-assistance"></a>Помощь NuGet

Хотя разработчик может вручную добавить необходимые правильные ссылки, которые может использовать NuGet для выбора правильного блока (либо нормали _v4_ привязки или Переадресация типа _v4_ сборки) при устанавливается пакет NuGet.

Таким образом `Xamarin.Android.Support.v4` пакет NuGet теперь содержит следующую логику:

Если приложение предназначено для API уровня 13 (Gingerbread 3.2) или более поздней версии:

*   `Xamarin.Android.Support.v13` NuGet автоматически добавляется как зависимость
*   _Переадресация типа_ `Xamarin.Android.Support.v4.dll` будет ссылаться в проекте

Если приложение предназначено для ничего ниже, чем 13 уровень API, вы получите обычный `Xamarin.Android.Support.v4.dll` привязки, в ссылках вашего проекта.

## <a name="do-i-have-to-use-support-v13"></a>Нужно ли использовать v13 поддержки?

Если приложение предназначено для API уровня 13 или выше, и вы решили использовать `Xamarin Android Support-v4` пакет NuGet, а затем `Xamarin Android Support v13` пакет NuGet — это требуемая зависимость.

Мы думаем, что стоит совместимости и меньшее количество проблем, это очень незначительное увеличения размера приложения (два JAR-файлы отличаются от 17 КБ).

Если вы являетесь adamant об использовании `Support-v4` в приложение, предназначенное для API уровня 13 или выше, чтобы всегда вручную загрузить `.nupkg`, извлеките его содержимое и ссылки на сборку.
