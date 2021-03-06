Стандарты кодирования
#####################

Разработчики CakePHP будут использовать руководство по стилю кодирования `PSR-12
<https://www.php-fig.org/psr/psr-12/>`_ в дополнение к следующим правилам
стандартов кодирования.

Рекомендуется, чтобы и другие, разработчики использовали данные стандарты.

Вы можете использовать `CakePHP Code Sniffer
<https://github.com/cakephp/cakephp-codesniffer>`_, чтобы проверить, что ваш код
соответствует требованиям стандартов.

Добавление новых функций
========================

Не следует добавлять никаких новых функций, не имея собственных тестов, которые
должны быть переданы перед передачей новых функций в репозиторий.

Установка IDE
=============

Убедитесь, что ваша среда IDE настроена на "trim right" - обрезку пробелов с права.
В строке не должно быть лишних пробелов.

Большинство современных IDE также поддерживают файл ``.editorconfig``. CakePHP
содержит скелет приложения, который отправляется с ним по умолчанию. Он уже содержит
настройки по умолчанию.

Мы рекомендуем использовать плагин `IdeHelper <https://github.com/dereuromark/cakephp-ide-helper>`_, если вы
хотите максимизировать совместимость с IDE. Это поможет сохранить обновленные аннотации, которые сделают
IDE полностью понимающим, как работают все классы вместе и обеспечит лучшую подсказку и автозаполнение.

Отступ
======

Для отступов будут использоваться четыре пробела.

Итак, отступы должны выглядеть так::

    // base level
        // level 1
            // level 2
        // level 1
    // base level

Или::

    $booleanVariable = true;
    $stringVariable = 'moose';
    if ($booleanVariable) {
        echo 'Boolean value is true';
        if ($stringVariable === 'moose') {
            echo 'We have encountered a moose';
        }
    }

В случаях, когда вы используете вызов многострочной(multi-line) функции, используйте следующие
методические рекомендации:

*  Открытая скобка многострочной функции должна быть последним элементом на строке.
*  На одной строке разрешён только один аргумент, при вызове многострочной функции.
*  Закрывающая скобка, при вызове многострочной функции, должна быть на отдельной строке.

В качестве примера, вместо использования следующего форматирования::

    $matches = array_intersect_key($this->_listeners,
                    array_flip(preg_grep($matchPattern,
                        array_keys($this->_listeners), 0)));

Используйте такое форматирование::

    $matches = array_intersect_key(
        $this->_listeners,
        array_flip(
            preg_grep($matchPattern, array_keys($this->_listeners), 0)
        )
    );

Длина строки
============

Рекомендуется придерживаться длины линии около 100 символов, для лучшей
читаемости кода. Ограничение в 80 или 120 символов заставляет разносить сложную логику или выражения по функциям, а также давать функциям и объектам более короткие, ёмкие и выразительные имена. Длина строки не должна превышать 120 символов.

Вкратце:

* 100 символов - это мягкий предел.
* 120 символов - это жёсткий предел.

Управляющие структуры
=====================

Управляющие структуры например "``if``", "``for``", "``foreach``",
"``while``", "``switch``" и т.п.. Ниже приведён пример с "``if``"::

    if ((expr_1) || (expr_2)) {
        // action_1;
    } elseif (!(expr_3) && (expr_4)) {
        // action_2;
    } else {
        // default_action;
    }

*  В управляющих структурах должен быть 1 (один) пробел перед первой
   скобкой и 1 (один) пробел между последней круглой скобкой и открытой скобкой.
*  Всегда используйте фигурные скобки в управляющих структурах, даже если они не нужны.
   Они повышают читаемость кода, и они дают вам меньше логических ошибок.
*  Открытие фигурных скобок должно быть размещено на той же линии, что и элемент управляющей структуры.
   Закрытие фигурных скобок должно быть размещено на новых линиях, и они должны иметь тот же уровень отступов,
   что и управляющая структура. Заявления включенные в фигурные скобки, должны начинаться с новой строки,
   а код содержащийся внутри них должен получить новый уровень отступов.
*  Внутренние назначения не должны использоваться внутри структур управления

::

    // неправильно = нет фигурных скобок, плохо размещенное заявление
    if (expr) statement;

    // неправильно = нет фигурных скобок
    if (expr)
        statement;

    // хорошо
    if (expr) {
        statement;
    }

    // неправильно = встроенное задание
    if ($variable = Class::function()) {
        statement;
    }

    // хорошо
    $variable = Class::function();
    if ($variable) {
        statement;
    }

