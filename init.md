[< к содержанию](./readme.md)  

## git init

На этой странице подробно описывается команда `git init`. Вы узнаете об основном функционале и дополнительных возможностях этой команды. Приводятся следующие сведения:

+ использование команды `git init` и ее опции;
+ обзор каталога `.git`;
+ пользовательские значения переменных + среды для каталога `git init`;
+ сравнение `git init` и `git clone`;
+ создание чистых репозиториев с помощью `git init`;
+ шаблоны для `git init`.

Команда `git init` создает новый репозиторий **Git**. С ее помощью можно преобразовать существующий проект без управления версиями в репозиторий **Git** или инициализировать новый пустой репозиторий. Большинство остальных команд **Git** невозможно использовать без инициализации репозитория, поэтому данная команда обычно выполняется первой в рамках нового проекта.

При выполнении команды `git init` в текущем рабочем каталоге создается подкаталог `.git` со всеми необходимыми метаданными **Git** для нового репозитория. Метаданные включают подкаталоги для объектов, ссылок и файлов шаблонов. Кроме того, создается файл **HEAD**, который указывает на текущий извлеченный коммит.

Кроме создания каталога `.git`, корневой каталог существующего проекта не изменяется каким-либо образом (в отличие от **SVN, Git** не требует наличия подкаталога `.git` в каждом подкаталоге).

По умолчанию команда `git init` инициализирует конфигурацию **Git** в подкаталоге `.git` по соответствующему пути. При необходимости путь подкаталога можно изменить. Если присвоить переменной среды `$GIT_DIR` пользовательское значение пути, команда `git init` инициализирует файлы конфигурации **Git** по этому пути. Такой же результат можно получить, если передать команде аргумент `--separate-git-dir`. Часто отдельный подкаталог `.git` создается из тех соображений, что системные файлы конфигурации с точкой перед именем (`.bashrc, .vimrc `и др.) должны размещаться в домашнем каталоге, а папка `.git `— в другом месте.
Использование
По сравнению с **SVN**, создавать новые проекты с управлением версиями при помощи команды `git init` намного проще. **Git** не требует создавать репозиторий, импортировать файлы и извлекать рабочую копию. Кроме того, для **Git** не требуются права администратора или доступ к серверу. Для получения полноценного репозитория **Git** достаточно перейти в подкаталог проекта и выполнить команду `git init`.

`git init`
Преобразование текущего каталога в репозиторий **Git**. Команда создает подкаталог `.git` в текущем каталоге и позволяет начать регистрацию версий проекта.

`git init <directory>`
Создание пустого репозитория **Git** в указанном каталоге. При выполнении этой команды будет создан новый подкаталог — он будет содержать только подкаталог .`git` .

Если команда `git init` уже выполнялась по отношению к каталогу проекта и в нем есть подкаталог `.git`, команду `git init` можно безопасно выполнить для этого каталога повторно. Существующая конфигурация `.git` при этом не изменится.

Сравнение `git init` и `git clone`
Краткое замечание: `git init` и `git clone` легко спутать, поскольку обе команды можно использовать для инициализации нового репозитория **Git**. Однако команда `git clone` зависит от `git init` ипредназначена для создания копии существующего репозитория. Выполнение `git clone` сначала вызывает `git init`, чтобы создать новый репозиторий, затем копирует данные из существующего репозитория и извлекает новый набор рабочих файлов. Подробнее см. на странице о команде `git clone`.

Чистые репозитории: `git init` --bare
`git init --bare <directory>`
Инициализируйте пустой репозиторий **Git** без рабочего каталога. Общедоступные репозитории необходимо всегда создавать с флагом `--bare` (см. пояснения ниже). Обычно названия репозиториев после инициализации с флагом `--bare` оканчиваются на `.git.` Так, чистый вариант репозитория под названием `my-project `должен храниться в каталоге m`y-project.git.`

