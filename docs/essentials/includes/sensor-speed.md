---
ms.topic: include
ms.openlocfilehash: e4dfd1ac12f3010939d483381a785091d71599ed
ms.sourcegitcommit: 676c5a6795ab4896ccd1b288424bf2040b1208aa
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2018
ms.locfileid: "52294831"
---
## <a name="sensor-speedxrefxamarinessentialssensorspeed"></a>[Скорость датчика](xref:Xamarin.Essentials.SensorSpeed)

- **Fastest** (Максимальная) — максимально быстрое получение данных датчика (возврат в поток пользовательского интерфейса не гарантирован).
- **Game** (Игра) — скорость, подходящая для игр (возврат в поток пользовательского интерфейса не гарантирован).
- **Normal** (Нормальная) — скорость по умолчанию, которая подходит для изменений ориентации экрана.
- **UI** (Пользовательский интерфейс) — скорость, которая подходит для типичного пользовательского интерфейса.

Если нет гарантии, что обработчик событий будет запущен в потоке пользовательского интерфейса, и этому обработчику событий требуется доступ к элементам интерфейса, используйте метод [`MainThread.BeginInvokeOnMainThread`](~/essentials/main-thread.md) для запуска кода в потоке пользовательского интерфейса.