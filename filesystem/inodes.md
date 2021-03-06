# Inodes

## Содержание урока

Помните, что наша файловая система состоит из всех наших фактических файлов и базы данных, которая управляет этими файлами? База данных известна как таблица inode. 

<b>Что такое inode?</b>

inode (индексный узел) является записью в этой таблице и для каждого файла есть один. Он описывает все о файле, например:

<ul>
<li>Тип файла - обычный файл, каталог, символьное устройство и т. д.</li>
<li>Владелец </li>
<li>Группа</li>
<li>Разрешения доступа</li>
<li>Timestamps - mtime (время последней модификации файла), ctime (время последнего изменения атрибута), atime (время последнего доступа)</li>
<li>Количество жестких ссылок на файл</li>
<li>Размер файла</li>
<li>Количество блоков, выделенных для файла</li>
<li>Указатели на блоки данных файла - самое главное!</li>
</ul>

В основном inodes хранят все о файле, кроме имени файла и самого файла!

<b>Когда создали inodes?</b>

Когда создается файловая система, также выделяется пространство для inodes. Существуют алгоритмы, позволяющие определить, сколько места в папке требуется вам в зависимости от объема диска и т.д. Вероятно, в какой-то момент вашей жизни были обнаружены ошибки из-за проблем с дисковым пространством. Ну, то же самое может произойти и для inodes (хотя и не так часто). Помните, что хранение данных зависит как от данных, так и от базы данных (inodes). 

Чтобы узнать, сколько инодов осталось в вашей системе, используйте команду <b>df -i</b>

<b>Информация об Inode</b>

Иноды идентифицируются по номерам, когда файл создается, ему присваивается номер inode, номер присваивается в последовательном порядке. Когда вы создаете новый файл, он получает номер inode, который ниже других, это связано с тем, что после удаления inodes они могут быть повторно использованы другими файлами. Чтобы просмотреть номера индексов<b>ls -li</b>:

<pre>
pete@icebox:~$ ls -li
140 drwxr-xr-x 2 pete pete 6 Jan 20 20:13 Desktop
141 drwxr-xr-x 2 pete pete 6 Jan 20 20:01 Documents
</pre>

Первое поле в этой команде перечисляет номер inode.

Вы также можете просмотреть подробную информацию о файле со статусом, он также сообщает вам информацию об inode.

<pre>
pete@icebox:~$ stat ~/Desktop/
  File: ‘/home/pete/Desktop/’
  Size: 6               Blocks: 0          IO Block: 4096   directory
Device: 806h/2054d      Inode: 140         Links: 2
Access: (0755/drwxr-xr-x)  Uid: ( 1000/   pete)   Gid: ( 1000/   pete)
Access: 2016-01-20 20:13:50.647435982 -0800
Modify: 2016-01-20 20:13:06.191675843 -0800
Change: 2016-01-20 20:13:06.191675843 -0800
 Birth: -
</pre>


<b>Как inodes размещает файлы?</b>

Мы знаем, что наши данные где-то на диске, к сожалению, не были сохранены последовательно, поэтому мы должны использовать inodes. Inodes указывают на фактические блоки данных ваших файлов. В типичной файловой системе (не все работают одинаково) каждый индекс содержит 15 указателей, первые 12 указателей указывают непосредственно на блоки данных. 13-й указатель указывает на блок, содержащий указатели на большее количество блоков, 14-й указатель указывает на другой вложенный блок указателей, а 15-й указатель снова указывает на другой блок указателей! Глупо, я знаю! Причина этого заключается в том, чтобы сохранить структуру inode одинаковой для каждого inode, но иметь возможность ссылаться на файлы разных размеров. Если у вас был небольшой файл, вы могли бы найти его быстрее с помощью первых 12 прямых указателей, более крупные файлы можно найти с помощью гнезд указателей. В любом случае структура inode одинакова.

## Задание

Понаблюдайте за некоторыми номерами inodes для разных файлов, какие из них обычно создаются первыми?

## Вопрос

Как вы видите, сколько инодов осталось в вашей системе?

## Ответ

df -i