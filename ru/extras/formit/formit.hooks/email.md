---
title: "email"
description: "Хук email для Formit"
translation: "extras/formit/formit.hooks/email"
---

## FormIt email хук

Email хук отправит содержимое вашей HTML формы на любой адрес электронной почты.

## Поддерживаемые параметры

| Имя                     | Описание                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| emailTpl                | Обязательный. Чанк tpl для сообщения электронной почты. Если он не указан, будет отправлен список полей с их значениями.                                                                                                                                                                                                                                                                                                                                                                          |
| emailSubject            | Тема письма.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| emailUseFieldForSubject | Если указано "1" и передано поле "тема", то значение этого поля будет использоваться в качестве строки темы электронного письма.                                                                                                                                                                                                                                                                                                                                                                  |
| emailTo                 | Список адресов получателей электронной почты, разделенных запятыми.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| emailToName             | Необязательный. Список имен, разделенных запятыми, для попарного сопряжения со значениями `emailTo`.                                                                                                                                                                                                                                                                                                                                                                                              |
| emailFrom               | Необязательный. Если установлено, будет указан адрес отправителя "From:" для электронного письма. Если не установлен, сначала будет осуществлен поиск поля формы "email". Если ничего не найдено, по умолчанию будет установлена системная настройка `emailsender`. **ПРИМЕЧАНИЕ**. Всегда устанавливайте для системной настройки `emailFrom` действительный адрес электронной почты (который разрешен для отправки с вашего сервера), чтобы избежать отклонения писем из-за нарушений SPF/DMARC. |
| emailFromName           | Необязательный. Если установлено, будет указано имя отправителя "From:" для электронного письма.                                                                                                                                                                                                                                                                                                                                                                                                  |
| emailHtml               | Необязательный. Должно ли электронное письмо быть в формате HTML. По умолчанию 1.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| emailConvertNewlines    | Необязательный. Если установлено значение 1, все символы новой строки будут преобразованы в теги `<br>`.                                                                                                                                                                                                                                                                                                                                                                                          |
| emailReplyTo            | Электронное письмо, на которое нужно ответить. Если не установлен, сначала будет искать поле формы "email". Если ничего не найдено, по умолчанию будет установлено значение, установленное в `emailFrom`. **ПРИМЕЧАНИЕ**. Установите для `emailReplyTo` действительный адрес электронной почты из того же домена, что и `emailFrom`, чтобы избежать отклонения электронной почты из-за нарушений SPF/DMARC.                                                                                       |
| emailReplyToName        | Необязательный. Имя поля для ответа через "Reply-To:"                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| emailCC                 | Список писем, разделенных запятыми, для отправки через "CC:".                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| emailCCName             | Необязательный. Список имен, разделенных запятыми, для попарного сопряжения со значениями `emailCC`.                                                                                                                                                                                                                                                                                                                                                                                              |
| emailBCC                | Список email адресов, разделенных запятыми, для отправки через скрытую копию ("BCC").                                                                                                                                                                                                                                                                                                                                                                                                             |
| emailBCCName            | Необязательный. Список имен, разделенных запятыми, для сопряжения со значениями `emailBCC`.                                                                                                                                                                                                                                                                                                                                                                                                       |
| emailMultiWrapper       | Оборочивает значения, переданные через чекбоксы/списки множественного выбора этим значением. По умолчанию используется только значение. (1.6.0+)                                                                                                                                                                                                                                                                                                                                                  |
| emailMultiSeparator     | Разделяет чекбоксы/списки множественного выбора этим значением. По умолчанию используется новая строка. (1.6.0+)                                                                                                                                                                                                                                                                                                                                                                                  |
| emailSelectField        | Имя поля формы, которое выбирает адреса электронной почты для отправки. (4.2.5+)                                                                                                                                                                                                                                                                                                                                                                                                                  |
| emailSelectTo           | Разделенный точкой с запятой список адресов электронной почты, разделенных запятыми, для отправки туда писем. (4.2.5+)                                                                                                                                                                                                                                                                                                                                                                            |
| emailSelectToName       | Список разделенных точкой с запятой имен электронной почты для отправки туда писем. (4.2.5+)                                                                                                                                                                                                                                                                                                                                                                                                      |

