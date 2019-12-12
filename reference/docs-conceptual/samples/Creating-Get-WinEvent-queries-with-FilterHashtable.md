---
ms.date: 09/13/2019
title: Создание запросов Get-WinEvent с помощью FilterHashtable
ms.openlocfilehash: 35d18dc894d90e698b38395b79ff4cf395515909
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "73444392"
---
# <a name="creating-get-winevent-queries-with-filterhashtable"></a>Создание запросов Get-WinEvent с помощью FilterHashtable

Чтобы прочитать исходную запись блога **специалистов по сценариям** от 3 июня 2014 г., которая называется Use FilterHashTable to Filter Event Log with PowerShell (Использование FilterHashTable для фильтрации журнала событий с помощью PowerShell), перейдите [сюда](https://devblogs.microsoft.com/scripting/use-filterhashtable-to-filter-event-log-with-powershell/).

Эта статья является выдержкой из исходной записи блога. Здесь показано, как использовать параметр **FilterHashtable** командлета `Get-WinEvent` для фильтрации журналов событий. Использование командлета `Get-WinEvent` PowerShell представляет собой эффективный метод для фильтрации журналов событий и журналов диагностики Windows. Если в запросе `Get-WinEvent` используется параметр **FilterHashtable**, производительность будет более высокой.

При работе с объемными журналами событий отправка объектов по конвейеру команде `Where-Object` не является эффективной. До выхода версии PowerShell 6 для получения данных журнала также использовался командлет `Get-EventLog`. Например, приведенные ниже команды являются неэффективными для фильтрации журналов **Microsoft-Windows-Defrag**:

```powershell
Get-EventLog -LogName Application | Where-Object Source -Match defrag

Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'defrag' }
```

В следующей команде используется хэш-таблица, что повышает производительность:

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='*defrag'
}
```

## <a name="blog-posts-about-enumeration"></a>Записи блога, посвященные перечислению

В этой статье представлены сведения о том, как использовать перечисляемые значения в хэш-таблице. Дополнительные сведения о перечислении см. в записях блога **специалистов по сценариям**. Сведения для создания функции, возвращающей перечисляемые значения, см. в [этой записи блога](https://devblogs.microsoft.com/scripting/hey-scripting-guy-weekend-scripter-enumerations-and-values).
Дополнительные сведения см. в [ряде записей блога специалистов по сценариям, посвященных перечислению](https://devblogs.microsoft.com/scripting/?s=about+enumeration).

## <a name="hash-table-key-value-pairs"></a>Пары "ключ — значение" в хэш-таблице

Для создания эффективных запросов используйте командлет `Get-WinEvent` с параметром **FilterHashtable**.
**FilterHashtable** принимает хэш-таблицу в качестве фильтра для получения конкретных сведений из журналов событий Windows. Хэш-таблица использует пары **ключ — значение**. Дополнительные сведения о хэш-таблицах см. [здесь](/powershell/module/microsoft.powershell.core/about/about_hash_tables).

Если пары **ключ — значение** находятся в одной строке, они должны быть разделены точкой с запятой. Если пары **ключ — значение** находятся в разных строках, точка с запятой не требуется. Например, в этой статье пары **ключ — значение** расположены в разных строках и разделены точкой с запятой.

В этом примере используется несколько пар **ключ — значение** для параметра **FilterHashtable**. Готовый запрос включает в себя значения **LogName**, **ProviderName**, **Keywords**, **ID** и **Level**.

Допустимые пары **ключ — значение** показаны в следующей таблице и включены в документацию для параметра **FilterHashtable**
командлета [Get-WinEvent](/powershell/module/microsoft.powershell.diagnostics/Get-WinEvent).

В следующей таблице приведены имена ключей, типы данных и сведения о том, принимаются ли подстановочные знаки для значения данных.

|    Имя ключа    | Тип данных значения | Принимает ли подстановочные знаки? |
| -------------- | --------------- | ---------------------------- |
| LogName        | `<String[]>`    | Да                          |
| ProviderName   | `<String[]>`    | Да                          |
| Path           | `<String[]>`    | Нет                           |
| Keywords       | `<Long[]>`      | Нет                           |
| Key             | `<Int32[]>`     | Нет                           |
| Level          | `<Int32[]>`     | Нет                           |
| StartTime      | `<DateTime>`    | Нет                           |
| EndTime        | `<DateTime>`    | Нет                           |
| UserID         | `<SID>`         | Нет                           |
| Data           | `<String[]>`    | Нет                           |
| `<named-data>` | `<String[]>`    | Нет                           |

Ключ `<named-data>` представляет именованное поле данных событий. Например, событие Perflib 1008 может содержать следующие данные о событии:

```xml
<EventData>
  <Data Name="Service">BITS</Data>
  <Data Name="Library">C:\Windows\System32\bitsperf.dll</Data>
  <Data Name="Win32Error">2</Data>
