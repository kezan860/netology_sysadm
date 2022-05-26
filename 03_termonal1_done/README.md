# Работа в терминале (Лекция 1)

Вопросы:

1. Какие ресурсы выделены по-умолчанию?

***Ответ:***
```
1. ОЗУ - 1024 МБ
2. vCPU - 2
3. vGPU - 4 МБ
4. Объекм жесткого диска - 64 ГБ
```
2. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?

***Ответ:*** Добавление команд в VargantFile:
```
1. ОЗУ -  v.memory = n (где n - любое десятичное число > 0)
2. vCPU -  v.cpus = n (где n - любое десятичное число > 0)
```

3. Какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?

***Ответ:*** Название переменной - HISTSIZE, находится на 2154 строчке
4. Что делает директива ignoreboth в bash?

***Ответ:***<br>
ignoreboth это сокращение для 2х директив ignorespace and ignoredups, <br>
ignorespace - не сохранять команды начинающиеся с пробела, <br>
ignoredups - не сохранять команду, если такая уже имеется в истории
5. В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?

***Ответ:*** То, что находится между круглыми скобками (), выполняется в отдельном подпроцессе. 
А то, что находится между фигурными скобками {} — выполняется в контексте текущей оболочки,
используются там где нужна скорость выполнения скрипта.
6. С учётом ответа на предыдущий вопрос, как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?

***Ответ:***<br>
touch {000001..100000}.py - создаст в текущей директории 100000 файлов с расширением py

300000 файлов данной командой сделать невозможно, ошибка: Argument list too long 
7. В man bash поищите по /\[\[. Что делает конструкция [[ -d /tmp ]]

***Ответ:*** проверяет условие у -d /tmp и возвращает ее статус (0 или 1), наличие катаолга /tmp
8. Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:

bash is /tmp/new_path_directory/bash
bash is /usr/local/bin/bash
bash is /bin/bash

(прочие строки могут отличаться содержимым и порядком) В качестве ответа приведите команды, которые позволили вам добиться указанного вывода или соответствующие скриншоты.

***Ответ:***

```
* # mkdir /tmp/new_path_dir/
* # cp /bin/bash /tmp/new_path_dir/
* # type -a bash
* bash is /usr/bin/bash
* bash is /bin/bash
* # PATH=/tmp/new_path_dir/:$PATH
* # type -a bash
* bash is /tmp/new_path_dir/bash
* bash is /usr/bin/bash
* bash is /bin/bash
```

9. Чем отличается планирование команд с помощью batch и at?

***Ответ:***
   1) at - команда запускается в указанное время (в параметре)
   2) batch - запускается когда уровень загрузки системы снизится ниже 1.5
