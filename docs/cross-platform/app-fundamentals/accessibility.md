---
title: Специальные возможности в приложения Xamarin
description: Здесь содержатся различные советы для создания приложений со специальными возможностями. Например он содержит рекомендации по крупного шрифта, высокая контрастность, самоописанием интерфейсы и многое другое.
ms.prod: xamarin
ms.assetid: E587F0CF-7C1D-41F8-B5A8-DA3E738EDA81
author: asb3993
ms.author: amburns
ms.date: 03/22/2017
ms.openlocfilehash: 0ec264e0f3d381fdac46c79dd479da2bc768954f
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61282193"
---
# <a name="accessibility-in-xamarin-apps"></a>Специальные возможности в приложения Xamarin

_Убедитесь, что ваши приложения работать с самого широкого аудитории_

Специальные возможности ссылается на концепцию Разработка пользовательских интерфейсов приложений, которые работают хорошо отображения и ввода помощь компонентов операционной системы, такие как большого типа, высокая контрастность, увеличение, чтение с экрана (текст в речь), обратной связи visual или haptic подсказки, и альтернативные методы ввода.

Для настольных и мобильных платформ, таких как iOS, Android и Windows предоставляют встроенные API-интерфейсы, помочь программистам в создании приложений со специальными возможностями, такими как [Google TalkBack](https://play.google.com/store/apps/details?id=com.google.android.marvin.talkback) и [Apple VoiceOver](http://www.apple.com/accessibility/ios/voiceover/).

## <a name="platform-specific-apis"></a>API для конкретных платформ

Чтобы реализовать рекомендации в этом документе, используйте API, предоставляемые каждой платформы:

- [**Android специальных возможностей**](~/android/app-fundamentals/accessibility.md)
- [**iOS специальных возможностей**](~/ios/app-fundamentals/accessibility.md)
- [**Специальные возможности OS X**](~/mac/app-fundamentals/accessibility.md)
- [**Xamarin.Forms**](~/xamarin-forms/app-fundamentals/accessibility/index.md)

<a name="checklist" />

## <a name="accessibility-checklist"></a>Контрольный список специальных возможностей

Следуйте приведенным ниже советам, чтобы убедиться, что ваши приложения доступны для широкой аудитории возможных. Ознакомьтесь с [Android контрольный список проверки специальных возможностей](https://developer.android.com/training/accessibility/testing.html) и [странице специальных возможностей корпорации Apple](http://www.apple.com/accessibility/) Дополнительные сведения.

### <a name="support-large-fonts-and-high-contrast"></a>Поддержка больших шрифты и высокой контрастности

Избежать жесткого задания измерения и вместо этого предпочитают макеты, которые можно изменить размер для размещения больших размерах шрифта.
Протестируйте цветовых схем в режиме высокой контрастности, чтобы гарантировать, что они могут быть прочитаны.

### <a name="make-the-user-interface-self-describing"></a>Сделать пользователя интерфейс с самоописанием

Пометить все элементы интерфейса пользователя-с описание и указания, которые совместимы с чтения API-интерфейсы на каждой платформе.

### <a name="ensure-that-images-and-icons-have-an-alternate-text-description"></a>Убедитесь, что изображения и значки описанием альтернативный текст

Изображения и значки, которые являются частью пользовательского интерфейса приложения (например, кнопок и индикаторы состояния, например) должны быть снабжены Описание специальных возможностей.

### <a name="design-the-visual-tree-with-accessible-navigation-in-mind"></a>Проектирование визуального дерева с доступным навигации в виду

Используйте соответствующую компоновку элементов управления или API-интерфейсов, чтобы при переходе между элементами управления, используя альтернативные методы ввода следует за же логический поток как с помощью сенсорного экрана.

Исключите ненужные элементы из средства чтения с экрана (декоративных изображений или меток для полей, которые уже доступны, например).

### <a name="dont-rely-on-audio-or-color-cues-alone"></a>Не полагайтесь на аудио- или цвет подсказки только

Избегайте ситуаций, где единственным значение, указывающее ход выполнения, завершение или другое состояние — звука или изменения цвета. Либо разработать пользовательский интерфейс для незащищенного визуальные подсказки (с звук и цвет только с подкреплением), либо добавьте отдельных специальных индикаторы.

При выборе цвета, старайтесь избегать трудно отличить для пользователей с цветовой слепотой палитры.

### <a name="captioning-for-video-text-for-audio"></a>Субтитров для видео, текста для аудио

Предоставить подписи для видео-контента, а также для чтения скрипт для звукового содержимого. Это также полезно для элементов управления, скорость аудио и видео содержимого и обеспечения этого тома и кнопки воспроизведения, паузы их легко найти и использовать.

### <a name="localize"></a>Localize

Описание специальных возможностей можно (и нужно будет локализовано где приложение поддерживает несколько языков.



## <a name="related-links"></a>Связанные ссылки

- [Android специальных возможностей](~/android/app-fundamentals/accessibility.md)
- [iOS специальных возможностей](~/ios/app-fundamentals/accessibility.md)
- [Специальные возможности OS X](~/mac/app-fundamentals/accessibility.md)
- [Специальные возможности в Xamarin.Forms](~/xamarin-forms/app-fundamentals/accessibility/index.md)
