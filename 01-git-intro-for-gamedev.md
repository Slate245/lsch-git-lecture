---
css:
  - Презентации/common.css
highlightTheme: nord
---
<link rel="stylesheet"          href="https://fonts.googleapis.com/css2?family=Noto+Sans">
<style>
.nohljsln .hljs-ln-numbers  {
display: none;
}
</style>

## Как настроить git в проекте и не умереть?

_<small>ЛШ 2024</small>_

note: Привет, народ. Сегодня мы поговорим о контроле версий, настройке его в ваших проектах, чем он полезен, как его готовить и как со всем этим жить.

---
`git config --global user.name`
<br>

<split left="1" right="2">
::: block 
![[photo-cropped.png]] <!-- element style="max-height: 50%;" -->
:::

- профессиональный веб-разработчик с 2020 года
- два раза разрабатывал игру в палатке
- заставил квадратики двигаться в Unity
- не любит презентации
- [@Slate245](https://t.me/Slate245)
</split>

note: Для начала обязательный слайд обо мне. Вроде так делают умные ребята, чтобы вы знали, почему вообще меня есть смысл слушать, с какими вопросами ко мне можно идти и в какой юзернейм в телеграме кидаться тапками.

Меня зовут Ваня Беспалов, я профессиональный веб-разработчик уже 4 года, сейчас работаю в Сбермаркете разработчиком интерфейсов. Я был на ЛШ в 2018 и 2019 годах в нашей мастерской на направлении гейм-дизайна, где вел разработку двух игр, после чего еще был чем-то средним между ГД и продактом на сайд-проектах после мастерской. Мое самое большое достижение в Unity - заставить двигаться квадратик влево-вправо.

---
![[pWCYY9yODcBQ4.webp]]

note: Чтобы мы с вами разговаривали на одном языке, давайте проясним понятия

---

> [!example] Проект
> Папка с файлами исходного кода, ассетами и всем что нужно для разработки вашей игры

---

> [!example] Репозиторий
> Хранилище истории изменений в проекте

---

> [!example] Контроль версий
> Система, записывающая изменения в файлах, чтобы потом можно было вернуться к любой из прошлых версий

---

> [!example] Git
> Распределенная система контроля версий

---
> [!example] Commit (коммит)
> Фиксированное состояние проекта после изменений

---

> [!example] Merge (мерж)
> Процесс объединения разных ветвей изменений в git

---
### Что хотим?
::: block
🎯 Понять профит контроля версий<!-- element class="fragment" -->

🎯 Понять как настраивать git<!-- element class="fragment" -->

🎯 Подготовиться встречать будущее<!-- element class="fragment" -->
:::<!-- element align="left" -->

note:

Наша цель сегодня - понять в чем профит от git-а, как настроить его под конкретный проект и подготовиться к неизбежному будущему, когда над проектом вы будете работать не в одиночку.

По ходу лекции у нас будет перерыв в который можно будет выдохнуть и задать вопросы, поэтому, пожалуйста, фиксируйте их, чтобы ничего не забыть. Ладно, с преамбулой покончено, так что git init.

---

`git init`

### ...И что теперь?<!-- element class="fragment" -->

note: И что теперь?

---

::: block <!-- element class="r-stack" -->
![[rake.webp]]
![[confidence.webp]]<!-- element class="fragment" -->
:::
note: Система контроля версий - не серебряная пуля. Наличие репозитория само по себе не спасет вас от всех возможных проблем, которые может подкинуть разработка проекта. Но она может дать вам то, чего больше всего не хватает в работе над сложными и запутанными системами - уверенность.

---

![[save-game.webp]]
note: Контроль версий напоминает сохранения в играх. Вот вы одолели кучу мелких врагов и заходите в комнату, заставленную аптечками и боеприпасами. Ваш инстинкт? Я совершенно точно буду сохраняться. 

Так же и с контролем версий. Закончили любой фрагмент работы - сохранитесь... то есть закомитьтесь. Так вы создадите для себя отличную точку опоры - момент во времени, к которому всегда можно вернуться.

---

![[map.webp]]
note:Только, в отличии от бессвязного набора опорных точек, история изменений - это граф. Карта пути вашего проекта от папки с парочкой файлов до невероятно классной игры, собравшей все возможные награды индустрии... ну или огромной кучи макаронного кода, в которой вы сами не можете разобраться. Тут как пойдет. В любом случае у вас под рукой будет история разработки по которой можно перемещаться, которую можно читать и в которой можно искать ответы.

---
```bash
rm -rf /path/to/my/project/*
# Чертчертчертчертчертчерт
cd /path/to/my/project
git restore .
# Фух!
```
note: Наличие истории изменений поможет вам с легкостью экспериментировать, быстро менять фокус и даже находить баги. Если захочется - вы сможете без страха полностью удалить ваш проект. Полюбоваться первозданной чистотой пустой директории, а потом восстановить все в прежнем виде как ни в чем не бывало.

---

### Работа в команде
![[teamwork.webp]]

note: Система контроля версий незаменима при работе в команде

Мы увидели как история изменений может быть полезна для единственного разработчика. Но в реальном мире мы редко работаем над проектами в одиночку. 

Когда-нибудь писали работу совместно с кем-то еще? Работали с правками? Названия файлов типа "Работа_финал_на_проверку_точно_финал_1_(чистовое)" отзываются внутри? 

---
![[files.webp]]
note: А теперь представьте работу над проектом, состоящим из десятка-другого файлов. Это реалии работы в команде. И системы контроля версий придуманы как раз для того, чтобы усмирить такой хаос.

---
```mermaid
gitGraph
commit
branch feature
commit
checkout main
branch design-changes
commit
checkout main
commit
checkout feature
commit
checkout main
merge feature
checkout design-changes
commit
checkout main
merge design-changes
```
note: В git вы легко можете создать параллельную вселенную, где другой человек сможет вносить изменения в те же файлы, что и вы. При этом никто из вас не будет мешать другому. Такие параллельные вселенные потом можно (и нужно) соединять с основной. Это не всегда прямолинейно и просто, бинарные файлы невозможно мержить, например. Но ничто не сравнится с ощущением, когда объединяешь несколько разрозненных ветвей без конфликтов и работа нескольких людей как будто по волшебству встает на свои места 🤌

---
### Резюме
::: block

✅ Контроль версий дает уверенность<!-- elementclass="fragment" --> 

✅ Полезен и в одиночку и в команде<!-- elementclass="fragment" -->

✅ История изменений - карта вашего пути<!-- elementclass="fragment" -->

✅ Помогает навести порядок<!-- elementclass="fragment" -->
::: <!-- element align="left"  -->
note: Резюмируя

Основной профит от системы контроля версий - уверенность.

Они упрощают работу как в одиночку, так и в команде.

История изменений - карта вашего пути в текущий момент времени. Возможность всегда посмотреть на то, как было раньше (и если надо - вернуться к тому состоянию)

Система контроля версий помогает упорядочить проект. Что логично, ведь она - средство организации. Упорядочить хаос сложно. И это нормально. Не ждите, что у вас сразу получится чистая и понятная история разработки. У вас будут появляться конфликты в ветках. Возможно, вы даже грохните репозиторий с концами. Это нормально, никто не говорил, что будет легко. Но я постараюсь вам помочь и поделиться своими знаниями о расположении грабель, на которые лучше все-таки не наступать.

Раз уж git помогает нам упорядочить проект, давайте об этом и поговорим

---
### Как организовать проект?
note:Как организовывать проект?

В первую очередь нужно взять на себя ответственность за порядок в проекте. 

---
![[responsibility.webp]]
note: Знать где место для каждого файла. Ну ладно, для каждого _типа_ файла. Установить соглашения об организации проекта с другими людьми (держим в уме, что ты сам через два месяца - уже другой человек). И следить за тем, чтобы эти соглашения соблюдались.

Это довольно сложная задача, особенно, если все соглашения есть только у вас в голове. Поэтому помните о важности документации.

---
```fs[1-5|5]
super-basic-project-structure 
├── Assets 
├── Packages 
├── ProjectSettings 
└── README.md
```
<!-- element class="nohljsln" -->

note: Начните с одного файла README в корне проекта. Титульный лист, оглавление, глоссарий и инструкция по использованию в одном. Каждый раз, когда меняются требования и меняется структура или устройство проекта - обновляйте README. Думайте о том, как свежий разработчик должен войти в процесс работы над проектом, README пишется для него (а так же для вас, когда вы в конце концов забудете почему от удаления coconut.jpg игра крашится).

Не ограничивайте себя одним гигантским файлом README. Добавляйте документацию по мере необходимости. Выделите под нее отдельную папку, если проект того требует. Или, что как по мне более прикольно - документируйте каждую значимую часть вашего проекта файлом README в соответствующей папке. Очень удобно, когда документация располагается рядом с тем, что вы документируете.

---
```fs[5]
super-basic-project-structure 
├── Assets 
├── Packages 
├── ProjectSettings
├── .gitignore
└── README.md
```
<!-- element class="nohljsln" -->
note: По-умолчанию git хранит информацию обо всех файлах в вашем проекте. Это довольно неудобно, когда в ходе работы периодически возникают временные файлы, ОС добавляет свои загадочные файлы (привет, .DS_Store) и разнообразные файлы с тестовых сборок пытаются занять свое место в истории контроля версий. Для подобных случаев есть механизм игнорирования файлов - .gitignore

---
::: block

```gitignore
/[Ll]ibrary/
/[Tt]emp/
/[Oo]bj/
/[Bb]uild/
/[Bb]uilds/
/[Ll]ogs/
/[Uu]ser[Ss]ettings/

# MemoryCaptures can get excessive in size.
# They also could contain extremely sensitive data
/[Mm]emoryCaptures/

# Recordings can get excessive in size
/[Rr]ecordings/
```
<!-- element  style="width: 100%" -->
```gitignore
# Autogenerated VS/MD/Consulo solution and 
# project files
ExportedObj/
.consulo/
*.csproj
*.unityproj
*.sln
*.suo
*.tmp
*.user
*.userprefs
*.pidb
*.booproj
# и так далее
```
<!-- element class="fragment" style="width: 100%" -->

:::<!-- element  class="r-stack"-->
note: .gitignore - текстовый файл в котором каждая строчка говорит git-у какие файлы игнорировать. Для большинства типов проектов (в том числе и [для Unity](https://github.com/github/gitignore/blob/main/Unity.gitignore)) есть заранее составленные гитигноры. Они не учитывают специфику именно _вашего_ проекта, поэтому используйте их только как основу. Хорошее правило для их дополнения - если какие-то файлы не влияют на работу с вашим проектом и от их отсутствия ничего не изменится - добавьте в гитигнор.

Тут же надо упомянуть, что git не хранит информацию о пустых папках. Если вам по какой-то причине нужно сохранить в истории пустую папку - добавьте в нее файл .gitkeep. А еще лучше - README с описанием зачем нужна эта папка.

---
![[Pasted image 20240626205300.png]]
note: Место для перерыва и вопросов

---
![[fat_cartman.webp]]
note: Хорошо, мы поговорили о том, как организовывать проект, посмотрели как исключать из контроля версий определенные файлы, но как быть с файлами, которые проекту нужны, но занимают много места?

А разве с ними надо как-то по-особенному обходиться? Оказывается - да. 

---
### git-lfs
note: Дело в том, что git хранит не изменения, которые мы сделали в файлах, а каждую версию файла, которую мы закоммитили. Когда файлы весят несколько килобайт это не вызывает проблем. Но когда тебе надо сохранить 10 изменений в модели, весящей 20Мб, начинаешь искать обходные пути (или покупать абонемент в магазин жестких дисков).

Для решения этой проблемы придумали git-lfs. Хранилище больших файлов для git.

---
![[Pasted image 20240628123414.png]]
note: Принцип работы LFS, если не вдаваться в детали, такой: "А что, если те же файлы, но в другое место?"

---
![[git-lfs.gif]]
note: В LFS можно отслеживать любой файл. После этого в репозитории будет храниться только маленький файл с метаданными об объекте, в который сохранен отслеживаемый файл. Этот объект помещается во внешнее хранилище (сервер в интернете, гугл диск или S3). При внесении изменений в отслеживаемый файл будет создан и сохранен во внешнем хранилище новый объект, а метаданные в репозитории обновятся. При клонировании репозитория другим разработчиком, будет загружен только актуальный отслеживаемый файл из внешнего хранилища.

---
<split even gap="2" >
::: block
👍 упрощает работу с большими файлами <!-- element class="fragment" data-fragment-index="1" -->

👍 поддерживается всеми большими git-серверами<!-- element class="fragment" data-fragment-index="2" -->

👍 позволяет защищать файлы от синхронного редактирования<!-- element class="fragment" data-fragment-index="5" -->
:::<!-- element align="left"  -->

::: block
👎 git-сервера ограничивают объем памяти под репозиторий<!-- element class="fragment" data-fragment-index="3" -->

👎 конфликты все равно нельзя исключить полностью<!-- element class="fragment" -->
:::<!-- element align="topleft" data-fragment-index="4"   -->
</split>

note: LFS поддерживается всеми значимыми git-серверами, но облачные решения ограничивают как максимальный объем памяти под ваш репозиторий, так и под большие файлы. Учитывайте это, когда будете настраивать свои проекты.

Кроме этого, у git-а нет механизма разрешения конфликта в больших файлах. Зачастую такие файлы бинарные и простыми способами в них конфликты не разрешить. Поэтому в LFS предусмотрено блокирование файлов. При добавлении файла в отслеживание через LFS можно указать, что в будущем его можно будет заблокировать - запретить его изменять. Такие файлы становятся доступны только для чтения на локальном компьютере, чтобы вы случайно не могли изменить его. Чтобы внести изменения файл надо заблокировать. Тогда он перестанет быть readonly и только вы сможете отправить изменения в нем на сервер. Это исключает одновременную правку одного и того же файла двумя людьми.

---
### Резюме
::: block

✅ Берем ответственность за порядок и поддерживаем его<!-- elementclass="fragment" --> 

✅ Ведем полезную документацию и записываем соглашения<!-- elementclass="fragment" -->

✅ Игнорим ненужные файлы <!-- elementclass="fragment" -->

✅ Настраиваем LFS, если оно поддерживается выбранным git-сервером<!-- element class="fragment" -->
::: <!-- element align="left"  -->
note: Подведем итоги

Чтобы организовать проект нужно взять ответственность за расположение файлов в нем. Для этого нужно договориться с другими разработчиками о правилах ведения проекта, решить в каких папках что должно лежать и зафиксировать эти договоренности.

Полезная документация - лучший друг разработчика (особенно забывчивого). Ведите ее прямо в репозитории, чтобы она была рядом с кодом. Поддерживайте ее актуальность. И позволяйте ей изменяться вместе с вашим проектом.

Все, что оказывается в папке с проектом, но не необходимо для работы над ним - в .gitignore. Не пишите этот файл с нуля, используйте шаблон, адаптируя его под свой проект.

Настройте LFS для хранения больших файлов, если используете git-сервер (github, gitlab, bitbucket, gitea...).Да, это дополнительная работа, но она воздастся вам строицей. Обязательно настройте блокировку на файлах ассетов, с которыми будут работать художники. Вы не хотите разбираться с мердж-конфликтом двух бинарных ассетов, поверьте мне.

---
### Как настроить git в проекте и не умереть?
note: Отвечая на вопрос из темы лекции - как настроить git в проекте и не умереть?

---
#### Методично
note: Методично. В незнакомом окружении двигаться надо осторожно, постоянно проверяя палкой путь впереди, кидаясь болтами в поиске аномалий и в шлеме на голове, рассчитанном на удар граблей в лоб. Помните, что любая разработка - это вечный поиск. Никто не подскажет вам готовое решение под нужды именно вашего проекта. Но многие шли похожими путями. Расположение самых болючих граблей известно и даже иногда нанесено на карту.

---
### Дайте себе уверенность
![[confidence.webp]]
note: Используйте git для контроля версий вашего проекта. Дайте себе возможность экспериментировать без страха все поломать. Но экспериментируйте ответственно. Если вы не знаете как работает какая-то команда - прочитайте мануал, посмотрите видосик про нее, а не вызывайте ее неподумав.

---
### Заботьтесь о будущем
![[caring.webp]]
note: Заботьтесь о будущем. Думайте, что на любой ваш проект может прийти свежий человек. Оставьте для него удобную и понятную дорогу. С указателями и табличками "не влезай, убьет!". Потому что этим свежим человеком вполне вероятно окажетесь вы сами.

---
### Дружите с командной строкой
![[coding-cat.webp]]
note: Я нарочно не касался того, как работать с GUI-клиентами для git-а. Советую вам освоиться с интерфейсом командной строки. Потому что именно с расчетом на него git создавался и через него можно воспользоваться всеми фишками, что git может предложить.

---
### Используйте то, в чем уверены
![[tools.webp]]
note: Для работы на мастерской рекомендую вам самостоятельно определиться с местом хранения репозитория. Помните, что у облачных решений есть ограничение на объем репозитория. Если у вас есть опыт в хостинге своих сервисов - вы сможете поднять собственный git-сервер. Но не рекомендую делать это в лесу. Думаю, что для проектов на мастерской вам хватит того, что предлагают бесплатные планы gitlab или github. Но в профессиональной деятельности они могут быть плохим вариантом. Хорошенько почитайте про ограничения, прежде, чем начинать пользоваться любыми сервисами.

---
### Конец

::: block <!-- element class="r-stack" -->

::: block <!-- element class="fragment current-visible" -->

- Клиенты: [GitButler](https://gitbutler.com/), [LazyGit](https://github.com/jesseduffield/lazygit), [GH Desktop](https://github.com/apps/desktop), [Fork](https://git-fork.com/), и [др.](https://git-scm.com/downloads/guis)
- GitOps на [Github](https://docs.github.com/ru/actions), [GitLab](https://docs.gitlab.com/ee/topics/build_your_application.html), [Gitea](https://docs.gitea.com/usage/actions/overview)
- [блокирование файлов в LFS](https://github.com/git-lfs/git-lfs/wiki/File-Locking)
- соглашения [conventional commits](https://www.conventionalcommits.org/ru/v1.0.0/)
- [Trunk-based development](https://trunkbaseddevelopment.com/5-min-overview/), [Github flow](https://docs.github.com/ru/get-started/using-github/github-flow), [Gitlab Flow](https://about.gitlab.com/topics/version-control/what-is-gitlab-flow/)

:::

![[giphy (1).gif]]<!-- element class="fragment" -->

:::

note: Надеюсь, контроль версий в целом и git в частности стал для вас более понятным.

Вряд ли, конечно, ваши художники или ГД будут пользоваться командной строкой. Но зная принципы работы с git-ом, вы сможете легко помочь им разобраться хоть в Fork, хоть в SourceTree, хоть в GitHubDesktop, хоть в GitButler. 

Если вам будет интересно посмотреть, что на основе git делают в больших конторах - почитайте про CI/CD и GitOps в целом. Это настолько глубокая кроличья нора, что мы это даже обзорно посмотреть не успеем.

Если у вас возникнут вопросы, помните, что меня можно легко найти в телеграме, и я с радостью вам отвечу, если не сплю. Спасибо вам всем за внимание, если есть вопросы - задавайте, а если нет - идите делать игры!
