---
title: "Расширенная установка"
translation: "getting-started/installation/advanced-installation"
---

- [Предварительные шаги по установке](#AdvancedInstallation-InstallationPreSteps)
  - [Переименование или перемещение ядра](#AdvancedInstallation-RenamingorMovingtheCore)
  - [Изменение ключа конфигурации](#AdvancedInstallation-ChangingtheConfigurationKey)
- [Дополнительные параметры](#AdvancedInstallation-AdvancedOptions)
- [Параметры базы данных](#AdvancedInstallation-DatabaseOptions)
  - [Сопоставление и Кодировка](#AdvancedInstallation-CollationsandCharsets)
  - [Создание Администратора по умолчанию](#AdvancedInstallation-CreatinganAdministratorUser)
- [Конфигурация контекста](#AdvancedInstallation-ContextConfiguration)
- [Проверки перед установкой](#AdvancedInstallation-PreInstallationChecks)
- [Резюме после установки](#AdvancedInstallation-PostInstallationSummary)
- [Смотрите также](#AdvancedInstallation-SeeAlso)


Это руководство для установки MODx с расширенным перечнем опций. Рекомендуется устанавливать этот дистрибутив, только если:

- Вы планируете переименовать папки manager/ или connectors/ или переместить каталог core/
- У вас есть доступ по SSH или вы можете легко перемещать и создавать директории для записи на вашем сервере.

Возможно, вы захотите сначала изучить [Требования к серверу](getting-started/server-requirements "Server Requirements"). Если после прочтения этого документа у вас по-прежнему возникают проблемы с установкой, прочитайте страницу [Устранение неполадок при установке](getting-started/installation/troubleshooting-installation "Troubleshooting Installation").

## Предварительные шаги по установке

После того как вы [скачали](getting-started/installation "Installation") расширенный (Advanced) дистрибутив MODx Revolution, загрузите и распакуйте его на свой сервер. В корневом каталоге две папки - core/ и setup/. Если вы планируете переместить каталог core/, перейдите к следующему разделу. Если же вы не собираетесь этого делать или изменили конфигурационный ключ, зайдите в папку **setup/** в вашем браузере и перейдите к разделу [Дополнительные параметры](#AdvancedInstallation-AdvancedOptions) этого документа.

### Переименование или перемещение ядра

MODx Revolution позволяет вам переименовать и/или переместить папку core/ для повышения уровня безопасности вашего сайта. Вы также можете переместить каталог core/ за пределы корня сайта, чтобы обеспечить дополнительную безопасность установки MODx.

Если вы решите переименовать или переместить ядро, MODx рекомендует сделать это перед установкой. Просто переименуйте или переместите каталог core/ на начальном этапе и установщик откроет вам страницу с просьбой указать новое местоположение ядра:

![](/download/attachments/18678479/setup-corefinder.png?version=1&modificationDate=1280289614000)

Введите в текстовое поле абсолютный путь, куда вы переместили основной каталог. Если MODx сможет найти ядро, вы продолжите установку. Если MODx по-прежнему не может найти каталог по указанному вами пути, проверьте, правильно ли вы его ввели, что это абсолютный путь и что вы сделали каталог доступным для чтения (и записи файлов в папку core/cache/).

MODx может также попросить вас сделать доступным для записи файл setup/includes/core.config.php. Это необходимо для изменения пути к ядру системы, и вы должны это сделать прежде, чем продолжить.

### Изменение ключа конфигурации

Далее MODx попросит вас выбрать язык. Затем будет показана страница приветствия, а ниже будет предложено изменить ключ конфигурации MODx. Это позволяет запускать несколько сайтов с общим ядром, поэтому каждому отдельному сайту потребуется свой уникальный конфигурационный ключ.

Чтобы изменить его, просто нажмите на предложенную установщиком ссылку для изменения ключа конфигурации, и вы увидите текстовое поле:

![](/download/attachments/18678479/setup-configKey.png?version=1&modificationDate=1280289975000)

Укажите пользовательский, уникальный ключ конфигурации и нажмите Далее.

## Расширенные настройки

Теперь вам будет предложено несколько вариантов установки, аналогичные окну [Базовая установка](getting-started/installation/basic-installation "Basic Installation"), но с двумя дополнительными опциями внизу. 'Новая установка' будет единственной опцией, доступной для выбора, что вам и нужно. Ниже вы можете настроить разрешения для создания новых файлов или папок в вашей установке MODx. Значения по умолчанию должны работать корректно,но, если сервер задаёт лишние ограничения, вы можете изменить права доступа для каталогов/файлов на 0775/0664 соответственно.

Ниже вам будут представлены две опции:

![](/download/attachments/18678479/setup-advopt.png?version=1&modificationDate=1280290324000)

Они будут недоступны во время новых установок. (Во время обновлений рекомендуется также снять эти флажки.) Нажмите 'Далее', чтобы перейти к следующему шагу.

## Параметры базы данных

Далее вы увидите форму с запросом информации о вашей базе данных:

![](/download/attachments/18678479/setup-db1.png?version=1&modificationDate=1280290454000)

Добавьте имя хоста базы данных, которое является URL-адресом, по которому находится ваша база данных. Для большинства пользователей это будет 'localhost'. Если ваш сервер MySQL подключен к другому порту, укажите его следующим образом: "my.database.com;port=3307", а для port= добавьте IP/имя хоста.

Кроме того, если вы хотите, вы можете указать другой префикс таблиц базы данных. В этом случае MODx добавит пользовательский префикс всем таблицам - может оказаться полезным, если вы хотите сделать несколько установок MODx в одной базе данных.

По завершении нажмите ссылку 'Проверить соединение с сервером базы данных и отобразить список доступных сопоставлений'. Если у вас есть какие-либо ошибки, они будут показаны ниже. В этом случае, проверьте правильность имени пользователя и пароля вашей базы данных. Кроме того, если у вашего пользователя нет прав для создания базы данных, вам может потребоваться сделать это вручную.

### Сопоставление и Кодировка

Затем появится следующая форма для настройки кодировки и сопоставления вашей базы данных:

![](/download/attachments/18678479/setup-db2.png?version=1&modificationDate=1280290459000)

Для большинства пользователей подходят значения по умолчанию. Однако, если вам нужно изменить их, **убедитесь**, что сопоставление соответствует кодировке. Нажмите 'Попытка создания или выборки из базы данных' после того, как вы закончите.

### Создание Администратора по умолчанию

![](/download/attachments/18678479/setup-db3.png?version=1&modificationDate=1280290462000)

Следующая форма содержит несколько полей для настройки вашего администратора. Укажите имя пользователя, которое вы хотите использовать в качестве имени администратора.

MODX **не рекомендует** использовать 'admin' в качестве имени администратора, поскольку оно чаще всего применяется и в первую очередь проверяется хакерами.

В этом же окне введите свой адрес электронной почты (или email вашего администратора) и укажите пароль. Нажмите Далее, когда закончите.

## Конфигурация контекста

Далее MODx покажет форму подробной настройки контекста. Здесь вы можете указать пути к контексту web (основному контексту), а также каталогам для ваших connectors/ и manager/ папок. MODx рекомендует не изменять пути к web/ контексту без особых причин.

Переименование каталогов manager/ и connectors/ может добавить дополнительный уровень безопасности вашему сайту. Просто измените пути и URL в предоставленных текстовых полях. Примечание. Если вносите изменения, каталоги **выше** любого из этих путей должны быть доступны для записи, чтобы позволить MODx записать в них директории manager/ и/или connectors/.

Убедитесь, что вы изменили **и** путь **и** URL!

Когда закончите, нажмите 'Далее', чтобы продолжить.

## Проверки перед установкой

Затем MODx продолжит список проверок, чтобы убедиться, что ваша система готова к установке. В случае сбоя любого из них вам нужно будет следовать предложенным указаниям, чтобы убедиться, что ваше программное окружение соответствует [Требованиям к серверу](getting-started/server-requirements "Server Requirements") и имеет корректные каталоги, доступные для записи.

Когда все будет готово и все проверки пройдены, нажмите 'Установить', чтобы продолжить.

Если появился пустой экран или нет возможности продолжить после нажатия 'Установить', проверьте следующие этапы:
1. Убедитесь, что каталоги "/\[root\]", "/core/config", "/core/packages", "/core/cache" и "/core/export" доступны для записи. (root - корневой каталог установки.)
2. Убедитесь, что в настройках php.ini для memory\_limit установлено значение 128M, а для max\_execution_time - 120.
3. Убедитесь, что MODx может создавать каталоги manager и connectors; это делается путем указания прав записи в родительские директории этих каталогов (так как вы можете изменить место их установки)
4. Отправьте сообщение на [форум Revolution](http://modxcms.com/forums/index.php/board,280.0.html) относительно вашей проблемы. Укажите информацию о настройке и установке вашего сервера, и мы постараемся помочь вам найти решение.

## Резюме после установки

Затем MODx сообщит вам, возникли ли какие-либо ошибки во время установки, и предложит вам выполнить переустановку, если возникла какая-либо из этих ошибок.

Когда установка будет успешной, нажмите 'Далее' для продолжения, и вам будет представлена заключительная настройка:

![](/download/attachments/18678479/setup-cleanup1.png?version=1&modificationDate=1280290901000)

MODx рекомендует вам обязательно удалить каталог setup/ после установки, чтобы защитить ваш сайт от тех, кто попытается запустить установку. Для этого активируйте флажок 'Отметьте этот пункт, чтобы удалить каталог и файлы программы установки с вашего сервера'.

Когда все будет готово, нажмите 'Войти', чтобы появилась форма входа в интерфейс панели управления. Вы закончили!

### Смотрите также

1. [Базовая установка](getting-started/installation/basic-installation)
  1. [MODx Revolution на Debian](getting-started/installation/basic-installation/modx-revolution-on-debian)
  2. [Руководство Lighttpd](getting-started/installation/basic-installation/lighttpd-guide)
  3. [Проблемы с WAMPServer 2.0i](getting-started/installation/basic-installation/problems-with-wampserver-2.0i)
  4. [Установка на сервер под управлением ModSecurity](getting-started/installation/basic-installation/installation-on-a-server-running-modsecurity)
  5. [MODX и Suhosin](getting-started/installation/basic-installation/modx-and-suhosin)
  6. [Конфигурация сервера Nginx](getting-started/installation/basic-installation/nginx-server-config)
2. [Расширенная установка](getting-started/installation/advanced-installation)
3. [Установка Git](getting-started/installation/git-installation)
4. [Установка из командной строки](getting-started/installation/command-line-installation)
  1. [Файл Xml с параметрами установки](getting-started/installation/command-line-installation/the-setup-config-xml-file)
5. [Устранение неполадок при установке](getting-started/installation/troubleshooting-installation)
6. [Успешная установка, что делать дальше?](getting-started/installation/successful-installation,-now-what-do-i-do)
7. [Использование MODx Revolution с SVN](getting-started/installation/using-modx-revolution-from-svn)