Тернарный оператор
------------------

Тернарные операторы допустимы, если вся тернарная операция проходит на одной строке.
Более длинные тернарные операторы должны быть разделены с использованием ``if else``.
Тернарные операторы не должны быть вложенными. По желанию можно использовать круглые скобки,
при проверке состояния тернартного оператора, для большей ясности::

    // Хорошо, просто и читабельно
    $variable = isset($options['variable']) ? $options['variable'] : true;

    // Плохо - вложенные тернарные операции
    $variable = isset($options['variable']) ? isset($options['othervar']) ? true : false : false;

Файлы шаблонов
--------------

В файлах шаблонов (.php файлы) разработчикам следует пользоваться ключевыми словами управляющих структур.
Ключевые словами управляющих структур легче читать в сложных файлах шаблонов. Контрольные
структуры могут либо содержаться в большем блоке PHP, либо в отдельном теге PHP::

    <?php
    if ($isAdmin):
        echo '<p>You are the admin user.</p>';
    endif;
    ?>
    <p>The following is also acceptable:</p>
    <?php if ($isAdmin): ?>
        <p>You are the admin user.</p>
    <?php endif; ?>

Сравнение
=========

Всегда старайтесь быть максимально строгими. Если нестрогий тест преднамерен,
разумным будет прокоментировать это, чтобы не перепутать его с ошибкой.

Для тестирования, если переменная равна нулю, рекомендуется использовать строгую проверку::

    if ($value === null) {
        // ...
    }

Значение для проверки должно быть размещено с правой стороны::

    // не рекомендуется
    if (null === $this->foo()) {
        // ...
    }

    // рекомендуется
    if ($this->foo() === null) {
        // ...
    }

Вызовы функций
==============

Функции следует вызывать без пробела между именем функции и началом
скобки. Между каждым параметром функции должен быть один пробел::

    $var = foo($bar, $bar2, $bar3);

Как вы могли увидеть выше, должен быть один пробел по обе стороны от знака равенства (=).

Определение метода
==================

Пример определения метода::

    public function someFunction($arg1, $arg2 = '')
    {
        if (expr) {
            statement;
        }

        return $var;
    }

Параметры со значением по умолчанию должны быть последними в определении функции.
Постарайтесь, чтобы ваши функции возвращали что-то, по крайней мере, ``true`` или ``false``, поэтому
можно определить, был ли вызов функции успешным::

    public function connection($dns, $persistent = false)
    {
        if (is_array($dns)) {
            $dnsInfo = $dns;
        } else {
            $dnsInfo = BD::parseDNS($dns);
        }

        if (!($dnsInfo) || !($dnsInfo['phpType'])) {
            return $this->addError();
        }

        return true;
    }

На обеих сторонах знака равенства есть пробелы.

Тип подсказки
-------------

Аргументы, которые ожидают объекты, массивы или обратные вызовы (callable), могут быть определены в соответсвии с их типом.
Однако мы вводим их только для общедоступных методов, поскольку typehinting не является 'cost-free'::

    /**
     * Some method description.
     *
     * @param \Cake\ORM\Table $table The table class to use.
     * @param array $array Some array value.
     * @param callable $callback Some callback.
     * @param bool $boolean Some boolean value.
     */
    public function foo(Table $table, array $array, callable $callback, $boolean)
    {
    }

Здесь ``$table`` должен быть экземпляром от ``\Cake\ORM\Table``, ``$array`` должен быть от
``array`` и ``callback`` должны иметь тип ``callable`` (валидный обратный вызов).

Обратите внимание: если вы хотите разрешить ``$array`` также быть экземпляром
``\ArrayObject`` вы не должны описывать typehint, поскольку ``array`` принимает только примитивный тип::

    /**
     * Some method description.
     *
     * @param array|\ArrayObject $array Some array value.
     */
    public function foo($array)
    {
    }

Анонимные функции (Замыкания)
-----------------------------

Определение анонимных функций следует из `PSR-12
<https://www.php-fig.org/psr/psr-12/>`_ руководства по стилю кодирования, где они
объявленны пробелом после ключевого слова `function`, и пробелом до и после
ключевого слова `use`::

    $closure = function ($arg1, $arg2) use ($var1, $var2) {
        // code
    };

