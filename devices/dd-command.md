# dd

## Содержание урока

Инструмент dd очень полезен для конвертирования и копирования данных. Он считывает данные из файла или потока данных и записывает их в файл или поток данных.

Рассмотрим следующую команду:

<pre>$ dd if=/home/pete/backup.img of=/dev/sdb bs=1024 </pre>

Эта команда копирует содержимое backup.img в /dev/sdb. Она будет копировать данные в блоках по 1024 байта, пока не будут скопированы все данные. 

<ul>
<li>if=file - входной файл, считанный из файла вместо стандартного ввода</li>
<li>of=file - выходной файл, запись в файл вместо стандартного вывода</li>
<li>bs=bytes - размер блока, он считывает и записывает эти многочисленные байты данных за раз. Вы можете использовать разные показатели, указав размер с k для килобайта, m для мегабайта и т. Д., Поэтому 1024 байта равно 1k</li>
<li>count=number - Количество блоков для копирования.</li>
</ul>

Вы увидите некоторые команды dd, которые используют опцию count, обычно с dd, если вы хотите скопировать файл, который составляет 1 мегабайт, вы хотите увидеть этот файл с размером 1 мегабайт, когда он будет скопирован. Предположим, вы выполните следующую команду: 

<pre>$ dd if=/home/pete/backup.img of=/dev/sdb bs=1M count=2</pre>

Наш файл backup.img - 10M, однако мы говорим в этой команде, чтобы скопировать более 1M 2 раза, поэтому копируется только 2M, в результате чего наши скопированные данные будут неполными. Count может пригодиться во многих ситуациях, но если вы просто копируете данные, вы можете в значительной степени опустить count и даже bs. Если вы действительно хотите оптимизировать свою передачу данных, тогда вы начнёте использовать эти параметры.

dd чрезвычайно эффективен, вы можете использовать его для создания резервных копий всего, включая целые дисководы, восстановление образов дисков и многое другое. Будьте осторожны, так как этот мощный инструмент может стоить вам многого, если вы не уверены, что делаете.

## Задание

Используйте команду dd для создания резервной копии вашего диска и установки вывода в файл .img.

## Вопрос

Какова опция dd для размера блока?

## Ответ

bs