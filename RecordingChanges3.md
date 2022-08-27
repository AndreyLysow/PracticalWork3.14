[<Основы Git: Запись изменений в Git- репозитория ](./RecordingChanges.md)

## Индексация изменённых файлов
Давайте модифицируем файл, уже поступающий под версионным контролем. Если вы измените отслеживаемый файл CONTRIBUTING.mdи после этого снова выполните команду `git status`, то результат будет примерно таким:
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```
Файл CONTRIBUTING.mdнаходится в секции «Изменения, не подготовленные для фиксации» — это означает, что отслеживаемый файл был изменён в рабочем каталоге, но пока не проиндексирован. Для того, чтобы проиндексировать его, необходима команда [git add](./add.md). Это многофункциональная команда, используемая для добавления под версионный контроль новых файлов, для индексации изменений, а также для других целей, например для указаний файлов с исправленным конфликтом слияния. Вам может быть понятно, если вы будете думать об этом как «добавить этот контент в следующий коммит», а не как «добавить этот файл в проект». Выполним git add, чтобы проиндексировать `CONTRIBUTING.md`, а затем снова выполним git status:
```
$ git add CONTRIBUTING.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md
```
Теперь оба файла проиндексированы и отправятся в следующую коммит. В этот момент вы, предположим, вспомнили одно небольшое изменение, которое вы хотите сделать `CONTRIBUTING.md` до коммита. Вы открываете файл, вносите и сохраняете необходимые изменения и вроде бы готовы к комиссии. Но давайте раз выполним git status:
```
$ vim CONTRIBUTING.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```
Что за чёрт? Теперь `CONTRIBUTING.md` выступают как проиндексированный и непроиндексированный одновременно. Как такое возможно? Такая очевидная ситуация, когда Git индексирует файл в том состоянии, в котором он оказался, когда вы выполнили задание git add. Если вы выполняете коммит сейчас, то файл `CONTRIBUTING.md` попадает в коммит в том состоянии, в котором он стоит, когда вы последний раз выполняете задание [git add](./add.md), а не в том, в котором он находится в предстоящем рабочем каталоге в момент выполнения `git commit.` Если вы изменили файл после выполнения git add, вам потребуется снова выполнить проверку [git add](./add.md), чтобы проиндексировать последнюю версию файла:
```
$ git add CONTRIBUTING.md
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md
```