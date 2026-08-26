Шаг 1. Обновить Termux и установить GitОткройте Termux и выполните:

pkg update && pkg upgrade
pkg install git

Шаг 2. Настроить имя и email для Git

git config --global user.name "Ваше Имя"
git config --global user.email "you@example.com"

Шаг 3. Аутентификация с GitHub (два варианта)Вариант A — SSH (рекомендуется)

1. Сгенерировать ключ:

ssh-keygen -t ed25519 -C "you@example.com"

 2. Посмотреть публичный ключ:
cat ~/.ssh/id_ed25519.pub

3. Скопировать содержимое и добавить в GitHub → Settings → SSH and GPG keys → New SSH key.
4. Проверить подключение:
ssh -T git@github.com

Шаг 4. Клонирование репозитория или инициализация локальногоКлонировать существующий репозиторий:

git clone git@github.com:username/repo.git
# или по HTTPS
git clone https://github.com/username/repo.git

Инициализировать папку на телефоне как репозиторий:

cd /путь/к/папке
git init
git remote add origin git@github.com:username/repo.git

Шаг 5. Обычный рабочий цикл (изменения → коммит → push)

git status
git add .
git commit -m "Сообщение коммита"
git push origin main
# или 
git push origin master (в зависимости от ветки)

Для получения изменений:

git pull origin main

Полезные советы и особенности Android/TermuxПрава доступа к файлам: Termux по умолчанию работает в своём каталоге (/data/data/com.termux/files/home). Чтобы работать с файлами в общей памяти (например, Download), выполните:

termux-setup-storage

и используйте путь /storage/emulated/0/Download или ~/storage/downloads.SSH‑агент: можно запустить ssh-agent в Termux, чтобы не вводить пароль ключа каждый раз:

eval $(ssh-agent)
ssh-add ~/.ssh/id_ed25519

Ключ с паролем: при генерации ключа можно задать passphrase; тогда при добавлении в агент вводите его один раз.Редакторы: в Termux доступны vim, nano (pkg install vim nano).Автоматизация: можно написать скрипт для автоматического add/commit/push, но будьте осторожны с автоматическим пушем конфиденциальных данных.