Флаг --bare приводит к созданию репозитория без рабочего каталога. В таком репозитории нельзя редактировать файлы и вносить изменения. Чистый репозиторий создается для выполнения команд `git push` и `git pull`, но не для прямых коммитов. Центральные репозитории всегда следует создавать чистыми, поскольку при отправке веток в обычный репозиторий существует риск перезаписи изменений. Просто представьте, что флаг --bare превращает репозиторий из среды разработки в хранилище. По этой причине для рабочих процессов Git центральный репозиторий практически всегда создается чистым, а локальные репозитории разработчиков — обычными.

Обучающее руководство Git: чистые репозитории
Команда git init --bare чаще всего используется для создания удаленного центрального репозитория:
```
ssh <user>@<host> cd path/above/repo git init --bare my-project.git
```
Сначала устанавливается SSH‑соединение с сервером, на котором будет размещаться центральный репозиторий. Затем нужно перейти в каталог, где планируется хранить проект, и с помощью флага --bare создать центральный репозиторий‑хранилище. Позднее разработчики смогут клонировать каталог my-project.git для создания локальной копии на рабочих компьютерах.

Шаблоны  git init
`git init <directory> --template=<template_directory>`
Инициализация нового репозитория Git и копирование в него файлов из каталога .

С помощью шаблонов можно инициализировать новый репозиторий с заранее заданным подкаталогом .git . В настройках шаблона можно указать каталоги и файлы, которые будут по умолчанию скопированы в подкаталог .git нового репозитория. Доступные по умолчанию шаблоны Git обычно находятся в каталоге `/usr/share/git-core/templates` (путь может отличаться).

Доступные по умолчанию шаблоны — это удобный справочный ресурс, в котором можно найти примеры использования возможностей шаблонов. В таких шаблонах в том числе показана настройка полезной функции `Git hook`. При создании шаблона можно задать нужные элементы Git hook. Это позволит инициализировать новые репозитории **Git** с готовыми к работе элементами hook. Дополнительные сведения о `Git hook` см. на странице о `Git hook`.

Настройка
Все варианты конфигураций для команды `git init` можно использовать с аргументом . При указании аргумента  команда выполняется в соответствующем каталоге. Если каталог не существует, он будет создан. Помимо вышеописанных опций git init имеет еще ряд параметров командной строки. Их полный перечень приводится ниже.

**-Q**

**--QUIET**

Вывод только критических сообщений, сообщений об ошибках и предупреждений. Вывод других сообщений блокируется.

**--BARE**

Создание чистого репозитория (см. раздел «Чистые репозитории» выше).

**--TEMPLATE=**

Указание каталога с шаблонами для использования (см. раздел «Шаблоны git init» выше).

**--SEPARATE-GIT-DIR=**

Создание текстового файла, содержащего путь к каталогу . Данный файл служит ссылкой на каталог .git и может быть полезен, если каталог .git нужно хранить отдельно от рабочих файлов проекта (например, на другом диске). Параметр `--separate-git-dir` обычно используют в следующих случаях:

Необходимо хранить системные файлы конфигурации с точкой перед именем (`.bashrc, .vimrc` и др.) в домашнем каталоге, а папку `.git` — в другом месте.
История **Git** стала занимать слишком много места и требует переноса на диск большей емкости.
Проект **Git** требуется разместить в общедоступном каталоге, например `www:root`
Можно выполнить команду `git init --separate-git-dir` для существующего репозитория. В этом случае каталог `.git` будет перемещен по указанному пути .

`--SHARED[=(FALSE|TRUE|UMASK|GROUP|ALL|WORLD|EVERYBODY|0XXX)]`

Назначение прав доступа для нового репозитория. Данный параметр позволяет с помощью указания прав Unix задать пользователей и группы, которым разрешено осуществлять операции `push и pull` в репозитории.

Примеры
Создание нового репозитория Git для существующей базы кода
```
cd /path/to/code \ 
git init \ 
git add . \ 
git commit
```
Создание нового чистого репозитория
`git init --bare /path/to/repo.git`
Создание шаблона `git init` и инициализация нового репозитория *Git* на основе этого шаблона
```
mkdir -p /path/to/template \ 
echo "Hello World" >> /absolute/path/to/template/README \
git init /new/repo/path --template=/absolute/path/to/template \ 
cd /new/repo/path \ 
cat /new/repo/path/README
```