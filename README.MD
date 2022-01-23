1. Установить Oracle Linux 8.5
  - Во время разметки выбрать btrfs и удалить swap
  - В настройках сети исправить название хоста
  - Добавить юзера alfes с админскими правами во время установки
2. После установки убедиться, что sshd запущен и порт 22 открыт в файрволле
***
1. Устанавливаем ансибль и прочие пакеты `pipenv install`.
2. Устанавливаем модули ансибля `ansible-galaxy collection install -r requirements.yml`.
3. Генерим ключ ssh-keygen -t rsa.
4. Запускаем `ansible-playbook --ask-become-pass -i inventory.yml add_user.yml`, чтобы скопировать ключ в рута на каждой удалённой машине. Это, возможно, не очень секьюрно, но позволит запускать задачи без эскалации привилегий (не нужно будет пароль вводить каждый раз). Заодно отключаем возможность подключиться по ssh с паролем.
5. Для проверки плейбука `ansible-playbook -i inventory.yml --check main.yml` где
  * `--ask-become-pass` запрашивает пароль sudo
  * `-i inventory.yml` параметр пути до файла с хостами
  *  `--check` выполняет проверку (dry run) вместо запуска
  *  `main.yml` путь до плейбука
 
## Разрегистрировать ноды на мастере
```sh
kubectl cordon s1.local && \
kubectl drain s1.local --force --ignore-daemonsets --delete-emptydir-data && \
kubectl delete node s1.local && \
kubectl cordon s2.local && \
kubectl drain s2.local --force --ignore-daemonsets --delete-emptydir-data && \
kubectl delete node s2.local 
```