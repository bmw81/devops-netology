# Домашнее задание к занятию «`Системы контроля версий`». Выполнил студент `Белов Михаил`

## Задание 1. Создать и настроить репозиторий для дальнейшей работы на курсе

### Создание репозитория и первого коммита

1. Зарегистрируйте аккаунт на https://github.com/. Если предпочитаете другое хранилище для репозитория, можно использовать его.

2. Создайте публичный репозиторий, который будете использовать дальше на протяжении всего курса, желательное с названием devops-netology. Обязательно поставьте галочку Initialize this repository with a README.

[Ссылка на репозиторий](https://github.com/bmw81/devops-netology)

3. Создайте авторизационный токен для клонирования репозитория.

`Profile - Settings - Developer Settings - Personal access tokens - Tokens(classic) - Generate new token - Generate new token(classic) - Задать необходимые права`

4. Склонируйте репозиторий, используя протокол HTTPS (git clone ...).
![Repository clone](/img/repository_clone.png)

5. Перейдите в каталог с клоном репозитория (cd devops-netology).

6. Произведите первоначальную настройку Git, указав своё настоящее имя, чтобы нам было проще общаться, и email (git config --global user.name и git config --global user.email johndoe@example.com).

7. Выполните команду git status и запомните результат.
![git status - 1](/img/git_status_1.png)

8. Отредактируйте файл README.md любым удобным способом, тем самым переведя файл в состояние Modified.

9. Ещё раз выполните git status и продолжайте проверять вывод этой команды после каждого следующего шага.
![git status - 2](/img/git_status_2.png)

10. Теперь посмотрите изменения в файле README.md, выполнив команды git diff и git diff --staged.
![git diff](/img/git_diff.png)
![git diff --staged](/img/git_diff_staged.png)

11. Переведите файл в состояние staged (или, как говорят, просто добавьте файл в коммит) командой git add README.md.

12. И ещё раз выполните команды git diff и git diff --staged. Поиграйте с изменениями и этими командами, чтобы чётко понять, что и когда они отображают.
![git diff --stage - 2](/img/git_diff_stage_2.png)
![git diff - 2](/img/git_diff_2.png)

13. Теперь можно сделать коммит git commit -m 'First commit'.
![commit - 1](/img/first_commit.png)

14. И ещё раз посмотреть выводы команд git status, git diff и git diff --staged.

![Git status after commit](/img/git_status_after_commit.png)

### Создание файлов .gitignore и второго коммита

1. Создайте файл .gitignore (обратите внимание на точку в начале файла), проверьте его статус сразу после создания.
![.gitignore create](/img/gitignore_create.png)

2. Добавьте файл .gitignore в следующий коммит (git add...).
```
git add .gitignore
```
3. На одном из следующих блоков вы будете изучать Terraform, давайте сразу создадим соотвествующий каталог terraform и внутри этого каталога — файл .gitignore по примеру: https://github.com/github/gitignore/blob/master/Terraform.gitignore.
![.gitignore terraform](/img/gitignore_terraform.png)

4. В файле README.md опишите своими словами, какие файлы будут проигнорированы в будущем благодаря добавленному .gitignore.

`- Содержимое директории .terraform`

`- Файлы содержащие в названии ".tfstate"`

`- Файлы crash.log и начинающиеся на "crash" с расширением .log `

`- Файлы с расширением .tfvars и .tfvars.json`

`- Файлы override.tf, override.tf.json, а также другие файлы, заканчивающиеся на _override.tf и _override.tf.json`

`- Файлы .terraformrc и terraform.rc`

5. Закоммитьте все новые и изменённые файлы. Комментарий к коммиту должен быть Added gitignore.
![Commit - 2](/img/git_commit_2.png)