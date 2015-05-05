# Список изменений
## v0.3 (05.05.2015)
- Изменён принцип хранения шаблонов модуля. Теперь все шаблоны каждой из форм хранятся в папке, заданной через конфиг (formConfig), в переменной templateFolder. <br>Например шаблон формы обратной связи (feedback) выглядит так:
```
{THEME}/uniform/
└── feedback/ 
    ├── config.tpl - файл конфига
    ├── email.tpl - файл email-сообщения
    └── form.tpl - файл вывода формы
```
- Добавлены теги для вывода контента формы по условию, в зависимости от значения, переданного в форме. Подробное описание в файле **Default/uniform/test/form.tpl**
- Добавлены теги для вывода данных в email-сообщение по условию, в зависимости от значения, переданного в форме. Подробное описание в файле **Default/uniform/callback/email.tpl**

## v0.2 (04.05.2015)
- Изменена обработка контента шаблона email-сообщения, теперь символ переноса строки (`\n`) не заменяется на `<br>` в тексте шаблона, а только в тексте пришедших полей.
- В шаблон email-сообщения добавлены теги  квадратных скобках для вывода информации, заключенной в них только в том случаи, если поле заполнено. Например для вывода поля с имененм **name** можно прописать так:
```
[name]Имя: {name}[/name]
```
- В шаблоне email-сообщения теперь можно использовать тег `{all_mail_fields}` для вывода всех полей, которые приходят из формы. Очень удобно для последующего детального составления шаблона. Можно просто скопировать нужные теги и вставить в шаблон. <br>Пример для формы заказа звонка:
```
[phone]{phone}[/phone] : 456-789
[name]{name}[/name] : Иван
[calltime]{calltime}[/calltime] : anytime
```
- **Добавлена обработка селектов**, теперь при неудачной отправке формы значение селекта сохранится. Для этого добавлены новые теги, выводящие текст в них, если option был выбран. Составление тега происходит по следующей схеме:
[uf_select_**name селекта**_**value элемента**] <br>
Пример:
```html
<select name="calltime" class="uf-input">
    <option value="anytime" [uf_select_calltime_anytime]selected[/uf_select_calltime_anytime]>в любое время</option>
    <option value="9-12" [uf_select_calltime_9-12]selected[/uf_select_calltime_9-12]>c 9:00 до 12:00</option>
    <option value="12-15" [uf_select_calltime_12-15]selected[/uf_select_calltime_12-15]>c 12:00 до 15:00</option>
    <option value="15-18" [uf_select_calltime_15-18]selected[/uf_select_calltime_15-18]>c 15:00 до 18:00</option>
</select>
```
- **Добавлена обработка чекбоксов**, теперь при неудачной отправке формы отмеченные чекбоксы сохранятся.  Для этого добавлены новые теги, выводящие текст в них, если чекбокс был отмечен. Составление тега происходит по следующей схеме:
[uf_checkbox_**name чекбокса**_**value чекбокса**] <br>
Пример:
```html
<input type="checkbox" name="checkboxName[]" value="one" [uf_checkbox_checkboxName_one]checked[/uf_checkbox_checkboxName_one]> Чекбокс 1
<input type="checkbox" name="checkboxName[]" value="two" [uf_checkbox_checkboxName_two]checked[/uf_checkbox_checkboxName_two]> Чекбокс 2
<input type="checkbox" name="checkboxName[]" value="tree" [uf_checkbox_checkboxName_tree]checked[/uf_checkbox_checkboxName_tree]> Чекбокс 3
```
- **Добавлена обработка радиокнопок**, теперь при неудачной отправке формы отмеченные радиокнопки сохранятся. Для этого добавлены новые теги, выводящие текст в них, если радиокнопка была отмечена. Составление тега происходит по следующей схеме:
[uf_radio_**name радиокнопки**_**value радиокнопки**] <br>
Пример:
```html
<input type="radio" name="sendTo[]" value="one" [uf_radio_sendTo_one]checked[/uf_radio_sendTo_one]> Радиокнопка 1
<input type="radio" name="sendTo[]" value="two" [uf_radio_sendTo_two]checked[/uf_radio_sendTo_two]> Радиокнопка 2
<input type="radio" name="sendTo[]" value="tree" [uf_radio_sendTo_tree]checked[/uf_radio_sendTo_tree]> Радиокнопка 3
```
- Добавлены новые теги `[uf_default_value]текст[/uf_default_value]`, выводящие текст между ними, если форма только что открыта. Такие теги полезны, если требуется изначально сделать выбранным какой либо пункт селекта, или чекбокс, или добавить в поле свой текст, который не должен переписывать собой данные при неудачной отправке формы.
- Исправлена ошибка, из-за которой пи первом ткрытии формы не обрабатывались теги ошибки заполнения email: `[uf_email_error][/uf_email_error]`.
- Добавлен новый тег `{* любой текст *}` для возможности оставлять комментарии в шаблонах, которые не должны попадать на сайт. (аналог комментариев в php).

## v0.1 (25.04.2015)
- Первый релиз модуля.