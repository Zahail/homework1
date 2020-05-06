# homework1
Задание выполнялось по методичке https://github.com/dmitry-lyutenko/manual_kernel_update/blob/master/manual/manual.md

Поставил CentOS 7. Установил **Vagrant**, **Packer**, **VirtualBox**. 
**Git** уже был в дистрибутиве. Зарегистрировал аккаунты на **GitHub** и **Vagrant Cloud**.

Склонировал к себе репозиторий https://github.com/dmitry-lyutenko/manual_kernel_update

Запустил виртуальную машину с помощью `vagrant up`, обновил ядро и конфигурацию загрузчика. Подключившись к машине командой `vagrant shh`,
 проверил версию ядра `uname -r`.

Далее в файле `centos.json` в секции `builders` заменил "iso_url" и "iso_checksum", т.к. ссылка была нерабочая. Получилось 
собрать образ с помошью `packer build centos.json` и импортировать его в Vagrant. 

Затем провел тестирование созданного образа. Для этого создал Vagrantfile на основе файла из репы manual_kernel_update, изменив 
`:box_name => "centos-7-5"` и добавив скрипт `box.vm.provision "shell", path: "stage-1-kernel-update.sh"` для обновления ядра.
Запустил виртуальную машину и проверил наличие нового ядра.

Залил полученный образ в Vagrant Cloud https://app.vagrantup.com/zahail/boxes/centos-7-5
