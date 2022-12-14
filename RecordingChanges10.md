[<Основы Git: Запись изменений в Git- репозитория ](./RecordingChanges.md)

## Перемещение файлов
В отличие от многих других систем контроля версий, **Git** не отслеживает сдвиг файлов. Когда вы переименовываете файл в **Git**, в журнале не найдено никаких метаданных, говорящих о том, что файл был переименован. Тем не менее, **Git** довольно быстро обнаружил обнаружение перемещений файлов чуть позже.

Таким образом, наличие в **Git** команды mvвыглядит несколько странным образом. Если вам нужно переименовать файл в **Git**, вы можете сделать что-то вроде:
```
$ git mv file_from file_to
```
и это отлично сработает. На самом деле, если вы обнаружили что-то вроде этого и посмотрите на статус, вы обнаружили, что **Git** считает, что произошло переименование файла:
```
$ git mv README.md README
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README
```
Однако это эквивалентно выполнению следующей команды:
```
$ mv README.md README
$ git rm README.md
$ git add README
```
**Git** неявно определяет, что произошло переименование, поэтому неважно, переименуете вы файл так или используете команду mv. Единственное отличие состоит лишь в том, что mv — одна команда вместо трёх — это функция для удобства. Важно другое — вы можете использовать любой удобный способ переименования файла, а затем командами addили rmперед коммитом.