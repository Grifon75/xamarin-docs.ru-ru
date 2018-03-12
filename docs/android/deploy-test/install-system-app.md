---
title: "Установка Xamarin.Android в качестве системного приложения"
description: "В этом руководстве обсуждаются различия между системными и пользовательскими приложениями и описывается установка приложения Xamarin.Android в качестве системного приложения. Это руководство предназначено для авторов пользовательских образов Android. Здесь не объясняется, как создать пользовательский образ."
ms.topic: article
ms.prod: xamarin
ms.assetid: 0113143B-7D8D-4C4C-B2F5-B966A2E7CE1F
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 02/15/2018
ms.openlocfilehash: ad2080c61c9cc7fb376997bc56668b6db135dbae
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="installing-xamarinandroid-as-a-system-app"></a>Установка Xamarin.Android в качестве системного приложения

_В этом руководстве обсуждаются различия между системными и пользовательскими приложениями и описывается установка приложения Xamarin.Android в качестве системного приложения. Это руководство предназначено для авторов пользовательских образов Android. Здесь не объясняется, как создать пользовательский образ._

## <a name="system-app"></a>Системное приложение

Авторы пользовательских образов Android и изготовители устройств Android имеют возможность включить приложение Xamarin.Android в свой образ и (или) устройство в качестве _системного приложения_. Системным называется приложение, которое считается важным для правильной работы устройства или предоставляет важные функциональные возможности с точки зрения автора образа.

Системные приложения устанавливаются в папке **/system/app/** (каталог только для чтения в файловой системе) и пользователь не может их удалять или перемещать без прав суперпользователя (root). Все остальные приложения, устанавливаемые пользователем самостоятельно (через Google Play или загружая файл неопубликованного приложения), называются _пользовательскими приложениями_. Пользователь может удалять пользовательские приложения, а в большинстве случаев — перемещать в другое расположение на устройстве (например, на внешнее хранилище).

Системные приложения ведут себя так же, как и пользовательские, но с несколькими важными исключениями.

- Системные приложения обновляются точно так же, как _пользовательские приложения_. Но при этом в каталоге **/system/app/** всегда сохраняется копия этого приложения, а значит всегда можно всегда выполнить откат к его исходной версии.

- Системные приложения могут получать некоторые системные разрешения, недоступные для пользовательских приложений. Например, разрешение [`BLUETOOTH_PRIVILEGED`](https://developer.android.com/reference/android/Manifest.permission.html#BLUETOOTH_PRIVILEGED), которое разрешает сопряжение с устройствами Bluetooth без вмешательства пользователя, предоставляется только системным приложениям.

У разработчиков есть возможность распространять приложения Xamarin.Android в качестве системных приложений. Для этого нужно не только включить в настраиваемый образ пакет APK, но и вручную скопировать из него две общие библиотеки **libmonodroid.so** и **libmonosgen 2.0.so** в файловую систему образа ОС. Этот процесс описан в этом руководстве.

## <a name="restrictions"></a>Ограничения

Это руководство предназначено для авторов пользовательских образов Android. Здесь не объясняется, как создать пользовательский образ.

Здесь мы предполагаем, что вы уже знакомы с концепцией [упаковки выпуска APK для Xamarin.Android](~/android/deploy-test/publishing/index.md) и хорошо понимаете [архитектуру ЦП](~/android/app-fundamentals/cpu-architectures.md) для приложений Android.

## <a name="install-a-xamarinandroid-app-as-a-system-app"></a>Установка Xamarin.Android в качестве системного приложения

Ниже описан процесс установки приложения Xamarin.Android в качестве системного приложения.

1. **Создайте пакет выпуска APK для приложения Xamarin.Android** &ndash; этот процесс подробнее описан в руководстве [по публикации приложения](~/android/deploy-test/publishing/index.md).

2. **Извлеките из APK общие библиотеки**  &ndash; с помощью любой служебной программы, работающей с архивами ZIP, откройте файл APK и изучите содержимое папки **/lib/**. В этой папке есть подкаталог для каждого _двоичного интерфейса приложения_ (ABI), который поддерживается приложением. Здесь будут располагаться все общие библиотеки этого интерфейса ABI, необходимые для этого конкретного приложения:

    ![Снимок экрана со списком SO-файлов в папке armeabi-v7a файла образа taskypro.zip](install-system-app-images/install-system-app-01.png)

   На предыдущем снимке экрана мы видим только один поддерживаемый ABI (**armeabi-v7a**) с двумя **SO-файлами**, которые используются в приложении. Обратите внимание, что извлекать следует только те файлы ABI, которые подходят для целевой архитектуры образа ОС. Например, нет смысла копировать **SO-файлы** из папки **x86** на устройство или в образ **armeabi-v7a**.

3. **Скопируйте SO-файлы в каталог /system/lib** &ndash; скопируйте **SO-файлы**, извлеченные из APK на предыдущем шаге, в папку **/system/lib/** в настраиваемом образе.

4. **Скопируйте APK-файл в каталог /system/app** &ndash; последним шагом скопируйте APK-файл в каталог **/system/app** в настраиваемом образе.


## <a name="summary"></a>Сводка

В этом руководстве мы обсудили различия между _системными приложениями_ и _пользовательскими приложениями_, а также описали установку приложения Xamarin.Android в качестве системного приложения.



## <a name="related-links"></a>Связанные ссылки

- [Публикация приложения](~/android/deploy-test/publishing/index.md)
- [Архитектуры процессоров](~/android/app-fundamentals/cpu-architectures.md)
- [BLUETOOTH_PRIVILEGED](https://developer.android.com/reference/android/Manifest.permission.html#BLUETOOTH_PRIVILEGED)
- [Управление API](https://developer.android.com/ndk~/abis.html)