Любое из свойств email хука может содержать плейсхолдеры имен полей из вашей формы, которые будут обрабатываться.

## Использование

Просто укажите его как хук в вызове FormIt, а затем укажите свойства электронной почты в вызове FormIt.

```php
[[!FormIt?
    ...
    &hooks=`email`
    &emailTpl=`CentralizedDebtObligationEmailTpl`
    &emailSubject=`Кто-то еще купил пакет CDO`
    &emailTo=`sales@mortgagemoney.com`
    &emailCC=`boss@mortgagemoney.com`
    &emailBCC=`fbi@gov.com`
    &emailBCCName=`CDO информатор о мошенничестве`
]]
```

Обратите внимание, что свойство `&emailTpl` указывает на имя чанка. В этом блоке у вас будут плейсхолдеры для каждого поля в вашей форме. Наш чанк может выглядеть так:

```html
<p>Привет,</p>
<p>[[+name]] только что приобрел CDO пакет: [[+cdo_package]].</p>
<p>Его адрес: [[+email]]</p>
<p>Спасибо!</p>
```

Это конечно предполагает, что у вас есть поля "name", "cdo_package" и "email" в вашей форме.

### Добавление динамики в адресацию

FormIt, начиная с версии 4.2.5+, мог выбирать получателя почты по числовому значению поля, то есть по значению параметра 'select'. Таким образом можно избежать создания поддельного поля формы, в котором пользователь может легко отправить любой почтовый адрес. Пользователь будет видеть только нумерованный список получателей, которые будут перенаправлены на адреса электронной почты с помощью свойств FormIt.

Для этого вы можете использовать следующие свойства FormIt:

```php
&emailSelectTo=`mail1@my.domain,mail2@my.domain;different@my.domain`
&emailSelectToName=`Mail1,Mail2;Different`
&emailSelectField=`emailselect`
```

и следующее поле формы

```php
<select name="emailselect">
    <option value="1" [[!+fi.emailselect:default=`1`:FormItIsSelected=`1`]]>Адрес 1</option>
    <option value="2" [[!+fi.emailselect:default=`1`:FormItIsSelected=`2`]]>Адрес 2</option>
</select>
```

Если выбран Адрес 1, почта будет отправляться на `mail1@my.domain,mail2@my.domain`, если же выбран Адрес 2, почта будет отправлена на`different@my.domain`.

### Использование поля Темы в качестве строки Темы электронного письма

Предположим, у вас есть поле темы в вашей форме. Вы хотите, чтобы это было темой отправляемого электронного письма. Хук электронной почты может делать следующее:

```php
[[!FormIt?
    ...
    &emailUseFieldForSubject=`1`
]]
```

Будет выполнен поиск поля с именем "тема", которое будет использоваться в электронном письме. Если он не будет найден или окажется пуст, по умолчанию будет использовано значение `&emailSubject`.

### Работа с чекбоксами и множественным выбором в электронном письме

FormIt, начиная с версии 1.6.0+, автоматически обрабатывает чекбоксы и объединяет их в одно поле. Вы можете использовать свойства `&emailMultiSeparator` и `&emailMultiWrapper`, чтобы указать, как они соединяются. Например, чтобы обернуть флажки в теги `<li>`:

```php
[[!FormIt?
    ...
    &emailMultiWrapper=`<li>[[+value]]</li>`
]]
```

Или просто разделить при помощи BR тегов:

```php
[[!FormIt?
    ...
    &emailMultiSeparator=`<br />`
]]
```

## Смотрите также

1. [FormIt хук email](extras/formit/formit.hooks/email)
2. [FormIt хук FormItAutoResponder](extras/formit/formit.hooks/formitautoresponder)
3. [FormIt хук FormItSaveForm](extras/formit/formit.hooks/formitsaveform)
4. [FormIt хук math](extras/formit/formit.hooks/math)
5. [FormIt хук recaptcha](extras/formit/formit.hooks/recaptcha)
6. [FormIt хук redirect](extras/formit/formit.hooks/redirect)
7. [FormIt хук spam](extras/formit/formit.hooks/spam)
8. [FormIt прехук FormItLoadSavedForm](extras/formit/formit.hooks/prehooks.formitloadsavedform)