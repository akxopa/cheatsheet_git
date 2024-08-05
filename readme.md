
# Как работать с GIT

Шпаргалка по GIT

## Локально

#### Создаем репозиторий
Зайти в терминал и создать папку проекта `mkdir my_project`

#### Инициализируем Git-репозиторий
Зайти в папку проекта и сделать ее git-репозиторием `cd my_project && git init`

#### Отслеживаем статус проекта
Статус проета __my_project__ можно отследить командой `git status`

#### Подготовка к сохраниеню
Запоминаем состояние фаила `git add todo.txt` или `git add --all`, если хотим внести все фаилы в репозитории __my_project__

#### Коммит
`git commit -m 'Какие изменения произошли'`

#### История коммитов
Вывести историю коммитов (по умолчанию в обратном порядке) `git log`

## SSH
1. В домашней деректории `cd ~` генерируем SSH-ключ
Согласно инструкции [GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) можно сделать командами `ssh-keygen -t ed25519 -C "your_email@example.com"` или `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

2. Скопировать публичный ключ `pbcopy < ~/.ssh/id_ed25519.pub` для ed25519 или `pbcopy < ~/.ssh/id_rsa.pub` для rsa 4096

3. Добавляем в настройках GitHub новый SSH ключ. Копируем публичный ключ в поле.
Проверить ключ можно командой `ssh -T git@github.com`

## Связываем локальный и удаленный репозитории
1. Перейди на страницу удалённого репозитория, выбери тип SSH и скопируйте URL

2. В локальном репозитории проекта __my_project__ выполнить команду `git remote add origin git@github.com:%ИМЯ_АККАУНТА%/my_project.git`

3. Направить изменения в удаленный репозиторий `git push -u origin main` или `git push -u origin master`. Для последующих изменений `git push`