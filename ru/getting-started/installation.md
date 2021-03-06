---
title: "Установка"
translation: "getting-started/installation"
---


Эта страница предназначена только для ** новых установок **. Если вы хотите обновить, см.[Обновление MODx](administering-your-site/upgrading-modx "Upgrading MODx").

Перед началом установки вы должны убедиться, что ваш сервер соответствует [Требованиям к серверу](getting-started/server-requirements "Server Requirements").

## Скачивание MODX

Чтобы загрузить MODX Revolution 2.x, у вас есть два варианта: MODX Site или через Git:

### С сайта MODX

Самый быстрый способ запустить ваш сайт Revolution - это получить копию прямо со страницы [Загрузки MODX](http://modxcms.com/download/). Там вы найдете загрузки для MODX Revolution.

Стоит отметить, что эти пакеты в основном являются снимками Git, нашего программного обеспечения для контроля версий, на момент их упаковки. С тех пор многое могло измениться, включая исправления ошибок и добавление новых функций. Обратите внимание на дату выпуска для каждого пакета. Git всегда будет иметь самую последнюю версию Revolution.

#### «Традиционный» против «Продвинутый»

Вы, наверное, заметили, что есть несколько разных типов пакетов на выбор. Некоторые из них помечены как «Расширенные», другие просто старые «modx-2.1.0-xxxx-#.zip». Так что же означают эти ярлыки?

- Традиционный - эти пакеты представляют собой готовые снимки из Git. Вы можете просто распаковать файлы на свой сервер и следовать [Базовая установка](getting-started/installation/basic-installation "Basic Installation") руководства по установке MODX. Большинство пользователей должны выбрать эту версию.

- Продвинутый - Эти пакеты немного меньше половины размера «традиционных» загрузок, поскольку содержимое «ядра» сжато. Программа установки MODX попытается распаковать или «собрать» этот пакет во время установки. Рекомендуется использовать это только в том случае, если вы планируете перемещать каталоги core, manager или connectors, у вас есть доступ по SSH и вы знакомы с тем, как сделать папки доступными для записи. Пожалуйста, следуйте документации [Расширенная установка](getting-started/installation/advanced-installation "Advanced Installation").

### С Git

MODX Revolution управляется на [GitHub](http://github.com/modxcms). Пожалуйста, прочитайте [Установка Git](getting-started/installation/git-installation "Git Installation") документ, чтобы узнать, как использовать MODX Revolution с Git.

## Установка MODX

MODX поставляется с несколькими дистрибутивами для скачивания. Шаги установки будут отличаться в каждом дистрибутиве, поэтому, пожалуйста, выберите руководство по установке дистрибутива ниже:

- Традиционный дистрибутив: [Базовая установка](getting-started/installation/basic-installation "Basic Installation")
- Продвинутый дистрибутив: [Продвинутая установка](getting-started/installation/advanced-installation "Advanced Installation")
- Сборка с Git: [Git Installation](getting-started/installation/git-installation "Git Installation")

Смотрите также страницу [Установка из командной строки](getting-started/installation/command-line-installation "Command Line Installation").

После завершения установки, если у вас все еще есть проблемы, пожалуйста, прочитайте страницу [Устранение неполадок при установке](getting-started/installation/troubleshooting-installation "Troubleshooting Installation").