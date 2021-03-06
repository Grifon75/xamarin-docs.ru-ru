---
title: Текст в Xamarin.Forms
description: Xamarin.Forms есть три основных представления для работы с текстом, и в этой статье объясняется, как их использовать для ввода и отображения текста в приложениях Xamarin.Forms.
ms.prod: xamarin
ms.assetid: 4DBA7689-E5C8-4583-8FB4-02AB208B4416
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/26/2018
ms.openlocfilehash: 8754f6573b00334fd228b1c9bd094cd91565976c
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61363921"
---
# <a name="text-in-xamarinforms"></a>Текст в Xamarin.Forms

[![Загрузить образец](~/media/shared/download.png) загрузить пример](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Text)

_С помощью Xamarin.Forms, чтобы ввести или отображения текста._

Xamarin.Forms есть три основных представления для работы с текстом:

- **[Метка](#Label)**  &mdash; для представления одного или нескольких строк текста. Можно отображать текст с несколькими вариантами форматирования в той же строке.
- **[Запись](#Entry)**  &mdash; для ввода текста, только одна строка. Запись имеет режим пароля.
- **[Редактор](#Editor)**  &mdash; для ввода текста, который может занять более одной строки.

Можно изменить внешний вид текста с помощью встроенных или пользовательских [стили](#Styles) и некоторые элементы управления поддерживают пользовательские [шрифты](#Fonts).

<a name="Label" />

## <a name="labellabelmd"></a>[Label](label.md)

`Label` Представление используется для отображения текста. Она может отображать несколько строк текста или одну строку текста. `Label` можно представить текст с несколькими параметрами форматирования, используется во встроенной. Представление метки можно переносить или усечения текста, когда он не может поместиться на одной строке.

![](images/label.png "Пример метки")

См. в разделе [метка](label.md) статья более подробные сведения.

Сведения о настройке шрифт, используемый в метке, см. в разделе [шрифты](fonts.md).

<a name="Entry" />

## <a name="entryentrymd"></a>[Ввод](entry.md)

`Entry` используется для ввода однострочный текст. `Entry` предложения контроль над цветов и шрифтов. `Entry` имеет режим пароль и может показывать замещающий текст, пока не будет введен текст.

![](images/entry.png "Пример записи")

См. в разделе [запись](entry.md) для получения дополнительной информации.

Обратите внимание, что, в отличие от `Label`, `Entry` не может иметь параметры пользовательского шрифта.

<a name="Editor" />

## <a name="editoreditormd"></a>[Редактор](editor.md)

`Editor` используется для ввода многострочный текст. `Editor` предложения контроль над цветов и шрифтов.

![](images/editor.png "Пример редактора")

См. в разделе [редактор](editor.md) для получения дополнительной информации.

<a name="Fonts" />

## <a name="fontsfontsmd"></a>[Шрифты](fonts.md)

Многие элементы управления поддерживают параметры шрифта, с помощью встроенных шрифтов на каждой платформе или пользовательских шрифтов, поставляемых вместе с вашим приложением. См. в разделе [шрифты](fonts.md) статья более подробные сведения.

<a name="Styles" />

## <a name="stylesstylesmd"></a>[Стили](styles.md)

Ссылаться на [работы со стилями](~/xamarin-forms/user-interface/styles/index.md) чтобы узнать, как настроить шрифт, [цвет](~/xamarin-forms/user-interface/colors.md)и другие свойства отображения всего нескольких элементов управления.

## <a name="related-links"></a>Связанные ссылки

- [Текст (пример)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Text)
