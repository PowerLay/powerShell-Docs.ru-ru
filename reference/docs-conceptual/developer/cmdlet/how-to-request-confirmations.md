---
title: Как запросить подтверждения | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f24f77d5-e224-4b62-b128-535e045d333e
caps.latest.revision: 9
ms.openlocfilehash: 19e96b612a8778d82cdbafb528a7ffeb01f15f99
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72369683"
---
# <a name="how-to-request-confirmations"></a><span data-ttu-id="37617-102">Как запросить подтверждение</span><span class="sxs-lookup"><span data-stu-id="37617-102">How to Request Confirmations</span></span>

<span data-ttu-id="37617-103">В этом примере показано, как вызывать методы [System. Management. Automation. командлет. ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) и [System. Management. Automation. командлет. ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) для запроса подтверждения от пользователя до выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="37617-103">This example shows how to call the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) methods to request confirmations from the user before an action is taken.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37617-104">Дополнительные сведения о том, как Windows PowerShell обрабатывает эти запросы, см. в разделе [запрос подтверждения](./requesting-confirmation-from-cmdlets.md).</span><span class="sxs-lookup"><span data-stu-id="37617-104">For more information about how Windows PowerShell handles these requests, see [Requesting Confirmation](./requesting-confirmation-from-cmdlets.md).</span></span>

## <a name="to-request-confirmation"></a><span data-ttu-id="37617-105">Запрос подтверждения</span><span class="sxs-lookup"><span data-stu-id="37617-105">To request confirmation</span></span>

1. <span data-ttu-id="37617-106">Убедитесь, что параметру `SupportsShouldProcess` атрибута командлет присвоено значение `true`.</span><span class="sxs-lookup"><span data-stu-id="37617-106">Ensure that the `SupportsShouldProcess` parameter of the Cmdlet attribute is set to `true`.</span></span> <span data-ttu-id="37617-107">(Для функций это параметр атрибута CmdletBinding.)</span><span class="sxs-lookup"><span data-stu-id="37617-107">(For functions this is a parameter of the CmdletBinding attribute.)</span></span>

    ```csharp
    [Cmdlet(VerbsDiagnostic.Test, "RequestConfirmationTemplate1",
            SupportsShouldProcess = true)]
    ```

2. <span data-ttu-id="37617-108">Добавьте в командлет параметр `Force`, чтобы пользователь мог переопределить запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="37617-108">Add a `Force` parameter to your cmdlet so that the user can override a confirmation request.</span></span>

    ```csharp
    [Parameter()]
    public SwitchParameter Force
    {
      get { return force; }
      set { force = value; }
    }
    private bool force;
    ```

3. <span data-ttu-id="37617-109">Добавьте инструкцию `if`, которая использует возвращаемое значение метода [System. Management. Automation. командлет. ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) , чтобы определить, вызывается ли метод [System. Management. Automation. командлет. ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) .</span><span class="sxs-lookup"><span data-stu-id="37617-109">Add an `if` statement that uses the return value of the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) method to determine if the [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) method is called.</span></span>

4. <span data-ttu-id="37617-110">Добавьте второй оператор `if`, использующий возвращаемое значение метода [System. Management. Automation. командлет. ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) и значение параметра `Force`, чтобы определить, следует ли выполнять операцию.</span><span class="sxs-lookup"><span data-stu-id="37617-110">Add a second `if` statement that uses the return value of the [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) method and the value of the `Force` parameter to determine whether the operation should be performed.</span></span>

## <a name="example"></a><span data-ttu-id="37617-111">Пример</span><span class="sxs-lookup"><span data-stu-id="37617-111">Example</span></span>

<span data-ttu-id="37617-112">В следующем примере кода методы [System. Management. Automation. командлет. ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) и [System. Management. Automation. командлет. ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) вызываются из переопределения [метода Метод System. Management. Automation. командлет. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) .</span><span class="sxs-lookup"><span data-stu-id="37617-112">In the following code example, the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) methods are called from within the override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span> <span data-ttu-id="37617-113">Однако эти методы также можно вызывать из других методов обработки ввода.</span><span class="sxs-lookup"><span data-stu-id="37617-113">However, you can also call these methods from the other input processing methods.</span></span>

```csharp
protected override void ProcessRecord()
{
  if (ShouldProcess("ShouldProcess target"))
  {
    if (Force || ShouldContinue("", ""))
    {
      // Add code that performs the operation.
    }
  }
}
```

## <a name="see-also"></a><span data-ttu-id="37617-114">См. также:</span><span class="sxs-lookup"><span data-stu-id="37617-114">See Also</span></span>

[<span data-ttu-id="37617-115">Запись командлета Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="37617-115">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)