1. Установить Oracle Linux 8.5
  - Во время разметки выбрать btrfs и удалить swap
  - В настройках сети исправить название хоста
  - Добавить юзера alfes с админскими правами во время установки
2. После установки убедиться, что sshd запущен и порт 22 открыт в файрволле
***
1. Сначала ssh-keygen.
2. Для каждой машины ssh-copy-id alfes@192.168.109.143
3. Для проверки плейбука `ansible-playbook  --ask-become-pass -i /home/alfes/ansible/inventory.yml --check /home/alfes/ansible/main.yml` где
  * `--ask-become-pass` запрашивает пароль sudo
  * `-i /home/alfes/ansible/inventory.yml` параметр пути до файла с хостами
  *  `--check` выполняет проверку вместо запуска
  *  `/home/alfes/ansible/main.yml` путь до плейбука
 