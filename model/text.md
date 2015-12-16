# Модель отображения
## Все есть блоки
В HTML документ все есть блоки, но как эти блоки взаимодействуют и как располагаются на странице? Рассмотрим в сегодняшней лекции.

![Все есть блоки](./img/2015-10-17 14-17-01 Яндекс.png)
В HTML-документе каждому элементу на странице соответствует прямоугольная область (бокс или блок).
Движок рендеринга в браузере определяет размеры и положение боксов на странице, а также их свойства вроде цвета, фоновой картинки для того, чтобы отобразить их на экране.

В языке CSS есть специальная боксовая модель (также блоковая модель или блочная модель, англ. box model),
которая описывает, из чего состоит бокс и какие свойства влияют на его размеры. В ней у каждого бокса есть 4 области:
margin (внешние отступы), border (рамка), padding (внутренние поля, набивка), и content (контент или содержимое).

Внутренняя область элемента (content area) содержит текст и другие элементы, расположенные внутри (контент или содержимое).
У неё часто бывает фон, цвет или изображение (в таком порядке: фоновый цвет скрывается под непрозрачным изображением), и
она находится внутри content edge; её размеры называются ширина контента (content width или content-box width), и высота
контента (content height или content-box height). Иногда еще говорят «внутренняя ширина/высота элемента»

Ширина элемента расчитывается по формуле

ширина элемента = width + padding-left + padding-right + border-left + border-right

высота элемента = height + padding-top + padding-bottom + border-top + border-bottom

