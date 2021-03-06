---
title: Проверка подлинности пользователей с помощью поставщика удостоверений
description: В этой статье описываются способы использования Xamarin.Auth для управления процессом проверки подлинности в приложении Xamarin.Forms.
ms.prod: xamarin
ms.assetid: D44745D5-77BB-4596-9B8C-EC75C259157C
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 06/19/2017
ms.openlocfilehash: 786f1503fcc0cc07f76a7cdc55731d341607429f
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61331117"
---
# <a name="authenticating-users-with-an-identity-provider"></a>Проверка подлинности пользователей с помощью поставщика удостоверений

[![Загрузить образец](~/media/shared/download.png) загрузить пример](https://developer.xamarin.com/samples/xamarin-forms/WebServices/OAuthNativeFlow/)

_Xamarin.Auth — это кроссплатформенный пакет SDK для проверки подлинности пользователей и хранения учетной записью. Он включает в себя структур проверки подлинности OAuth, которые предоставляют поддержку использования поставщиков удостоверений, например Google, Майкрософт, Facebook и Twitter. В этой статье описываются способы использования Xamarin.Auth для управления процессом проверки подлинности в приложении Xamarin.Forms._

OAuth — это открытый стандарт для проверки подлинности, а также позволяет владелец ресурса может уведомлять поставщика ресурсов, что разрешение следует предоставлять третьим лицам получить доступ к информации о без совместного использования удостоверения владельцев ресурса. Примером этого может выдаче пользователю возможность уведомлять поставщика удостоверений (например, Google, Майкрософт, Facebook или Twitter), в предоставлении этого разрешения приложению для доступа к своим данным, без предоставления общего доступа удостоверение пользователя. Обычно он используется подход для пользователей для входа в веб-сайтов и приложений с помощью поставщика удостоверений, но без предоставления пароля для веб-сайта или приложения.

Общий обзор потока проверки подлинности при использовании поставщика удостоверений OAuth выглядит следующим образом:

1. Приложение переходит в браузере URL-адрес поставщика удостоверений.
1. Поставщик удостоверений выполняет проверку подлинности пользователя и возвращает код авторизации приложению.
1. Приложение выполняет обмен кода авторизации для маркера доступа от поставщика удостоверений.
1. Приложение использует маркер доступа для доступа к API на поставщика удостоверений, например API для запроса основных пользовательских данных.

Пример приложения демонстрирует использование Xamarin.Auth, чтобы реализовать собственную аутентификацию поток от Google. Хотя Google используется в качестве поставщика удостоверений в этом разделе, этот подход также применима и для других поставщиков удостоверений. Дополнительные сведения о проверке подлинности с помощью конечной точки OAuth 2.0 от Google, см. в разделе [с помощью OAuth 2.0 для API-интерфейсы для доступа к Google](https://developers.google.com/identity/protocols/OAuth2) на веб-сайте компании Google.

> [!NOTE]
> В iOS 9 и более поздней версии приложение Transport Security (ATS) обеспечивает безопасных соединений между Интернет-ресурсов (например, server серверной части приложения) и приложения, тем самым предотвращая случайное раскрытие конфиденциальной информации. Поскольку ATS включена по умолчанию в приложениях, созданных для iOS 9, все подключения будут применяться требования к безопасности ATS. Если соединения не удовлетворяют этим требованиям, они вызовут сбой с исключением.
> Если невозможно использовать из могут быть присоединены ATS `HTTPS` протокола и безопасный обмен данными для Интернет-ресурсов. Это достигается путем обновления приложения **Info.plist** файла. Дополнительные сведения см. в разделе [безопасность транспорта приложения](~/ios/app-fundamentals/ats.md).

## <a name="using-xamarinauth-to-authenticate-users"></a>С помощью Xamarin.Auth для проверки подлинности пользователей

Xamarin.Auth поддерживает два подхода к приложениям взаимодействовать с конечной точкой авторизации поставщика удостоверений:

1. С помощью внедренных веб-представление. Эта возможность была распространенной практикой, но больше не рекомендуется по следующим причинам:

    - Приложения, на котором размещена веб-представлении можно получить доступ к полной проверки подлинности учетных данных пользователя, не только предоставления авторизации OAuth, предназначенного для приложения. Это нарушает принцип наименьших прав доступа, эти приложения имеют доступ к более мощные учетные данные, чем это необходимо, потенциально увеличивать поверхность атаки приложения.
    - Ведущее приложение может записать имена пользователей и пароли, автоматически отправлять формы и обходить согласия пользователя и скопируйте файлы cookie сеанса и использовать их для выполнения действий, прошедшего проверку подлинности как пользователь.
    - Embedded веб-представления не находиться в состоянии проверки подлинности с другим приложениям или веб-браузере устройства, требующее от пользователя для входа в систему для каждого запроса авторизации, которое считается взаимодействие с пользователем плох.
    - Несколько конечных точек авторизации действий обнаружения и блокировки, полученные из веб-представлений запросов на авторизацию.

1. С помощью веб-браузере устройства, который является рекомендуемым подходом. С помощью обозревателя устройств для OAuth запросов повышает удобство использования приложения, как пользователям нужно только войти в поставщик удостоверений один раз в устройство, повышение скорости преобразования потоков входа и авторизации в приложении. Браузер на устройстве также обеспечивает повышенную безопасность, как приложения могут проверять и изменять содержимое в веб-представление, но не содержимое, отображаемое в браузере. Это подход для использования в этом статья и образец приложения.

На следующей схеме показан общий обзор того, как пример приложения использует Xamarin.Auth для проверки подлинности пользователей и получения их основные данные:

![](oauth-images/google-auth.png "С помощью Xamarin.Auth для проверки подлинности с помощью Google")

Приложение отправляет запрос на проверку подлинности с помощью Google `OAuth2Authenticator` класса. Ответ проверки подлинности возвращается, когда пользователь успешно прошел аутентификацию с помощью Google через их страницы входа, который включает в себя маркер доступа. Затем приложение отправляет запрос Google для основных пользовательских данных, с помощью `OAuth2Request` класс с маркером доступа, включаются в запрос.

### <a name="setup"></a>Установка

Проект консоли Google API должны создаваться для интеграции Google вход с помощью приложения Xamarin.Forms. Это можно обеспечить, выполнив следующие действия.

1. Перейдите к [консоли Google API](http://console.developers.google.com) веб-сайта и войдите с помощью учетной записи Google.
1. Из раскрывающегося списка проект выберите существующий проект или создайте новую.
1. На боковой панели в разделе «Диспетчер API», выберите **учетные данные**, а затем выберите **вкладке экран согласия OAuth**. Выберите **адрес электронной почты**, укажите **имя продукта для пользователей**и нажмите клавишу **Сохранить**.
1. В **учетные данные** выберите **создайте учетные данные** выберите в раскрывающемся списке и выберите **идентификатор клиента OAuth**.
1. В разделе **тип приложения**, выберите платформу, мобильными приложениями, которые будут выполняться на (**iOS** или **Android**).
1. Заполните необходимые сведения и выберите **создать** кнопки.

> [!NOTE]
> Идентификатор клиента позволяет приложению получить доступ к включенных API-интерфейсов Google и для мобильных приложений является уникальным для нескольких платформ. Таким образом **идентификатор клиента OAuth** должен быть создан для каждой платформы, которую будет использовать входа в Google.

После выполнения этих действий, можно использовать Xamarin.Auth инициировать поток проверки подлинности OAuth2 с помощью Google.

### <a name="creating-and-configuring-an-authenticator"></a>Создание и настройка средства проверки подлинности

В Xamarin.Auth `OAuth2Authenticator` класс отвечает за обработку проверки подлинности OAuth. В следующем примере кода показано создание экземпляров `OAuth2Authenticator` класс при проверке подлинности с помощью веб-браузере устройства:

```csharp
var authenticator = new OAuth2Authenticator(
    clientId,
    null,
    Constants.Scope,
    new Uri(Constants.AuthorizeUrl),
    new Uri(redirectUri),
    new Uri(Constants.AccessTokenUrl),
    null,
    true);
```

`OAuth2Authenticator` Класса требуется ряд параметров, которые являются следующим образом:

- **Идентификатор клиента** — определяет клиент, который выполняет запрос и могут быть получены из проекта в [консоли Google API](http://console.developers.google.com).
- **Секрет клиента** — это должен быть `null` или `string.Empty`.
- **Область** — определяет доступ к API, запрашиваемый приложением, и значение сообщает экран согласия, который отображается для пользователя. Дополнительные сведения об областях см. в разделе [запроса авторизации API](https://developers.google.com/+/web/api/rest/oauth) на веб-сайте компании Google.
- **Авторизация URL-адрес** — данный параметр определяет, где будет получен код авторизации из URL-адрес.
- **URL-адрес перенаправления** – это определяет URL-адрес, куда будут отправляться ответ. Значение этого параметра должен соответствовать одному из значений, отображающиеся в **учетные данные** вкладку для проекта в [Google Developers Console](https://console.developers.google.com/).
- **URL-адрес AccessToken** – это определяет URL-адрес, используемый для запроса маркеров доступа, после получения кода авторизации.
- **GetUserNameAsync Func** — необязательный `Func` , будет использоваться асинхронно получить имя пользователя учетной записи, когда он является успешно проверена.
- **С помощью собственного пользовательского интерфейса** — `boolean` значение, указывающее, следует ли использовать веб-браузере устройства для выполнения запроса на проверку подлинности.

### <a name="setup-authentication-event-handlers"></a>Настройка проверки подлинности обработчики событий

Перед представлением пользовательского интерфейса, обработчик событий для `OAuth2Authenticator.Completed` событий должны регистрироваться, как показано в следующем примере кода:

```csharp
authenticator.Completed += OnAuthCompleted;
```

Эти события возникают, когда пользователь успешно проходит проверку подлинности или отменяет входа в систему.

Кроме того, обработчик событий для `OAuth2Authenticator.Error` событие также может быть зарегистрировано.

### <a name="presenting-the-sign-in-user-interface"></a>Представление входа в пользовательском интерфейсе

Интерфейс входа в систему могут отображаться для пользователя с помощью имени входа Xamarin.Auth презентатор, в которой должны быть инициализированы в каждом проекте платформы. В следующем примере кода показано, как инициализировать средство отображения имени входа в `AppDelegate` класс в проекте iOS:

```csharp
global::Xamarin.Auth.Presenters.XamarinIOS.AuthenticationConfiguration.Init();
```

В следующем примере кода показано, как инициализировать средство отображения имени входа в `MainActivity` класс в проекте Android:

```csharp
global::Xamarin.Auth.Presenters.XamarinAndroid.AuthenticationConfiguration.Init(this, bundle);
```

Проект библиотеки .NET Standard затем можно вызвать операцию презентатор входа следующим образом:

```csharp
var presenter = new Xamarin.Auth.Presenters.OAuthLoginPresenter();
presenter.Login(authenticator);
```

Обратите внимание, что аргумент `Xamarin.Auth.Presenters.OAuthLoginPresenter.Login` метод `OAuth2Authenticator` экземпляра. Когда `Login` вызова метода, входа в пользовательском интерфейсе отображаются для пользователя на вкладке веб-браузере устройства, как показано на следующем снимке экрана:

![](oauth-images/login.png "Google Sign-In")

### <a name="processing-the-redirect-url"></a>Обработка URL-адрес перенаправления

Как только пользователь завершит процесс проверки подлинности, элемент управления будет отправлять приложения из вкладку веб-браузера. Это достигается путем регистрации схему URL-адрес для URL-адрес перенаправления, который возвращается из процесса проверки подлинности и затем обнаружить и обработать пользовательский URL-адрес, после его отправки.

При выборе схему URL-адрес должен быть сопоставлен приложения, приложения должны использовать схему, основанную на имени, находящийся под его контролем. Это можно сделать с помощью имя идентификатора пакета в iOS и имя пакета на устройстве Android, а затем обращение их, чтобы сделать схему URL-адрес. Тем не менее некоторые поставщики удостоверений, например, Google, назначьте идентификаторы клиента, используя доменные имена, которые затем в обратном порядке и используются в качестве схемы URL-адрес. Например, если Google создает идентификатор клиента `902730282010-ks3kd03ksoasioda93jldas93jjj22kr.apps.googleusercontent.com`, схема URL-адрес будет `com.googleusercontent.apps.902730282010-ks3kd03ksoasioda93jldas93jjj22kr`. Обратите внимание, что только один `/` могут проявиться после компонент схемы. Таким образом, полный пример, URL-адрес перенаправления, используя схему URL-адрес является `com.googleusercontent.apps.902730282010-ks3kd03ksoasioda93jldas93jjj22kr:/oauth2redirect`.

При получении ответа от поставщика удостоверений, который содержит схему URL-адрес веб-браузер, он пытается загрузить URL-адрес, что приводит к ошибке. Вместо этого пользовательские схемы URL-адрес передается в операционную систему, вызывая событие. Операционная система осуществляет поиск зарегистрированных схем, и если он найден, операционная система будет запустится приложение, зарегистрированные схемы и отправить его URL-адрес перенаправления.

Механизм для регистрации схему URL-адрес в операционную систему и обработке схеме конкретной платформы.

#### <a name="ios"></a>iOS

В iOS, схему URL-адрес зарегистрирован в **Info.plist**, как показано на следующем снимке экрана:

![](oauth-images/info-plist.png "Регистрация схемы URL-адреса")

**Идентификатор** значение может быть любым и **роли** должно быть присвоено значение **средство просмотра**. **Схемы URL-адресов** значение, которое начинается с `com.googleusercontent.apps`, можно получить из идентификатора клиента iOS для проекта на [консоли Google API](http://console.developers.google.com).

По завершении запроса на авторизацию поставщик удостоверений перенаправляет URL-адрес перенаправления для приложения. Так как URL-адрес использует схему приводит запуска приложения iOS, передачи в URL-адрес в качестве параметра запуска, где он обрабатывается `OpenUrl` переопределить приложения `AppDelegate` класс, который показан в следующем примере кода:

```csharp
public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
{
    // Convert NSUrl to Uri
    var uri = new Uri(url.AbsoluteString);

    // Load redirectUrl page
    AuthenticationState.Authenticator.OnPageLoading(uri);

    return true;
}
```

`OpenUrl` Метод преобразует URL-адрес, полученных из `NSUrl` к типу .NET `Uri`, перед обработкой URL-адрес перенаправления с `OnPageLoading` метод открытой `OAuth2Authenticator` объекта. В результате Xamarin.Auth чтобы закрыть вкладку веб-браузера и синтаксический анализ полученных данных OAuth.

#### <a name="android"></a>Android

В Android схему URL-адрес зарегистрирован, указав [ `IntentFilter` ](https://developer.xamarin.com/api/type/Android.App.IntentFilterAttribute/) атрибут `Activity` , обрабатывающий схемы. По завершении запроса на авторизацию поставщик удостоверений перенаправляет URL-адрес перенаправления для приложения. Как URL-адрес использует схему приводит к Android, запустив приложение, передачи в URL-адрес в качестве параметра запуска, где он обрабатывается `OnCreate` метод `Activity` зарегистрированном для обработки пользовательских схема URL-адреса. В следующем примере кода показан класс из примера приложения, который обрабатывает пользовательские схемы URL-адрес:

```csharp
[Activity(Label = "CustomUrlSchemeInterceptorActivity", NoHistory = true, LaunchMode = LaunchMode.SingleTop )]
[IntentFilter(
    new[] { Intent.ActionView },
    Categories = new [] { Intent.CategoryDefault, Intent.CategoryBrowsable },
    DataSchemes = new [] { "<insert custom URL here>" },
    DataPath = "/oauth2redirect")]
public class CustomUrlSchemeInterceptorActivity : Activity
{
    protected override void OnCreate(Bundle savedInstanceState)
    {
        base.OnCreate(savedInstanceState);

        // Convert Android.Net.Url to Uri
        var uri = new Uri(Intent.Data.ToString());

        // Load redirectUrl page
        AuthenticationState.Authenticator.OnPageLoading(uri);

        Finish();
    }
}
```

`DataSchemes` Свойство [ `IntentFilter` ](https://developer.xamarin.com/api/type/Android.App.IntentFilterAttribute/) должно быть присвоено идентификатор обратном клиента, полученный из идентификатора клиента Android для проекта на [консоли Google API](http://console.developers.google.com).

`OnCreate` Метод преобразует URL-адрес, полученных из `Android.Net.Url` к типу .NET `Uri`, перед обработкой URL-адрес перенаправления с `OnPageLoading` метод открытой `OAuth2Authenticator` объекта. В результате Xamarin.Auth закрыть вкладку веб-браузера, а синтаксический анализ полученных данных OAuth.

> [!IMPORTANT]
> В Android использует Xamarin.Auth `CustomTabs` API для взаимодействия с веб-браузер и операционной системы. Тем не менее, он не гарантирует, что `CustomTabs` совместимый обозреватель будет установлен на устройстве пользователя.

### <a name="examining-the-oauth-response"></a>Проверка ответа OAuth

После синтаксического анализа полученных данных OAuth, вызовут Xamarin.Auth `OAuth2Authenticator.Completed` событий. В обработчике событий для данного события `AuthenticatorCompletedEventArgs.IsAuthenticated` свойства позволяют определить, является ли проверка подлинности успешно пройдена, как показано в следующем примере кода:

```csharp
async void OnAuthCompleted(object sender, AuthenticatorCompletedEventArgs e)
{
  ...
  if (e.IsAuthenticated)
  {
    ...
  }
}
```

Данные, собранные с успешной проверки подлинности доступна в `AuthenticatorCompletedEventArgs.Account` свойство. Это включает в себя маркер доступа, который может использоваться для подписывания запросов для данных в API, предоставляемые поставщиком удостоверений.

### <a name="making-requests-for-data"></a>Создание запросов для данных

После приложение получает маркер доступа, он используется для создания запроса к `https://www.googleapis.com/oauth2/v2/userinfo` API для запроса основных пользовательских данных от поставщика удостоверений. Этот запрос выполняется с помощью элемента Xamarin.Auth `OAuth2Request` класс, который представляет запрос, который проходит проверку подлинности, используя учетную запись, полученную `OAuth2Authenticator` экземпляра, как показано в следующем примере кода:

```csharp
// UserInfoUrl = https://www.googleapis.com/oauth2/v2/userinfo
var request = new OAuth2Request ("GET", new Uri (Constants.UserInfoUrl), null, e.Account);
var response = await request.GetResponseAsync ();
if (response != null)
{
  string userJson = response.GetResponseText ();
  var user = JsonConvert.DeserializeObject<User> (userJson);
}
```

А также метод HTTP и URL-адреса API `OAuth2Request` экземпляр также задает `Account` экземпляр, который содержит маркер доступа, который подписывает запрос на URL-адрес, указанный по `Constants.UserInfoUrl` свойство. Затем поставщик удостоверений возвращает основных пользовательских данных в ответ JSON, включая имя пользователя и адрес электронной почты, при условии, что маркер доступа он распознает как допустимые. Ответ JSON считывается и десериализируется в `user` переменной.

Дополнительные сведения см. в разделе [вызова интерфейса API Google](https://developers.google.com/identity/protocols/OAuth2InstalledApp#callinganapi) на портале разработчиков Google.

### <a name="storing-and-retrieving-account-information-on-devices"></a>Хранения и извлечения сведений учетной записи на устройствах

Надежно хранит Xamarin.Auth `Account` объектов в учетной записи хранения, чтобы приложения не всегда нужно пройти повторную проверку подлинности пользователей. `AccountStore` Класс хранит сведения об учетной записи и поддерживается службами цепочку ключей в iOS и `KeyStore` класс в Android.

В следующем примере кода как `Account` безопасно сохранен объект:

```csharp
AccountStore.Create ().Save (e.Account, Constants.AppName);
```

Сохраненные учетные записи однозначно определяются с помощью ключа, состоящие из учетной записи `Username` свойство и идентификатор службы, который является строкой, который используется при получении учетных записей из учетной записи хранилища. Если `Account` сохраненный ранее, вызов `Save` метод снова перезапишет его.

`Account` объекты для службы можно получить, вызвав `FindAccountsForService` метод, как показано в следующем примере кода:

```csharp
var account = AccountStore.Create ().FindAccountsForService (Constants.AppName).FirstOrDefault();
```

`FindAccountsForService` Возвращает `IEnumerable` коллекцию `Account` объектов с первого элемента в коллекции, установить в качестве учетной записи сопоставленной.

## <a name="summary"></a>Сводка

В этой статье описываются способы использования Xamarin.Auth для управления процессом проверки подлинности в приложении Xamarin.Forms. Предоставляет Xamarin.Auth `OAuth2Authenticator` и `OAuth2Request` классы, используемые в приложениях Xamarin.Forms использовать Поставщики удостоверений, например Google, Майкрософт, Facebook и Twitter.


## <a name="related-links"></a>Связанные ссылки

- [OAuthNativeFlow (пример)](https://developer.xamarin.com/samples/xamarin-forms/WebServices/OAuthNativeFlow/)
- [OAuth 2.0 для собственных приложений](https://tools.ietf.org/html/draft-ietf-oauth-native-apps-12)
- [С помощью OAuth 2.0 для доступа к API Google](https://developers.google.com/identity/protocols/OAuth2)
- [Xamarin.Auth (NuGet)](https://www.nuget.org/packages/xamarin.auth/)
- [Xamarin.Auth (GitHub)](https://github.com/xamarin/Xamarin.Auth)
