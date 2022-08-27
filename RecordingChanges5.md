[<Основы Git: Запись изменений в Git- репозитория ](./RecordingChanges.md)

## Игнорирование файлов
массив, у вас есть группа файлов, которые вы не только не хотите автоматически включать в репозиторий, но и видеть в списках неотслеживаемых. К таким файлам обычно относятся автоматически генерируемые файлы (различные логи, результаты программ и т.п. сборки). В таком случае вы можете создать файл `.gitignore`. с перечислением шаблонов, соответствующих такому файлу. Вот пример файла .gitignore:
```
$ cat .gitignore
*.[oa]
*~
```
Первая строка предписывает Git игнорировать любые файлы, заканчивающиеся на «.o» или «.a» — объектные и архивные файлы, которые появляются во время сборки кода. Вторая строка предписывает игнорировать все файлы, записываемые на тильду ( ~), который используется во многих текстовых редакторах, например Emacs, для обозначения временных файлов. Вы можете также включить каталоги log, tmp или pid; автоматически принимающую документацию; и т.д. д. и т.д. п. Хорошая практика корректирует настройки файла .gitignoreдо того, как начать серьезно работать, это защитит вас от случайного добавления в репозиторий файлов, которые вы там видеть не хотите.

К шаблонам в файле `.gitignore` применяются применяемые правила:

Пустые строки, а также строки, начинающиеся с #, ухудшаются.

Стандартные шаблоны являются глобальными и рекурсивно применяются для дерева всего каталога.

Чтобы избежать рекурсии використовуйте символ слеш (/) в начале шаблона.

Чтобы журнал событий добавил слеш (/) в конце шаблона.

Можно инвертировать шаблон, используя восклицательный знак (!) в качестве первого символа.

Glob-шаблоны пользуются упрощёнными регулярными выражениями, используемыми командными интерпретаторами. ( Символ *) соответствует 0 или более символам; последовательности [abc] — в случае использования символа в скобках (в случае использования a, b или c); знак вопроса ( ?) соответствует одному символу; и квадратные скобки, в которых используются сопоставления символов, разделенные дефисом ( [0-9]), соответствуют любому символу из интервала (в случае использования от 0 до 9). Вы также можете использовать множество звёздочек, чтобы указать вложенные каталоги: ближайшие a/**/z, a/z, a/b/z, a/b/c/zи так далее.

Вот ещё один пример файла .gitignore:
```
# Исключить все файлы с расширением .a
*.a

# Но отслеживать файл lib.a даже если он подпадает под исключение выше
!lib.a

# Исключить файл TODO в корневом каталоге, но не файл в subdir/TODO
/TODO

# Игнорировать все файлы в каталоге build/
build/

# Игнорировать файл doc/notes.txt, но не файл doc/server/arch.txt
doc/*.txt

# Игнорировать все .txt файлы в каталоге doc/
doc/**/*.txt
```
***
**Подсказка**
GitHub поддерживает полный список примеров .gitignoreфайлов для поиска проектов и языков https://github.com/github/gitignore , это может стать отправной точкой для .gitignoreбудущего проекта.
***
**Примечание**
В обычном случае репозиторий будет иметь один файл .gitignoreв корневом каталоге, из правил которого будут рекурсивно вести ко всем подкаталогам. Так же возможно использовать .gitignoreфайлы в подкаталогах. Правила из этих файлов ведутся только к каталогам, в которых они находятся. Например, репозиторий исходного кода ядра Linux содержит 206 файлов .gitignore.
***