</EventData>
```

Эти события можно запросить с помощью следующей команды:

```powershell
Get-WinEvent -FilterHashtable @{LogName='Application'; 'Service'='Bits'}
```

> [!NOTE]
> Возможность создавать запросы `<named-data>` была добавлена в PowerShell 6.

## <a name="building-a-query-with-a-hash-table"></a>Создание запроса с использованием хэш-таблицы

Для проверки результатов и устранения проблем полезно создавать по одной паре **ключ — значение** для хэш-таблицы за раз. Запрос получает данные из журнала **Application**. Хэш-таблица создается в результате запроса `Get-WinEvent –LogName Application`.

Для начала создайте запрос `Get-WinEvent`. Используйте пару **ключ — значение** параметра **FilterHashtable** с ключом **LogName** и значением **Application**.

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
}
```

Продолжайте выполнять сборку хэш-таблицы с использованием ключа **ProviderName**. **ProviderName** — это имя, отображаемое в поле **источника** в средстве **Просмотра событий Windows**. Например, **среда выполнения .NET** на следующем снимке экрана:

![Изображение источников в средстве "Просмотр событий Windows".](./media/creating-get-winEvent-queries-with-filterhashtable/providername.png)

Обновите хэш-таблицу и добавьте пару **ключ — значение** с ключом **ProviderName и значением **.NET Runtime**.

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
}
```

Если запрос должен получить данные из архивных журналов событий, используйте ключ **Path**. Значение **Path** указывает полный путь к файлу журнала. Дополнительные сведения см. в записи блога **специалистов по сценариям** [Use PowerShell to Parse Saved Event Logs for Errors](https://devblogs.microsoft.com/scripting/use-powershell-to-parse-saved-event-logs-for-errors) (Анализ сохраненных журналов событий на наличие ошибок с помощью PowerShell).

## <a name="using-enumerated-values-in-a-hash-table"></a>Использование перечисляемых значений в хэш-таблице

**Keywords** — следующий ключ в хэш-таблице. Тип данных **Keywords** представляет собой массив типа значения `[long]`, который содержит большое число. Используйте следующую команду, чтобы найти максимальное значение `[long]`:

```powershell
[long]::MaxValue
```

```Output
9223372036854775807
```

Для ключа **Keywords** PowerShell использует число, а не строку, такую как **Security**. В средстве **Просмотр событий Windows** значения **Keywords** отображаются в виде строк, но они являются перечисляемыми значениями. Если вы используете ключ **Keywords** со строковым значением, в хэш-таблице отображается сообщение об ошибке.

Откройте средство **Просмотр событий Windows** и в окне **Действия** щелкните **Фильтровать текущий журнал**.
В раскрывающемся меню **Ключевые слова** отображаются доступные ключевые слова, как показано на следующем снимке экрана:

![Изображение ключевых слов средства "Просмотр событий Windows".](./media/creating-get-winEvent-queries-with-filterhashtable/keywords.png)

Используйте следующую команду для отображения имен свойств `StandardEventKeywords`.

```powershell
[System.Diagnostics.Eventing.Reader.StandardEventKeywords] | Get-Member -Static -MemberType Property
```

```Output
   TypeName: System.Diagnostics.Eventing.Reader.StandardEventKeywords
