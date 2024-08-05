
# Как работать с GIT

Шпаргалка по GIT

### Локальный репозиторий

1. Создаем репозиторий.<br>
Зайти в терминал и создать папку проекта `mkdir my_project`.

2. Инициализируем Git-репозиторий.<br>
Зайти в папку проекта и сделать ее git-репозиторием `cd my_project && git init`.

3. Отслеживаем статус проекта.<br>
Статус проета *my_project* можно отследить командой `git status`.

4. Подготовка к сохраниеню.<br>
Запоминаем состояние фаила `git add todo.txt` или `git add --all`, если хотим внести все фаилы в репозитории *my_project*.

5. Коммит.<br>
`git commit -m 'Какие изменения произошли'`.

6. История коммитов
Вывести историю коммитов (по умолчанию в обратном порядке) `git log`.

### SSH
1. В домашней деректории `cd ~` генерируем SSH-ключ. <br>Согласно инструкции [GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) можно сделать командами `ssh-keygen -t ed25519 -C "your_email@example.com"` или `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

2. Скопировать публичный ключ `pbcopy < ~/.ssh/id_ed25519.pub` для ed25519 или `pbcopy < ~/.ssh/id_rsa.pub` для rsa 4096

3. Добавляем в настройках GitHub новый SSH ключ. Копируем публичный ключ в поле.
Проверить ключ можно командой `ssh -T git@github.com`

### Связываем локальный и удаленный репозитории
1. Перейди на страницу удалённого репозитория, выбери тип SSH и скопируйте URL

2. В локальном репозитории проекта *my_project* выполнить команду `git remote add origin git@github.com:%ИМЯ_АККАУНТА%/my_project.git`

3. Направить изменения в удаленный репозиторий `git push -u origin main` или `git push -u origin master`. Для последующих изменений `git push`