Цепочки методов
===============

Цепочка методов должна иметь несколько методов, распределенных по отдельным линиям, и
с отступом из четырёх пробелов::

    $email->from('foo@example.com')
        ->to('bar@example.com')
        ->subject('A great message')
        ->send();

Комментарии в коде
==================

Все комментарии должны быть написаны на английском языке и должны четко описывать
прокомментированный блок кода.

Комментарии могут включать следующие теги `phpDocumentor <http://phpdoc.org>`_:

*  `@author <http://phpdoc.org/docs/latest/references/phpdoc/tags/author.html>`_
*  `@copyright <http://phpdoc.org/docs/latest/references/phpdoc/tags/copyright.html>`_
*  `@deprecated <http://phpdoc.org/docs/latest/references/phpdoc/tags/deprecated.html>`_
   Использование формата ``@version <vector> <description>``, где ``version``
   и ``description`` являются обязательными. Версия относится к той, которая уже устарела.
*  `@example <http://phpdoc.org/docs/latest/references/phpdoc/tags/example.html>`_
*  `@ignore <http://phpdoc.org/docs/latest/references/phpdoc/tags/ignore.html>`_
*  `@internal <http://phpdoc.org/docs/latest/references/phpdoc/tags/internal.html>`_
*  `@link <http://phpdoc.org/docs/latest/references/phpdoc/tags/link.html>`_
*  `@see <http://phpdoc.org/docs/latest/references/phpdoc/tags/see.html>`_
*  `@since <http://phpdoc.org/docs/latest/references/phpdoc/tags/since.html>`_
*  `@version <http://phpdoc.org/docs/latest/references/phpdoc/tags/version.html>`_

Теги PhpDoc очень похожи на теги JavaDoc в Java. Теги обрабатываются только в том случае, если
они являются первыми в строке DocBlock, например::

    /**
     * Tag example.
     *
     * @author this tag is parsed, but this @version is ignored
     * @version 1.0 this tag is also parsed
     */

::

    /**
     * Example of inline phpDoc tags.
     *
     * This function works hard with foo() to rule the world.
     *
     * @return void
     */
    function bar()
    {
    }

    /**
     * Foo function.
     *
     * @return void
     */
    function foo()
    {
    }

Блокам комментариев, за исключением первого блока в файле, должна всегда
предшествовать новая строка.

Типы переменных
---------------

Типы переменных использующихся в DocBlocks:

Type
    Описнаие
mixed
    Переменная с неопределенным (или множественным) типом.
int
    Целочисленная переменная типа (целое число).
float
    Плавающий тип (point number).
bool
    Логический тип (true или false).
string
    Строковый тип (любые значения в " " или ' ').
null
    Null тип. Обычно используется в сочетании с другим типом.
array
    Массив.
object
    Object (объект). При необходимости следует использовать определенное имя класса.
resource
	Тип ресурса (возвращается, например, mysql\_connect()).
	Помните, что когда вы указываете тип как смешанный, вы должны указать,
	неизвестно ли оно или какие могут быть возможные типы.
callable
    Callable функция.

Вы также можете комбинировать типы, используя символ '|'::

    int|bool

Для более чем двух типов обычно лучше всего использовать ``mixed``.

При возврате самого объекта, например. для цепочки, следует использовать вместо этого ``$this``::

    /**
     * Foo function.
     *
     * @return $this
     */
    public function foo()
    {
        return $this;
    }

Подключаемые файлы
==================

``include``, ``require``, ``include_once`` и ``require_once`` не должны
иметь круглых скобок::

    // ошибка = круглые скобки
    require_once('ClassFileName.php');
    require_once ($class);

    // хорошо = нет круглых скобок
    require_once 'ClassFileName.php';
    require_once $class;

При включении файлов с классами или библиотеками используйте вегда только функцию
`require\_once <http://php.net/require_once>`_.

PHP теги
========

Всегда используйте длинные теги (``<?php ?>``) Вместо коротких тегов (``<? ?>``). Короткие
echo должны использоваться в файлах шаблонов (**.php**), где это необходимо.

Короткое echo
-------------

Короткое эхо должно использоваться в файлах шаблонов вместо ``<?php echo``. После
``<?=`` должен следовать один пробел, потом имя переменной или функции,
снова один пробел и закрывающий тег ``?>`` php::

    // неправильно = есть точка с запятой, нет пробелов
    <td><?=$name;?></td>

    // хорошо = есть пробелы, нет точки с запятой
    <td><?= $name ?></td>

