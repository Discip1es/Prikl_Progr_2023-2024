# Шаблон консольного приложения C# создает операторы верхнего уровня

Начиная с .NET версии 6, шаблон проекта для новых консольных приложений C# создает следующий код в файле _Program.cs_ :
```cs
// See https://aka.ms/new-console-template for more information 
Console.WriteLine("Hello, World!");
```
В новых выходных данных используются последние функции C#, упрощающие код, который необходимо написать для программы. Для .NET 5 и более ранних версий шаблон консольного приложения создает следующий код:

```cs
using System;

namespace MyApp // Note: actual namespace depends on the project name.
{
    internal class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```
Эти две формы представляют одну и ту же программу. Оба значения допустимы в C# 10.0. При использовании более новой версии необходимо только написать текст метода  `Main`. Компилятор синтезирует  `Program`  класс с методом  `Main`  и помещает все операторы верхнего уровня в этот  `Main`  метод. Вам не нужно включать другие элементы программы, компилятор создаст их автоматически. Дополнительные сведения о коде, который компилятор создает при использовании операторов верхнего уровня, см. в статье об  [операторах верхнего уровня](https://learn.microsoft.com/ru-ru/dotnet/csharp/fundamentals/program-structure/top-level-statements)  в разделе Основы руководства по C#.

У вас есть два варианта работы с руководствами, которые еще не были обновлены для использования .NET более 6 шаблонов:

-   Используйте новый стиль программы, добавляя новые операторы верхнего уровня по мере добавления компонентов.
-   Преобразование нового стиля программы в старый с помощью класса  `Program`  и метода  `Main`.

