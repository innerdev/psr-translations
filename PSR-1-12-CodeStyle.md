Код-стайл нужен для того, чтобы чтение кода от разных разработчиков не вызывало неудобств.

Пример
======

Сразу приведем пример кода, написанного по PSR-1/PSR-12 (т.е. по этому гайду):

```
<?php

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;

use function Vendor\Package\{functionA, functionB, functionC};

use const Vendor\Package\{ConstantA, ConstantB, ConstantC};

class Foo extends Bar implements FooInterface
{
    public function sampleFunction(int $a, int $b = null): array
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```


Общие положения (PSR-1)
=======================

Должны использоваться только теги <?php и <?.
Должна использоваться кодировка UTF-8 without BOM.
PHP-файл должен или объявлять функции и классы или вызывать сайд-эффект, но не одновременно.
Неймспейсы и классы должны следовать PSR-0 (https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md) и PSR-4 (https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md).
Имена классов должны быть написаты в StudlyCaps.
Константы класса должны быть написан прописными (большими) буквами, с использованием символа _ вместо пробела.
Названия методов должны быть написаны в camelCase.

Сайд-эффект:
------------

Пример одновременного объявления функции и сайд-эффекта:

```
<?php
// сайд-эффект
ini_set('error_reporting', E_ALL);

// сайд-эффект
include "file.php";

// сайд-эффект
echo "<html>\n";

// объявление
function foo()
{
    // какой-то код
}
```

Пример файла, объявляющие функции и не вызывающего сайд-эффект:

```
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
```

Неймспейсы и имена классов
==========================

Неймспейсы и классы должны следовать PSR-0 (https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md) и PSR-4 (https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md).

Это означает, что каждый класс находится в собственном файле и находится в пространстве имен по крайней мере одного уровня: имя vendor верхнего уровня.

Имена классов должны быть написаты в StudlyCaps.

Пример класса:

```
<?php
// PHP 5.3 или более поздний:
namespace Vendor\Model;

class Foo
{
}
```

В PHP 5.2 или более раннем вместо неймспейсов следует использовать псевдо-нейминг:

```
<?php
// PHP 5.2.x and earlier:
class Vendor_Model_Foo
{
}
```


Константы, свойства и методы
============================

Константы класса должны быть написан прописными (большими) буквами, с использованием символа _ вместо пробела. Например:

```
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```


Свойства класса могу быть объявлены по-разному, например: $StudlyCaps, $camelCase или $under_score. Какой бы нейминг вы не выбрали, нужно убедиться, что вы придерживаетесь его всегда на уровне пакета, класса или метода.

Названия методов должны быть написаны в camelCase.


Подробный разбор правил code style (PSR-12)
===========================================

Файлы
-----

В дополнение к сказанному выше:
PHP-файл должен содержать только окончение строки Unix LF.
PHP-файл должен заканчиваться не пустой строкой, "закрытой" с помощью LF.
Закрывающий тег ?> не должен использоваться.

Строки
------

Не должно быть жесткого лимита на длину строк.
Мягкий лимит должен быть 120 символов.
Не рекомендуется писать строки длиннее 80 символов, строки длиннее рекомендуется разбивать на подстроки так, чтобы они вмещались в лимит в 80 символов.
Не должно быть пробелов в конце строк.
Пустые строки могут быть добавлены в код, чтобы улучшить читаемость кода.
Не должно быть больше, чем одного выражение в одной строке.

Отступы
-------

Отстыпом должны являться 4 пробела, нельзя использовать табуляцию для отступов.

Ключевые слова и типы
---------------------

