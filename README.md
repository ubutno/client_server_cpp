# client_server_cpp

## 1 Цель работы
  Приобретение навыков по анализу структуры, функциональности и угроз специально встраиваемого дефекта программного продукта — потайного хода (backdoor), а также изучение методов защиты от уязвимости такого вида.
## 2 Постановка задачи
  Необходимо реализовать клиент-серверную программу, использующую сокеты для сетевого соединения. Программу клиент добавить в автозагрузку, реализовать удаленное удаление фалов.
## 3 Теоретические исследования
  Программа-шпион (spyware) — программное обеспечение, скрытно собирающее информацию о пользователе (персональные данные, настройки операционной системы, статистику работы и пр.). Шпионское программное обеспечение применяется для проведения маркетинговых исследований, распространения целевой рекламы, деструктивных воздействий. Информация о пользователе и системе может существенно упростить последующую компьютерную атаку. 
Шпионские программы распространяются в результате:
•	посещения веб-сайтов (для установки шпионских программ активно используются ActiveX-компоненты);
•	установки бесплатных и условно-бесплатных программ (например, кодек DivX содержит утилиту для скрытной загрузки и установки SpyWare.Gator)
Большинство шпионских программ не уведомляют об этом пользователей, эксплуатируя встроенные в программу дефекты, потайные ходы (Backdoor) — программные компоненты, специально оставленные или встроенные в программу с целью скрытого получения несанкционированного доступа к данным или для удаленного управления вычислительной системой.
## 4	Описание решения
Клиент-сервер реализован через интерфейс для взаимодействия с сетевыми ресурсами вычислительной системы: Windows Sockets. Программа сервер передается на компьютер, в котором должно произойти удаление. После запуска клиент не показывает свое окно и добавляет себя в автозагрузку, и уже готов взаимодействовать с сервером. Для отслеживания возникших ошибок язык си имеет большой набор возвращаемых значений функций, которые описаны в Приложении В.
Процесс занесения программы в автозагрузку реализован через работу с реестром. Для добавления программы в автозагрузку необходимо прописать её по адресу «Software\Microsoft\Windows\CurrentVersion\Run»

В поле значение необходимо указать расположение запускаемого exe файла, за его получение отвечает функция GetModuleFileName, а само занесенее в реестр происходит с помощью функций RegOpenKey и RegSetValueEx.
Удаление файла с компьютера сервера происходит с помощью функции _unlink, которая удаляет указанный файл из каталога. В случае успеха функция возвращает 0, а при неудаче -1.

## 5  Вывод
  В ходе работы были получены навыки работы с клиент-серверными программами, сокетами. Изучена теория сетей, на практике применены все знания, разработана клиент-серверная программа, обладающая функционалом удаления файлов удаленно, используя открытые порты машины. Была реализована функция автозагрузки autorun, которая напрямую работает с реестром.
