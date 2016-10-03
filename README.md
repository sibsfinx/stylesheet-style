## 1. Компоненты
1.1. Подключаем компоненты через [bower](http://bower.io/), не складываем исходники в проект. Указываем версии подключенных компонентов. [Подробнее](https://github.com/BrandyMint/frontend-styleguide/blob/master/components.md)

## 2. Разметка
2.1. Не добавляем классы в разметку, если они не используются стилями, 
   скриптами или тестами (перед удалением существующих можно поискать в проекте). 

2.2. Framework-first! Сначала выполняем вёрстку средствами фреймворка, 
   далее добавляем элементам кастомные классы. Чаще всего это Twitter Bootstrap.
   Исходники фреймворка *никогда* не модифицируем.

2.3. Классы, id и роли именуем через дефисы: `.some-block-element`.

2.4. Не добавляем лишних dom-элементов

## 3. Стили

3.1. В главных файлах (подключаемых в через теги link) — никаких стилей, только `import` (`require` в стилях не используем).

3.2. Для стилей используем только классы, никаких id.
   В крайнем случае допустимы селекторы.

3.3. Классы именуем осмысленно, по схеме вида "блок-элемент-модификатор" — например, 
  `.user-info-title` или `.user-info-avatar-status-bullet`.
  Таким образом защищаем делаем код менее связанным, 
  чтобы стили не пересекались, где не нужно.

   * если блок отображает набор элементов, то он должен носить их
     название во множественном числе (`posts`, `companies` и т.д.);
   * если блок отображает один элемент, то он должен носить его название
     (`post`, `company`);
   * если блок отображает элемент UI, то он должен носить его название
     (`menu`, `tag-page`, `toolbar-item`), причем это название можно дополнить
     логическим названием этого элемента UI (`top-menu`, `filters-list`, `filters-list-item`
     `company-type-select`)
   
3.4. Классы-свойства и классы-модификаторы применяются к элементам
   отдельно и определяются вместе с элементом, которые они
   модифицируют.

   ```
   # posts.html.haml
   .posts-list
     .posts-list-item
       ...
     .posts-list-item.posts-list-item-active
       ...
   
   // posts.css.sass
   .posts-list
     ...
   .posts-list-item
     ...
     &.posts-list-item-active
       ...
   ```
   
3.5. Активно используем переменные.
   Основные переменные (размеры шрифтов, цвета и размеры основных блоков)
   указываются в файлах `variables`
   Переменные, относящиеся только к одному модулю или блоку, можно определять в файле со стилем этого модуля/блока.
   Используем имеющиеся переменные перед тем, как добавить новые — `grep` и `ack` вам в помощь.

3.6. Используем %extend.
   Повторяющийся код выносим в mixin'ы и placeholder'ы.
   Предпочительнее начинать с плейсхолдеров (%some-placeholder), при необходимости использования параметров преобразуем их в миксины.
   Все миксины указываются в `mixins`

3.7. Framework-first! Внимательно изучаем ипользуемый фреймворк [Twitter Bootstrap Sass](https://github.com/twbs/bootstrap-sass),
   перед добавлением новой переменной или миксина проверяем их наличие во фреймворке.

3.8. Используем вложенность SASS, но в меру: не допускать вложенности дальше 4 уровня.
   Вложенность в SASS работает как для селекторов, так и для свойств.
   
3.9. Стремимся к минимальной вложенности селекторов в css/sass — лучше сделать отдельные css-классы для элементов, 
   чем вкладывать один селектор в другой; это повышает читаемость и стабильность.

3.10. Переменные, миксины и плейсхолдеры именуем так же, как в Twitter Bootstrap — через дефисы, например `$some-brand-color`

3.11. Комментарии ставим всегда на новую строку.

3.12. Придерживаемся [SASS Style Guide](http://css-tricks.com/sass-style-guide/)

3.12.1. Отступы только в пробелах (отступ — два пробела)

3.12.2. Пробелы — после знаков препинания, скобки пробелами не обособляем

3.12.3. Один селектор — одна строка; одно свойство — одна строка

3.12.4. Похожие свойства держим рядом

3.12.5. Порядок стилей для селектора — `@extend`, блочные свойства, текстовые и остальные свойства, потом — `@include`, последними — вложенные.

3.12.6 Медиа-запросы `@media` вкладываем в стили селектора вместо того, чтобы группировать селекторы по медиа-запросу отдельно.



## Что почитать?

http://thesassway.com/beginner/how-to-structure-a-sass-project

http://css-tricks.com/sass-style-guide/
