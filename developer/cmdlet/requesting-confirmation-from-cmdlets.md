---
title: Запрос на подтверждение из командлетов | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ConfirmImpact [PowerShell Programmer's Guide], described
- ShouldContinue [PowerShell Programmer's Guide], described
- user feedback [PowerShell Programmer's Guide], requesting
- ShouldProcess [PowerShell Programmer's Guide], described
- ConfirmPreference [PowerShell Programmer's Guide], described
ms.assetid: 37d6e87f-57b7-40bd-b645-392cf0b6e88e
caps.latest.revision: 13
ms.openlocfilehash: ec441831f5e3231a44c9875d1b6d2bf6280a6965
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56853400"
---
# <a name="requesting-confirmation-from-cmdlets"></a><span data-ttu-id="4a8f7-102">Запрос на подтверждение от командлетов</span><span class="sxs-lookup"><span data-stu-id="4a8f7-102">Requesting Confirmation from Cmdlets</span></span>

<span data-ttu-id="4a8f7-103">Командлеты следует запрашивать подтверждение, когда они будут внесены изменения в системе за пределами среды Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-103">Cmdlets should request confirmation when they are about to make a change to the system that is outside of the Windows PowerShell environment.</span></span> <span data-ttu-id="4a8f7-104">Например если командлет является добавление учетной записи пользователя или остановить процесс, командлет должна требовать подтверждения от пользователя перед началом.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-104">For example, if a cmdlet is about to add a user account or stop a process, the cmdlet should require confirmation from the user before it proceeds.</span></span> <span data-ttu-id="4a8f7-105">Напротив Если командлет является изменением переменной Windows PowerShell, командлет не требует подтверждения.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-105">In contrast, if a cmdlet is about to change a Windows PowerShell variable, the cmdlet does not need to require confirmation.</span></span>

<span data-ttu-id="4a8f7-106">Чтобы сделать запрос на подтверждение, необходимо указать командлет, он поддерживает запросы на подтверждение, что он должен вызвать [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) и [ System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) (необязательно) методы, чтобы отобразить сообщение с подтверждением запроса.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-106">In order to make a confirmation request, the cmdlet must indicate that it supports confirmation requests, and it must call the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) (optional) methods to display a confirmation request message.</span></span>

## <a name="supporting-confirmation-requests"></a><span data-ttu-id="4a8f7-107">Поддержка запросов подтверждения</span><span class="sxs-lookup"><span data-stu-id="4a8f7-107">Supporting Confirmation Requests</span></span>

<span data-ttu-id="4a8f7-108">Для поддержки запросов подтверждения, необходимо задать командлет `SupportsShouldProcess` параметр атрибута командлет, чтобы `true`.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-108">To support confirmation requests, the cmdlet must set the `SupportsShouldProcess` parameter of the Cmdlet attribute to `true`.</span></span> <span data-ttu-id="4a8f7-109">Это позволяет `Confirm` и `WhatIf` параметры командлета, предоставляемые Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-109">This enables the `Confirm` and `WhatIf` cmdlet parameters that are provided by Windows PowerShell.</span></span> <span data-ttu-id="4a8f7-110">`Confirm` Параметр позволяет пользователю управлять ли отображается запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-110">The `Confirm` parameter allows the user to control whether the confirmation request is displayed.</span></span> <span data-ttu-id="4a8f7-111">`WhatIf` Параметр позволяет пользователю определить, следует ли командлет выводит сообщение, или выполнение его действия.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-111">The `WhatIf` parameter allows the user to determine whether the cmdlet should display a message or perform its action.</span></span> <span data-ttu-id="4a8f7-112">Не добавляйте вручную `Confirm` и `WhatIf` параметров командлета.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-112">Do not manually add the `Confirm` and `WhatIf` parameters to a cmdlet.</span></span>

<span data-ttu-id="4a8f7-113">Следующий пример показывает объявление атрибута командлет, которая поддерживает запросы подтверждения.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-113">The following example shows a Cmdlet attribute declaration that supports confirmation requests.</span></span>

```csharp
[Cmdlet(VerbsDiagnostic.Test, "RequestConfirmationTemplate1",
        SupportsShouldProcess = true)]
```

## <a name="calling-the-confirmation-request-methods"></a><span data-ttu-id="4a8f7-114">Вызов методов запроса подтверждения</span><span class="sxs-lookup"><span data-stu-id="4a8f7-114">Calling the Confirmation request methods</span></span>

<span data-ttu-id="4a8f7-115">В коде командлета, вызов [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) метод перед выполнением операции, изменений в системе.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-115">In the cmdlet code, call the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) method before the operation that changes the system is performed.</span></span> <span data-ttu-id="4a8f7-116">Создать командлет, поэтому, если вызов возвращает значение `false`, эта операция не выполнена, и командлет обрабатывает следующей операции.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-116">Design the cmdlet so that if the call returns a value of `false`, the operation is not performed, and the cmdlet processes the next operation.</span></span>

## <a name="calling-the-shouldcontinue-method"></a><span data-ttu-id="4a8f7-117">Вызов метода ShouldContinue</span><span class="sxs-lookup"><span data-stu-id="4a8f7-117">Calling the ShouldContinue Method</span></span>

<span data-ttu-id="4a8f7-118">Большинство командлетов запросить подтверждение только с помощью [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) метод.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-118">Most cmdlets request confirmation using only the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) method.</span></span> <span data-ttu-id="4a8f7-119">Однако в некоторых случаях могут потребовать дополнительного подтверждения.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-119">However, some cases might require additional confirmation.</span></span> <span data-ttu-id="4a8f7-120">В этих случаях дополнить [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) вызывать с помощью вызова [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) метод.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-120">For these cases, supplement the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) call with a call to the [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) method.</span></span> <span data-ttu-id="4a8f7-121">Это позволяет командлета или поставщика, чтобы более точно управлять областью **Да для всех** ответ на запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-121">This allows the cmdlet or provider to more finely control the scope of the **Yes to all** response to the confirmation prompt.</span></span>

<span data-ttu-id="4a8f7-122">Если командлет вызывает [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) метод, командлет должен также содержать `Force` параметр-переключатель.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-122">If a cmdlet calls the [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) method, the cmdlet must also provide a `Force` switch parameter.</span></span> <span data-ttu-id="4a8f7-123">Если пользователь указывает `Force` когда пользователь вызывает командлет, командлет должен по-прежнему вызывать [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess), но его нужно пропустить вызов [ System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).</span><span class="sxs-lookup"><span data-stu-id="4a8f7-123">If the user specifies `Force` when the user invokes the cmdlet, the cmdlet should still call [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess), but it should bypass the call to [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).</span></span>

<span data-ttu-id="4a8f7-124">[System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) приведет к возникновению исключения при вызове из Неинтерактивный режим среды где пользователь не смогут получить уведомления.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-124">[System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) will throw an exception when it is called from a non-interactive environment where the user cannot be prompted.</span></span> <span data-ttu-id="4a8f7-125">Добавление `Force` параметр гарантирует, что при вызове в среде с неинтерактивной по-прежнему может выполняться команда.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-125">Adding a `Force` parameter ensures that the command can still be performed when it is invoked in a non-interactive environment.</span></span>

<span data-ttu-id="4a8f7-126">В следующем примере показан вызов [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) и [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).</span><span class="sxs-lookup"><span data-stu-id="4a8f7-126">The following example shows how to call [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).</span></span>

```csharp
if (ShouldProcess (...) )
{
  if (Force || ShouldContinue(...))
  {
     // Add code that performs the operation.
  }
}
```

<span data-ttu-id="4a8f7-127">Поведение [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) вызов может изменяться в зависимости от среды, в котором вызывается командлет.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-127">The behavior of a [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) call can vary depending on the environment in which the cmdlet is invoked.</span></span> <span data-ttu-id="4a8f7-128">С помощью предыдущего руководства помогут убедиться, что командлет работает согласованно с другими командлетами, независимо от того, хост-среды.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-128">Using the previous guidelines will help ensure that the cmdlet behaves consistently with other cmdlets, regardless of the host environment.</span></span>

<span data-ttu-id="4a8f7-129">Пример вызова [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) метод, см. в разделе [как запросить подтверждения](./how-to-request-confirmations.md).</span><span class="sxs-lookup"><span data-stu-id="4a8f7-129">For an example of calling the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) method, see [How to Request Confirmations](./how-to-request-confirmations.md).</span></span>

## <a name="specify-the-impact-level"></a><span data-ttu-id="4a8f7-130">Укажите уровень влияния</span><span class="sxs-lookup"><span data-stu-id="4a8f7-130">Specify the Impact Level</span></span>

<span data-ttu-id="4a8f7-131">При создании командлета, укажите уровень влияния (серьезность) изменения.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-131">When you create the cmdlet, specify the impact level (the severity) of the change.</span></span> <span data-ttu-id="4a8f7-132">Чтобы сделать это, установите для параметра `ConfirmImpact` параметра атрибута командлет на высокий, средний или низкий.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-132">To do this, set the value of the `ConfirmImpact` parameter of the Cmdlet attribute to High, Medium, or Low.</span></span> <span data-ttu-id="4a8f7-133">Можно указать значение для `ConfirmImpact` только также указывая `SupportsShouldProcess` параметра командлета.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-133">You can specify a value for `ConfirmImpact` only when you also specify the `SupportsShouldProcess` parameter for the cmdlet.</span></span>

<span data-ttu-id="4a8f7-134">Для большинства командлетов, нет необходимости явно указывать `ConfirmImpact`.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-134">For most cmdlets, you do not have to explicitly specify `ConfirmImpact`.</span></span>  <span data-ttu-id="4a8f7-135">Вместо этого используйте параметр по умолчанию параметра, Medium.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-135">Instead, use the default setting of the parameter, which is Medium.</span></span> <span data-ttu-id="4a8f7-136">Если задать `ConfirmImpact` высокий приоритет, операция будет подтвержден по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-136">If you set `ConfirmImpact` to High, the operation will be confirmed by default.</span></span> <span data-ttu-id="4a8f7-137">Зарезервируйте этот параметр для действий с высокой может нарушить работу системы, например переформатирование тома жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-137">Reserve this setting for highly disruptive actions, such as reformatting a hard-disk volume.</span></span>

## <a name="calling-non-confirmation-methods"></a><span data-ttu-id="4a8f7-138">Вызов методов без подтверждения</span><span class="sxs-lookup"><span data-stu-id="4a8f7-138">Calling Non-Confirmation Methods</span></span>

<span data-ttu-id="4a8f7-139">Если командлет или поставщика необходимо отправить сообщение, но не запросит подтверждение, оно может вызвать следующие три метода.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-139">If the cmdlet or provider must send a message but not request confirmation, it can call the following three methods.</span></span> <span data-ttu-id="4a8f7-140">Избегайте использования [System.Management.Automation.Cmdlet.Writeobject\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) метод для отправки сообщений из этих типов, так как [System.Management.Automation.Cmdlet.Writeobject\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) обычные выходные данные с обычной выходные данные командлета или поставщика услуг, что затрудняет написание скрипта.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-140">Avoid using the [System.Management.Automation.Cmdlet.Writeobject\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) method to send messages of these types because [System.Management.Automation.Cmdlet.Writeobject\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) output is intermingled with the normal output of your cmdlet or provider, which makes script writing difficult.</span></span>

- <span data-ttu-id="4a8f7-141">Чтобы предупредить пользователя и продолжить операцию, можно вызвать командлет или поставщика [System.Management.Automation.Cmdlet.Writewarning\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning) метод.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-141">To caution the user and continue with the operation, the cmdlet or provider can call the [System.Management.Automation.Cmdlet.Writewarning\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning) method.</span></span>

- <span data-ttu-id="4a8f7-142">Для предоставления дополнительных сведений, пользователя можно получить с помощью `Verbose` параметр, командлет или поставщика можно вызвать [System.Management.Automation.Cmdlet.Writeverbose\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) метод.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-142">To provide additional information that the user can retrieve using the `Verbose` parameter, the cmdlet or provider can call the [System.Management.Automation.Cmdlet.Writeverbose\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) method.</span></span>

- <span data-ttu-id="4a8f7-143">Для предоставления сведений о отладки на уровне, для других разработчиков или технической поддержки, можно вызвать командлет или поставщика [System.Management.Automation.Cmdlet.Writedebug\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) метод.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-143">To provide debugging-level detail for other developers or for product support, the cmdlet or provider can call the [System.Management.Automation.Cmdlet.Writedebug\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) method.</span></span> <span data-ttu-id="4a8f7-144">Пользователь может получить эти сведения с помощью `Debug` параметра.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-144">The user can retrieve this information using the `Debug` parameter.</span></span>

<span data-ttu-id="4a8f7-145">Командлеты и поставщики первый вызов следующих методов запросит подтверждение, перед тем как пытаться выполнить операцию, которая изменяет системе за пределами Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4a8f7-145">Cmdlets and providers first call the following methods to request confirmation before they attempt to perform an operation that changes a system outside of Windows PowerShell:</span></span>

- [<span data-ttu-id="4a8f7-146">System.Management.Automation.Cmdlet.Shouldprocess</span><span class="sxs-lookup"><span data-stu-id="4a8f7-146">System.Management.Automation.Cmdlet.Shouldprocess</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess)

- [<span data-ttu-id="4a8f7-147">System.Management.Automation.Provider.Cmdletprovider.Shouldprocess</span><span class="sxs-lookup"><span data-stu-id="4a8f7-147">System.Management.Automation.Provider.Cmdletprovider.Shouldprocess</span></span>](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess)

<span data-ttu-id="4a8f7-148">Это делается посредством вызова [System.Management.Automation.Cmdlet.Shouldprocess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) метод, который предлагает пользователю подтвердить операцию, в зависимости от того, как пользователь вызывает команду.</span><span class="sxs-lookup"><span data-stu-id="4a8f7-148">They do so by calling the [System.Management.Automation.Cmdlet.Shouldprocess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) method, which prompts the user to confirm the operation based on how the user invoked the command.</span></span>

## <a name="see-also"></a><span data-ttu-id="4a8f7-149">См. также</span><span class="sxs-lookup"><span data-stu-id="4a8f7-149">See Also</span></span>

[<span data-ttu-id="4a8f7-150">Запись командлета Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a8f7-150">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)