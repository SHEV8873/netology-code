#Домашнее задание к занятию "3.1. Работа в терминале, лекция 1"
|№ вопроса|Вопрос|Ответ|
|:-------------:|----------|--------------|
|1|Установите средство виртуализации Oracle VirtualBox|Установлено|
|2|Установите средство автоматизации Hashicorp Vagrant|Установлено|
|3|В вашем основном окружении подготовьте удобный для дальнейшей работы терминал|Подготовлен Windows Terminal|
|4|С помощью базового файла конфигурации запустите Ubuntu 20.04 в VirtualBox посредством Vagrant|Выполнено|
|5|Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?|Оперативная память - 1024 МБ, жесткий диск - 64 ГБ, количество процессоров - 2, предел загрузки ЦП - 100%, видеопамять - 4 МБ|
|6|Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: документация. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?|Добавить в Vagrantfile:<p>config.vm.provider "virtualbox" do &#124;v&#124;</p><p>v.memory = *объем оперативной памяти*</p><p>v.cpu = *количество процессоров*</p><p>v.customize ["modifyvm", :id, "--cpuexecutioncap", "*ограничение на использование времени ЦП*"]</p>|
|8|<p>Какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?</p><p>Что делает директива ignoreboth в bash?</p>|<p>переменная HISTFILESIZE=*максимальное число строк в файле history*, строки 554-557, 2067-2072 </p><p>HISTSIZE=*максимальное количество команд, сохраняемых в истории команд*, строки 562-564, 2062-2068</p><p>директива ignoreboth предписывает не сохранять в истории строки, начинающиеся с пробела, а так же строки, соответствующие предыдущей записи в истории (эквивалент одновременному применению директив ignorespace и ignoredups</p>|
|9|В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?|<p>Фигурные скобки используются в составных командах при группировке команд, которые выполняются как единое целое, перенаправления могут применяться для всего списка команд. Помещение списка команд между фигурными скобками приводит к тому, что список будет выполняться в текущем контексте оболочки, подоболочка не создается. Статус возврата - это статус выхода из списка. (строки 180-187).</p>Фигурные скобки используются как Brace Expansion - механизм, с помощью которого могут быть созданы произвольные строки. Этот механизм аналогичен расширению имени пути, но сгенерированные имена файлов могут не существовать. Шаблоны, которые нужно раскрыть в фигурные скобки, принимают форму необязательной преамбулы, за которой следует либо последовательность строк, разделенных запятыми, либо выражение последовательности между парой фигурных скобок, за которым следует необязательный постскриптум. Преамбула ставится перед каждой строкой, содержащейся в фигурных скобках, а затем добавляется постскриптум к каждой результирующей строке, расширяясь слева направо. Раскладки скобок могут быть вложенными. Результаты каждой развернутой строки не сортируются; порядок слева направо сохраняется (строки 706-732).|
|10|С учётом ответа на предыдущий вопрос, как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?|<p>touch {000001..100000}.*расширение файла*</p><p>Создать 300000 не получится вследствие ограничения ядра на размер аргумента командной строки ARG_MAX</p><p>getconf ARG_MAX</p>2097152|
|11|В man bash поищите по /\\[\\[. Что делает конструкция [[ -d /tmp ]]|Конструкция-условное выражение проверяет существование каталога tmp, и в зависимости от результата возвращает 0 или 1|
|12|<p>Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:</p><p>bash is /tmp/new_path_directory/bash</p><p>bash is /usr/local/bin/bash</p><p>bash is /bin/bash</p><p>(прочие строки могут отличаться содержимым и порядком) В качестве ответа приведите команды, которые позволили вам добиться указанного вывода или соответствующие скриншоты.</p>|<p>$ sudo cp /bin/bash /usr/local/bin</p><p>$ mkdir /tmp/new_path_directory</p><p>$ sudo cp /bin/bash /tmp/new_path_directory</p><p>$ echo $PATH</p><p>$ export PATH=/tmp/new_path_directory/:/usr/local/sbin:/usr/local/bin:/usr/sbin:/bin:/sbin:/usr/bin:/usr/games:/usr/local/games:/snap/bin</p><p>$ type -a bash</p><p>*вывод*</p><p>bash is /tmp/new_path_directory/bash</p><p>bash is /usr/local/bin/bash</p><p>bash is /bin/bash</p>bash is /usr/bin/bash|
|13|Чем отличается планирование команд с помощью batch и at?|Команда at используется для назначения одноразового задания (выполнение команд) на заданное время, а команда batch — для назначения одноразовых задач, которые должны выполняться, когда загрузка системы становится меньше определенного значения. Если средняя загрузка системы выше указанной, задания будут ждать в очереди.|
|14|Завершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука|<p>Выполнено</p>vagrant suspend|