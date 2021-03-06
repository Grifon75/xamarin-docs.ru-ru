---
title: Доступ к удаленным данным
description: В данной главе объясняется, как мобильное приложение eShopOnContainers обращается к данным из контейнерных микрослужб.
ms.prod: xamarin
ms.assetid: 42eba6f5-9784-4e1a-9943-5c1fbeea7452
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/07/2017
ms.openlocfilehash: 3a46b939fa87cd6535c9f86c46981c098542e7c9
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61277972"
---
# <a name="accessing-remote-data"></a>Доступ к удаленным данным

Многие современные решения на основе веб-сделать использование веб-служб, размещенных на веб-серверах, для предоставления функций для удаленных клиентских приложений. Операции, которые веб-служба предоставляет составляют веб-API.

Клиентские приложения, следует использовать веб-API, не зная, как реализованы данных или операций, которые предоставляет API. Для этого требуется, что API соответствовать общепринятым стандартам, приложения и веб-служба клиента согласовать формат данных и структуры данных, которыми обмениваются клиентские приложения и веб-службы.

## <a name="introduction-to-representational-state-transfer"></a>Общие сведения об архитектурных принципов Representational State Transfer

Representational State Transfer (REST) представляет собой архитектурный стиль для построения распределенных систем, на основе гиперсред. Основное преимущество модели REST является основана на открытых стандартах и не выполняет привязку реализации модели или клиентских приложений, использующих ее любой конкретной реализации. Таким образом веб-службы REST могут быть реализованы с помощью Microsoft ASP.NET Core MVC и клиентских приложений может разработки на любой язык и набор инструментов для создания HTTP-запросы и анализировать HTTP-ответы.

Модель REST использует схему переходов для представления объектов и служб в сети, называемые ресурсами. Систем, которые обычно реализуют REST используется протокол HTTP для передачи запросов на доступ к этим ресурсам. В таких системах клиентское приложение отправляет запрос в виде URI, идентифицирующий ресурс и метод HTTP (например, GET, POST, PUT или DELETE), указывающее операцию для выполнения на указанном ресурсе. Текст HTTP-запроса содержит данные, которые требуются для выполнения операции.

> [!NOTE]
> REST определяет модель запроса без отслеживания состояния. Таким образом HTTP-запросы должны быть независимыми и могут возникнуть в любом порядке.

Ответ REST запроса позволяет использовать стандартные коды состояния HTTP. Например запрос, возвращающий допустимые данные должны включать код ответа HTTP 200 (ОК), хотя запрос, который не удалось найти или удалить указанный ресурс должен вернуть ответ, который включает код состояния HTTP 404 (не найдено).

Веб-API RESTful определяет набор взаимосвязанных ресурсов и предоставляет основные операции, которые позволяют приложению управлять эти ресурсы и беспрепятственно перемещаться между ними. По этой причине URI, которые составляют типичный веб-API RESTful ориентированы на данные, которые он предоставляет и использовать средства по HTTP для работы с этими данными.

Данные, включенные в HTTP-запроса и соответствующие ответные сообщения из веб-сервера, клиентского приложения можно представить в различных форматах, известные как типы мультимедиа. Когда клиентское приложение отправляет запрос, который возвращает данные в тексте сообщения, оно может указать типы мультимедиа, он может обрабатывать в `Accept` заголовок запроса. Если веб-сервер поддерживает этот тип носителя, он может вернуть ответ, включающий `Content-Type` заголовок, который указывает формат данных в теле сообщения. Затем это ответственность за анализ ответного сообщения и интерпретировать результаты в теле сообщения соответствующим образом клиентское приложение.

Дополнительные сведения о REST см. в разделе [по проектированию API](/azure/architecture/best-practices/api-design/) и [реализации API](/azure/architecture/best-practices/api-implementation/).

## <a name="consuming-restful-apis"></a>Использование API-интерфейсов RESTful

Мобильное приложение eShopOnContainers использует шаблон Model-View-ViewModel (MVVM), а также элементы модели представляет шаблон сущности предметной области, используемые в приложении. Классы контроллера и репозитория в образце приложения eShopOnContainers принимать и возвращать многие из этих объектов модели. Таким образом они используются как объекты передачи данных (DTO), которые содержат все данные, передаваемые между мобильного приложения и контейнерные микрослужбы. Основным преимуществом использования DTO для передачи данных и получения данных из веб-службы является передача дополнительных данных в один удаленный вызов, приложение может сократить число удаленных вызовов, которые необходимо внести.

