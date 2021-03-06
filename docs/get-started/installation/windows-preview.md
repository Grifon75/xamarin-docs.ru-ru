---
title: Установка предварительной версии Xamarin в ОС Windows
description: В этом документе описывается, как установить предварительную версию Xamarin на 2019 г. Visual Studio, используя канал выпусков предварительной версии.
ms.prod: xamarin
ms.assetid: 9F730444-06E8-4B3F-8A19-CA95CD484FFA
author: asb3993
ms.author: amburns
ms.date: 03/20/2018
ms.openlocfilehash: 9ce56891eeab73f661a9c22cc047c4d0bcb10337
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61261081"
---
# <a name="installing-xamarin-preview-on-windows"></a>Установка предварительной версии Xamarin в ОС Windows

Visual Studio 2019 и Visual Studio 2017 не поддерживают альфа, бета-версии и стабильные каналы таким же образом, как в предыдущих версиях. Вместо этого есть два варианта:

- **выпуск** — эквивалент _стабильного_ канала в Visual Studio для Mac;
- **предварительная версия** — эквивалент _альфа-_ и _бета-_ каналов в Visual Studio для Mac.

> [!TIP]
> Чтобы опробовать функции предварительной версии, вы должны [скачать установщик предварительной версии Visual Studio](https://visualstudio.microsoft.com/vs/preview/), обеспечивающие возможность установки **предварительной версии** версиях Visual Studio side-by-Side с помощью стабильная ( Версия выпуска). Дополнительные сведения о новых 2019 г. Visual Studio можно найти в [заметки о выпуске](https://docs.microsoft.com/visualstudio/releases/2019/release-notes).

Предварительная версия Visual Studio может включать соответствующие предварительные версии функциональных возможностей Xamarin, в том числе следующие:

- Xamarin.Forms
- Xamarin.iOS
- Xamarin.Android
- Xamarin Profiler
- Xamarin Inspector
- Симулятор iOS удаленной работы для Xamarin

На снимке экрана **установщика предварительной версии** ниже показаны параметры и предварительной версии, и выпуска (обратите внимание на номера версий, указанные серым цветом: версия 15.0 относится к выпуску, а версия 15.1 — к предварительной версии):

![отображение параметров предварительной версии в установщике](windows-images/vs2017-installer.jpg)

В процессе установки, если выполняется параллельная установка, может применяться **псевдоним установки** (чтобы версии можно было различить в меню "Пуск"), как показано ниже:

[![Изменение псевдонима перед установкой](windows-images/vs2017-nickname-sml.png "edit nickname before installing")](windows-images/vs2017-nickname.png#lightbox)

### <a name="uninstalling-visual-studio-2019-preview"></a>Удаление предварительной версии Visual Studio 2019 г.

**Установщик Visual Studio** следует также удалить бета-версии Visual Studio 2019. Дополнительные сведения см. в руководстве по [удалению Xamarin](uninstalling-xamarin.md#uninstallvs2017).
