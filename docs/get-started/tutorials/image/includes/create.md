---
ms.openlocfilehash: 550828327eb6b72c1c9712e54e6e36c9e30bd1f0
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61384580"
---
# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

1. Запустите Visual Studio и создайте пустое приложение Xamarin.Forms **ImageTutorial**. Убедитесь, что в качестве механизма общего кода в приложении используется .NET Standard.

    > [!IMPORTANT]
    > Для фрагментов кода на C# и XAML в этом руководстве необходимо решение с именем **ImageTutorial**. Выбор другого имени приведет к ошибкам сборки при копировании кода из этого руководства в решение.

    Дополнительные сведения о создаваемой библиотеке .NET Standard см. в разделе [Структура приложения Xamarin.Forms](~/get-started/first-app/index.md) статьи [Краткое руководство по Xamarin.Forms глубокое погружение в обработку](~/get-started/first-app/index.md).

1. В **обозревателе решений** дважды щелкните файл **MainPage.xaml** в проекте **ImageTutorial**, чтобы открыть его. В **MainPage.xaml** удалите весь код шаблона и замените его приведенным ниже кодом.

    ```xaml
    <?xml version="1.0" encoding="utf-8"?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
                 xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                 x:Class="ImageTutorial.MainPage">
        <StackLayout Margin="20,35,20,20">
            <Image Source="http://upload.wikimedia.org/wikipedia/commons/thumb/f/fc/Papio_anubis_%28Serengeti%2C_2009%29.jpg/200px-Papio_anubis_%28Serengeti%2C_2009%29.jpg"
                   HeightRequest="300" />
        </StackLayout>
    </ContentPage>
    ```

    Этот код декларативно определяет пользовательский интерфейс для страницы, который состоит из [`Image`](xref:Xamarin.Forms.Image) в [`StackLayout`](xref:Xamarin.Forms.StackLayout). Свойство [`Image.Source`](xref:Xamarin.Forms.Image.Source) задает отображаемый образ с помощью универсального кода ресурса (URI). Свойство [`Image.Source`](xref:Xamarin.Forms.Image.Source) типа [`ImageSource`](xref:Xamarin.Forms.ImageSource) позволяет такие источники образов, как файлы, универсальные коды ресурса (URI) или ресурсы. Дополнительные сведения см. в разделе [Displaying images](~/xamarin-forms/user-interface/images.md#displaying-images) (Отображение изображений) в руководстве [Images in Xamarin.Forms](~/xamarin-forms/user-interface/images.md) (Изображения в Xamarin.Forms).

    Свойство [`HeightRequest`](xref:Xamarin.Forms.VisualElement) указывает высоту `Image` в аппаратно-независимых единицах.

    > [!NOTE]
    > В этом примере нет необходимости задавать свойство [`WidthRequest`](xref:Xamarin.Forms.VisualElement.WidthRequest). Это обусловлено тем, что [`Image`](xref:Xamarin.Forms.Image) по умолчанию сохраняет пропорции изображения.

1. На панели инструментов Visual Studio нажмите кнопку **Пуск** (треугольная кнопка, похожая на кнопку воспроизведения) для запуска приложения в выбранном удаленном симуляторе iOS или эмуляторе Android.

    [![Снимок экрана с изображением в iOS и Android](../images/create-image.png "Представление изображения в графическом режиме")](../images/create-image-large.png#lightbox "Представление изображения в графическом режиме")

    > [!NOTE]
    > Просмотр [`Image`](xref:Xamarin.Forms.Image) автоматически кэширует скачанные изображения на 24 часа. Дополнительные сведения см. в разделе [Downloaded image caching](~/xamarin-forms/user-interface/images.md#downloaded-image-caching) (Кэширование скачанного изображения) в руководстве [Images in Xamarin.Forms](~/xamarin-forms/user-interface/images.md) (Изображения в Xamarin.Forms).

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio для Mac](#tab/vsmac)

1. Запустите Visual Studio для Mac и создайте пустое приложение Xamarin.Forms **ImageTutorial**. Убедитесь, что в качестве механизма общего кода в приложении используется .NET Standard.

    > [!IMPORTANT]
    > Для фрагментов кода на C# и XAML в этом руководстве необходимо решение с именем **ImageTutorial**. Выбор другого имени приведет к ошибкам сборки при копировании кода из этого руководства в решение.

    Дополнительные сведения о создаваемой библиотеке .NET Standard см. в разделе [Структура приложения Xamarin.Forms](~/get-started/first-app/index.md) статьи [Краткое руководство по Xamarin.Forms глубокое погружение в обработку](~/get-started/first-app/index.md).

1. На **Панели решений** в проекте **ImageTutorial** дважды щелкните файл **MainPage.xaml**, чтобы открыть его. В **MainPage.xaml** удалите весь код шаблона и замените его приведенным ниже кодом.

    ```xaml
    <?xml version="1.0" encoding="utf-8"?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
                 xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                 x:Class="ImageTutorial.MainPage">
        <StackLayout Margin="20,35,20,20">
            <Image Source="http://upload.wikimedia.org/wikipedia/commons/thumb/f/fc/Papio_anubis_%28Serengeti%2C_2009%29.jpg/200px-Papio_anubis_%28Serengeti%2C_2009%29.jpg"
                   HeightRequest="300" />
        </StackLayout>
    </ContentPage>
    ```

    Этот код декларативно определяет пользовательский интерфейс для страницы, который состоит из [`Image`](xref:Xamarin.Forms.Image) в [`StackLayout`](xref:Xamarin.Forms.StackLayout). Свойство [`Image.Source`](xref:Xamarin.Forms.Image.Source) задает отображаемый образ с помощью универсального кода ресурса (URI). Свойство [`Image.Source`](xref:Xamarin.Forms.Image.Source) типа [`ImageSource`](xref:Xamarin.Forms.ImageSource) позволяет такие источники образов, как файлы, универсальные коды ресурса (URI) или ресурсы. Дополнительные сведения см. в разделе [Displaying images](~/xamarin-forms/user-interface/images.md#displaying-images) (Отображение изображений) в руководстве [Images in Xamarin.Forms](~/xamarin-forms/user-interface/images.md) (Изображения в Xamarin.Forms).

    Свойство [`HeightRequest`](xref:Xamarin.Forms.VisualElement) указывает высоту `Image` в аппаратно-независимых единицах.

    > [!NOTE]
    > В этом примере нет необходимости задавать свойство [`WidthRequest`](xref:Xamarin.Forms.VisualElement.WidthRequest). Это обусловлено тем, что [`Image`](xref:Xamarin.Forms.Image) по умолчанию сохраняет пропорции изображения.

1. На панели инструментов Visual Studio для Mac нажмите кнопку **Пуск** (треугольная кнопка, похожая на кнопку воспроизведения) для запуска приложения в выбранном симуляторе iOS или эмуляторе Android.

    [![Снимок экрана с изображением в iOS и Android](../images/create-image.png "Представление изображения в графическом режиме")](../images/create-image-large.png#lightbox "Представление изображения в графическом режиме")

    > [!NOTE]
    > Просмотр [`Image`](xref:Xamarin.Forms.Image) автоматически кэширует скачанные изображения на 24 часа. Дополнительные сведения см. в разделе [Downloaded image caching](~/xamarin-forms/user-interface/images.md#downloaded-image-caching) (Кэширование скачанного изображения) в руководстве [Images in Xamarin.Forms](~/xamarin-forms/user-interface/images.md) (Изображения в Xamarin.Forms).