### <a name="making-web-requests"></a>Выполнение веб-запросов

Мобильное приложение eShopOnContainers использует `HttpClient` класса для выполнения запросов по протоколу HTTP с JSON, используемой в качестве типа носителя. Этот класс предоставляет функциональные возможности для асинхронной отправки HTTP-запросов и получения HTTP-ответов из URI определен ресурс. `HttpResponseMessage` Класс представляет сообщение ответа HTTP, полученные от REST API, после HTTP-запроса. Он содержит сведения об ответе, включая код состояния, заголовков и любой текст. `HttpContent` Класс представляет тело HTTP и заголовки содержимого, таких как `Content-Type` и `Content-Encoding`. Можно прочитать содержимое с помощью любого из `ReadAs` методы, такие как `ReadAsStringAsync` и `ReadAsByteArrayAsync`, в зависимости от формата данных.

<a name="making_a_get_request" />

#### <a name="making-a-get-request"></a>Запрос GET

`CatalogService` Класс используется для управления процессом получения данных из микрослужбы каталога. В `RegisterDependencies` метод в `ViewModelLocator` класс, `CatalogService` класс регистрируется как сопоставление типов для `ICatalogService` типа с помощью контейнера внедрения зависимостей Autofac. Теперь, когда экземпляр `CatalogViewModel` создается класс, его конструктор принимает `ICatalogService` тип, который разрешает Autofac, возвращение экземпляра `CatalogService` класса. Дополнительные сведения о внедрения зависимостей, см. в разделе [введение внедрения зависимостей](~/xamarin-forms/enterprise-application-patterns/dependency-injection.md#introduction_to_dependency_injection).

Рис. 10-1 показано взаимодействие классов, которые считывают данные каталога из микрослужбы каталога для отображения `CatalogView`.

[![](accessing-remote-data-images/catalogdata.png "Извлечение данных из микрослужбы каталога")](accessing-remote-data-images/catalogdata-large.png#lightbox "извлечение данных из микрослужбы каталога")

**Рис. 10-1**: Получение данных из микрослужбы каталога

Когда `CatalogView` осуществляется переход, `OnInitialize` метод в `CatalogViewModel` класс называется. Этот метод возвращает данные каталога из микрослужбы каталога, как показано в следующем примере кода:

```csharp
public override async Task InitializeAsync(object navigationData)  
{  
    ...  
    Products = await _productsService.GetCatalogAsync();  
    ...  
}
```

Этот метод вызывает метод `GetCatalogAsync` метод `CatalogService` экземпляра, внедренном в `CatalogViewModel` по Autofac. Метод `GetCatalogAsync` показан в следующем примере кода:

```csharp
public async Task<ObservableCollection<CatalogItem>> GetCatalogAsync()  
{  
    UriBuilder builder = new UriBuilder(GlobalSetting.Instance.CatalogEndpoint);  
    builder.Path = "api/v1/catalog/items";  
    string uri = builder.ToString();  

    CatalogRoot catalog = await _requestProvider.GetAsync<CatalogRoot>(uri);  
    ...  
    return catalog?.Data.ToObservableCollection();            
}
```

Этот метод создает URI, который определяет ресурс, запрос будет отправлен и использует `RequestProvider` класса для вызова метода GET HTTP для ресурса, перед возвратом результатов для `CatalogViewModel`. `RequestProvider` Класс содержит функциональные возможности, отправляет запрос в виде URI, идентифицирующий ресурс, метод HTTP, указывающее операцию для выполнения на этот ресурс, и текст, который содержит все данные, необходимые для выполнения операции. Сведения о том, как `RequestProvider` класс внедряется в `CatalogService class`, см. в разделе [введение внедрения зависимостей](~/xamarin-forms/enterprise-application-patterns/dependency-injection.md#introduction_to_dependency_injection).

В следующем коде показано в примере `GetAsync` метод в `RequestProvider` класса:

```csharp
public async Task<TResult> GetAsync<TResult>(string uri, string token = "")  
{  
    HttpClient httpClient = CreateHttpClient(token);  
    HttpResponseMessage response = await httpClient.GetAsync(uri);  

    await HandleResponse(response);  
    string serialized = await response.Content.ReadAsStringAsync();  

    TResult result = await Task.Run(() =>   
        JsonConvert.DeserializeObject<TResult>(serialized, _serializerSettings));  

    return result;  
}
```

Этот метод вызывает метод `CreateHttpClient` метод, который возвращает экземпляр `HttpClient` класс с набором соответствующие заголовки. Затем он отправляет асинхронный запрос GET для ресурса с URI, с ответом, хранящихся в `HttpResponseMessage` экземпляра. `HandleResponse` Затем вызывается метод, который создает исключение, если ответ не включает код состояния HTTP успешно. Затем ответ читается как строку, преобразованную из формата JSON для `CatalogRoot` объекта, а возвращается в `CatalogService`.

`CreateHttpClient` Метод показан в следующем примере кода:

```csharp
private HttpClient CreateHttpClient(string token = "")  
{  
    var httpClient = new HttpClient();  
    httpClient.DefaultRequestHeaders.Accept.Add(  
        new MediaTypeWithQualityHeaderValue("application/json"));  

    if (!string.IsNullOrEmpty(token))  
    {  
        httpClient.DefaultRequestHeaders.Authorization =   
            new AuthenticationHeaderValue("Bearer", token);  
    }  
    return httpClient;  
}
```

Этот метод создает новый экземпляр класса `HttpClient` и задает `Accept` заголовок любых запросов, сделанных `HttpClient` экземпляр `application/json`, указывает, что метод ожидает содержимое сообщения ответа, которые необходимо отформатировать с помощью JSON. Затем, если маркер доступа был передан в качестве аргумента для `CreateHttpClient` , он добавляется метод `Authorization` заголовок любых запросов, сделанных `HttpClient` экземпляра, префикс строки `Bearer`. Дополнительные сведения об авторизации см. в разделе [авторизации](~/xamarin-forms/enterprise-application-patterns/authentication-and-authorization.md#authorization).

Когда `GetAsync` метод в `RequestProvider` вызываемый классом `HttpClient.GetAsync`, `Items` метод в `CatalogController` вызывается класс в проекте Catalog.API, как показано в следующем примере кода:

```csharp
[HttpGet]  
[Route("[action]")]  
public async Task<IActionResult> Items(  
    [FromQuery]int pageSize = 10, [FromQuery]int pageIndex = 0)  
{  
    var totalItems = await _catalogContext.CatalogItems  
        .LongCountAsync();  

    var itemsOnPage = await _catalogContext.CatalogItems  
        .OrderBy(c=>c.Name)  
        .Skip(pageSize * pageIndex)  
        .Take(pageSize)  
        .ToListAsync();  

    itemsOnPage = ComposePicUri(itemsOnPage);  
    var model = new PaginatedItemsViewModel<CatalogItem>(  
        pageIndex, pageSize, totalItems, itemsOnPage);             

    return Ok(model);  
}
```

Этот метод извлекает данные каталога из базы данных SQL с использованием EntityFramework и возвращает его как ответное сообщение, включающий успешно код состояния HTTP и коллекция JSON в формате `CatalogItem` экземпляров.

#### <a name="making-a-post-request"></a>Формирование запроса POST

`BasketService` Класс используется для управления извлечения данных и обновления процесс с микрослужбой basket. В `RegisterDependencies` метод в `ViewModelLocator` класс, `BasketService` класс регистрируется как сопоставление типов для `IBasketService` типа с помощью контейнера внедрения зависимостей Autofac. Теперь, когда экземпляр `BasketViewModel` создается класс, его конструктор принимает `IBasketService` тип, который разрешает Autofac, возвращение экземпляра `BasketService `класса. Дополнительные сведения о внедрения зависимостей, см. в разделе [введение внедрения зависимостей](~/xamarin-forms/enterprise-application-patterns/dependency-injection.md#introduction_to_dependency_injection).

Рис. 10-2 показано взаимодействие классов, которые отправляют данных корзины, отображаемых объектом `BasketView`, чтобы микрослужба корзины.

[![](accessing-remote-data-images/basketdata.png "Отправляет данные в микрослужбе корзины")](accessing-remote-data-images/basketdata-large.png#lightbox "отправляет данные в микрослужбе корзины")

**Рис. 10-2**: Отправляет данные в микрослужбе корзины

При добавлении элемента в корзину `ReCalculateTotalAsync` метод в `BasketViewModel` класс называется. Этот метод обновляет общее число элементов в корзине и отправляет данные корзины в микрослужбе корзины, как показано в следующем примере кода:

```csharp
private async Task ReCalculateTotalAsync()  
{  
    ...  
    await _basketService.UpdateBasketAsync(new CustomerBasket  
    {  
        BuyerId = userInfo.UserId,   
        Items = BasketItems.ToList()  
    }, authToken);  
}
```

Этот метод вызывает метод `UpdateBasketAsync` метод `BasketService` экземпляра, внедренном в `BasketViewModel` по Autofac. В следующем показан метод `UpdateBasketAsync` метод:

```csharp
public async Task<CustomerBasket> UpdateBasketAsync(CustomerBasket customerBasket, string token)  
{  
    UriBuilder builder = new UriBuilder(GlobalSetting.Instance.BasketEndpoint);  
    string uri = builder.ToString();  
    var result = await _requestProvider.PostAsync(uri, customerBasket, token);  
    return result;  
}
```

Этот метод создает URI, который определяет ресурс, запрос будет отправлен и использует `RequestProvider` класса для вызова метода POST HTTP для ресурса, перед возвратом результатов для `BasketViewModel`. Обратите внимание, что маркер доступа, полученный из IdentityServer во время процесса проверки подлинности, требуется для авторизации запросов в микрослужбе корзины. Дополнительные сведения об авторизации см. в разделе [авторизации](~/xamarin-forms/enterprise-application-patterns/authentication-and-authorization.md#authorization).

В следующем примере кода показан один из `PostAsync` методы в `RequestProvider` класса:

```csharp
public async Task<TResult> PostAsync<TResult>(  
    string uri, TResult data, string token = "", string header = "")  
{  
    HttpClient httpClient = CreateHttpClient(token);  
    ...  
    var content = new StringContent(JsonConvert.SerializeObject(data));  
    content.Headers.ContentType = new MediaTypeHeaderValue("application/json");  
    HttpResponseMessage response = await httpClient.PostAsync(uri, content);  

    await HandleResponse(response);  
    string serialized = await response.Content.ReadAsStringAsync();  

    TResult result = await Task.Run(() =>  
        JsonConvert.DeserializeObject<TResult>(serialized, _serializerSettings));  

    return result;  
}
```

Этот метод вызывает метод `CreateHttpClient` метод, который возвращает экземпляр `HttpClient` класс с набором соответствующие заголовки. Затем он отправляет асинхронный запрос POST для ресурса с URI, с данными сериализованный корзины, отправляемых в формате JSON и ответа, сохраняемого в `HttpResponseMessage` экземпляра. `HandleResponse` Затем вызывается метод, который создает исключение, если ответ не включает код состояния HTTP успешно. Затем ответ читается как строку, преобразованную из формата JSON для `CustomerBasket` объекта, а возвращается в `BasketService`. Дополнительные сведения о `CreateHttpClient` метод, см. в разделе [внесения получить запрос на](#making_a_get_request).

Когда `PostAsync` метод в `RequestProvider` вызываемый классом `HttpClient.PostAsync`, `Post` метод в `BasketController` вызывается класс в проекте Basket.API, как показано в следующем примере кода:

```csharp
[HttpPost]  
public async Task<IActionResult> Post([FromBody]CustomerBasket value)  
{  
    var basket = await _repository.UpdateBasketAsync(value);  
    return Ok(basket);  
}
```

Этот метод использует экземпляр `RedisBasketRepository` класса для сохранения данных корзины в кэш Redis и возвращает его, отформатированное сообщение ответа, которое включает в себя успешно код состояния HTTP и JSON `CustomerBasket` экземпляра.

#### <a name="making-a-delete-request"></a>Выполнении запроса на удаление

Рис. 10-3 показано взаимодействие классов, которые удаления устаревших данных корзины в микрослужбе корзины, `CheckoutView`.

![](accessing-remote-data-images/checkoutdata.png "Удаление данных из микрослужба корзины")

**Рис. 10-3**: Удаление данных из микрослужба корзины

При вызове процесс подсчета стоимости покупок `CheckoutAsync` метод в `CheckoutViewModel` класс называется. Этот метод создает новый заказ, перед удалением корзины покупок, как показано в следующем примере кода:

```csharp
private async Task CheckoutAsync()  
{  
    ...  
    await _basketService.ClearBasketAsync(_shippingAddress.Id.ToString(), authToken);  
    ...  
}
```

Этот метод вызывает метод `ClearBasketAsync` метод `BasketService` экземпляра, внедренном в `CheckoutViewModel` по Autofac. В следующем показан метод `ClearBasketAsync` метод:

```csharp
public async Task ClearBasketAsync(string guidUser, string token)  
{  
    UriBuilder builder = new UriBuilder(GlobalSetting.Instance.BasketEndpoint);  
    builder.Path = guidUser;  
    string uri = builder.ToString();  
    await _requestProvider.DeleteAsync(uri, token);  
}
```

Этот метод создает URI, идентифицирующий ресурс, который будет отправляться запрос и использует `RequestProvider` класса для вызова метода DELETE HTTP в ресурсе. Обратите внимание, что маркер доступа, полученный из IdentityServer во время процесса проверки подлинности, требуется для авторизации запросов в микрослужбе корзины. Дополнительные сведения об авторизации см. в разделе [авторизации](~/xamarin-forms/enterprise-application-patterns/authentication-and-authorization.md#authorization).

В следующем коде показано в примере `DeleteAsync` метод в `RequestProvider` класса:

```csharp
public async Task DeleteAsync(string uri, string token = "")  
{  
    HttpClient httpClient = CreateHttpClient(token);  
    await httpClient.DeleteAsync(uri);  
}
```

Этот метод вызывает метод `CreateHttpClient` метод, который возвращает экземпляр `HttpClient` класс с набором соответствующие заголовки. Затем он отправляет асинхронный запрос DELETE к ресурсу, указанному в URI. Дополнительные сведения о `CreateHttpClient` метод, см. в разделе [внесения получить запрос на](#making_a_get_request).

Когда `DeleteAsync` метод в `RequestProvider` вызываемый классом `HttpClient.DeleteAsync`, `Delete` метод в `BasketController` вызывается класс в проекте Basket.API, как показано в следующем примере кода:

```csharp
[HttpDelete("{id}")]  
public void Delete(string id)  
{  
    _repository.DeleteBasketAsync(id);  
}
```

Этот метод использует экземпляр `RedisBasketRepository` класса, чтобы удалить данные корзины из кэша Redis.

## <a name="caching-data"></a>Кэширование данных

Можно повысить производительность приложения путем кэширования часто используемых данных в быстрое хранилище, расположенное ближе к приложению. Если устройство хранения расположен ближе к приложению, чем исходный оригинал, то кэширование может значительно повысить ответа время ожидания при получении данных.

Наиболее распространенная форма кэширования является сквозного чтения кэширования, где приложение извлекает данные, ссылаясь на кэш. Если данные находятся не в кэше, извлекаются из хранилища данных и добавляются в кэш. Приложения можно реализовать сквозного чтения кэширования с шаблоном "кэш". Этот шаблон определяет, находится ли элемент в кэше. Если элемент отсутствует в кэше, чтение из хранилища данных и добавляются в кэш. Дополнительные сведения см. в разделе [кэш на стороне](/azure/architecture/patterns/cache-aside/) шаблон.

> [!TIP]
> Кэширование данных часто читаемых и изменяются редко. Эти данные могут добавляться в кэш по запросу первый раз, он извлекается приложением. Это означает, что приложению необходимо получить только один раз данные из хранилища данных и последующие доступа могут выполняться с помощью кэша.

Распределенные приложения, такие как эталонное приложение eShopOnContainers, должен предоставить одно или оба указанных ниже кэши:

-   Общий кэш, которую можно запустить несколько процессов или машин.
-   Частный кэш, где данные хранятся локально на устройстве, запустив его.

Мобильное приложение eShopOnContainers использует частный кэш, где данные хранятся локально на устройстве, на котором выполняется экземпляр приложения. Сведения о кэше, используемые в образце приложения eShopOnContainers, см. в разделе [Микрослужбы .NET: архитектура контейнерных приложений .NET](https://aka.ms/microservicesebook).

> [!TIP]
> Можно Рассматривайте кэш как хранилище временных данных, которое может стать недоступным в любое время. Убедитесь, что данные хранятся в хранилище исходных данных, а также в кэше. Затем к минимуму вероятность потери данных, если кэш становится недоступным.

### <a name="managing-data-expiration"></a>Управление истечением срока актуальности данных

Нецелесообразно ожидать, что кэшированные данные всегда будут согласованы с исходными данными. Данные в хранилище исходных данных может измениться после он был кэширован, вызывая кэшированные данные устаревают. Таким образом приложения должны реализовать стратегию, которая позволяет гарантировать, что данные в кэше, как максимально актуальны, но можно также обнаруживать и обработать ситуации, возникающие, когда данные в кэше устарели. Наиболее кэширования Включить кэш быть перенастроены на истечение срока хранения данных и таким образом уменьшить период, для которого данные могут быть устаревшими.

> [!TIP]
> Значение по умолчанию время при настройке кэша. Многие кэши реализуют истечения срока действия, которая объявляет данные недействительными и удаляет его из кэша, если они недоступны в течение указанного периода. Тем не менее необходимо соблюдать осторожность при выборе срока действия. Если он становится слишком короткий, данных устареют слишком быстро, и преимущества кэширования, которые будет снижена. Если он становится слишком много времени, данные риски, перестанут быть актуальными. Таким образом время окончания срока действия должно соответствовать шаблону доступа для приложений, использующих данные.

Когда кэшированные данные устаревают, должны удаляться из кэша и приложение должно получить данные из исходных данных хранения и поместите его обратно в кэш.

Это также возможно, что переполнение кэша, если данные могут оставаться слишком долго. Таким образом, запросы на добавление новых элементов в кэш может потребоваться удалить некоторые элементы в рамках процесса под названием *вытеснения*. Службы кэширования обычно исключают данные на основе наименее недавно использовавшихся. Тем не менее существуют другие политики вытеснения, в том числе, недавно использованные и первый in-first-out. Дополнительные сведения см. в разделе [руководстве по кэшированию](/azure/architecture/best-practices/caching/).

<a name="caching_images" />

### <a name="caching-images"></a>Кэширование изображений

Мобильное приложение eShopOnContainers использует изображения удаленных продуктов, которые получают преимущества от кэширования. Эти изображения отображаются по [ `Image` ](xref:Xamarin.Forms.Image) элемента управления и `CachedImage` управление, предоставляемое [FFImageLoading](https://www.nuget.org/packages/Xamarin.FFImageLoading.Forms/) библиотеки.

Xamarin.Forms [ `Image` ](xref:Xamarin.Forms.Image) элемент управления поддерживает кэширование загруженных изображений. Кэширование включено по умолчанию и сохраняется локально на 24 часа. Кроме того, можно настроить срок действия [ `CacheValidity` ](xref:Xamarin.Forms.UriImageSource.CacheValidity) свойство. Дополнительные сведения см. в разделе [Скачанный образ кэширование](~/xamarin-forms/user-interface/images.md#downloaded-image-caching).

В FFImageLoading `CachedImage` управления — это замена для Xamarin.Forms [ `Image` ](xref:Xamarin.Forms.Image) элемента управления, предоставляя дополнительные свойства, включения дополнительных функций. Для этой функции элемент управления обеспечивает можно настроить кэширование, при поддержке ошибки и загрузки изображения-заполнители. В следующем примере кода показано, как мобильное приложение eShopOnContainers использует `CachedImage` контролировать, `ProductTemplate`, который является шаблон данных, используемые [ `ListView` ](xref:Xamarin.Forms.ListView) контролировать `CatalogView`:

```xaml
<ffimageloading:CachedImage
    Grid.Row="0"
    Source="{Binding PictureUri}"     
    Aspect="AspectFill">
    <ffimageloading:CachedImage.LoadingPlaceholder>
        <OnPlatform x:TypeArguments="ImageSource">
            <On Platform="iOS, Android" Value="default_campaign" />
            <On Platform="UWP" Value="Assets/default_campaign.png" />
        </OnPlatform>
    </ffimageloading:CachedImage.LoadingPlaceholder>
    <ffimageloading:CachedImage.ErrorPlaceholder>
        <OnPlatform x:TypeArguments="ImageSource">
            <On Platform="iOS, Android" Value="noimage" />
            <On Platform="UWP" Value="Assets/noimage.png" />
        </OnPlatform>
    </ffimageloading:CachedImage.ErrorPlaceholder>
</ffimageloading:CachedImage>
```

`CachedImage` Задает `LoadingPlaceholder` и `ErrorPlaceholder` свойства для образов платформы. `LoadingPlaceholder` Свойство задает изображение, отображаемое при изображение, указанное `Source` свойство получено и `ErrorPlaceholder` свойство задает изображение, отображаемое, если произошла ошибка при попытке получения изображения определяется `Source` свойство.

Как и предполагает название, `CachedImage` управления кэширует удаленного изображения на устройстве для времени, заданного параметром значения `CacheDuration` свойство. Если значение этого свойства не задано явно, применяется значение по умолчанию 30 дней.

## <a name="increasing-resilience"></a>Повышение устойчивости

Все приложения, которые обмениваются данными с удаленными службами и ресурсами должен быть чувствительны ко временным сбоям. Временные сбои включают кратковременной потерей сетевого подключения для служб, временную недоступность службы или наличие времени ожидания, когда служба занята. Эти ошибки часто устраняются, и если повторить действие через некоторый промежуток вполне вероятно, для успешного выполнения.

Временные сбои может иметь огромное влияние на качество предполагаемых приложения, даже если оно тщательно протестировано во всех ожидаемых обстоятельствах. Чтобы надежно работает приложение, которое обменивается данными с удаленными службами, необходимо иметь возможность выполнять все указанные ниже:

-   Обнаруживать ошибки, при их возникновения и определить, если сообщения об ошибках, скорее всего, будут временными.
-   Повторите операцию, если определит, что сбой является скорее всего, будут временными и отслеживать количество повторных попыток операция.
-   Использование стратегии повтора, который указывает количество повторных попыток, задержку между попытками и действия для использования после неудачной попытки.

Эта обработка временного сбоя достигается путем заключения всех попыток доступа к удаленной службе в коде, реализующем шаблон повторных попыток.

### <a name="retry-pattern"></a>Шаблон повторов

Если приложение обнаруживает сбой при попытке отправить запрос к удаленной службе, он может обработать этот сбой в любой из следующих способов:

-   Повторное выполнение данной операции. Приложение может повторить запрос сбоя сразу же.
-   Повторите операцию через некоторое время. Приложение следует подождать подходящее количество времени до повторным выполнением запроса.
-   Отмена операции. Приложение должно отменить операцию и сформировать отчет об исключении.

Используемая стратегия повторных попыток должен быть настроен так, в соответствии с бизнес-требований приложения. Например очень важно оптимизировать число повторных попыток и интервал для предпринятой операции повтора. Если операция является частью взаимодействия с пользователем, интервал повторных попыток должно быть Краткосрочный и всего несколько повторных попыток, чтобы не заставлять пользователя дожидаться ответа. Если операция является частью долго выполняющегося рабочего процесса, когда Отмена и перезапуск рабочего процесса является дорогостоящим или много времени, он подходит для ожидания между повторными и повторить несколько раз.

> [!NOTE]
> Стратегии Агрессивный Повтор с минимальной задержкой между попытками и большое количество повторных попыток, может привести к снижению удаленной службы, на котором выполняется ближе к или достигнуто максимальное число. Кроме того такая стратегия повторных попыток также может повлиять на скорость реагирования приложения, если оно непрерывно пытается выполнить операцию, завершившуюся сбоем.

Если запрос по-прежнему не работает после количества повторных попыток, лучше для приложения, чтобы предотвратить дальнейшие запросы к тому же ресурсу и сообщение об ошибке. Затем после определенного периода, приложение может сделать один или несколько запросов к ресурсу, чтобы узнать, если они успешно. Дополнительные сведения см. в разделе [шаблон автоматического выключения](#circuit_breaker_pattern).

> [!TIP]
> Никогда не применяйте механизм с бесконечными повторными попытками. Используйте конечное число повторных попыток или реализуйте [Размыкатель цепи](/azure/architecture/patterns/circuit-breaker/) шаблон, чтобы разрешить службе для восстановления.

В мобильном приложении eShopOnContainers пока не реализованы шаблона повторных попыток при создании запросов к веб-RESTful. Тем не менее `CachedImage` элемента управления, предоставляемые [FFImageLoading](https://www.nuget.org/packages/Xamarin.FFImageLoading.Forms/) библиотека поддерживает обработки временных сбоев, повторив попытку загрузки образа. В случае сбоя загрузки изображений дальнейшие попытки больше выполняться. Число попыток задается `RetryCount` свойство и повторных попыток произойдет после задержки, заданной `RetryDelay` свойство. Если значения этих свойств не задано явно, по умолчанию применяются значения — 3 для `RetryCount` свойство и 250 мс для `RetryDelay` свойство. Дополнительные сведения о `CachedImage` управления, см. в разделе [кэширования изображений](#caching_images).

Образце приложения eShopOnContainers реализации шаблона повторных попыток. Дополнительные сведения, в том числе о том, как объединить шаблона повторных попыток с `HttpClient` , представлена в разделе [Микрослужбы .NET: архитектура контейнерных приложений .NET](https://aka.ms/microservicesebook).

Дополнительные сведения о шаблоне повторных попыток, см. в разделе [повторите](/azure/architecture/patterns/retry/) шаблон.

<a name="circuit_breaker_pattern" />

### <a name="circuit-breaker-pattern"></a>Шаблон автоматического выключения

В некоторых ситуациях ошибки может произойти из-за ожидаемой событий, которые принимают больше времени, чтобы исправить. Такие сбои могут быть от частичной потери подключения до полного отказа службы. В таких ситуациях не имеет смысла, если для приложения повторить операцию, которая, скорее всего, выполняются успешно и вместо этого следует принимать, что операция завершилась ошибкой и обработать его.

Шаблон автоматического выключения может препятствовать приложение несколько раз пытается выполнить операцию, которая, вероятнее всего переход на другой, а также приложение, чтобы определить, устранена ли ошибка.

> [!NOTE]
> Назначение шаблона размыкателя цепи отличается от шаблона повторных попыток. Шаблон повторов позволяет приложению повторять операцию, ожидая, что она будет успешного выполнена. Шаблон автоматического выключения препятствует выполнению операции, которая, скорее всего, сбой приложения.

Автоматическое выключение действует как прокси для операций, которые может завершиться ошибкой. Прокси-сервер должен отслеживать количество недавних сбоев, произошедших и использовать эту информацию, чтобы решить, следует ли разрешить операцию продолжить, или же немедленно вернуть исключение.

В мобильном приложении eShopOnContainers в настоящее время не реализует шаблон автоматического выключения. Тем не менее выполняет eShopOnContainers. Дополнительные сведения см. в разделе [Микрослужбы .NET: архитектура контейнерных приложений .NET](https://aka.ms/microservicesebook).

> [!TIP]
> Объедините шаблоны повторных попыток и Размыкатель цепи. Приложение можно объединять шаблоны повторных попыток и Размыкатель цепи с помощью шаблона повторных попыток попытка вызвать операцию через автоматический выключатель. Тем не менее логика повторных попыток должно быть чувствительно к любым исключениям, возвращаемым автоматическим выключением и отказываться от повторных попыток, если Размыкатель цепи сообщает, что неисправность не является временной.

Дополнительные сведения о шаблон автоматического выключения, см. в разделе [Размыкатель цепи](/azure/architecture/patterns/circuit-breaker/) шаблон.

## <a name="summary"></a>Сводка

Многие современные решения на основе веб-сделать использование веб-служб, размещенных на веб-серверах, для предоставления функций для удаленных клиентских приложений. Операции, которые веб-служба предоставляет составляют веб-API, и клиентские приложения должны иметь возможность использовать веб-API, не зная, как реализованы данных или операций, которые предоставляет API-Интерфейс.

Можно повысить производительность приложения путем кэширования часто используемых данных в быстрое хранилище, расположенное ближе к приложению. Приложения можно реализовать сквозного чтения кэширования с шаблоном "кэш". Этот шаблон определяет, находится ли элемент в кэше. Если элемент отсутствует в кэше, чтение из хранилища данных и добавляются в кэш.

При взаимодействии с веб-API, приложения должны быть чувствительны ко временным сбоям. Временные сбои включают кратковременной потерей сетевого подключения для служб, временную недоступность службы или наличие времени ожидания, когда служба занята. Эти ошибки часто устраняются, и если повторить действие через некоторый промежуток, будет успешно выполнен. Таким образом приложения следует заключить в нее все попытки доступа к веб-API в коде, который реализует механизм обработки временных сбоев.


## <a name="related-links"></a>Связанные ссылки

- [Скачайте электронную книгу (2 МБ в формате PDF)](https://aka.ms/xamarinpatternsebook)
- [eShopOnContainers (GitHub) (пример)](https://github.com/dotnet-architecture/eShopOnContainers)