![Бокс](http://www.w3.org/TR/css3-box/box.png)

### Размеры содержимого (content size)
Любой блок имеет ширину и высоту **содержимого** кооторые можно задать при помощи css правил.
```css
div {
   width: 200px;
   height: 200px;
}
```
Ширину и высоту можно ограничить как снизу так и сверху, использую свойства min/max-width
```css
div {
  max-width: 100px;
  min-width: 10px
}
```
Если не задана ширина - в **некоторых** вслучаях блок заполнит все свободно пространство(в ширину), в других случаях будет зависеть от ширины содержимого(такста, других элементов).
Если не задана высота, то высота элемента = высоте содержимого

Так же на размер бокса влияют другие параметры:
### margin
Отступы (margin area) добавляют пустое пространство кокруг элемента и определяют расстояние до соседних элементов.

Величина отступов задается по отдельности в разных направлениях свойствами margin-top, margin-right, margin-bottom, margin-left или общим свойством margin.
Если значение не установлено - значение = 0([зависит от элемента](http://codepen.io/anon/pen/VvrPyx))
```css
div {
  margin-top: 10px;
  margin-right: 11px;
  margin-bottom: 12px;
  margin-left: 13px;
}
/*Сокращенная форма записи*/
p {
 /*margin: [top] [right] [bottom] [left]*/
  margin: 10px 11px 12px 13px;
}
p {
 /* 3 парметра*/
 /*margin: [top] [right & left] [bottom]*/
  margin: 10px 11px 12px;
}
p {
 /* 2 парметра*/
 /*margin: [top & bottom] [right & left]*/
  margin: 10px 11px;
}
p {
  /* 1 парметр*/
 /*margin: [top & bottom & right & left]*/
  margin: 10px;
}
```
Если указать другие единицы измерения ([Пример](http://codepen.io/anon/pen/dYZzdE)):

* em - считается относительно размера шрифта родителя
* rem - считается относительо размера шрифта корневого элемента
* vw/vh - рачитывается отсительно размеров viewport(1vw = 1% от viewport`а )
* % - считается относительно ширины радителя и margin-top/bottom не исключение

### padding
Поля элемента (padding area) — это пустая область, окружающая контент.
Она может быть залита каким-то цветом, покрыта фоновый картинкой, а её границы называются край поля (padding edge).
Если значения padding = 0, то padding edge схлапывается с content edge

Размеры полей задаются по отдельности с разных сторон свойствами padding-top, padding-right, padding-bottom, padding-left или общим свойством padding.
[Пример](http://codepen.io/anon/pen/ojoeVK)

### border
Область рамки (border area) окружает поля элемента, а ее граница называется край рамки (border edge).
Ширина рамки задается отдельным свойством  border-width или в составе свойства border.
Размеры элемента с учетом полей и рамки иногда называют внешней шириной/высотой элемента.

```css
div {
  border-width: 1px;
  /*top | right | bottom | left*/
  border-width: 1px 2px 3px 4px;
  /*thin | medium | thick*/
  border-width: thin;
}
```

Рамке можно задавать цвет([border-color](https://webref.ru/css/border-color)) и стиль([border-style](https://webref.ru/css/border-style)) при помощи свойств  ([w3c](http://www.w3.org/TR/CSS21/box.html#border-properties))

### box-sizing
Если элементу явно не задавать ширину - элемент займет всю ширину своего родителя(т.е. ширина самого элемента займет всю ширину). Ширина содержимого(content width) будет расчитываться автоматически относительно padding, border, margin. width = element width - padding-left - padding-right - margin-left - margin-right - border-left-width - border-right-width([Пример](http://codepen.io/anon/pen/BoYzvG?editors=110))

Если элементу ЯВНО задать ширину то ширина самого элемента будет расчитывать по формуле:
```
Element width = width + padding-left + padding-right + border-left + border-right
```
([Пример](http://codepen.io/anon/pen/BoYzvG?editors=110)) и элемент может вылезти за границы своего родителя.

Для того что бы задать размеры самого элемента с учетом рамок и отступов можно использовать свойства box-sizing.

Свойство box-sizing позволяет изменить этот алгоритм, чтобы свойства width и height задавали размеры не контента, а размеры блока.

Значения свойства box-sizing:

* content-box - Основывается на стандартах CSS, при этом свойства width и height задают ширину и высоту контента и не включают в себя значения отступов, полей и границ.
* padding-box(только в FF) - Свойства width и height включают в себя значения полей, но не отступов (margin) и границ (border).
* border-box - Свойства width и height включают в себя значения полей и границ, но не отступов (margin). Эта модель используется браузером Internet Exporer в режиме совместимости.

```css
/*box-sizing: content-box | border-box | padding-box*/
width: 200px;
padding: 10px;
margin: 10px;
border: 1px solid;
```
[Пример](http://codepen.io/anon/pen/meqXJE)

### Поток документа
– это воспроизведение текста, написанного на западных языках, слева направо и сверху вниз и обычная схема компоновки текста традиционных HTML-документов. Обратите внимание, что направление потока может меняться для восточных языков.

Элементы можно вкладывать друг в друга. Чем раньше в коде расположен элемент, тем выше он расположен на странице.
Любой элемент с позиционированием static (`position: static;`) находится в общем потоке документа.
[Пример элементов в потоке](http://codepen.io/anon/pen/zvPRZQ)

Как вы уже заментили в стандартном потоке документа некоторые элемента располагатся по-разному. Некотрые всегда начинаются с новой строки, некоторые остаются в той же строке.

Существует несколько основных типов элементов:
* Блочные элементы
* Строчные элементы

### Блочные элементы
**Блочные элементы** - характеризуются тем, что занимают всю доступную ширину, высота элемента  определяется его содержимым, и он всегда начинается с новой строки.
В потоке блочные элементы располагаются сверху вниз. Блочные элементы создают вокруг
себя анонимные блочные боксы, тем самым создают разрыв строки до и после себя:

![Анонимные боксы](http://www.w3.org/TR/css3-box/anonymous.png)

**Анонимный бокс** - это бокс, к которому нельзья обратиться из css.

Блочные элементы(по-умолчанию):
* p
* h1, h2, h3, h4, h5, h6
* ol, ul
* pre
* address
* blockquote
* dl
* div
* fieldset
* form
* hr
* table

Блочным элементам можно задавать высоту, ширину.
По умолчанию значение auto;
Если ширину не указывать - элемент займет ширину родительского элемента ([подробнее](https://developer.mozilla.org/ru/docs/Web/CSS/width)). [Пример](http://codepen.io/anon/pen/qOVgvN).
Если не указывать высоту - элемент будет по высоте своего содержимого.
```css
div {
  width: 200px;
  height: 200px;
}
```
Если высоту указывать в процентах - то высота будет считаться от высоты радотеля,
но только в том случае если высота родителья задана явно ([Пример](http://codepen.io/anon/pen/NGwoJL)).

Можно задавать внутренние отступы(padding):
```css
div {
  padding: 10px 11px 12px 13px;
}
```

Если для блока **задана ширина**, и добавить внетренние отступы - ширина элемента видимой части элемента(без margin) = ширина контента + отступы справа и слева. Аналогично высота элемента = высота контента + внетренние отступы по вертикали. ([Пример](http://codepen.io/anon/pen/bVaWYY)) Что бы этого избежать можно использовать свойство box-sizing(см. выше)
Если ширину не задавать, то элемент займет всю ширину и будет от этой ширины отталкиваться(т.е. ширина **содержимого** будет меняться, а не ширина самого элемента, см, выше)

Можно задавать отступы внешние(margin)
```css
div {
  margin: 10px 11px 12px 13px;
}
```
Значения можно указывать в %, em, rem, vw, vh и т. д. Если указывать значени в процентах - значение расчитывается от ШИРИНЫ родителя(неважно, по горизонтали или по-вертикали, [Пример](http://codepen.io/anon/pen/RWjvzL), сделано это для того что бы не уйти в рекурсию по высоте).

**Схлапывание** внешних отступов. Если расположить блочные элементы друг за другом и указать им вертикальные отступы - то между элементами будет отступ = max(margin-bottom(вержнего элемента), margin-top(нижнего элемента))
```CSS
.box1{
  margin: 10px 0;
}
/*Расстояние межде box1 и box2 будет 20px*/
.box2{
  margin: 20px 0;
}
/*Расстояние межде box2 и box3 будет 30px*/
.box3{
  margin: 30px 0;
}
```
Так же можно задавать отрицательные отступы. Если отступ отрицательный то расстояние расчитывает как сумма отступов, и в случае если результат отрицательный - один блок наедет на другой.
[Пример](http://codepen.io/anon/pen/rOYJpg)

![](http://htmlbook.ru/files/images/layout2/3-13.png)

Схлапывание отступов между родителем и потомком(для вертикальных отступов).
![](http://htmlbook.ru/files/images/layout2/3-17.png)
```css
h1 {
  margin: 0;
}
div {
  margin: 40px 0 25px 0;
}
p {
  margin: 20px 0 0 0;
}
```
```html
<h1>Heading content</h1>
<div>
  <p>Paragraph content</p>
</div>
```
[Пример](http://codepen.io/anon/pen/wKPyRX)

![результат](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/04/1398314904css-box-model_collapsing-margins2.png)

Возможно вы ожидали, что отступ от p до div будет 20px. Отступ просочится через родительский элемент наружу. Назвревает вопрос: "Как же тогда сдалать отступ относительно родителя?". Для этого нужно у родительского элемента указать padding или border не нулевой.


```css
h1 {
  margin: 0;
}
div {
  margin: 40px 0 25px 0;
  border-top: 1px solid #000;
}
p {
  margin: 20px 0 0 0;
}
```
```html
<h1>Heading content</h1>
<div>
  <p>Paragraph content</p>
</div>
```
[Пример](http://codepen.io/anon/pen/LpOQab)

![результат](http://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/04/1398314949css-box-model_collapsing-margins3.png)

Если не хочется чтобы были границы(`border`) обычно используют `padding: 1px` и значение `margin` уменьшают на `1px`
#### margin: auto
У margin есть значение auto, которое автоматически расчитывается браузером. Если ширина не задана - `margin: auto;` то же самое что `margin: 0;`. Если ширина указана - значени auto расчитывается автоматически.
```html
<div class=ml>margin-left: auto</div>
<div class=mr>margin-right: auto</div>
<div class=m>margin: 0 auto</div>
```
```css
div {
  width: 200px;
}
.ml {
  /*По-правому краю*/
  margin: 0 0 0 auto;
}
.mr {
  /*По-левому краю(по умолчанию)*/
  margin: 0 auto 0 0;
}
.m {
  /*По центру*/
  margin: 0 auto;
}
```
[Пример](http://codepen.io/anon/pen/BomYXP)
### Инлайн элементы

Инлайн(inline) элементы располагаются друг за другом в одной строке, при необходимости строка переносится.

Особенности строчных элементов:
1. До и после строчного элемента отсутствуют переносы строки.
2. Ширина и высота строчного элемента зависит только от его содержания, задать размеры с помощью CSS нельзя.
3. Можно задавать только горизонтальные отступы(горизонтальные отступы не [схлапываются](http://codepen.io/anon/pen/zvpwNe)).

```html
<p>Some <em>emphasized</em> text</p>
```
Элемент P - блочный элемент с нескольким инлайн-элементами внутри.  "emphasized" - инлайн элемент, но другие элементы ("Some" и "text") являются инлайн-элементами созданные блочным элементом P(это и есть анонимный инлайн бокс).
 Такие анонимные инлайн боксы наследуют некоторые свойства от родителей. Ненаслудуемые свойства устанавлиаются по умолчанию. Например цвет унаследуется от родителя, а фон останется прозрачным.

[Пример](http://codepen.io/anon/pen/BomraO)

Строчные элементы(по умолчанию):
* b, big, i, small, tt
* abbr, acronym, cite, code, dfn, em, kbd, strong, samp, var
* a, bdo, br, img, map, object, q, script, span, sub, sup
* button, input, label, select, textarea

Инлайн контекст форматирования:
* Можно увеличить размеры элемента за счет увеличения размера шрифта или размера высоты строки (свойства line-height, [Пример](http://codepen.io/anon/pen/XmVxmP), относительные размеры считаются относительноо размера шрифта элемента к которому применено свойство).
* Можно указвать внутренние отступы, правда только горизонтальные отступы будут будут влиять на окружающий контент ([Пример](http://codepen.io/anon/pen/gaoBWw)).
* Можно указывать внешние отступы, которые так же как и внутренние отступы влияют на окружающий контент только по горизонтали  ([Пример](http://codepen.io/anon/pen/KdZGqQ)).
* Можно указывать вертикально выравнивание отсительно друг друга при помощи свойства `vertical-align: top | bottom | middle | baseline` ([Пример](http://codepen.io/anon/pen/rOpqKP))

### Инлайн-блочные элемента

Особенности инлайн-блочных элементов:
* им можно задавать размеры, рамки и отступы, как и блочным элементам;
* их ширина по умолчанию зависит от содержания, а не растягивается на всю ширину контейнера;
* они не порождают принудительных переносов строк, поэтому могут располагаться на одной строке, пока помещаются в родительский контейнер;
* элементы в одной строке выравниваются вертикально подобно строчным элементам.

У всех элементов по-умолчанию установлено свойствао display, которое отвечает за тип контейнера (а иногда ещё и контейнера-потомка), который будет сгенерирован элементом.