
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
`git commit -m 'Какие изменения произошли'`.<br>
Хеш — основной идентификатор коммита. Git хеширует информацию о коммите с помощью алгоритма SHA-1 и получает для каждого коммита свой уникальный хеш — результат хеширования. Вместо хеша последнего коммита можно написать слово `HEAD`.

6. История коммитов
Вывести историю коммитов (по умолчанию в обратном порядке) `git log`. Сокращенный хеш `git log --oneline` или `git log --graph --oneline`.

### SSH
1. В домашней деректории `cd ~` генерируем SSH-ключ. <br>Согласно инструкции [GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) можно сделать командами `ssh-keygen -t ed25519 -C "your_email@example.com"` или `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

2. Скопировать публичный ключ `pbcopy < ~/.ssh/id_ed25519.pub` для ed25519 или `pbcopy < ~/.ssh/id_rsa.pub` для rsa 4096

3. Добавляем в настройках GitHub новый SSH ключ. Копируем публичный ключ в поле.
Проверить ключ можно командой `ssh -T git@github.com`

### Связываем локальный и удаленный репозитории
1. Перейди на страницу удалённого репозитория, выбери тип SSH и скопируйте URL

2. В локальном репозитории проекта *my_project* выполнить команду `git remote add origin git@github.com:%ИМЯ_АККАУНТА%/my_project.git`

3. Направить изменения в удаленный репозиторий `git push -u origin main` или `git push -u origin master`. Для последующих изменений `git push`

### Статус фаила

- untracked
- tracked
- staged
- modified

```mermaid
%% описание схемы
graph LR;
    untrecked -- "git add" --> staged/tracked;
    staged/tracked -- "git commit" --> tracked;
    tracked -- "diff changes in file" --> modified;
    modified -- "git add" --> staged/tracked;
%%    staged/tracked -- "diff changes in file" --> modified;
```

Схема создается с помощью [Mermaid](http://mermaid.js.org). Для быстрого погружения как нарисовать свою первую диаграму можно прочитать на [Хабре](https://habr.com/ru/articles/652867/).

```mermaid
stateDiagram-v2
    State1: untrecked
    State2: staged/tracked
    State3: tracked
    State4: modified
    State1 --> State2: git add
    State2 --> State3: git commit
    State3 --> State4: diff changes in file
    State4 --> State2: git add
    State2 --> State4: git add

```

### Сообщение к коммитам
Придерживайся одного сообщения стиля в проекте.

#### Conventional Commits

Общий вид: `<type>: <сообщение>` <br>
где *type* может принимать значениея `feat` или `fix`

Подробнее можно узнать в [спецификации](https://www.conventionalcommits.org/ru/v1.0.0-beta.4/#спецификация)

#### Корпоративный

Общий вид: `<Jira-ID>: <сообщение>` <br>
где *Jira-ID* идентификатор задачи проекта

#### GitHub-стиль

Общий вид: `#<номер задачи> <сообщение>`.

### Как внести измененния в коммит

1. В последний коммит внести изменения можно так:<br>
`git add`<br>
`git commit --amend --no-edit`<br>
Eсли нужно отредактировать сообщение к коммиту то поможет `git commit --ameng -m "add new massage"`.

2. Если нужно убрать из staging area<br>
`git restore --staged <file>`.

3. Откат коммита:<br>
`git reset --hard <commit hash>`

4. Откатить изменения до последней сохраненной версии: <br>
`git restore <file>`

### Как посмотреть изменения

Посмотреть изменения в modified:<br>
`git diff`

В staged:<br>
`git diff --staged`

Посмотреть изменения между коммитами с хеш *hash1* и *hash2*:<br>
`git diff <hash1> <hash2>`

Посмотреть изменения между текущим и предыдущим коммитом:<br>
`git diff HEAD~ HEAD` 

### Игнорируемые фаилы

Git игнорирует фаилы, которые следуют правилам в *.gitignore*. 
Посмотреть что игнорируется можно с помощью `git status --ignored`.

*.gitignore* следует закоммитить.

### Клонирование и копирование репозитория

Команда `git clone <адрес репозитория для копирования>` копирует проект на локальный репозиторий, и автоматически связывает локальный и удалённый репозиторий.

Fork позволяет получить копию репозитория в GitHub аккаунт.

### Ветки

`git branch <название_ветки>` создать ветку

`git branch` проверить в какой ветке в локальном репозитории

`git branch -a` посмотреть локальные и удаленные ветки

`git checkout <название_ветки>` переместитья в ветку

`git checkout -b <название_ветки>` создать ветку и переместиться в нее

#### Слияние веток

Для кооректного слияние ветки к основной, нужно вначале перейти в основную ветку. Затем выполнить команду `git merge <название_ветки>`.

`git branch -D <название_ветки>` команда, которая удалит ветку. Для "мягкого удаления" используй ключ *-d*.

#### Конфликт

При возникновении конфликта во время слияния, можно заглянуть в решения в [документации Git](https://git-scm.com/book/ru/v2/Инструменты-Git-Продвинутое-слияние).

#### Забираем изменения из удаленного репозитория

С помощью команды `git pull` можно подтянуть измененния текущей ветки.

Например:

```bash
$ git checkout main # перешли в main
$ git pull # подтянули новые изменения в main
$ git checkout my-branch # вернулись в рабочую ветку my-branch
$ git merge main # влили main в новую ветку my-branch
$ git push -u origin my-branch # отправили ветку my-branch в удалённый репозиторий

```
Удалить привязанный origin `git remote rm origin`.

### Режимы слияния

Состояне fast-forward: при слиянии не возможен конфликт, истории двух веток не расходятся и одна ветка является продолжением другой.

Fast-forward слияние веток можно отключить флагом `--no-ff`. 

Например:

```bash
# находимся в ветке main
# --no-edit отключает ввод сообщения для merge-коммита
# --no-ff отключает fast-forward слияние веток
$ git merge --no-edit --no-ff add-docs
Merge made by the 'ort' strategy.
 docs.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 docs.txt

# с флагом --graph
# Git нарисует ветки с помощью «палочек» и «звёздочек»
# получившийся коммит слияния: 6814789
$ git log --graph --oneline
*   6814789 (HEAD -> main) Merge branch 'add-docs'
|\
| * e08fa2a (add-docs) New docs 2
| * fd588b2 New docs 1
|/
* 997d9ce Commit 4
* 0313e8e Commit 3
* 5848aba Commit 2
* 04923d7 Commit 1 

```

При слиянии не-fast-forward создается коммит слияния

```bash
# находимся в ветке main
# --no-edit избавляет от необходимости
# вводить сообщение для merge-коммита
$ git merge --no-edit add-docs
Merge made by the 'ort' strategy.
 docs.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 docs.txt

# коммит слияния: 34f5f8f
$ git log --graph --oneline
*   34f5f8f (HEAD -> main) Merge branch 'add-docs'
|\
| * 8de42eb (add-docs) New docs 2
| * 4d3c346 New docs 1
* | 15d3f04 Commit 5
|/
* 73def1e Commit 4
* 9c30ab3 Commit 3
* 83cc5ec Commit 2
* 8e87fb2 Commit 1 

```

При *git push* и *не-fast-forward*. Рзешение конфликта с помощью: 
1. rebase
2. git push --force