Name             MemberType Definition
—-             ———- ———-
AuditFailure     Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
AuditSuccess     Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
CorrelationHint  Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
CorrelationHint2 Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
EventLogClassic  Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
None             Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
ResponseTime     Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
Sqm              Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
WdiContext       Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
WdiDiagnostic    Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
```

Перечисляемые значения описаны в **.NET Framework**. Дополнительные сведения см. в разделе о команде перечисления [StandardEventKeywords](/dotnet/api/system.diagnostics.eventing.reader.standardeventkeywords?redirectedfrom=MSDN&view=netframework-4.7.2).

Имена **ключевых слов** и перечисляемые значения выглядят следующим образом:

| Name             |  Значение            |
| ---------------- | ------------------|
| AuditFailure     | 4503599627370496  |
| AuditSuccess     | 9007199254740992  |
| CorrelationHint2 | 18014398509481984 |
| EventLogClassic  | 36028797018963968 |
| Sqm              | 2251799813685248  |
| WdiDiagnostic    | 1125899906842624  |
| WdiContext       | 562949953421312   |
| ResponseTime     | 281474976710656   |
| Нет             | 0                 |

Обновите хэш-таблицу и добавьте пару **ключ — значение** с ключом **Keywords** и значением перечисления **EventLogClassic** **36028797018963968** .

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
}
```

### <a name="keywords-static-property-value-optional"></a>Значение статического свойства Keywords (необязательно)

Значение ключа **Keywords** перечисляется, но имя статического свойства можно использовать в запросе с хэш-таблицей.
Вместо того чтобы использовать возвращаемую строку, имя свойства должно преобразовываться в значение с применением свойства **Value__** .

Например, следующий скрипт использует свойство **Value__** .

```powershell
$C = [System.Diagnostics.Eventing.Reader.StandardEventKeywords]::EventLogClassic
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=$C.Value__
}
```

## <a name="filtering-by-event-id"></a>Фильтрация по идентификатору события

Для получения более конкретных данных результаты запроса можно отфильтровать по **идентификатору события**. **Идентификатор события** указывается в хэш-таблице как ключ **ID**, а значение соответствует конкретному **идентификатору события**. В средстве **Просмотр событий Windows** отображается **идентификатор события**. В этом примере используется **идентификатор события 1023**.

Обновите хэш-таблицу и добавьте пару **ключ — значение** с ключом **ID** и значением **1023**.

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
   ID=1023
}
```

## <a name="filtering-by-level"></a>Фильтрация по уровню

Чтобы дополнительно уточнить результаты и включить только события, которые являются ошибками, используйте ключ **Level**.
В средстве **Просмотр событий Windows** значения **Level** отображаются в виде строковых значений, но они являются перечисляемыми значениями. Если вы используете ключ **Level** со строковым значением, в хэш-таблице отображается сообщение об ошибке.

У ключа **Level** есть такие значения, как **Error** (Ошибка), **Warning** (Предупреждение) или **Informational** (Информация). Используйте следующую команду для отображения имен свойств `StandardEventLevel`.

```powershell
[System.Diagnostics.Eventing.Reader.StandardEventLevel] | Get-Member -Static -MemberType Property
```

```Output
   TypeName: System.Diagnostics.Eventing.Reader.StandardEventLevel

Name          MemberType Definition
----          ---------- ----------
Critical      Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Critical {get;}
Error         Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Error {get;}
Informational Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Informational {get;}
LogAlways     Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel LogAlways {get;}
Verbose       Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Verbose {get;}
Warning       Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Warning {get;}
```

Перечисляемые значения описаны в **.NET Framework**. Дополнительные сведения см. в разделе о команде перечисления [StandardEventLevel](/dotnet/api/system.diagnostics.eventing.reader.standardeventlevel?redirectedfrom=MSDN&view=netframework-4.7.2).

Имена ключа **Level** и перечисляемые значения выглядят следующим образом:

| Name           | Значение |
| -------------- | ----- |
| Verbose        |   5   |
| Informational  |   4   |
| Предупреждение        |   3   |
| Ошибка          |   2   |
| Critical       |   1   |
| LogAlways      |   0   |

Хэш-таблица для готового запроса содержит ключ **Level** и его значение — **2**.

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
   ID=1023
   Level=2
}
```

### <a name="level-static-property-in-enumeration-optional"></a>Статическое свойство уровня в перечислении (необязательно)

Значение ключа **Level** перечисляется, но имя статического свойства можно использовать в запросе к хэш-таблице.
Вместо того чтобы использовать возвращаемую строку, имя свойства должно преобразовываться в значение с применением свойства **Value__** .

Например, следующий скрипт использует свойство **Value__** .

```powershell
$C = [System.Diagnostics.Eventing.Reader.StandardEventLevel]::Informational
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
   ID=1023
   Level=$C.Value__
}
```
