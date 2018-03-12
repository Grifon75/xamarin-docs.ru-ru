---
title: "Развертывание и тестирование"
description: "Тестирование на устройствах и отправка в магазин приложений"
ms.topic: article
ms.prod: xamarin
ms.assetid: 98257399-E9B3-4BAB-9204-0E89117DEA6D
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/17/2017
ms.openlocfilehash: fdd4311072efd5571724fbe00d12a96921054fa2
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="deployment-and-testing"></a>Развертывание и тестирование

## <a name="deployment-checklist"></a>Контрольный список развертывания

При развертывании тест Контрольные значения, или загрузке магазин приложений, необходимо выполнить действия, указанные на этой странице:

- В **центра разработки iOS**:
  - [Идентификаторы приложений](#App_IDs) были созданы.
  - [Группы приложений](#App_Groups) настроен (при необходимости).
  - [*Распределение* профили подготовки](#Provisioning_Profiles) создан.

- В решении:

  - Проверьте [идентификаторы набора и ссылки между проектами](~/ios/watchos/get-started/installation.md) заданы.
  - Проверьте значки [правильность настройки](~/ios/watchos/app-fundamentals/icons.md).
  - Проверьте соответствие номера версии пакета во всех проектах.
  - Настройка **Entitlements.plist** для группы приложений (при необходимости).

* Следуйте инструкциям, чтобы:
  - [Развертывание в целях тестирования для Apple Watch](~/ios/watchos/deploy-test/device.md), или
  - [Отправка в магазин приложений](~/ios/watchos/deploy-test/appstore.md).


## <a name="app-ids"></a>Идентификаторы приложений

Как было сказано в [инструкции по установке](~/ios/watchos/get-started/installation.md), все три проекта в приложении для наблюдения за связаны идентификаторы пакетов, таких как:

- Проект единого Xamarin.iOS- `com.xamarin.WatchKitCatalog`
- Проект расширения WatchKit- `com.xamarin.WatchKitCatalog.watchkitextension`
- Проект приложения Контрольные значения- `com.xamarin.WatchKitCatalog.watchkitapp`

Все три проекты требуют сопоставления подготовки профиля распределения, с помощью явно идентификаторы приложений для каждого, или подстановочный знак идентификатор приложения.

### <a name="explicit-app-ids"></a>Идентификаторы явную приложений

Создание **идентификатор приложения** ИД набора каждого каждый проект (который будет выглядеть следующим образом на центра разработки iOS):

![Идентификаторы пакетов в центра разработки iOS](images/appids-specific-sml.png)

При создании или настройке идентификаторы приложений, не забудьте включить конкретные компоненты, необходимые для приложения. Сюда могут входить push-уведомлений и группы приложений.

Необходимо создать профиль подготовки распространения для каждого идентификатора приложения.

### <a name="wildcard-app-id"></a>Идентификатор приложения подстановочный знак

Кроме того, можно создать шаблон **идентификатор приложения** выделяющий всех трех проектов `com.xamarin.*`.

Обратите внимание, что некоторые функции не может использоваться с подстановочным знаком идентификатор приложения (такие как push-уведомлений). Если вашему приложению требуется эти функции, необходимо создать явную идентификаторы приложений.

Для распространения только необходимо создать один распространения профиль подготовки для подстановочных знаков идентификатор приложения.

<a name="app-groups" />

## <a name="app-groups"></a>Группы приложений

Группы приложений можно использовать для обмена данными между вашего приложения iOS и расширением контрольных значений. Следует убедиться, что решение содержит:

- Настроить **группы приложения** на портале разработчика Apple **сертификатов, профили & идентификаторы** раздела.

- Включена **группы приложений** (, предоставленные **ID группы приложения**) в *оба* приложения iOS и расширении Watch **идентификатор приложения** и  **Entitlements.plist**.

### <a name="certificates-identifiers--profiles"></a>Сертификаты, идентификаторы и профили

Для использования группы приложений, создайте запись в **группы приложений** экрана. В следующем примере с тот же стиль обратного DNS, который широко применяется для идентификаторы приложений, но с именем группы `group.` префикс (который обязателен):

![Идентификатор](images/appgroups-new-sml.png)

Группа приложений будут отображаться в списке:

![Список идентификаторов](images/appgroups-setup-sml.png)

После создания группы ее можно ссылаться в вашей **идентификатор приложения** конфигурации. Не забудьте включить оба iOS приложение и расширении **идентификаторы приложений**.

![Доступные consifurations](images/appgroups-sml.png)

Сделать **не** включить группы приложений в код приложения Apple Watch. Не требуется включать в часах.

### <a name="entitlementsplist"></a>Entitlements.plist

Некоторые возможности приложения (например) Группы приложений) требуется задать прав.
Дважды щелкните, чтобы изменить **Entitlements.plist** файла в этих проектах:

- проект приложения iOS
- Проект расширения Контрольное значение

.![Редактор Entitlements.plist](images/entitlements-plist-sml.png)

Сделать **не** включите права в проекте приложения контрольных значений. Не требуется включать в часах.



## <a name="related-links"></a>Связанные ссылки

- [Руководство по отправке WatchKit Apple](https://developer.apple.com/app-store/watch/)