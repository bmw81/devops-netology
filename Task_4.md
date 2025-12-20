# Домашнее задание к занятию «`Инструменты Git`». Выполнил студент `Белов Михаил`

### Цель задания
В результате выполнения задания вы:

- научитесь работать с утилитами Git;
- потренируетесь решать типовые задачи, возникающие при работе в команде.

---

## Задание

Склонируйте репозиторий с исходным кодом Terraform.
![Clone repository](/img/clone_repository.png)
В клонированном репозитории:

1. Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea.
```
git log | grep aefea
```
`commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545`

2. Ответьте на вопросы.
- Какому тегу соответствует коммит 85024d3?
```
git log --grep=85024d3
git log | grep 85024d3
```
`Такой тег отсутствует:`
![Search commit](/img/search_commit.png)

3. Сколько родителей у коммита b8d720? Напишите их хеши.
`2 родителя:`
```
git show b8d720^1
```
`commit 56cd7859e05c36c06b56d013b55a252d0bb7e158`
```
git show b8d720^2
```
`commit 9ea88f22fc6269854151c571162c5bcf958bee2b`

4. Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами v0.12.23 и v0.12.24.
```
git log v0.12.23..v0.12.24 --pretty=format:"%h - %s"
```
`33ff1c03bb - v0.12.24`

`b14b74c493 - [Website] vmc provider links`

`3f235065b9 - Update CHANGELOG.md`

`6ae64e247b - registry: Fix panic when server is unreachable`

`5c619ca1ba - website: Remove links to the getting started guide's old location`

`06275647e2 - Update CHANGELOG.md`

`d5f9411f51 - command: Fix bug when using terraform login on Windows`

`4b6d06cc5d - Update CHANGELOG.md`

`dd01a35078 - Update CHANGELOG.md`

`225466bc3e - Cleanup after v0.12.23 release`

5. Найдите коммит, в котором была создана функция func providerSource, её определение в коде выглядит так: func providerSource(...) (вместо троеточия перечислены аргументы).
```
git log -S "func providerSource("
```
![Commit with function](/img/commit_with_function.png)
6. Найдите все коммиты, в которых была изменена функция globalPluginDirs.
```
 git log --oneline --all -S 'globalPluginDirs'
```
![Function change commit list](/img/commit_list.png)
7. Кто автор функции synchronizedWriters?
```
# Ищем файлы содержащие строку с именем функции:
git grep -l "synchronizedWriters"
# Ищем коммиты, в которых упоминается эта функция:
git log -S "synchronizedWriters"
```
![Function deleted](/img/function_deleted.png)
`Судя по записям коммитов, можно сделать вывод, что данная функция была удалена как неиспользуемая. В связи с этим не удается выяснить ее автора.`

