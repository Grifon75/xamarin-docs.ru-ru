---
title: Xamarin.Forms DataPages
description: В этой статье рассматриваются Xamarin.Forms DataPages, которые обеспечивают API, чтобы быстро и легко привязать источник данных к предварительно созданные представления.
ms.prod: xamarin
ms.assetid: DF16EAEE-DB78-42CA-9C59-51D9D6CB6B95
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 12/01/2017
ms.openlocfilehash: 2a74b636a41a72b26776157a774f0a33ef45a075
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61407686"
---
# <a name="xamarinforms-datapages"></a>Xamarin.Forms DataPages

![](~/media/shared/preview.png "Этот API доступна в предварительной версии")

> [!IMPORTANT]
> Требуется DataPages [Xamarin.Forms темы](~/xamarin-forms/user-interface/themes/index.md) ссылку для отображения.

Xamarin.Forms DataPages были объявлены в 2016 развития и доступны в предварительной версии для клиентов, оценить их и отправить отзыв.

DataPages предоставляют API, чтобы быстро и легко привязывать источник данных к предварительно созданные представления. Элементы списка и страницы сведений о автоматически будет отображать данные и могут быть настроены с использованием тем.

Чтобы увидеть, как работает развития ролик, просмотрите [руководство по началу работы](get-started.md).

[![](images/demo-sml.png "Пример DataPages приложения")](images/demo.png#lightbox "DataPages примера приложения")

## <a name="introduction"></a>Вступление

Источники данных и связанные данные страниц позволяют разработчикам быстро и легко использовать поддерживаемый источник данных и отображения ее, используя встроенный формирование шаблонов, который может быть модифицирован с темами.

DataPages добавляются приложения Xamarin.Forms, включив **Xamarin.Forms.Pages** пакет Nuget.

### <a name="data-sources"></a>Data Sources

Просмотр имеет некоторые готовые источники данных доступны для использования:

* **JsonDataSource**
* **AzureDataSource** (отдельных Nuget)
* **AzureEasyTableDataSource** (отдельных Nuget)

См. в разделе [руководство по началу работы](get-started.md) в качестве примера использования `JsonDataSource`.


### <a name="pages--controls"></a>Страницы и элементы управления

Следующие страницы и элементы управления, которые позволяют легко привязки к источникам данных, предоставленных:

* **ListDataPage** — см. в разделе [Приступая к работе пример](get-started.md).
* **DirectoryPage** — список с включенным группированием.
* **PersonDetailPage** — элемент единый данных представления, настроенные для конкретного типа объектов (запись контакта).
* **DataView** — представление для предоставления данных из источника в первоначальном виде.
* **CardView** — стиль представления, содержащего изображение, текст заголовка и текста описания.
* **Имиджевое изображение** — это представление визуализации изображений.
* **ListItem** — предварительно созданные представления с макетом, аналогичную собственные для iOS и Android списка элементов.

См. в разделе [Справочник по элементам управления DataPages](controls.md) примеры.



### <a name="under-the-hood"></a>Взгляд изнутри

Источник данных Xamarin.Forms, соответствует `IDataSource` интерфейс.

Инфраструктура Xamarin.Forms взаимодействует с источником данных через следующие свойства:

* `Data` — только для чтения список элементов данных, которые могут быть отображены.
* `IsLoading` — Логическое значение, указывающее, являются ли данные загружаются и доступны для подготовки к просмотру.
* `[key]` — индексатор для извлечения элементов.

Существует два способа `MaskKey` и `UnmaskKey` можно использовать, чтобы скрыть (или отобразить) свойства элемента данных (т. е. предотвратить их).
Ключ соответствует именованное свойство в объект элемента данных.
