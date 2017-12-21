# Модель учета переработки медицинских отходов с использованием технологии Blockchain и мультиподписи
*Автор: Кашинцев Марк*

## Основные субъекты модели

* **Пара ключей** *(Kpub, K)* - два числа, между которыми существует функциональная зависимость *Kpub = H(K)*, где *H(x)* - криптографическая хеш-функция.
* **Cеть** - некоторое количество компьютеров, подключенных друг к другу, способных осуществлять проверку электронной подписи и уведомлять друг друга о результате проверки. Участники сети так же занимаются построением распределенной базы данных типа Blockchain или любой другой базы данных, использующей в своей основе направленные ациклические графы, построенные с использованием криптографических хэш функций.
* **Токен** (*T*) - внутренняя валюта, используемая для расчетов между Клиентом и Подрядчиком.
* **Цифровая подпись** - криптографическая функция вида *SIG(data, K)*, где *data* - некоторые данные, *K* - приватный ключ

  Результатом функции является число, которое позволяет любому участнику сети зная *Kpub = H(K)* проверить, что это число было посчитано тем, кто имеет доступ к *K*.

## Участники модели

* **Клиент** - лицо или организация, заинтересованная в утилизации медицинских отходов. Характеризуется парой ключей *(Cpub, C)*.
* **Подрядчик** - личность или организация, предоставляющие услуги по утилизации медицинских отходов. Характеризуется парой ключей *(Rpub, R)*.
* **Доверенное лицо** - лицо или организация, уполномоченное Клиентом производить проверку выполнения заказа на переработку. Характеризуется парой ключей *(Opub, O)*, которые генерируются с использованием приватного ключа клиента *C* так, что любой компьютер в сети может проверить, что данное Доверенное лицо было назначено именно владельцем ключа *C*. Также возможен вариант, при котором *O* генерируется с использованием *C* и *R*, что дает возможность подтвердить договоренность Клиента и Подрядчика в выборе Доверенного лица.
* **Эмитент** - лицо или организация, имеющее право на выпуск некоторого числа токенов *T*, характеризуется парой ключей *(Epub, E)*.

Все участники модели также являются участниками Сети.

## Основной сценарий

### Шаг 1. Выпуск валюты

Имея в распоряжении приватный ключ *E*, эмитент производит эмиссию *N* токенов и автоматически становится их владельцем, уведомляя об этом сеть.

### Шаг 2. Передача валюты

Используя свой приватный ключ *E*, Эмитент может передать свои средства любому другому участнику сети, зная его публичный ключ. Предположим, что эмитент передает все свои средства Подрядчику с помощью публичного ключа *Cpub*, уведомляя об этом сеть.

Имея подвержденное сетью право распоряжаться *N* токенами, Подрядчик передает Клиенту, зная его публичный ключ *Cpub*, 1 токен, уведомляя об этом сеть.

### Шаг 3. Создание контракта на переработку.

Имея подтвержденное сетью право распоряжаться 1 токеном, Клиент создает *цифровой контракт* для заказа *RO* следующего вида:

<table>
  <tbody>
    <tr>
    <td><b>Заказ</b></td>
    <td colspan="3"><i>RO</i></td>
    </tr>
    <tr>
    <td><b>Дата</b></td>
      <td colspan="3">23.08.18 12:34:56.123</td>
    </tr>
    <tr>
    <td><b>Перечень работ</b></td>
      <td colspan="3">Утилизация единицы медицинских отходов № 123123</td>
    </tr>
    <tr>
    <td><b>Вознаграждение</b></td>
    <td colspan="3">1.00000000 <i>T</i></td>
    </tr>
    <tr>
    <td><b>Клиент</b></td>
    <td><i>Cpub</i></td>
    <td><b>Подпись Клиента</b></td>
    <td><i>SIG(RO, C)</i></td>
    </tr>
    <tr>
    <td><b>Подрядчик</b></td>
    <td><i>Rpub</i></td>
    <td><b>Подпись Подрядчика</b></td>
      <td></td>
    </tr>
    <tr>
    <td><b>Доверенное лицо</b></td>
    <td><i>Opub</i></td>
    <td><b>Подпись Доверенного лица</b></td>
      <td></td>
    </tr>
  </tbody>
</table>

Клиент отправляет этот контракт в Сеть, уведомляя всех ее участников, в том числе Подрядчика и Доверенное лицо, о его создании.

### Шаг 4. Передача отходов

Клиент передает отходы Подрядчику, указывая, что выполнение объязательств регулируется контрактом, созданным для заказа *RO*.

### Шаг 5. Выполнение обязательств

Подрядчик выполняет необходимый перечень работ, указанный в контракте для *RO*, после чего *дополняет контракт* своей подписью *SIG(RO, R)*, уведомляя об этом Сеть.

### Шаг 6. Подтверждение выполнения обязательств

Доверенное лицо, однозначно убедившись в правильности выполнения обязательств *RO* *дополняет контракт* своей подписью *SIG(RO, O)*, уведомляя об этом Сеть.

Теперь в сети содержится контракт следующего вида:

<table>
  <tbody>
    <tr>
    <td><b>Заказ</b></td>
    <td colspan="3"><i>RO</i></td>
    </tr>
    <tr>
    <td><b>Дата</b></td>
      <td colspan="3">23.08.18 12:34:56.123</td>
    </tr>
    <tr>
    <td><b>Перечень работ</b></td>
      <td colspan="3">Утилизация единицы медицинских отходов № 123123</td>
    </tr>
    <tr>
    <td><b>Вознаграждение</b></td>
    <td colspan="3">1.00000000 <i>T</i></td>
    </tr>
    <tr>
    <td><b>Клиент</b></td>
    <td><i>Cpub</i></td>
    <td><b>Подпись Клиента</b></td>
    <td><i>SIG(RO, C)</i></td>
    </tr>
    <tr>
    <td><b>Подрядчик</b></td>
    <td><i>Rpub</i></td>
    <td><b>Подпись Подрядчика</b></td>
    <td><i>SIG(RO, R)</i></td>
    </tr>
    <tr>
    <td><b>Доверенное лицо</b></td>
    <td><i>Opub</i></td>
    <td><b>Подпись Доверенного лица</b></td>
    <td><i>SIG(RO, O)</i></td>
    </tr>
  </tbody>
</table>

Имея все 3 подписи, любой участник Сети может подвердить факт выполнения работ, что дает Подрядчику подтвержденное Сетью право распоряжаться вознаграждением, приложенным к контракту.

## Преимущества

* В общем случае участники Сети не имеют прямых и косвенных контактов с участниками модели. Как правило, это географически распределенные компьютеры, принадлежащие энтузиастам.
* Любой человек, так или иначе подключенный к Cети, может узнать о создании контракта, о его участниках, перечне работ, вознаграждении и статусе, что дает возможность осуществлять общественный контроль и позволяет в некоторой степени исключить коррупцию.
* Большая часть вычислений приходится на Сеть, что избавляет от необходимости в дорогостоющем серверном оборудовании всех участников данной модели.

### Недостатки

* Так как операции производятся при помощи цифрового актива (т.е. криптовалюты), может возникнуть потребность в создании отдельного инструмента для интеграции системы с широкоиспользуемыми системами учета 1C и SAP.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Лицензия Creative Commons" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />Это произведение доступно по <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">лицензии Creative Commons С указанием авторства-Некоммерческая-Без производных 4.0 Всемирная</a>.
