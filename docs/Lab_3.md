# Лабораторная работа №3 "Базовое форматирование строк в C#"


Объединяйте литеральные и переменные текстовые данные, содержащие специальные символы, форматирование и Юникод, в значимые сообщения для конечного пользователя.

# Введение
Разработчик программного обеспечения должен уметь писать на C# код для объединения и форматирования литеральных и переменных данных, чтобы создать новое значение. Это значение может отображаться, сохраняться в файле или отправляться по сети. К счастью, C# предоставляет множество способов объединения и форматирования данных.

Предположим, вам требуется отобразить выходные данные приложения командной строки, которое вы пишете. Необходимо отображать значения, включая литеральный текст, текст в переменных, числовые данные и текстовые данные на других языках. Как вы правильно отформатируете его, чтобы пользователь мог понять сообщение от приложения?

В этом модуле вы будете использовать escape-последовательности символов для форматирования строк текста, включая специальные символы, включая вкладки и каналы строк, даже символы из разных языков, таких как кандзи или кириллица. Вы узнаете, как сцепить две строки и использовать интерполяцию строк для создания шаблона строк с заменяемыми частями.

По завершении этого модуля вы сможете управлять отображением данных для конечных пользователей ваших приложений.

## Цели обучения

В этом модуле вы узнаете, как выполнять следующие задачи:

-   Создание строковых данных, содержащих знаки табуляции, переноса строки и другие специальные символы
-   Создание строковых данных, содержащих символы Юникода
-   Объединение строковых данных в новое строковое значение с помощью конкатенации
-   Объединение строковых данных в новое строковое значение с помощью интерполяции

## Предварительные требования