Начиная с PHP 5.4 короткий echo тег (``<?=``) больше не следует рассматривать как
'короткий тег'. Теперь он всегда доступен, независимо от значения ``short_open_tag`` директивы ini.

Соглашение об именовании
========================

Функции
-------

Писать все имена функций нужно используя синтаксис camelBack::

    function longFunctionName()
    {
    }

Классы
-------

Писать все классы нужно используя синтаксис CamelCase, для примера::

    class ExampleClass
    {
    }

Переменные
----------

Имена переменных должны быть как можно более подробными, но по возможности короткими.
Все переменные должны начинаться со строчной буквы и должны быть
написанный на camelBack в случае нескольких слов. Переменные, ссылающиеся на объекты,
должны каким-либо образом ассоциироваться с классом своего объекта.

Пример::

    $user = 'John';
    $users = ['John', 'Hans', 'Arne'];

    $dispatcher = new Dispatcher();

Видимость элементов
-------------------

Используйте PHP ``public``, ``protected`` и ``private`` ключевые слова для методов и переменных.

Примеры адресов
---------------

Для всех примеров URL и почтовых адресов используйте "example.com", "example.org" и
"example.net", например:

*  Email: someone@example.com
*  WWW: `http://www.example.com <http://www.example.com>`_
*  FTP: `ftp://ftp.example.com <ftp://ftp.example.com>`_

Для этого зарезервировано доменное имя "example.com" (см. :rfc:`2606`) и
рекомендуется для использования в документации или в качестве примеров.

Файлы
-----

Имена файлов, которые не содержат классов, должны быть уменьшены и подчеркнуты,
например::

    long_file_name.php

Смена ролей
-----------

Для смены ролей используйте:

Type
    Description
(bool)
    Сменить на boolean.
(int)
    Сменить на integer.
(float)
    Сменить на float.
(string)
    Сменить на string.
(array)
    Сменить на array.
(object)
    Сменить на object.

Используйте ``(int)$var`` вместо ``intval($var)`` и ``(float)$var`` вместо
``floatval($var)``, если есть такая возможность.

Константы
---------

Константы должны быть определены заглавными буквами::

    define('CONSTANT', 1);

Если имя константы состоит из нескольких слов, они должны быть разделены
символом подчеркивания, например::

    define('LONG_NAMED_CONSTANT', 2);

Осторожность при использовании empty()/isset()
==============================================

Хотя ``empty()`` - простая в использовании функция, она может маскировать ошибки и вызывать
непреднамеренные эффекты, когда даны ``'0'`` и ``0``. Когда переменные или
свойства уже определены, использование ``empty()`` не рекомендуется.
При работе с переменными лучше полагаться на приведение типа к логическому,
вместо ``empty()``::

    function manipulate($var)
    {
        // Не рекомендуется, $var уже определен в области
        if (empty($var)) {
            // ...
        }

        // Корректно использовать тип boolean
        if (!$var) {
            // ...
        }
        if ($var) {
            // ...
        }
    }

Когда вы имеете дело с определенными свойствами, вы должны использовать ``null`` для проверки
``empty()``/``isset()``::

    class Thing
    {
        private $property; // Определено

        public function readProperty()
        {
            // Не рекомендуется, поскольку свойство определено в классе
            if (!isset($this->property)) {
                // ...
            }
            // Рекомендуется
            if ($this->property === null) {

            }
        }
    }

При работе с массивами лучше объединять значения по умолчанию с использованием проверок
``empty()``. Объединив значения по умолчанию, вы можете гарантировать, что требуемые ключи
определены::

    function doWork(array $array)
    {
        // Объединить значения по умолчанию, чтобы удалить необходимость в пустых проверках.
        $array += [
            'key' => null,
        ];

        // Не рекомендуется, как уже было сказанно
        if (isset($array['key'])) {
            // ...
        }

        // Рекомендуется
        if ($array['key'] !== null) {
            // ...
        }
    }

.. meta::
    :title lang=ru: Стандарты кодирования
    :keywords lang=ru: фигурные скобки, уровень отступов, логические ошибки, управляющие структуры, структуры управления, expr, стандарты кодирования, скобки, foreach, читаемость, moose, новые функции, репозиторий, разработчики
