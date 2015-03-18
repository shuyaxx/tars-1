<img height="67" width="192" src="https://raw.githubusercontent.com/artem-malko/artwork/master/tars/logo.png">
=============
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/artem-malko/tars?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

Сборщик html-верстки, основанный на <a href="http://gulpjs.com/" target="_blank">gulp.js</a>. Облегчает и ускоряет процесс html-верстки любой сложности. Подойдет как командам, так и отдельному разработчику. TARS решает большинство рутинных дел, связанных с версткой, чтобы вы получали больше удовольствия от работы.

TARS — сборщик-фреймворк, включающий в себя набор gulp-тасков, предоставляющий возможность легкого расширения (создания новых тасков) и модифицирования уже существующих. TARS предоставляет удобную архитектуру хранения тасков и вотчеров в проекте.

Это не npm-пакет. Такое решение было принято, чтобы каждый мог максимально комфортно кастомизировать сборщик под себя.

Основные фичи
-------------

Ниже перечислена только малая часть особенностей, на самом деле их гораздо больше)

* <a href="http://jade-lang.com/" target="_blank">Jade</a> или <a href="http://handlebarsjs.com/" target="_blank">Handlebars</a> на выбор в качестве html-шаблонизатора. Также можно использовать обычный html. Подробности <a href="/docs/html-processing.md">здесь</a>.
* Использование json (а точнее js-объекта, который может быть описан в json) для передачи данных в шаблоны (опционально, но очень крутая штука, которая позволит избавиться от копипаста). Подробнее <a href="/docs/html-processing.md#%D0%A0%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%BC%D0%BE%D0%B4%D1%83%D0%BB%D1%8F%D0%BC%D0%B8-%D0%B8-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D0%BC%D0%B8-%D0%B2-handlebars">тут</a>.
* <a href="http://sass-lang.com/" target="_blank">SCSS</a>, <a href="http://www.lesscss.ru/" target="_blank">LESS</a> или <a href="http://learnboost.github.io/stylus/" target="_blank">Stylus</a> в качестве препроцессора для css. Также в комплекте идет небольшой набор миксинов. Также можно использовать обычный css. Подробности <a href="/docs/css-processing.md">здесь</a>.
* Никаких внешних библиотек и плагинов (кроме <a href="https://ru.wikipedia.org/wiki/Html5_Shiv" target="_blank">html5shiv</a>). И да, это фича, так как вы вольны сами выбирать, какие библиотеки использовать.
* Используется модуль <a href="https://github.com/paulmillr/chokidar" target="_blank">chokidar</a> для вотчинга файлов.
* Расшариванием верстки с вашего компьютера во внешний веб, опционально. Ну и конечно же livereload в браузере (и не только локально) + графический интерфейс к панели управления устройствами, на которые расшаривается верстка.
* Можно легко добавлять новые таски и вотчеры. Есть примеры того, как создать и использовать новый таск или вотчер внутри TARS.
* Умная работа с изображениями. В первую очередь с вектором (svg). Больше не будет ада при верстке сайтов для экранов с высокой плотностью пикселей.
* Несколько режимов сборки (обычная, с минифицированными файлами, с хешем в названии css- и js-файлов для выкладки в продакшн).
* Создание архива с готовой сборкой.

Установка
----------

Необходимо <a href="http://nodejs.org/" target="_blank">установить `nodeJS`</a> версии выше или равной 0.8
Далее необходимо установить gulp глобально. (Возможно потребуются права суперюзера или администратора)

```shell
npm install -g gulp
```

<a href="../../../tars/archive/master.zip">Скачайте TARS</a> и распакуйте в рабочую директорию у себя на компьютере.
Затем устанавливаем зависимости. Команда запускается из папки с файлами TARS (обычно это tars-master).

```shell
npm install
```

Если не все зависимости были установлены, то последнюю операцию нужно повторить.

После установки всех зависимостей необходимо открыть tars-config (подробное описание опций <a href="/docs/options.md">здесь</a>) и настроить проект под себя. В конфиге вы можете выбрать шаблонизатор, css-препроцессор, использование уведомлений, имена папок для различной статики и т.д.
После настройки проекта, выполняем следующую команду:    

```shell
gulp init
```

Данная команда создаст базовую файловую структуру, подтянет таски для выбранных вами шаблонизатора и css-препроцессора.

Все готово, можно колбасить :)

Основные команды
----------------

`gulp init` — Инициализирует проект с заданными опциями в tars-config. Создает файловую структуру.

`gulp re-init` — Переинициализирует проект с заданными опциями в tars-config. Предлагается использовать данную команду, если вы инициализировали проект с неверными опциями. При переинициализации все папки и файлы удаляются.

`gulp` или `gulp build` — делает сборку проекта. Подключаются не минимизированные файлы. Тип сборки зависит от переданных ключей вместе с этой командой. Доступные ключи:

* `--min` – в html подключаются минимизированные файлы.
* `--release` – в html подключаются минимизированные файлы, в названии которых есть hash. Данный режим полезен, если вы напрямую выкладываете верстку на сервер. 

`gulp dev` — инициализация сборщика в режиме разработки. Создается dev-версия проекта, без всех минификаций. Также запускает вотчеры за файлами проекта. Доступные ключи:

* `--lr` – инициализация livereload (живая презагрузка страницы при изменениях в файлах проекта), если он включен в конфиге проекта.
* `--tunnel` – инициализация проекта с расшариванием верстки во внешний веб.

Ссылка будет указана в консоли. Также будет указана ссылка на панель управления устройствами, на которые расшарена верстка.

`gulp build-dev` — генерация dev-версии проекта без вотчеров.

Ключи, доступные при любом режиме сборки:
* `--ie8` – включить в сборку стили для ie8.

`gulp update-deps` – обновление всех зависимостей сборщика до последних стабильных. Может потребоваться какое-то время на выполнение данной команды. Желательно выполнять раз в неделю. Команда скопирует текущий package.json, добавит к его имени подчеркивание, скачает новый package.json с репозитория и выполнит npm install. Таким образом, если у вас что-то сломалось с новыми пакетами, то всегда можно вернуться на прошлую версию, просто вернув прошлый package.json
Также вы можете ознакомиться с <a href="/docs/update-guide.md" target="_blank">руководством по обновлению</a>.

Документация
------------

Важно! Все примеры в документации используют настройки по умолчанию.

* <a href="/docs/file-structure.md">Файловая структура</a>
* <a href="/docs/tasks-workflow.md">Работа с тасками и вотчерами</a>
* <a href="/docs/options.md">Опции</a>
* <a href="/docs/html-processing.md">Html</a>
* <a href="/docs/css-processing.md">Css</a>
* <a href="/docs/js-processing.md">Js</a>
* <a href="/docs/images-processing.md">Работа с изображениями</a>
* <a href="/docs/fonts-and-misc.md">Работа со шрифтами и misc-файлами</a>
* <a href="/docs/scenarios.md">Сценарии использования</a>
* <a href="/docs/update-guide.md">Руководство по обновлению</a>
* <a href="/docs/faq.md">FAQ</a>

Последние изменения
-------------------
Все последние изменения доступны по ссылке: <a href="/docs/changelog.md">История изменений</a>.

По всем вопросам можно писать в <a href="https://gitter.im/artem-malko/tars?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge" target="_blank">gitter</a> или на почту <a href="mailto:artem.malko@gmail.com">artem.malko@gmail.com</a><br/>
Баги и фича-реквесты сюда: <a href="https://github.com/artem-malko/tars/issues/new">issues</a>.
