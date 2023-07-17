# Как работает Git #

:white_check_mark: **Git** - это набор консольных утилит, которые отслеживают и фиксируют изменения в файлах.

С его помощью можно сравнивать, анализировать, редактировать, сливать изменения и возвращаться назад к последнему сохранению. Этот процесс называется контролем версий.

Все мы знаем, что у любого проекта существует много различных версий. Те, которые уже выпустили и те, которые находятся еще в разработке. 
Бывают ситуации, когда после внедрения изменений, нововведений в работающий код, что-то пошло не так и вообще всё сломалось. Как отследить на каком этапе поломка? Как вернуть всё как было и откатить до прежней версии? Как вообще можно каждому работать независимо друг от друга и от основного кода, а, когда всё готово, поделиться своими трудами с коллегами и внести их упорядоченно в новую версию проекта?

Все эти вопросы может разрешить система контроля версий, в частности Git!
Без СКВ пришлось бы долго вглядываться в код, чтобы понять как было до поломки. С Git достаточно просмотреть историю изменений (коммиты) и откатиться до нужной версии.

Также Git позволяет нескольким специалистам одновременно работать над кодом и его версиями, упорядочивает внесение изменений, их историю и отслеживание.

:white_check_mark: Git хранит проекты в **репозиториях**.

Репозиторий - это хранилище кода и истории его изменений.

Git работает локально и все репозитории хранятся в определенных папках на жестком диске. Так же репозитории можно хранить и в интернете в удалённом репозитории . Для этого существуют специальные сервисы, в частности - GitHub.

**GitHub** — это платформа, которая хранит Git-репозитории на своих серверах. Именно здесь и происходит уже непосредственное взаимодействие команды разработки, слияние новых частей кода с основным.

:white_check_mark: Каждая точка сохранения проекта носит название **коммит (commit)**. 

У каждого commit-a есть hash (уникальный id) и комментарий. Из таких commit-ов собирается **ветка**.

Ветка - это история изменений. Новый код/изменения фиксируются в ветвях. 

Большая часть работы выполняется в других ветках, а затем происходит объединение с основной веткой.

Всё это хранится в том же каталоге, что и проект, но в подпапке с именем **.git**.

:white_check_mark: Чтобы поделиться кодом со своими коллегами, вы **отправляете**
изменения в репозиторий. Чтобы получить новый код от ваших коллег,
вы **извлекаете** изменения из репозитория.
___
 ### Немного про ветки и их слияние (мерж/merge) ###
**Master** - это основная ветка проекта, в которую заливается только рабочий проверенный код. Новый функционал в конце концов оказывается в мастере. В этой ветке находится тот же самый код, что и на боевом сайте.

А теперь представьте, что вам нужно внести множество изменений в файлы вашего рабочего каталога, но эта работа экспериментальная – не факт, что всё получится хорошо. Вы бы не хотели, чтобы ваши изменения увидели другие сотрудники до тех пор, пока работа не будет закончена. Может просто ничего не коммитить до тех пор? Это плохой вариант. Мы уже знаем, что частые коммиты и пуши – залог сохранности вашей работы, а также возможность посмотреть историю изменений. К счастью, в Git есть механизм веток, который позволит нам коммитить и пушить, но не мешать другим сотрудникам.

:herb: Перед началом экспериментальных изменений вы должны создать ветку. У ветки есть имя. Пусть она будет называться my_test_work. Теперь все ваши коммиты будут идти именно туда. До этого они шли в основную ветку разработки – будем называть её master. Другими словами, раньше вы были в ветке master, а сейчас переключились на ветку my_test_work. Это выглядит так:

[![nqqdyaazdf-yivqjuvg50nlmrle.png](https://i.postimg.cc/k4hvzRsx/nqqdyaazdf-yivqjuvg50nlmrle.png)](https://postimg.cc/sQ7WZXtX)

:herb: После коммита «3» создана ветка и ваши новые коммиты «4»и «5» пошли в неё. А ваши коллеги остались в ветке master, поэтому их новые коммиты «6», «7», «8» добавляются в ветку master. История перестала быть линейной.

На что это повлияло? Сотрудники теперь не видят изменений файлов, которые вы делаете. А вы не видите их изменений в своих рабочих файлах. Хотя историю изменений в ветке master вы все-таки посмотреть можете.

Итак, теперь вы сможете никому не мешая сделать свою экспериментальную работу. Если её результаты вас не устроит, вы просто переключитесь на ветку master (на её последний коммит – на рисунке это коммит «8»). В момент переключения файлы в вашей рабочей папке станут такими же, как у ваших коллег, а ваши изменения исчезнут. Теперь ваша рабочая копия стала слепком из коммита «8». По картинке видно, что в нём нет ваших изменений, сделанных в ветке my_test_work.

:herb: Теперь мы знаем, что каждый может создать ветки и работать независимо. Можно по очереди работать то в одной ветке, то в другой – переключаясь между ними. Ветки переключает команда **checkout**.

### СЛИЯНИЕ ###

Ветки используются не только для временной независимой работы. Часто мы одновременную готовим несколько версий приложения. Например, одна версия уже почти готова к публикации и одна команда разработчиков вносят в неё последние исправления. В то же время другая команда уже занимается следующим обновлением. Им нельзя работать в предыдущей версии потому, что:

:herb: Их изменения не должны появиться в текущей версии;

:herb: Любые изменения могут что-то сломать, поэтому перед публикацией версии нужно вносить в неё как можно меньше изменений.

Словом, от веток много пользы. Но вернёмся к примеру с вашей экспериментальной работой. Ранее мы предположили, что она не удалась. Вы вернулись в ветку master и потеряли изменения, сделанные в ветке my_test_work. А если всё получилось? Вы хотите перенести свои изменения в ветку master, чтобы их увидели сотрудники, которые с ней работают. Git может помочь – выполним команду **merge** ветки my_test_work в ветку master:

[![hpqqcqure2awfvjspylfodhznkc.png](https://i.postimg.cc/PJScJqdy/hpqqcqure2awfvjspylfodhznkc.png)](https://postimg.cc/YLm8yMGL)

:herb: Здесь коммит «8» – это специальный коммит, который называется **merge-commit**. Когда мы выполняем команду **merge**, система сама создает этот коммит. В нём объединены изменения ваших коллег из коммитов «5», «6», «7», а также ваша работа из коммитов «3», «4».

:herb: Изменения из коммитов «1» и «2» объединять не нужно, ведь они были сделаны до создания ветки. А значит изначально были и в ветке master, и в ветке my_test_work.

Команда merge ничего не посылает в origin. Единственный ее результат – это merge-commit (на рисунке кружок с номером 8), который появится у вас на компьютере. Его нужно запушить, как и ваши обычные коммиты. Только после этого merge-commit отправится на origin – тогда коллеги увидят результат вашей работы, сделав pull.

*Материал о ветках и слиянии взят и скорректирован с сайта Habr.com* [ссылка на статью](https://habr.com/ru/companies/playrix/articles/348864/)


✨ Читайте в моей отдельной статье [Создали, удалили ветку в удалённом репозитории - что делать дальше?](https://github.com/Egessihora/Synchronization_of_BRANCHES_in_GIT.git)
___
В данном репозитории я буду выкладывать свои заметки о работе Git.

:arrow_up: В документах вы можете найти:
* базовые команды Git
* базовые команды Bash
* правила оформления коммитов и пример хорошего коммита

✨Надеюсь, они будут полезны не только мне ✨