-   Опыт работы с редактором .NET на начальном уровне
-   Опыт работы на начальном уровне с отображением сообщения в консоль с помощью  [Console.WriteLine()](https://learn.microsoft.com/ru-ru/dotnet/api/system.console.writeline#system-console-writeline)  методов и  [Console.Write(String)](https://learn.microsoft.com/ru-ru/dotnet/api/system.console.write#system-console-write(system-string))  .
-   Начальный опыт работы с типами данных, объявлением, инициализацией, установкой и получением значений из переменных.
# Упражнение. Объединение строк с помощью escape-последовательностей символов
Предположим, вас попросили создать макет программы командной строки, которая будет создавать счета на английском и японском языках. Вам пока не нужно создавать функции, создающие сами счета. Необходимо только предоставить интерфейс командной строки внутренним клиентам в отделе выставления счетов для их утверждения. Руководитель просит добавить форматирование, чтобы сделать текущий ход выполнения более понятным. Руководитель также просит предоставить инструкции для японского пользователя о том, как создавать счета на японском языке.
## Упражнение. Форматирование строк литералов в C #

В этом упражнении вы узнаете о различных методах отображения специальных символов и добавления различных типов форматирования в выходные данные.

### escape-последовательности

**Последовательность escape-символов**  — это инструкция для среды выполнения для вставки специального символа, который повлияет на выходные данные строки. В C# последовательность escape-символов начинается с обратной косой черты  `\`  , за которой следует экранизаемый символ. Например, последовательность  `\n`  добавит новую строку, а последовательность  `\t`  добавит табуляцию.

Следующий код использует последовательности escape-символов для добавления новых строк и вкладок:

```c#
Console.WriteLine("Hello\nWorld!");
Console.WriteLine("Hello\tWorld!");
```

После выполнения кода вы увидите такой результат:


```
Hello
World!
Hello   World!
```

Что делать, если необходимо вставить двойную кавычку в литеральную строку? Если вы не используете escape-последовательность символов, вы запутаете компилятор, так как он будет думать, что вы хотите завершить строку преждевременно. Компилятор не будет понимать назначение символов после второй двойной кавычки.


```c#
Console.WriteLine("Hello "World"!");
```

В редакторе .NET появится красная волнистая линия  `World`. Но если попытаться выполнить код в любом случае, вы увидите следующие выходные данные:


```
(1,27): error CS1003: Syntax error, ',' expected
(1,27): error CS0103: The name 'World' does not exist in the current context
(1,32): error CS1003: Syntax error, ',' expected
```

Чтобы справиться с этой ситуацией, используйте  `\"`  escape-последовательность:


```c#
Console.WriteLine("Hello \"World\"!");

```

При выполнении приведенного выше кода вы увидите следующие выходные данные:


```
Hello "World"!
```

Что делать, если необходимо использовать обратную косую черту для других целей, например для вывода пути к файлу?cs

```
Console.WriteLine("c:\source\repos");
```

К сожалению, C# резервирует обратную косую черту для escape-последовательностей, поэтому при выполнении кода компилятор отобразит следующую ошибку:


```
(1,22): error CS1009: Unrecognized escape sequence
```

Проблема заключается в последовательности  `\s`. Не  `\r`  выдает ошибку, так как это допустимая escape-последовательность для возврата каретки. Однако вы не хотите использовать возврат каретки в этом контексте.

Чтобы решить эту проблему, используйте  `\\`  для отображения одной обратной косой черты.

```
Console.WriteLine("c:\\source\\repos");
```

Экранирование символа обратной косой черты создает нужные выходные данные:


```
c:\source\repos
```

### Форматирование выходных данных с помощью escape-последовательностей символов

1.  Выделите весь код в редакторе .NET и нажмите клавишу  DELETE  или  BACKSPACE, чтобы удалить его.
    
2.  Чтобы создать макет программы командной строки, введите в редакторе следующий код:
    
   
    ```
    Console.WriteLine("Generating invoices for customer \"Contoso Corp\" ...\n");
    Console.WriteLine("Invoice: 1021\t\tComplete!");
    Console.WriteLine("Invoice: 1022\t\tComplete!");
    Console.WriteLine("\nOutput Directory:\t");    
    ```
    
3.  Теперь выполните код. В консоли вывода появятся следующие результаты:

    
    ```
    Generating invoices for customer "Contoso Corp" ...
    
    Invoice: 1021           Complete!
    Invoice: 1022           Complete!
    
    Output Directory:        
    ```
    

## Буквальный строковый литерал

Буквальная литеральная строка сохраняет все пробелы и символы без необходимости экранирования обратной косой чертой. Чтобы создать буквальную строку, используйте директиву  `@`  перед литеральной строкой.


```c#
Console.WriteLine(@"    c:\source\repos    
        (this is where your code goes)");
```

Обратите внимание, что литерал занимает две строки, и пробелы, создаваемые этой инструкцией C#, сохраняются в следующем выводе.

```
    c:\source\repos    
        (this is where your code goes)
```

### Форматирование выходных данных с помощью буквальных строковых литералов

1.  Добавьте следующую строку кода под ранее созданным кодом:

    
    ```c#
    Console.Write(@"c:\invoices");
    
    ```
    
2.  Теперь выполните код. Вы увидите следующий результат, включающий выходной каталог:

    
    ```
    Generating invoices for customer "Contoso Corp" ...
    
    Invoice: 1021           Complete!
    Invoice: 1022           Complete!
    
    Output Directory:
    c:\invoices    
    ```
    

## Escape-символы Юникода

Можно также добавлять закодированные символы в литеральные строки с помощью escape-последовательности  `\u`, за которой стоит набор из четырех символов, представляющих некоторый символ в Юникоде (UTF-16).


```c#
// Kon'nichiwa World
Console.WriteLine("\u3053\u3093\u306B\u3061\u306F World!");
```

>Здесь существует ряд особенностей. Во первых, некоторые консоли, такие как командная строка Windows, могут отображать не все символы Юникода. Эти символы будут заменены вопросительными знаками. Кроме того, в примерах здесь используется UTF-16. Для некоторых символов требуется UTF-32, поэтому нужна другая управляющая последовательность. Это сложная тема, и этот модуль лишь в общих чертах описывает возможные решения. В зависимости от ваших потребностей может потребоваться много времени на обучение и работу с символами Юникода в приложениях.

### Форматирование выходных данных с помощью escape-символов Юникода

Чтобы завершить макет средства командной строки, добавьте фразу на японском языке, которая переводится как "Создать счета на японском языке". Затем вы увидите буквальную строку, представляющую команду, которую может ввести пользователь. Вы также добавите несколько escape-последовательностей для форматирования.

1.  Добавьте в приложение следующий код:
    
   
    ```c#
    // To generate Japanese invoices:
    // Nihon no seikyū-sho o seisei suru ni wa:
    Console.Write("\n\n\u65e5\u672c\u306e\u8acb\u6c42\u66f8\u3092\u751f\u6210\u3059\u308b\u306b\u306f\uff1a\n\t");
    // User command to run an application
    Console.WriteLine(@"c:\invoices\app.exe -j");    
    ```
    
2.  Чтобы убедиться в правильности кода, сравните его со следующим:

    
    ```c#
    Console.WriteLine("Generating invoices for customer \"Contoso Corp\" ...\n");
    Console.WriteLine("Invoice: 1021\t\tComplete!");
    Console.WriteLine("Invoice: 1022\t\tComplete!");
    Console.WriteLine("\nOutput Directory:\t");
    Console.Write(@"c:\invoices");
    
    // To generate Japanese invoices:
    // Nihon no seikyū-sho o seisei suru ni wa:
    Console.Write("\n\n\u65e5\u672c\u306e\u8acb\u6c42\u66f8\u3092\u751f\u6210\u3059\u308b\u306b\u306f\uff1a\n\t");
    // User command to run an application
    Console.WriteLine(@"c:\invoices\app.exe -j");    
    ```
    
3.  Теперь выполните код. В консоли вывода появятся следующие результаты:
   
    ```
    Generating invoices for customer "Contoso Corp" ...
    
    Invoice: 1021            Complete!
    Invoice: 1022            Complete!
    
    Output Directory:
    c:\invoices
    
    日本の請求書を生成するには：
        c:\invoices\app.exe -j    
    ```
    

## Резюме

Вот что вы узнали о форматировании строк литерала до сих пор:

-   Чтобы вставить специальный символ в литеральную строку, например знак табуляции  `\t`, символ переноса строки  `\n`  или двойную кавычку  `\"`, используйте escape-последовательности.
-   Используйте escape-символ для обратной косой черты  `\\`, если необходимо использовать обратную косую черту в других сценариях.
-   Используйте директиву  `@`  для создания буквальных строковых литералов, чтобы сохранить форматирование пробелов и символов обратной косой черты в строке.
-   Используйте  `\u`  и код из четырех символов для представления символов Юникода (UTF-16) в строке.
-   Символы Юникода могут печататься неправильно в зависимости от приложения.


# Упражнение. Объединение строк с помощью объединения строк
Часто приходится объединять данные из множества различных источников, включая литеральные строки и переменные, содержащие текстовые и числовые данные. Здесь вы будете использовать конкатенацию (объединение) нескольких значений в новую строку.

## Что такое конкатенация строк?

Объединение строк — это простое объединение двух или более  `string`  значений в новое  `string`  значение. В отличие от сложения, второе значение добавляется в конец первого значения и т. д. В следующем упражнении вы напишете код для объединения  `string`  значений.

### Объединение литеральной строки и переменной

Чтобы объединить две строки, вы используете  _оператор конкатенации строк_, то есть символ "плюс" (`+`).

1.  Выделите весь код в редакторе .NET и нажмите клавишу  DELETE  или  BACKSPACE, чтобы удалить его.
    
2.  В редакторе кода введите следующий код:
    
    ```c#
    string firstName = "Bob";
    string message = "Hello " + firstName;
    Console.WriteLine(message);    
    ```
    
3.  Теперь выполните код. В консоли вывода появятся следующие результаты:
    
    OutputКопировать
    
    ```
    Hello Bob    
    ```
    
    Обратите внимание на порядок: первая строка  `"Hello "`  находится в новой строке, а значение в переменной  `firstName`  добавляется в конец.
    

### Объединение нескольких переменных и литеральных строк

В одной строке кода можно выполнять несколько операций конкатенации.

1.  Измените код, написанный ранее, следующим образом:
    
    ```c#
    string firstName = "Bob";
    string greeting = "Hello";
    string message = greeting + " " + firstName + "!";
    Console.WriteLine(message);    
    ```
    
    Здесь вы создадите более сложное сообщение, объединяя несколько переменных и литеральных строк.
    
2.  Теперь выполните код. В консоли вывода появятся следующие результаты:
    
    OutputКопировать
    
    ```
    Hello Bob!    
    ```
    

### Избегание промежуточных переменных

На предыдущих шагах вы использовали дополнительную переменную для хранения новой строки, полученной в результате операции объединения. Если у вас нет веских причин, можно (и следует) избегать использования промежуточных переменных, выполняя операцию конкатенации по мере необходимости.

1.  Измените код, написанный ранее, следующим образом:
    
    ```c#
    string firstName = "Bob";
    string greeting = "Hello";
    Console.WriteLine(greeting + " " + firstName + "!");    
    ```
    
2.  Теперь выполните код. Результат в консоли вывода должен быть таким же, даже если вы упростили код:
    
    OutputКопировать
    
    ```
    Hello Bob!    
    ```
    

## Резюме

Вот что вы узнали о сцеплении строк к настоящему времени:

-   Конкатенация строк позволяет объединять строковые литералы и переменные в одну строку.
-   Избегайте создания промежуточных переменных, если их добавление не повлияет на удобочитаемость.


# Упражнение. Объединение строк с помощью интерполяции строк
Хотя конкатенация строк проста и удобна,  _интерполяция строк_  популярнее в ситуациях, когда необходимо объединить множество строковых литералов и переменных в одно отформатированное сообщение.

## Что такое интерполяция строк?

Интерполяция строк объединяет несколько значений в одну литеральную строку с помощью шаблона и  _выражений интерполяции_.  **Выражение интерполяции`{ }` — это переменная, заключенная в символы открывающей и закрывающей фигурных скобок**. Литеральная строка преобразуется в шаблон, если он имеет префикс  `$`.

Иными словами, вместо написания следующей строки кода:

```c#
string message = greeting + " " + firstName + "!";
```

Можно написать более краткую строку кода:


```c#
string message = $"{greeting} {firstName}!";
```

В этом простом примере вы экономите несколько нажатий клавиш. Можно представить, насколько более краткой будет интерполяция строк в более сложных операциях. Более того, многие считают синтаксис интерполяции строк более понятным и удобочитаемым.

В следующем упражнении вы перепишите предыдущие сообщения с помощью интерполяции строк.

### Использование интерполяции строк для объединения строкового литерала и значения переменной

Чтобы выполнить интерполяцию двух строк вместе, создайте литеральную строку и добавьте перед строкой символ  `$`. Литеральная строка должна содержать по крайней мере один набор фигурных скобок  `{}`, и внутри этих символов необходимо указать имя переменной.

1.  Выделите весь код в редакторе .NET и нажмите клавишу  DELETE  или  BACKSPACE, чтобы удалить его.
    
2.  Введите следующий код в редакторе .NET:
    
    ```c#
    string firstName = "Bob";
    string message = $"Hello {firstName}!";
    Console.WriteLine(message);
    
    ```
    
3.  Теперь выполните код. В консоли вывода появятся следующие результаты:
    
   
    ```
    Hello Bob!
    
    ```
    

### Использование интерполяции строк с несколькими переменными и литеральными строками

В одной строке кода можно выполнять несколько операций интерполяции.

1.  Измените код, написанный ранее, следующим образом:
    
    
    ```c#
    int version = 11;
    string updateText = "Update to Windows";
    string message = $"{updateText} {version}";
    Console.WriteLine(message);    
    ```
    
2.  Теперь выполните код. В консоли вывода появятся следующие результаты:
    
    
    ```
    Update to Windows 11    
    ```
    

### Избегайте промежуточных переменных

Как и в предыдущем упражнении, можно исключить временную переменную для хранения сообщения.

1.  Измените код, написанный ранее, следующим образом:
    
    
    ```c#
    int version = 11;
    string updateText = "Update to Windows";
    Console.WriteLine($"{updateText} {version}");    
    ```
    
2.  Теперь выполните код. Результат в консоли вывода должен быть таким же, даже если вы упростили код:
    
    ```
    Update to Windows 11    
    ```
    

### Объединение буквальных литералов и интерполяции строк

Предположим, что в шаблоне необходимо использовать буквальный литерал. Можно одновременно использовать символ  `@`  для префикса буквального литерала и  `$` — символ интерполяции строки.

1.  Удалите код из предыдущих шагов и введите следующий код в редакторе .NET:

    
    ```c#
    string projectName = "First-Project";
    Console.WriteLine($@"C:\Output\{projectName}\Data");    
    ```
    
2.  После выполнения кода вы увидите приведенный ниже результат.
    
    ```
    C:\Output\First-Project\Data    
    ```
    
    В этом примере  `$`  символ позволяет ссылаться на  `projectName`  переменную внутри квадратных скобок, в то время как  `@`  символ позволяет использовать неэкранированные символы  `\`  .
    

## Резюме

Вот что вы узнали о интерполяции строк к настоящему времени:

-   Интерполяция строк улучшает конкатенацию строк за счет уменьшения количества символов, необходимых в некоторых ситуациях.
-   Можно сочетать интерполяцию строк и буквальные литералы, сочетая их символы и используя их в качестве префикса для шаблона строки.


# Выполнение задачи

Проблемы с кодом укрепит полученные знания и помогут вам получить некоторую уверенность, прежде чем продолжить.

В этой задаче вы напечатаете инструкции для конечного пользователя, чтобы сообщить о том, где приложение будет выводить файлы данных. Вы не будете создавать файлы. Вам нужно только отобразить отформатированные инструкции в окне консоли.

Вам предстоит использовать все то, что вы узнали об escape-последовательностях символов, буквальных строках, Юникоде и интерполяции строк, чтобы предоставить инструкции как на английском, так и на русском языке.

### Задача. Форматирование и отображение инструкций

1.  Выделите весь код в редакторе .NET и нажмите клавишу  DELETE  или  BACKSPACE, чтобы удалить его.
    
2.  Начните решать задачу с помощью следующих двух строк кода.
    

```c#
string projectName = "ACME";

string russianMessage = "\u041f\u043e\u0441\u043c\u043e\u0442\u0440\u0435\u0442\u044c \u0440\u0443\u0441\u0441\u043a\u0438\u0439 \u0432\u044b\u0432\u043e\u0434";
```

Переменная  `projectName`  будет использоваться в выходных данных дважды.

Переменная  `russianMessage`  содержит сообщение на русском языке. Эту переменную необходимо использовать в коде, который выводит сообщение.

Вы не можете менять эти две строки кода, но можно добавить код выше и ниже каждой строки. Для формирования нужных выходных данных необходимо использовать эти две строки кода.

1.  Метод или  `Console.Write()`  можно использовать  `Console.WriteLine()`  только дважды.

Иными словами, для выполнения этой задачи можно создать только две инструкции, фактически выводящие текст на печать в консоли. Если необходимо напечатать дополнительные переносы строки или добавить любое форматирование, необходимо использовать все, что вы узнали в этом модуле.

1.  Для формирования выходных данных используйте escape-последовательности символов, буквальные строки, Юникод и интерполяцию строк.

Для выполнения этой задачи код должен формировать следующие выходные данные.


```
View English output:
  c:\Exercise\ACME\data.txt

Посмотреть русский вывод:
  c:\Exercise\ACME\ru-RU\data.txt
```

Обратите внимание на переносы строк, табуляцию и то, как в выходных данных используются две обязательные строки кода.

# Вывод

Ваша цель состояла в том, чтобы написать код, который форматирует строки с помощью специальных символов, таких как двойные кавычки, новые строки, табуляции и другие пробелы, а также символы Юникода. Вы также объединили строки с помощью двух разных методов.

Используя escape-последовательности символов, вы добавили специальные символы в строки литералов с помощью специальных экранируемых последовательностей или с помощью буквальных строк. Вы добавили символы Юникода из других наборов языков, таких как японский кандзи и русский кириллица, в литеральные строки. Вы использовали простое объединение строк с символом + и обновили интерполяцию строк для объединения значений в шаблон строки.

Без возможности форматирования выходных данных вы будете строго ограничены в том, какие типы информации вы можете представить пользователю. Однако теперь вы можете предоставлять пользователям сложные инструкции и отзывы с широким спектром форматирования, символов и языков.

