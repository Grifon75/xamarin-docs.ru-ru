## <a name="firewall-configuration"></a>Конфигурация брандмауэра

Порядок тестов, которые требуется отправить в Xamarin Test Cloud компьютер, отправка тестов должен быть могут взаимодействовать с серверами Test Cloud. Брандмауэр необходимо настроить для разрешения трафика сети через серверы, расположенные в **testcloud.xamarin.com** на портах 80 и 443. Эта конечная точка находится под управлением DNS и IP-адрес может быть изменена. 

В некоторых ситуациях теста (или на устройстве под управлением теста) должны взаимодействовать с веб-серверах, защищенных брандмауэром. В этом сценарии брандмауэра необходимо разрешить трафик от следующих IP-адресов:

* **195.249.159.238**
* **195.249.159.239**