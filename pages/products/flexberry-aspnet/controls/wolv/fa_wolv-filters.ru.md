---
title: Фильтры WebObjectListView
sidebar: flexberry-aspnet_sidebar
keywords: Flexberry ASP-NET
toc: true
permalink: ru/fa_wolv-filters.html
lang: ru
---

Если включить настройку [WOLV](fa_web-object-list-view.html) `Filter=true`, то на тулбаре появится кнопка с фильтрами. При нажатии на кнопку появится первая строка, в которой можно накладывать фильтры. Первый контрол в ячейке фильтров - операция, второй - значение. Особым образом обрабатываются свойства типа `bool` и наследники `Enum`: для логических полей генерируется `DropDownList` с тремя значениями - `Пусто`, `Да`, `Нет`, для `Enum` - `DropDownList` с диапазоном значений перечисления (caption'ы).

Для того чтобы использовать свой контрол в фильтрах, нужно:

* чтобы контрол реализовывал интерфейс `IFilterControl`
* добавить в WebControlProvider.xml к соотвествующему типу строчку:

    ```xml
    ...
    <propertytype name="ИмяТипа">
      <control .../>
      <editcontrol ...>
      <filtercontrol typename="ИмяТипаКонтрола" codefile="ФайлКодаКонтрола" />
    </propertytype>
    ...
    ```
    
* Если нужна возможность ручного определения функции ограничения для специфического контрола фильтрации, то нужно реализовать интерфейс `ICSSoft.STORMNET.Web.Tools.IComparableFilterControl`.

То есть контрол для фильтра можно задать аналогично контролу для редактирования или просмотра, только не указывается имя свойства данных, потому что
используется интерфейс.

![](/images/pages/products/flexberry-aspnet/controls/wolv/wolv-filters.png)

При нажатии на ячейку правой кнопкой мыши появляется контекстное меню, в котором можно наложить фильтр на колонку.

![](/images/pages/products/flexberry-aspnet/controls/wolv/wolv-context-filters.png)

## Контролы для фильтрации

В качестве контролов для фильтров на данный момент могут использоваться:

* [AlphaNumericTextBox](fa_alpha-numeric-textbox.html)
* [DatePicker](fa_date-picker.html)
* [MasterEditorLinkedAjaxLookUp](fa_master-editor-linked-ajax-lookup.html)

По умолчанию для свойств различных типов будут использоваться следующие контролы для фильтрации (используемые контролы для различных типов могут переопределяться в файле `WebControlProvider.xml`):

* Для свойств с типами `int`, `Nullable<int>` и `NullableInt` используется [AlphaNumericTextBox](fa_alpha-numeric-textbox.html)
* Для свойств с типами `DateTime`, `Nullable<DateTime>` и `NullableDateTime` используется [DatePicker](fa_date-picker.html)
* Для свойств с типами `bool` и `Enum` используется `DropDownList`
* Для свойств с остальными типами используется `TextBox`

## Правила фильтрации

Правила фильтрации элементов на списковых формах:

* при вводе некорректных значений (в том числе числовых) все операции фильрации будут возвращать пустой список элементов и будет выводиться соответствующее сообщение для пользователя
* пустое значение (за исключением полей с типами, допускающими значение `null`) будет обрабатываться так же как некорректное (если выбрана операция фильтрации)
* для строковых полей или полей, допускающих значение `null`, пустое значение рассматривается как null, при этом операции `больше равно` и `меньше равно` не будут ограничивать список 
* исключения в случае ввода некорректных значений в общем случае выбрасываться не будут

{% include note.html content="Исключения пока будут выбрасываться только в случае когда контрол, используемый для фильтрации в WOLV, выбрасывает исключение при установке некорректного значения в свойство Text (из-за механизма работы ASP.NET)." %}

### Особенности работы с фильтрами

Особенности работы с символом `*`:

* если фильтр накладывается на поле строкового типа, то `*` определяет любое количество символов, то есть:

    * `*123` будет искать все строки, оканчивающиеся на `123`.
    * `123*` будет искать все строки, начинающиеся на `123`.
    * `*123*` будет искать все строки, содержащие подстроку `123`.
    
* если фильтр накладывается на поле нестрокового типа, то `*` не интерпретируется каким-нибудь особым образом (например, если по числовому столбцу искать `*123*`, то ничего не будет найдено, поскольку ни одно число не представлено подобной последовательностью символов).

### Передача параметров фильтров через GET-запрос

Параметры фильтрации можно передавать через GET-запрос, то есть можно указать необходимый параметр в адресной строке и таким образом наложить ограничение на список. В дальнейшем можно настроить быстрый доступ к полученному списку через ссылку или контрол. Строка GET-запроса выглядит следующим образом: 

`?WOLF_WebObjectListView1=<НомерКолонки>:<Фильтр>`.

Нумерация колонок идет слева направо и начинается с `0` (не учитывая колонку с кнопками).

{% include warning.html content="Учитываются все колонки списка, а не только отображенные на странице." %}

Допустимо применение разделителя `|` между параметрами, в таком случае параметры объединяются по принципу `И`.

В результате указанные значения фильтра будут проставлены в соответствующие колонки.

Например, есть список квартир:

![](/images/pages/products/flexberry-aspnet/controls/wolv/apartments1.png)

Необходимо получить ограниченный список: "Квартиры №1 стандартной отделки". На странице отображены не все колонки. Колонка "Номер" нулевая по счету на списке по умолчанию, колонка `Вид отделки` - десятая. GET-запрос будет выглядеть как `?WOLF_WebObjectListView1=0:1|10:Стандартная`.

В результате список примет следующий вид: 

![](/images/pages/products/flexberry-aspnet/controls/wolv/apartments2.png)
