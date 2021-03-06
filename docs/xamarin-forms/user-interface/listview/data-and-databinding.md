---
title: Источники данных ListView
description: В этой статье объясняется, как для заполнения ListView Xamarin.Forms с данными и как использовать привязку данных с помощью ListView.
ms.prod: xamarin
ms.assetid: B5571660-1E82-4379-95C3-0725288CF5D9
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/30/2018
ms.openlocfilehash: e53f6dce47dd7db60267d21c8d816ece554dc46c
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61320016"
---
# <a name="listview-data-sources"></a>Источники данных ListView

[![Загрузить образец](~/media/shared/download.png) загрузить пример](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/ListView/SwitchEntryTwoBinding)

Объект [ `ListView` ](xref:Xamarin.Forms.ListView) используется для отображения списков данных. Вы узнаете о заполнении ListView с данными, и как можно привязать к выбранному элементу.

## <a name="itemssource"></a>ItemsSource

Объект [ `ListView` ](xref:Xamarin.Forms.ListView) заполняется данными с помощью [ `ItemsSource` ](xref:Xamarin.Forms.ItemsView`1.ItemsSource) свойство, которое может принимать любое коллекция, реализующая `IEnumerable`. Самый простой способ заполнения `ListView` предполагает использование массива строк:

```xaml
<ListView>
      <ListView.ItemsSource>
          <x:Array Type="{x:Type x:String}">
            <x:String>mono</x:String>
            <x:String>monodroid</x:String>
            <x:String>monotouch</x:String>
            <x:String>monorail</x:String>
            <x:String>monodevelop</x:String>
            <x:String>monotone</x:String>
            <x:String>monopoly</x:String>
            <x:String>monomodal</x:String>
            <x:String>mononucleosis</x:String>
          </x:Array>
      </ListView.ItemsSource>
</ListView>
```

Ниже приведен аналогичный код C#:

```csharp
var listView = new ListView();
listView.ItemsSource = new string[]
{
  "mono",
  "monodroid",
  "monotouch",
  "monorail",
  "monodevelop",
  "monotone",
  "monopoly",
  "monomodal",
  "mononucleosis"
};

//monochrome will not appear in the list because it was added
//after the list was populated.
listView.ItemsSource.Add("monochrome");
```

![](data-and-databinding-images/itemssource-simple.png "ListView отображения списка строк")

Выше метод будет заполнять `ListView` со списком строк. По умолчанию `ListView` вызовет `ToString` и отображения результата в `TextCell` для каждой строки. Чтобы настроить способ отображения данных, см. в разделе [внешний вид ячейки](~/xamarin-forms/user-interface/listview/customizing-cell-appearance.md).

Так как `ItemsSource` отправлен в массив, не будет обновляться при изменении базового списка или массива. Если требуется ListView на автоматическое обновление при элементы добавления, удаления и изменения в базовом списке, необходимо использовать `ObservableCollection`. [`ObservableCollection`](xref:System.Collections.ObjectModel.ObservableCollection`1) определяется в `System.Collections.ObjectModel` и так же, как `List`, за исключением того, что их можно уведомить `ListView` о любых изменениях:

```csharp
ObservableCollection<Employee> employees = new ObservableCollection<Employee>();
listView.ItemsSource = employees;

//Mr. Mono will be added to the ListView because it uses an ObservableCollection
employees.Add(new Employee(){ DisplayName="Mr. Mono"});
```

<a name="Data_Binding" />

## <a name="data-binding"></a>Привязка данных
Привязка данных является «объединяющей» связывает свойства данного объекта пользовательского интерфейса к свойствам объекта среды CLR, например класс в вашей модели представления. Привязка данных полезно в тех случаях, поскольку он упрощает разработку пользовательских интерфейсов, заменив массу скучно стандартный код.

Привязка данных работает путем синхронизации объектов при изменении их связанных значений. Вместо того, чтобы написать обработчики событий для каждый раз при изменении значения элемента управления, устанавливать привязки и включить привязку в вашей модели представления.

Дополнительные сведения о привязке данных см. в разделе [основы привязки данных](~/xamarin-forms/xaml/xaml-basics/data-binding-basics.md) которого является четвертой частью [серия статей основы XAML Xamarin.Forms](~/xamarin-forms/xaml/xaml-basics/index.md).

### <a name="binding-cells"></a>Привязка ячеек
Свойства ячеек (и дочерних ячеек) могут быть привязаны к свойствам объектов в `ItemsSource`. Например ListView может использоваться для представления списка сотрудников.

Класса "Сотрудник":

```csharp
public class Employee
{
    public string DisplayName {get; set;}
}
```

`ObservableCollection<Employee>` создается и задается как `ListView`в `ItemsSource`:

```csharp
ObservableCollection<Employee> employees = new ObservableCollection<Employee>();
public EmployeeListPage()
{
  //defined in XAML to follow
  EmployeeView.ItemsSource = employees;
  ...
}
```

Список заполняется данными:

```csharp
public EmployeeListPage()
{
  ...
  employees.Add(new Employee{ DisplayName="Rob Finnerty"});
  employees.Add(new Employee{ DisplayName="Bill Wrestler"});
  employees.Add(new Employee{ DisplayName="Dr. Geri-Beth Hooper"});
  employees.Add(new Employee{ DisplayName="Dr. Keith Joyce-Purdy"});
  employees.Add(new Employee{ DisplayName="Sheri Spruce"});
  employees.Add(new Employee{ DisplayName="Burt Indybrick"});
}
```

В следующем фрагменте показано `ListView` привязан к список сотрудников:

```xaml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:constants="clr-namespace:XamarinFormsSample;assembly=XamarinFormsXamlSample"
x:Class="XamarinFormsXamlSample.Views.EmployeeListPage"
Title="Employee List">
  <ListView x:Name="EmployeeView">
    <ListView.ItemTemplate>
      <DataTemplate>
        <TextCell Text="{Binding DisplayName}" />
      </DataTemplate>
    </ListView.ItemTemplate>
  </ListView>
</ContentPage>
```

Обратите внимание на то, что привязка была настроена в коде для простоты, несмотря на то, что он может привязаны в XAML.

Предыдущий часть XAML определяет `ContentPage` , содержащий `ListView`. Источник данных `ListView` задается с помощью `ItemsSource` атрибута. Макет каждой строки в `ItemsSource`определяется внутри `ListView.ItemTemplate` элемент.

Это результат:

![](data-and-databinding-images/bound-data.png "С помощью привязки данных ListView")

### <a name="binding-selecteditem"></a>SelectedItem привязки

Часто необходимо привязать к выбранному элементу списка `ListView`, вместо того чтобы использовать обработчик событий для реагирования на изменения. Чтобы сделать это в XAML, создайте привязку `SelectedItem` свойство:

```xaml
<ListView x:Name="listView"
 SelectedItem="{Binding Source={x:Reference SomeLabel},
 Path=Text}">
 …
</ListView>
```

При условии, что `listView` `ItemsSource` является список строк, `SomeLabel` будет иметь свойства text, привязанного к `SelectedItem`.

## <a name="related-links"></a>Связанные ссылки

- [Двусторонней привязки (пример)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/ListView/SwitchEntryTwoBinding)
