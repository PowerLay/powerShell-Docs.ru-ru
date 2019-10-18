---
title: Отчеты об ошибках командлетов | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- error records [PowerShell], terminating
- non-terminating errors [PowerShell]
- error records [PowerShell]
- terminating errors [PowerShell]
- error records [PowerShell], non-terminating
ms.assetid: 0b014035-52ea-44cb-ab38-bbe463c5465a
caps.latest.revision: 8
ms.openlocfilehash: 5dfec318438ca139518c596011ac5e56445738ea
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72365923"
---
# <a name="cmdlet-error-reporting"></a>Отчеты об ошибках командлетов

Командлеты должны сообщать об ошибках по-разному в зависимости от того, завершаются ли ошибки ошибками или неустранимыми ошибками. Завершающие ошибки — это ошибки, вызывающие немедленное завершение конвейера, или ошибки, возникающие, если нет причин продолжать обработку. Неустранимые ошибки — это ошибки, сообщающие о текущем состоянии ошибки, но командлет может продолжать обрабатывать входные объекты. В случае неустранимых ошибок пользователь обычно получает извещение о проблеме, но командлет продолжит обрабатывать следующий входной объект.

## <a name="terminating-and-nonterminating-errors"></a>Завершение и неустранимые ошибки

Чтобы определить, является ли условие ошибки завершающим ошибкой или неустранимой ошибкой, можно использовать следующие рекомендации.

- Не мешает ли командлету успешно обрабатывать любые дальнейшие входные объекты? Если это так, это Неустранимая ошибка.

- Условие ошибки, связанное с определенным входным объектом или подмножеством входных объектов? Если да, это Неустранимая ошибка.

- Принимает ли командлет несколько входных объектов, что может привести к успешности обработки другого входного объекта? Если да, это Неустранимая ошибка.

- Командлеты, которые могут принимать несколько входных объектов, должны определить, какие из них завершаются, а какие — нет, даже если конкретная ситуация относится только к одному входному объекту.

- Командлеты могут получать любое количество входных объектов и отправлять любое количество объектов Success или Error перед вызовом завершающего исключения. Между числом полученных входных объектов и количеством отправленных объектов Success и Error не связано никаких отношений.

- Командлеты, которые могут принимать только 0-1 входных объектов и создавать только объекты вывода 0-1, должны обрабатывать ошибки как прерывающие работу и создавать завершающие исключения.

## <a name="reporting-nonterminating-errors"></a>Сообщает о неустранимых ошибках

Отчет о незавершающей ошибке всегда должен быть выполнен в реализации командлета метода [System. Management. Automation. командлет. BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) , метода [System. Management. Automation. командлет. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) или метод [System. Management. Automation. командлет. EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) . Эти типы ошибок выводятся путем вызова метода [System. Management. Automation. командлета. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) , который, в свою очередь, отправляет запись об ошибке в поток ошибок.

## <a name="reporting-terminating-errors"></a>Создание отчетов о прекращении ошибок

Для завершения ошибок выдаются исключения или вызывается метод [System. Management. Automation. командлет. ThrowTerminatingError](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) . Имейте в виду, что командлеты также могут перехватывать и воссоздавать исключения, такие как **OutOfMemory**, однако они не требуют повторных порождения исключений, так как среда выполнения PowerShell также будет перехватывать их.

Можно также определить собственные исключения для проблем, характерных для конкретной ситуации, или добавить дополнительные сведения к существующему исключению с помощью записи об ошибке.

## <a name="error-records"></a>Записи об ошибках

PowerShell описывает неустранимую ошибку в объектах [System. Management. Automation. ерроррекорд](/dotnet/api/System.Management.Automation.ErrorRecord) . Каждый объект предоставляет сведения о категории ошибок, дополнительный целевой объект и сведения о состоянии ошибки.

### <a name="error-identifiers"></a>Идентификаторы ошибок

Идентификатор ошибки представляет собой простую строку, определяющую условие ошибки в командлете.
PowerShell объединяет этот идентификатор с идентификатором командлета, чтобы создать полный идентификатор ошибки, который можно использовать позже при фильтрации потоков ошибок или ошибок ведения журнала, при ответе на определенные ошибки или с другими действиями, специфичными для пользователя.

При указании идентификаторов ошибок следует следовать приведенным ниже рекомендациям.

- Присвойте разные идентификаторы ошибок различным путям кода. Каждый путь кода, вызывающий [System. Management. Automation. командлет. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) или [System. Management. Automation. командлет. ThrowTerminatingError](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) , должен иметь собственный идентификатор ошибки.

- Идентификаторы ошибок должны быть уникальными для типов исключений среды CLR как для завершающих, так и для неустранимых ошибок.

- Не меняйте семантику идентификатора ошибки между версиями командлета или поставщика PowerShell. После установки семантики идентификатора ошибки она должна оставаться постоянной в течение жизненного цикла командлета.

- Для завершения ошибок используйте уникальный идентификатор ошибки для конкретного типа исключения CLR. Если тип исключения изменяется, используйте новый идентификатор ошибки.

- Для неустранимых ошибок используйте конкретный идентификатор ошибки для конкретного входного объекта.

- Выберите текст для идентификатора, который кратко соответствует сообщению об ошибке. Не используйте пробелы или знаки препинания.

- Не создавайте идентификаторы ошибок, которые не воспроизводимы. Например, не создавайте идентификаторы, включающие идентификатор процесса. Идентификаторы ошибок полезны только в том случае, если они соответствуют идентификаторам, которые видят другие пользователи, испытывающие одну и ту же проблему.

### <a name="error-categories"></a>Категории ошибок

Категории ошибок используются для группирования ошибок пользователя. PowerShell определяет эти категории и командлеты, и поставщики PowerShell должны выбирать между ними при создании записи об ошибке.

Описание доступных категорий ошибок см. в описании перечисления [System. Management. Automation. ErrorCategory](/dotnet/api/System.Management.Automation.ErrorCategory) . В общем случае следует избегать использования **ошибок**, **ундефинедеррор**и **Общая ошибка** везде, где это возможно.

Пользователи могут просматривать ошибки на основе категории, когда они устанавливают `$ErrorView` в **категоривиев**.

## <a name="see-also"></a>См. также статью

[Обзор командлетов](./cmdlet-overview.md)

[Типы выходных данных командлета](./types-of-cmdlet-output.md)

[Справочник по Windows PowerShell](../windows-powershell-reference.md)