---
title: Справочник по Windows PowerShell | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Windows PowerShell SDK
ms.assetid: cbba4879-bcac-484a-9906-4bbe2cd1eb33
caps.latest.revision: 11
ms.openlocfilehash: 48b2b2b9ab2a39cf185ed54bcfa99d46562e13b6
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "72366283"
---
# <a name="windows-powershell-reference"></a>Справочник по Windows PowerShell

Windows PowerShell — это Microsoft .NET среда, подключенная к инфраструктуре, разработанная для административной автоматизации. Windows PowerShell предоставляет новый подход к созданию команд, составлению решений и созданию графических средств управления на основе пользовательского интерфейса.

Windows PowerShell позволяет системному администратору автоматизировать администрирование системных ресурсов за счет выполнения команд либо напрямую, либо с помощью сценариев.

## <a name="developer-audience"></a>Аудитория разработчиков

Пакет средств разработки программного обеспечения (SDK) для Windows PowerShell написан для разработчиков команд, которым требуются справочные сведения об API, предоставляемых Windows PowerShell. Разработчики команд используют Windows PowerShell для создания команд и поставщиков, расширяющих задачи, которые могут выполняться Windows PowerShell.

## <a name="windows-powershell-resources"></a>Ресурсы Windows PowerShell

Помимо пакета SDK для Windows PowerShell, дополнительные сведения см. в следующих ресурсах.

[Начало работы с помощью Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell) Общие сведения о Windows PowerShell: язык, командлеты, поставщики и использование объектов.

[Написание модуля Windows PowerShell](./module/writing-a-windows-powershell-module.md) Содержит сведения и примеры для администраторов, разработчиков скриптов и разработчиков командлетов, которым необходимо упаковать и распространить свои решения Windows PowerShell с помощью модулей Windows PowerShell.

[Написание командлета Windows PowerShell](./cmdlet/writing-a-windows-powershell-cmdlet.md) Содержит сведения и примеры кода для руководителей программ, которые разрабатывают командлеты и для разработчиков, реализующих код командлетов.

[Блог группы разработчиков Windows PowerShell](https://blogs.msdn.microsoft.com/PowerShell/) Лучший ресурс для обучения и совместной работы с другими пользователями Windows PowerShell. Прочитайте блог группы разработчиков Windows PowerShell, а затем присоединитесь к форуму пользователей Windows PowerShell (Microsoft. public. Windows. PowerShell). Используйте Windows Live Search для поиска других блогов и материалов по Windows PowerShell. Затем, когда вы разрабатываете свой опыт, вы сможете бесплатно вносить свои идеи.

[Обозреватель модулей PowerShell](/powershell/module/) Содержит последние версии разделов справки по командной строке.

## <a name="class-libraries"></a>Библиотеки классов

[System. Management. Automation.](/dotnet/api/System.Management.Automation) это пространство имен является корневым пространством имен для Windows PowerShell. Он содержит классы, перечисления и интерфейсы, необходимые для реализации пользовательских командлетов. В частности, класс [System. Management. Automation. командлет](/dotnet/api/System.Management.Automation.Cmdlet) является базовым классом, из которого должны быть производными все классы командлетов. Дополнительные сведения о командлетах см. в разделе.

[System. Management. Automation. Provider](/dotnet/api/System.Management.Automation.Provider) . это пространство имен содержит классы, перечисления и интерфейсы, необходимые для реализации поставщика Windows PowerShell. В частности, класс [System. Management. Automation. Provider. кмдлетпровидер](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) является базовым классом, из которого все классы поставщиков Windows PowerShell должны быть производными.

[Microsoft. PowerShell. Commands.](/dotnet/api/Microsoft.PowerShell.Commands) это пространство имен содержит классы для командлетов и поставщиков, реализованных в Windows PowerShell. Аналогичным образом рекомендуется создать *yourname*. Пространство имен Commands для этих командлетов, которые вы реализуете.

[System. Management. Automation. Host](/dotnet/api/System.Management.Automation.Host) . это пространство имен содержит классы, перечисления и интерфейсы, которые командлет использует для определения взаимодействия между пользователем и Windows PowerShell.

[System. Management. Automation. internal](/dotnet/api/System.Management.Automation.Internal) это пространство имен содержит базовые классы, используемые другими классами пространства имен. Например, класс [System. Management. Automation. internal. кмдлетметадатааттрибуте](/dotnet/api/System.Management.Automation.Internal.CmdletMetadataAttribute) является базовым классом для класса [System. Management. Automation. CmdletAttribute](/dotnet/api/System.Management.Automation.CmdletAttribute) .

[System. Management. Automation. пространства](/dotnet/api/System.Management.Automation.Runspaces) имен содержит классы, перечисления и интерфейсы, используемые для создания пространства выполнения Windows PowerShell. В этом контексте пространство выполнения Windows PowerShell — это контекст, в котором один или несколько конвейеров Windows PowerShell вызывают командлеты. То есть командлеты работают в контексте пространства выполнения Windows PowerShell. Дополнительные сведения Абаутвиндовс пространства выполнения PowerShell см. в разделе [пространства выполнения Windows PowerShell](https://msdn.microsoft.com/en-us/a1582cfe-f06d-4aff-adc6-71f49a860ce9).
