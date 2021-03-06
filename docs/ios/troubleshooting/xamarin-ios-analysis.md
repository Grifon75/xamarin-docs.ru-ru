---
title: Правила анализа Xamarin.iOS
description: В этом документе описывается набор правил анализа, проверьте параметры проекта Xamarin.iOS, чтобы определить, доступны другие/better-optimized параметры.
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: C29B69F5-08E4-4DCC-831E-7FD692AB0886
ms.technology: xamarin-ios
author: lobrien
ms.author: laobri
ms.date: 03/06/2018
ms.openlocfilehash: 8a4990ce7b2bcacbd4b97b214458531b3d94122e
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61416387"
---
# <a name="xamarinios-analysis-rules"></a>Правила анализа Xamarin.iOS

Xamarin.iOS анализа — это набор правил, проверяющих параметры проекта, чтобы помочь вам определить, если доступны параметры оптимизированного более или менее.

Правила анализа следует запустите так часто, возможно, чтобы найти возможные улучшения на раннем этапе и сократить время разработки.

Для запуска этих правил в Visual Studio для Mac в меню, выберите **проекта > выполнить анализ кода**.

> [!NOTE]
> Xamarin.iOS анализ выполняется только на вашей текущей конфигурации. Мы настоятельно рекомендуем запустить средство для отладки **и** конфигурации выпуска.

<a name="XIA0001" />

## <a name="xia0001-disabledlinkerrule"></a>XIA0001: DisabledLinkerRule

- **Проблема:** Компоновщик отключен на устройстве в режиме отладки.
- **Исправление:** Попробуйте для выполнения кода с ключом компоновщика избежать сюрпризов.
Чтобы настроить его, перейти к проекту > сборка iOS > Поведение компоновщика.

<a name="XIA0002" />

## <a name="xia0002-testcloudagentreleaserule"></a>XIA0002: TestCloudAgentReleaseRule

- **Проблема:** Сборки приложений, которые инициализируют агент Test Cloud будут отклонены Apple, при отправке, так как они используют закрытый API.
- **Исправление:** Добавьте или исправьте необходимые #if и определяет в коде.

<a name="XIA0003" />

## <a name="xia0003-ipadebugbuildsrule"></a>XIA0003: IPADebugBuildsRule

- **Проблема:** Конфигурации отладки, который использует ключи подписывания разработчика не должна создавать IPA, как только он нужен для распространения, использующую теперь мастера публикации.
- **Исправление:** Отключите построения IPA в параметрах проекта для конфигурации отладки.

<a name="XIA0004" />

## <a name="xia0004-missing64bitsupportrule"></a>XIA0004: Missing64BitSupportRule

- **Проблема:** Поддерживаемая архитектура для «выпуск | устройство» не является 64-разрядная версия совместима, отсутствует ARM64. Это проблема, так как Apple не принимает только приложения iOS 32 бита в AppStore.
- **Исправление:** Дважды щелкните проект iOS, перейдите к сборке > iOS, сборки и изменить поддерживаемых архитектур, поэтому он содержит ARM64.

<a name="XIA0005" />

## <a name="xia0005-float32rule"></a>XIA0005: Float32Rule

- **Проблема:** Не используется параметр float32 (--aot параметры =-O = float32) приводит к увеличивает производительность, особенно на мобильных устройствах, где математические операции двойной точности значительно медленнее. Обратите внимание на то, что .NET с помощью двойной точности на внутреннем уровне даже в число с плавающей запятой, поэтому Включение этого параметра влияет на точность и, возможно, совместимости.
- **Исправление:** Дважды щелкните проект iOS, перейдите к сборке > iOS, сборки и снимите флажок «Выполнять все операции 32-разрядное число с плавающей запятой как 64-разрядное число с плавающей запятой».

<a name="XIA0006" />

## <a name="xia0006-httpclientavoidmanaged"></a>XIA0006: HttpClientAvoidManaged

- **Проблема:** Мы рекомендуем использовать собственный обработчик HttpClient вместо управляемого для повышения производительности, меньший размер исполняемого файла и для упрощения поддержки новых стандартов.
- **Исправление:** Дважды щелкните проект iOS, перейдите к сборке > iOS сборки и измените реализацию HttpClient NSUrlSession (iOS 7 и более поздние) или CFNetwork для поддержки версии предшествующие iOS 7.
