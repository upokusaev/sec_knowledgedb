# Пользователи в linux

Linux система многопользовательская, т.е. на одном компьютере может быть несколько различных пользователей,  
каждый со своими собственными настройками, данными и правами доступа к различным системным функциям.  

Кроме пользователей в Linux для разграничения прав существуют группы.  
Каждая группа так же как и отдельный пользователь обладает неким набором прав доступа к различным компонентам  
системы и каждый пользователь-член этой группы автоматически получает все права группы.  

## Права доступа

Любой файл и каталог в Linux имеет пользователя-владельца и группу-владельца.  
То есть любой файл и каталог принадлежит какому-то пользователю системы и какой-то группе.  
Кроме того, у любого файла и каталога есть три группы прав доступа: одна для пользователя-владельца,  
одна для членов группы-владельца и одна для всех остальных пользователей системы.  
Каждая группа состоит из прав на чтение, запись и запуск файла на исполнение.  
Для каталогов право на исполнение и право на чтение всегда идут вместе и означают одно и то же.  

Команда `ls -l`, может быть использована для отображения прав доступа и владельца.  

команда `ls -l file1.txt` отобразит:  
`-rwxr–rw- 1 user user 0 Jan 19 12:59 file1.txt`

* `-rwxr–rw-` –  эта часть строки показывает права доступа. Здесь 4 главные буквы на которые вам надо обратить внимание: `r,w,x,d`. **d** означает, что тип файла – это каталог. В нашем примере, такой буквы нет (она стояла бы первой в строке), здесь вместо нее стоит символ **"-"** (который в основном означает “нет”). Буква **x** означает разрешение на выполнение файла или папки (это разрешение необходимо для входа в папку). Буква **w** означает разрешение на запись файла или папки (редактирование, удаление и т.д.) И наконец последняя буква **r**, которая означает чтение. Если у вас есть права на чтение файла, вы можете прочесть содержимое файла, но не сможете предпринять другие действия (к примеру, вы можете прочитать код скрипта, но не сможете выполнить его).
* 1 – число хард связи. Проще говоря, хард связь это дополнительное имя для существующего файла.
* user user – это значение показывает владельца файла и его группу.
* 0 – это значение показывает размер файла.
* Jan 19 12:59 – отображает дату последнего изменения.
* file1.txt – предоставляет имя файла или папки.

## Изменение прав и владельца

Утилита **chmod** - изменяет права доступа
Утилита **chown** - меняет владельца

[← Назад](../README.md)