Все ключевые слова и типы (https://www.php.net/manual/en/reserved.keywords.php, https://www.php.net/manual/en/reserved.other-reserved-words.php) должны быть написаны строчными буквами.
Необходимо использовать короткую запись типов при возможности (bool вместо boolean, int вместо integer). [это не рекомендации для разработчиков PHP, случайно? - прим. ред]

Объявление выражений, неймспейсов и импортов
============================================

Шапка PHP-файла может состоять из разных блоков. В этом случае, каждый блок отделяется от другого пустой строкой и не должен содержать пустых строк внутри себя.

Обычно шапка файла состоит из следующего:

Открывающий <?php тег.
PHPDoc для файла.
Одно или несколько declare выражений.
Объявление неймспейса.
Одно или несколько использований use для: классов, функций и констант (именно в этом порядке).
Остальной код в файле.

Выражения import не должны начинаться с обратного слеша (\).

Пример правильно написанной шапки файла:

```
<?php

/**
 * This file contains an example of coding styles.
 */

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;
use Vendor\Package\AnotherNamespace\ClassE as E;

use function Vendor\Package\{functionA, functionB, functionC};
use function Another\Vendor\functionD;

use const Vendor\Package\{CONSTANT_A, CONSTANT_B, CONSTANT_C};
use const Another\Vendor\CONSTANT_D;

/**
 * FooBar is an example class.
 */
class FooBar
{
    // ... additional PHP code ...
}
```

Составные неймспейсы с глубиной больше двух недопустимы. Пример правильно составленного составного неймспейса:

```
<?php

use Vendor\Package\SomeNamespace\{
    SubnamespaceOne\ClassA,
    SubnamespaceOne\ClassB,
    SubnamespaceTwo\ClassY,
    ClassZ,
};
```

Неправильно составленный неймспейс, так делать нельзя:

```
<?php

use Vendor\Package\SomeNamespace\{
    SubnamespaceOne\AnotherNamespace\ClassA,
    SubnamespaceOne\ClassB,
    ClassZ,
};
```

Выражение declare(strict_types=1) не должно содержать пробелов внутри себя и должно быть написано в точности как указано (закрывающая точка с запятой является опциональной).


Наследование и имплементирование
================================

Ключевые слова extends и implements должны быть написаны на той же строке, что и объявление класса.
Открывающая фигурная скобка должна идти с новой строки; закрывающая - с новой строки после тела класса.
До или после открывающей/закрывающий фигурной скобки, относящейся к классу, не должно быть пустых строк.

Пример:

```
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```

Перечисление наследующихся классов или имплементируемых интерфейсов может быть написано и с новой строки. В таком случае это одно имя на каждой строке, а перенос строки делается сразу же за словом implenets или extends.

Например:

```
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```

Трейты
------

Ключевое слово use для имплементации трейтов должно быть объявлено сразу же за открывающе кавычкой, относящейся к объявлению класса:

```
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;
}
```

Каждый трейт должен быть имплементирован с помощью своего собственного слова use и быть написанным с новой строки:

```
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;
use Vendor\Package\SecondTrait;
use Vendor\Package\ThirdTrait;

class ClassName
{
    use FirstTrait;
    use SecondTrait;
    use ThirdTrait;
}
```

Если в классе больше нет кода, кроме как подключение трейта, сразу за use должна идти закрывающая фигурная скобка:

```
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;
}
```

В противном случае, после use обязана стоять пустая строка:

```
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;

    private $property;
}
```

Если используются операторы insteadof или as, они должны быть написаны как в примере (обратите внимание на отступы, пробелы и новые строки):

```
<?php

class Talker
{
    use A;
    use B {
        A::smallTalk insteadof B;
    }
    use C {
        B::bigTalk insteadof C;
        C::mediumTalk as FooBar;
    }
}
```

Свойства и константы
--------------------

Область видимости обязана быть добавлена ко всем свойствам.
Область видимости обязана быть добавлена ко всем константам класса, если позволяет версия языка.
Ключевое слово var не должно быть использовано.
Не должно быть объявления больше чем одного свойства на строку.
У свойств не должно быть символа _ с целью указать область видимости. [видимо, речь про какое-то страшное легаси; а еще привет питону - прим. ред.]

Пример правильного определения свойств:

```
<?php

namespace Vendor\Package;

class ClassName
{
    public $foo = null;
    public static int $bar = 0;
}
```

Методы и функции
----------------

Область видимости должна быть добавлена к каждому методу.
У методов не должно быть символа _ с целью указать область видимости.
После имени метода или функции не должно стоять пробела.
Открывающая и закрывающая фигурные скобки для определения тела метода должны располагаться с новой строки и каждая в своей собственной строке.
не должно быть пустых строк до или после открывающих/закрывающий фигурных скобок, относящихся к объявлению тела метода.

Пример правильного объявления метода:

```
<?php

namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

Пример правильного объявления функции:

```
<?php

function fooBarBaz($arg1, &$arg2, $arg3 = [])
{
    // function body
}
```

Аргументы методов и функций
---------------------------

При объявлении аргументов методов и функций не должно быть пробела до запятой, и должен быть один пробел после запятой.
Аргументы со значением по умолчанию должны идти в конце списка аргументов.

Пример объявления аргументов:

```
<?php

namespace Vendor\Package;

class ClassName
{
    public function foo(int $arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

Аргументы могут быть написаны каждый с новой строки. В таком случае первый аргумент должен быть написан сразу же с новой строки и в одной строке должен быть только один аргумент.
Закрывающая скобка метода ) должна и открывающая фигурная скобка { должны располагаться на одной строке с одним пробелом между ними, и находиться на новой строке после последнего аргумента.

Пример объявления:

```
<?php

namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

Если указан тип возвращаемого значения, он должен быть указан следующим образом (обратите внимание на символ ":", пробелы и отступы):

```
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(int $arg1, $arg2): string
    {
        return 'foo';
    }

    public function anotherFunction(
        string $foo,
        string $bar,
        int $baz
    ): string {
        return 'foo';
    }
}
```

Если тип возвращаемого значения может быть nullable, нельзя разделять между собой знак вопроса и название типа:

```
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(?string $arg1, ?int &$arg2): ?string
    {
        return 'foo';
    }
}
```

Если используется символ & не должно быть пробела между ним и аргументом. Также не должно быть пробела между тремя точками и аргументом:

```
public function process(string $algorithm, ...$parts)
{
    // processing
}
```

При комбинировании трех точек и & между ними также не должно быть пробела:

```
public function process(string $algorithm, &...$parts)
{
    // processing
}
```

abstract, final, и static
---------------------------

Если указаны abstract или final, они должны идти перед определением области видимости.
Если указан static, он должен идти после определения области видимости.

Например:

```
<?php

namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
```

Вызов функций и методов
-----------------------

При вызове функции и метода не должно быть пробела между именем функции или метода и открывающий скобкой (. Не должно быть пробела после открывающей скобки (. И не должно быть пробела перед закрывающей скобкий ).
В списке аргументов не должно быть пробелов перед запятой, а после запятой всегда должен быть один пробел.

Пример:

```
<?php

bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

Аргументы вызываемой функции или метода могут быть написаны каждый с новой строки. В таком случае первый аргумент должен начинаться с новой строки и должен быть только один аргумент в строке.
Один аргумент (например, массив) тоже может быть разбит на несколько строк, но не означает разбиения списка аргументов. 

Например:

```
<?php

$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```

Пример для "одиночного" аргумента:

```
<?php

somefunction($foo, $bar, [
  // ...
], $baz);

$app->get('/hello/{name}', function ($name) use ($app) {
    return 'Hello ' . $app->escape($name);
});
```

Управляющие конструкции
=======================

Основные правила для управляющих конструкций:

Должен быть пробел после ключевого слова (if/else и т.п.).
Не должно быть пробела после открывающей фигурной скобки.
Не должно быть пробела перед закрывающий фигурной скобкой.
Должен быть пробел после закрывающей скобки ) и открывающей {.
Тело конструкции должно начинаться с новой строки после {.
Закрывающая } должна идти на новой строке после тела.

if, elseif, else
----------------

Пример для этих конструкций (обратите внимание на отступы, пробелы, переносы строк и другое):

```
<?php

if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```

Ключевое слово elseif следует использовать вместо else if.

Условие внутри ( и ) может быть разбито на несколько строк. В таком случае первое условие должно сразу начинаться с новой строки после (. Закрвающая ) должна располагаться с новой строки. Закрвающая ) и открывающая { должны располагаться вместе, между ними должен быть пробел. Булевый оператор должен располагаться в начале каждой строки или в конце, но не одновременно и так и так (в примере располагается в начале).

Пример:

```
<?php

if (
    $expr1
    && $expr2
) {
    // if body
} elseif (
    $expr3
    && $expr4
) {
    // elseif body
}
```

switch, case
------------

Конструкция switch должна выглядеть как в примере ниже. Выражение case должно иметь отступ слева от switch. Выражение break должно располагаться на том же уровне отступов слева, что и тело case. Обязательно должен быть комментарий // no break, в случае отсутствия завершающего case ключевого слова.

Пример:

```
<?php

switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```

Аргументы switch могут начинаться каждый с новой строки. Для них действуют те же правила, что и для if (см. выше).

Пример:

```
<?php

switch (
    $expr1
    && $expr2
) {
    // structure body
}
```

while, do while
---------------

Выражение while должно выглядеть следующим образом (обратите внимание на отступы, кавычки, пробелы и прочее):

```
<?php

while ($expr) {
    // structure body
}
```

Аргументы для while могут располагаться каждый с новой строки. В этом случае для них действуют те же правила, что для if и switch.

Пример:

```
<?php

while (
    $expr1
    && $expr2
) {
    // structure body
}
```

Выражение do while выглядит следующим образом (обратите внимание на отступы, кавычки, пробелы и прочее):

```
<?php

do {
    // structure body;
} while ($expr);
```

Аргументы для do while могут располагаться каждый с новой строки. В таком случае для них действуют те же правила, что и для if, switch, while.

Например:

```
<?php

do {
    // structure body;
} while (
    $expr1
    && $expr2
);
```

for
---

Цикл for выглядит следющим образом (обратите внимание на отступы, кавычки, пробелы и прочее):


```
<?php

for ($i = 0; $i < 10; $i++) {
    // for body
}
```

Аргументы цикла for могут располагаться каждый с новой строки. В таком случае каждый аргумент располагается в новой строке. Первый аргумент должен начинаться с новой строки. Закрывающая ) и открывающая { должны располагаться с новой строки и меть пробел между собой.

Например:

```
<?php

for (
    $i = 0;
    $i < 10;
    $i++
) {
    // for body
}
```

foreach
-------

Цикл foreach выглядит следующим образом. Расположение аргументов на разных строках, судя по всему, не предусмотрено в PSR и, видимо, не рекомендуется или даже запрещено:

```
<?php

foreach ($iterable as $key => $value) {
    // foreach body
}
```

try, catch, finally
-------------------

try-catch-finally выглядит следующим образом. Обратите внимание на кавычки, пробелы, отступы и отступы на новую строку:

```
<?php

try {
    // try body
} catch (FirstThrowableType $e) {
    // catch body
} catch (OtherThrowableType | AnotherThrowableType $e) {
    // catch body
} finally {
    // finally body
}
```

Операторы
=========

Если вокруг оператора разрешены пробелы, можно использовать несколько для удобства чтения. [довольно странный совет, я бы не рекомендовал его использовать - прим. ред.]

Унарные операторы
-----------------

Операторы инкремента и декремента не должны иметь пробела между собой и именем переменной:

```
$i++;
++$j;
```

Оператор каста (изменения типа) не должен иметь пробелов внутри ( и ):

```
$intValue = (int) $input;
```

Бинарные операторы
------------------

Всем бинарным операторам (арифметические, сравнения, присваивания, битовые, логические, строковые и типов, см. список ниже) должен предшествовать один пробел и один пробел должен идти после них.

Например:

```
if ($a === $b) {
    $foo = $bar ?? $a ?? $b;
} elseif ($a > $b) {
    $foo = $a + $b * $c;
}
```


Список всех операторов: https://www.php.net/manual/en/language.operators.arithmetic.php, https://www.php.net/manual/en/language.operators.comparison.php, https://www.php.net/manual/en/language.operators.assignment.php, https://www.php.net/manual/en/language.operators.bitwise.php, https://www.php.net/manual/en/language.operators.logical.php, https://www.php.net/manual/en/language.operators.string.php, https://www.php.net/manual/en/language.operators.type.php

Тернарные операторы
-------------------

В тернарном операторе до и после ? и : должен идти хотя бы один пробел:

```
$variable = $foo ? 'foo' : 'bar';
```

Если значение среднего операнда опущено, тернарный оператор должен выглядеть следующим образом:

```
$variable = $foo ?: 'bar';
```

Замыкания (Closures)
====================

Замыкание должно быть объявлено с пробелом после ключевого слова function и пробелом до и после ключевого слова use.
Открывающая фигурная скобка должна идти на той же строке, где и объявление. Закрывающая - на следующей строке после тела объявления.
Не должно быть пробела после открывающей скобки ( в списке аргументов, как не должно быть пробела и перед закрывающей скобки ) в списке аргументов.
В списке аргументов не должно быть пробелов перед запятыми и должен быть один пробел после каждой запятой.
Аргументы, имеющие значение по умолчанию, должно идти в конце списка аргументов.
Если указан возвращаемый тип, он должен быть оформлен так же как для функций и методов (см. выше).
Если присутствует ключевое слово use, двоеточие должно следовать за закрывающими круглыми скобками списка аргументов, без пробелами между ) и :.

Например:

```
<?php

$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};

$closureWithArgsVarsAndReturn = function ($arg1, $arg2) use ($var1, $var2): bool {
    // body
};
```

Список аргументов может быть разбит на несколько строк. В общем и целом, должны быть применены те же правила, что для функций и методов.

Примеры (обратите внимание на отступы, пробелы, переносы строк при использовании ключевого слова use):

```
<?php

$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
```

Все те же правила оформления применяются и в случае, если замыкание используется как аргумент при вызове другой функции или метода:

```
<?php

$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```

Анонимные классы
================

Анонимные классы в общем и целом оформляются так же, как и замыкания из секции выше. Общее объявление выглядит следующим образом:

```
<?php

$instance = new class {};
```

Открывающая фигурная скобка может располагаться на той же строке, что и ключевое слово class, если список аргументов для implements не переносистя на новую строку:

```
<?php

// Brace on the same line
$instance = new class extends \Foo implements \HandleableInterface {
    // Class content
};
```

Если список аргументов для implements переносится на новую строку, открывающая фигурная скобка должна идти с новой строки:

```
<?php

// Brace on the next line
$instance = new class extends \Foo implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // Class content
};
```