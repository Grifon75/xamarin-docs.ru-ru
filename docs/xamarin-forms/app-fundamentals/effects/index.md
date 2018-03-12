---
title: "Произведенный эффект"
description: "Xamarin.Forms пользовательские интерфейсы, отображаются с использованием собственные элементы управления целевой платформы, позволяя приложениям Xamarin.Forms сохранить соответствующий внешний вид для каждой платформы. Эффекты позволяют собственных элементов управления для каждой платформы, нужно настроить, не прибегая к использованию в реализацию пользовательского средства отрисовки."
ms.topic: article
ms.prod: xamarin
ms.assetid: 8AF168A7-4CD9-4603-B961-15B8B1543784
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 03/01/2017
ms.openlocfilehash: dd8b98982052e15744bf67ece6a25cd940a9875a
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="effects"></a>Произведенный эффект

_Xamarin.Forms пользовательские интерфейсы, отображаются с использованием собственные элементы управления целевой платформы, позволяя приложениям Xamarin.Forms сохранить соответствующий внешний вид для каждой платформы. Эффекты позволяют собственных элементов управления для каждой платформы, нужно настроить, не прибегая к использованию в реализацию пользовательского средства отрисовки._

## <a name="introduction-to-effectsintroductionmd"></a>[Общие сведения о эффекты](introduction.md)

Эффекты позволяют собственные элементы управления на каждой платформе, которую нужно изменить и обычно используются для изменения небольшой стилей. В этой статье содержатся вводные эффекты, описываются границу между эффекты и пользовательские модули подготовки отчетов и описывает `PlatformEffect` класса.

## <a name="creating-an-effectcreatingmd"></a>[Создание эффекта](creating.md)

Эффекты упростить настройку элемента управления. В этой статье показано, как для создания эффекта, которое изменяет цвет фона [ `Entry` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Entry/) управления, когда элемент управления получает фокус.

## <a name="passing-parameters-to-an-effectpassing-parametersindexmd"></a>[Передача параметров в силу](passing-parameters/index.md)

Создание эффект, настраивается с помощью параметров позволяет эффект для повторного использования. Эти статьи показано использование свойства для передачи параметров в силу и изменив параметр во время выполнения.

## <a name="invoking-events-from-an-effecttouch-trackingmd"></a>[Вызов события из эффекта](touch-tracking.md)

Эффекты можно вызывать события. В этой статье показано, как создать событие, которое реализует низкоуровневые пальцем мультисенсорные отслеживания и уведомляет приложения для нажатия сенсорный ввод, перемещение, а также версии.