# Домашнее задание к занятию «`Ветвления в Git`». Выполнил студент `Белов Михаил`

### Цель задания
В процессе работы над заданием вы потренеруетесь делать merge и rebase. В результате вы поймете разницу между ними и научитесь решать конфликты.

Обычно при нормальном ходе разработки выполнять rebase достаточно просто. Это позволяет объединить множество промежуточных коммитов при решении задачи, чтобы не засорять историю. Поэтому многие команды и разработчики предпочитают такой способ.

---
## Задание «Ветвление, merge и rebase»

**Шаг 1.** Предположим, что есть задача — написать скрипт, выводящий на экран параметры его запуска. Давайте посмотрим, как будет отличаться работа над этим скриптом с использованием ветвления, merge и rebase.

Создайте в своём репозитории каталог branching и в нём два файла — merge.sh и rebase.sh — с содержимым:

```
#!/bin/bash
# display command line options

count=1
for param in "$*"; do
    echo "\$* Parameter #$count = $param"
    count=$(( $count + 1 ))
done
```
Этот скрипт отображает на экране все параметры одной строкой, а не разделяет их.
![Create scripts](/img/create_scripts.png)

**Шаг 2.** Создадим коммит с описанием Prepare commit to main и отправим его в ветку main.
![Commit scripts to main](/img/commit_scripts.png)

**Подготовка файла merge.sh**

**Шаг 1.** Создайте ветку git-merge.
![New branch create](/img/new_branch_create.png)

**Шаг 2.** Замените в ней содержимое файла merge.sh на:
```
#!/bin/bash
# display command line options

count=1
for param in "$@"; do
    echo "\$@ Parameter #$count = $param"
    count=$(( $count + 1 ))
done
```
![Change merge-script](/img/change_marge_script.png)

**Шаг 3.** Создайте коммит `merge: @ instead *`, отправьте изменения в репозиторий.
![Push new branch](/img/push_new_branch.png)

**Шаг 4.** Разработчик подумал и решил внести ещё одно изменение в merge.sh:
```
#!/bin/bash
# display command line options

count=1
while [[ -n "$1" ]]; do
    echo "Parameter #$count = $1"
    count=$(( $count + 1 ))
    shift
done
```
Теперь скрипт будет отображать каждый переданный ему параметр отдельно.

**Шаг 5.** Создайте коммит merge: use shift и отправьте изменения в репозиторий.
![Change merge-script-2](/img/change_merge_script-2.png)

**Изменим main**

**Шаг 1.** Вернитесь в ветку main. 
![Back to main](/img/back_to_main.png)
**Шаг 2.** Предположим, что пока мы работали над веткой git-merge, кто-то изменил main. Для этого изменим содержимое файла rebase.sh на:
```
#!/bin/bash
# display command line options

count=1
for param in "$@"; do
    echo "\$@ Parameter #$count = $param"
    count=$(( $count + 1 ))
done

echo "====="
```
В этом случае скрипт тоже будет отображать каждый параметр в новой строке.

**Шаг 3.** Отправляем изменённую ветку main в репозиторий.
![Push to main](/img/push_to_main.png)

**Подготовка файла rebase.sh**

**Шаг 1.** Предположим, что теперь другой участник нашей команды не сделал git pull либо просто хотел ответвиться не от последнего коммита в main, а от коммита, когда мы только создали два файла merge.sh и rebase.sh на первом шаге.

Для этого при помощи команды git log найдём хеш коммита Prepare commit to main и выполним git checkout на него так: 
`git checkout a454dd0441d67f903dbc31dfc71f15dc36477894`. 

**Шаг 2.** Создадим ветку git-rebase, основываясь на текущем коммите. 
![Create branch git-rebase](/img/branch_git-rebase_create.png)
**Шаг 3.** И изменим содержимое файла rebase.sh на следующее, тоже починив скрипт, но немного в другом стиле:
```
#!/bin/bash
# display command line options

count=1
for param in "$@"; do
    echo "Parameter: $param"
    count=$(( $count + 1 ))
done

echo "====="
```
**Шаг 4.** Отправим эти изменения в ветку git-rebase с комментарием git-rebase 1.

**Шаг 5.** И сделаем ещё один коммит git-rebase 2 с пушем, заменив echo "Parameter: $param" на echo "Next parameter: $param".
![Push branch git-rebase](/img/push_git-rebase_branch.png)

**Промежуточный итог**

Мы сэмулировали типичную ситуации в разработке кода, когда команда разработчиков работала над одним и тем же участком кода, и кто-то из разработчиков предпочитает делать merge, а кто-то — rebase. Конфликты с merge обычно решаются просто, а с rebase бывают сложности, поэтому давайте смержим все наработки в main и разрешим конфликты.

Если всё было сделано правильно, то на странице network в GitHub, находящейся по адресу https://github.com/ВАШ_ЛОГИН/ВАШ_РЕПОЗИТОРИЙ/network, будет примерно такая схема:

![Network](/img/network.png)

`Моя схема с веткой fix из прошлого задания:`
![My scheme](/img/my_scheme.png)

**Merge**

Сливаем ветку git-merge в main и отправляем изменения в репозиторий, должно получиться без конфликтов:
![Merge](/img/merge.png)

В результате получаем такую схему:

![Network-2](/img/network-2.png)

**Rebase**

**Шаг 1.** Перед мержем ветки git-rebase выполним её rebase на main. Да, мы специально создали ситуацию с конфликтами, чтобы потренироваться их решать. 

**Шаг 2.** Переключаемся на ветку git-rebase и выполняем git rebase -i main. В открывшемся диалоге должно быть два выполненных коммита, давайте заодно объединим их в один, указав слева от нижнего fixup. В результате получаем:
![Git rebase](/img/git_rebase.png)

Если посмотреть содержимое файла rebase.sh, то увидим метки, оставленные Git для решения конфликта:
![Rebase conflict](/img/rebase_conflict.png)

**Шаг 3.** Удалим метки, отдав предпочтение варианту

**Шаг 4.** Сообщим Git, что конфликт решён git add rebase.sh и продолжим rebase git rebase --continue.

**Шаг 5.** Опять получим конфликт в файле rebase.sh при попытке применения нашего второго коммита. Давайте разрешим конфликт, оставив строчку echo "Next parameter: $param".

**Шаг 6.** Далее опять сообщаем Git о том, что конфликт разрешён — git add rebase.sh — и продолжим rebase — git rebase --continue.

В результате будет открыт текстовый редактор, предлагающий написать комментgit rebase --abortарий к новому объединённому коммиту:

```
# This is a combination of 2 commits.
# This is the 1st commit message:

Merge branch 'git-merge'

# The commit message #2 will be skipped:

# git 2.3 rebase @ instead * (2)
```
Все строчки, начинающиеся на #, будут проигнорированны.

После сохранения изменения Git сообщит:
git 
