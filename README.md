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
