[<Основы Git: Запись изменений в Git- репозитория ](./RecordingChanges.md)

## Игнорирование индексации
Несмотря на то, что индекс может быть удивительно необычным для создания коммитов именно таким, как вам и задержанным, он временами несколько сложнее, чем вам необходимо в процессе работы. Если у вас есть желание пропустить этап индексирования, **Git** предоставляет простой способ. Добавление параметра `-a` в команду `git commit` заставляет **Git** автоматически индексировать каждый уже отслеживаемый на момент коммита файл, использует вам запросы без [git add](./add.md):
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md

no changes added to commit (use "git add" and/or "git commit -a")
$ git commit -a -m 'Add new benchmarks'
[master 83e38c7] Add new benchmarks
 1 file changed, 5 insertions(+), 0 deletions(-)
```
Обратите внимание, что в данном случае перед коммитом вам не нужно выполнять файл [git add](./add.md), `CONTRIBUTING.md` потому что `-a `флажок включает все файлы. Это удобно, но осторожно `-a`.