Если вы хотите использовать старые шаблоны, см. раздел  [Использование старого стиля программы](https://learn.microsoft.com/ru-ru/dotnet/core/tutorials/top-level-templates#use-the-old-program-style)  далее в этой статье.

## Использовать новый стиль программы

Функции, упрощающие новую программу, — это  _операторы верхнего уровня_,  _глобальные директивы  `using`_  и  _неявные директивы  `using`_  .

Термин  [_операторы верхнего уровня_](https://learn.microsoft.com/ru-ru/dotnet/csharp/fundamentals/program-structure/top-level-statements)  означает, что компилятор создает элементы класса и метода для программы main. Класс и  `Main`  метод, созданные компилятором, объявляются в глобальном пространстве имен. Вы можете взглянуть на код для нового приложения и предположить, что оно содержит инструкции внутри метода, созданного  `Main`  более ранними шаблонами, но в глобальном пространстве имен.

В программу можно добавить дополнительные операторы, так же как и дополнительные операторы в метод  `Main`  в традиционном стиле. Вы можете  [получить доступ (  `args`  аргументы командной строки),](https://learn.microsoft.com/ru-ru/dotnet/csharp/fundamentals/program-structure/top-level-statements#args)[использовать  `await`](https://learn.microsoft.com/ru-ru/dotnet/csharp/fundamentals/program-structure/top-level-statements#await)и  [задать код выхода](https://learn.microsoft.com/ru-ru/dotnet/csharp/fundamentals/program-structure/top-level-statements#exit-code-for-the-process). Можно даже добавлять функции. Они создаются как локальные функции, вложенные в созданный метод  `Main`. Локальные функции не могут включать модификаторы доступа (например,  `public`  или  `protected`).

Операторы верхнего уровня и  [неявные директивы  `using`](https://learn.microsoft.com/ru-ru/dotnet/core/tutorials/top-level-templates#implicit-using-directives)  упрощают код вашего приложения. Для изучения существующего учебника добавьте новые операторы в файл  _Program.cs_, созданный шаблоном. Вы можете представить, что написанные вами операторы находятся между открывающей и закрывающей фигурными скобками в методе  `Main`  в инструкциях учебника.

Если вы предпочитаете использовать старый формат, скопируйте код из второго примера, приведенного в этой статье, и продолжайте работу с учебником.

Дополнительные сведения см. в руководстве  [Операторы верхнего уровня](https://learn.microsoft.com/ru-ru/dotnet/csharp/whats-new/tutorials/top-level-statements).

[](https://learn.microsoft.com/ru-ru/dotnet/core/tutorials/top-level-templates#implicit-using-directives)

## Неявные директивы  `using`

Термин  _неявные  `using`  директивы_  означает, что компилятор автоматически добавляет набор  [`using`  директив](https://learn.microsoft.com/ru-ru/dotnet/csharp/language-reference/keywords/using-directive)  на основе типа проекта. Для консольных приложений следующие директивы неявно включаются в приложение:

-   `using System;`
-   `using System.IO;`
-   `using System.Collections.Generic;`
-   `using System.Linq;`
-   `using System.Net.Http;`
-   `using System.Threading;`
-   `using System.Threading.Tasks;`

Другие типы приложений включают в себя дополнительные пространства имен, общие для этих типов приложений.

Если вам нужны директивы  `using`, которые не включены неявно, вы можете добавить их в файл  _.cs_, содержащий операторы верхнего уровня, или другие файлы  _.cs_. Для директив  `using`, которые вам нужны во всех файлах  _.cs_  в приложении, используйте  [глобальные директивы  `using`](https://learn.microsoft.com/ru-ru/dotnet/core/tutorials/top-level-templates#global-using-directives).

[](https://learn.microsoft.com/ru-ru/dotnet/core/tutorials/top-level-templates#disable-implicit-using-directives)

### Отключение неявных директив  `using`

Если вы хотите удалить это поведение и вручную управлять всеми пространствами имен в проекте, добавьте  [`<ImplicitUsings>disable</ImplicitUsings>`](https://learn.microsoft.com/ru-ru/dotnet/core/project-sdk/msbuild-props#implicitusings)  в файл проекта в элементе  `<PropertyGroup>`  , как показано в следующем примере:
```xml
<Project Sdk="Microsoft.NET.Sdk">  
	<PropertyGroup> 
		... 
		<ImplicitUsings>disable</ImplicitUsings>  
	</PropertyGroup>  
</Project>
```
## Глобальные директивы  `using`

_Глобальная директива  `using`_  импортирует пространство имен для всего приложения, а не отдельного файла. Эти глобальные директивы можно добавить, включив элемент  [`<Using>`](https://learn.microsoft.com/ru-ru/dotnet/core/project-sdk/msbuild-props#using)  в файл проекта или директиву  `global using`  в файл кода.

Вы также можете добавить  [`<Using>`](https://learn.microsoft.com/ru-ru/dotnet/core/project-sdk/msbuild-props#using)  элемент с атрибутом  `Remove`  в файл проекта, чтобы удалить определенную  [неявную  `using`  директиву](https://learn.microsoft.com/ru-ru/dotnet/core/tutorials/top-level-templates#implicit-using-directives). Например, если функция неявных  `using`  директив включена с  [`<ImplicitUsings>enable</ImplicitUsings>`](https://learn.microsoft.com/ru-ru/dotnet/core/project-sdk/msbuild-props#implicitusings)помощью , при добавлении  `System.Net.Http`  следующего  `<Using>`  элемента пространство имен удаляется из неявно импортированных пространств имен:
```xml
<ItemGroup>  
	<Using Remove="System.Net.Http" />  
</ItemGroup>
```
## Использование старого стиля программы

Начиная с .NET пакета SDK 6.0.300, шаблон  `console`  имеет параметр  `--use-program-main`  . Используйте его для создания консольного проекта, который не использует операторы верхнего уровня и имеет  `Main`  метод .
```cmd
dotnet  new console --use-program-main
```
`Program.cs` Созданный объект выглядит следующим образом:
```cs
namespace  MyProject; 
class  Program 
{ 
	static void Main(string[] args) 
		{ 
			Console.WriteLine("Hello, World!"); 
		} 
}
```
### Использование старого стиля программы в Visual Studio

1.  При создании нового проекта вы перейдете на страницу настройки  **Дополнительные сведения**. На этой странице установите флажок  **Не использовать операторы верхнего уровня**  проверка.
    
    ![Visual Studio не использует операторы верхнего уровня проверка box](https://learn.microsoft.com/ru-ru/dotnet/core/tutorials/media/top-level-templates/vs-additional-information.png)
    
2.  После создания проекта содержимое  `Program.cs`  выглядит следующим образом:
      
    ```cs
    namespace MyProject;
    class Program
    {
      static void Main(string[] args)
      {
        Console.WriteLine("Hello, World!");
      }
    }
    ```
 Visual Studio сохраняет значение параметров при следующем создании проекта на основе того же шаблона, поэтому по умолчанию при создании проекта консольного приложения в следующий раз будет установлен флажок "Не использовать операторы верхнего уровня" проверка. Содержимое  `Program.cs`  файла может отличаться в соответствии со стилем кода, определенным в глобальных параметрах текстового редактора  `EditorConfig`  Visual Studio или в файле.

Дополнительные сведения см. в  [разделах Создание переносимых настраиваемых параметров редактора с помощью EditorConfig](https://learn.microsoft.com/ru-ru/visualstudio/ide/create-portable-custom-editor-options)  и  [Параметры, Текстовый редактор, C#, Дополнительно](https://learn.microsoft.com/ru-ru/visualstudio/ide/reference/options-text-editor-csharp-advanced).