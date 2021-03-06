# Обзор Upstart

## Содержание урока

Upstart был разработан Canonical, так что какое-то время это была реализация init на Ubuntu, однако на современных установках Ubuntu теперь используется systemd. Upstart был создан для улучшения Sys V, для устранения таких проблем как: строгие процессы запуска, блокировки задач и т.д. Событие Upstart и модель, управляемая заданиями, позволяют ему реагировать на события по мере их возникновения.

Чтобы узнать, используете ли вы Upstart, проверьте наличие каталога /usr/share/upstart.

Задания - это действия, которые выполняет Upstart, а события - это сообщения, полученные от других процессов для запуска заданий. Чтобы просмотреть список заданий и их конфигурацию:

<pre>
pete@icebox:~$ ls /etc/init
acpid.conf                   mountnfs.sh.conf
alsa-restore.conf            mtab.sh.conf
alsa-state.conf              networking.conf
alsa-store.conf              network-interface.conf
anacron.conf                 network-interface-container.conf
</pre>

Внутри этих конфигураций будет содержаться информация о том, как начинать работу и когда её начинать.

Например, в файле networking.conf можно было бы сказать что-то простое:
<pre>
start on runlevel [235]
stop on runlevel [0]
</pre>

Это означает, что он начнет настройку сети на уровне выполнения 2, 3 или 5 и прекратит работу в сети на уровне запуска 0. Существует много способов написать конфигурационный файл.

Способ, на которым работает Upstart, заключается в том, что:

<ol>
<li>Во-первых, он загружает конфигурации заданий из /etc/init</li>
<li>Как только произойдет запуск, он будет запускать задания, вызванные этим событием.</li>
<li>Эти задания будут создавать новые события, а затем эти события вызовут новые задания</li>
<li>Upstart продолжает делать это до тех пор, пока не выполнит все необходимые задания</li>
</ol>

## Задание

Если вы используете Upstart, проверьте, можете ли вы определить конфигурацию задания в /etc/init.

## Вопрос

Какова реализация init, используемая в Ubuntu?

## Ответ

upstart
