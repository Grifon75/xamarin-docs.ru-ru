---
ms.openlocfilehash: 5929648b802c27916c0a21142907644781d59d0d
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61193255"
---
# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

1. Запустите Visual Studio и создайте пустое приложение Xamarin.Forms **LocalDatabaseTutorial**. Убедитесь, что в качестве механизма общего кода в приложении используется .NET Standard.

    > [!IMPORTANT]
    > Для фрагментов кода на C# и XAML в этом руководстве необходимо решение с именем **LocalDatabaseTutorial**. Выбор другого имени приведет к ошибкам сборки при копировании кода из этого руководства в решение.

    Дополнительные сведения о создаваемой библиотеке .NET Standard см. в разделе [Структура приложения Xamarin.Forms](~/get-started/first-app/index.md) статьи [Краткое руководство по Xamarin.Forms глубокое погружение в обработку](~/get-started/first-app/index.md).

1. В **обозревателе решений** выберите проект **LocalDatabaseTutorial**, щелкните правой кнопкой мыши и выберите **Управление пакетами NuGet...**.

    ![Снимок экрана пункта меню "Управление пакетами NuGet"](../images/vs/add-nuget-packages.png "пункт меню \"Добавить пакеты NuGet\"")

1. В разделе **Диспетчер пакетов NuGet** выберите вкладку **Обзор**, выполните поиск пакета NuGet **sqlite-net-pcl**, выберите его и нажмите кнопку **Установить**, чтобы добавить его в проект.

    ![Снимок экрана пакета NuGet для SQLite.NET в диспетчере пакетов NuGet](../images/vs/add-package.png "пакет NuGet для SQLite.NET")

    > [!NOTE]
    > Существует ряд пакетов NuGet с похожими названиями. Правильный пакет имеет следующие атрибуты:
    > - **Автор(ы)**: Фрэнк А. Крюгер (Frank A. Krueger)
    > - **Идентификатор:** sqlite-net-pcl
    > - **Ссылка в NuGet:** [sqlite-net-pcl](https://www.nuget.org/packages/sqlite-net-pcl/)  
    >
    > Несмотря на название, этот пакет NuGet можно использовать в проектах .NET Standard.

    Этот пакет будет использоваться для включения операций базы данных в приложение.

1. Создайте решение, чтобы убедиться в отсутствии ошибок.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio для Mac](#tab/vsmac)

1. Запустите Visual Studio для Mac и создайте пустое приложение Xamarin.Forms **LocalDatabaseTutorial**. Убедитесь, что в качестве механизма общего кода в приложении используется .NET Standard.

    > [!IMPORTANT]
    > Для фрагментов кода на C# и XAML в этом руководстве необходимо решение с именем **LocalDatabaseTutorial**. Выбор другого имени приведет к ошибкам сборки при копировании кода из этого руководства в решение.
    
    Дополнительные сведения о создаваемой библиотеке .NET Standard см. в разделе [Структура приложения Xamarin.Forms](~/get-started/first-app/index.md) статьи [Краткое руководство по Xamarin.Forms глубокое погружение в обработку](~/get-started/first-app/index.md).

1. На **Панели решения** выберите проект **LocalDatabaseTutorial**, щелкните правой кнопкой мыши и выберите **Добавить > Добавить пакеты NuGet...**.

    ![Снимок экрана пункта меню "Добавить пакеты NuGet"](../images/vsmac/add-nuget-packages.png "пункт меню \"Добавить пакеты NuGet\"")

1. В окне **Добавление пакетов** выполните поиск пакета NuGet **sqlite-net-pcl**, выберите его и нажмите кнопку **Добавить пакет**, чтобы добавить его в проект.

    ![Снимок экрана пакета NuGet для SQLite.NET в диспетчере пакетов NuGet](../images/vsmac/add-package.png "пакет NuGet для SQLite.NET")

    > [!NOTE]
    > Существует ряд пакетов NuGet с похожими названиями. Правильный пакет имеет следующие атрибуты:
    > - **Автор**: Фрэнк А. Крюгер (Frank A. Krueger)
    > - **Идентификатор:** sqlite-net-pcl
    > - **Ссылка в NuGet:** [sqlite-net-pcl](https://www.nuget.org/packages/sqlite-net-pcl/)  
    >
    > Несмотря на название, этот пакет NuGet можно использовать в проектах .NET Standard.

    Этот пакет будет использоваться для включения операций базы данных в приложение.

1. Создайте решение, чтобы убедиться в отсутствии ошибок.
