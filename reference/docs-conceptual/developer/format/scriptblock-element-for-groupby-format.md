---
title: Элемент ScriptBlock для GroupBy (Format) | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 30183927-6f0e-4717-b6f5-f07a6e134cfb
caps.latest.revision: 6
ms.openlocfilehash: 37a297228eb33ff75daf94a12635d42b52c6cc9f
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72364933"
---
# <a name="scriptblock-element-for-groupby-format"></a><span data-ttu-id="2943f-102">Элемент ScriptBlock для элемента GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="2943f-102">ScriptBlock Element for GroupBy (Format)</span></span>

<span data-ttu-id="2943f-103">Задает скрипт, запускающий новую группу при изменении ее значения.</span><span class="sxs-lookup"><span data-stu-id="2943f-103">Specifies the script that starts a new group whenever its value changes.</span></span>

<span data-ttu-id="2943f-104">Элемент конфигурации (Format) Виевдефинитионс элемент (Format) элемент представления (Format) элемент GroupBy для элемента ScriptBlock представления (Format) для GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="2943f-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) ScriptBlock Element for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="2943f-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="2943f-105">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="2943f-106">Атрибуты и элементы</span><span class="sxs-lookup"><span data-stu-id="2943f-106">Attributes and Elements</span></span>

<span data-ttu-id="2943f-107">В следующих разделах описываются атрибуты, дочерние элементы и родительский элемент элемента `ScriptBlock`.</span><span class="sxs-lookup"><span data-stu-id="2943f-107">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="2943f-108">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="2943f-108">Attributes</span></span>

<span data-ttu-id="2943f-109">Нет.</span><span class="sxs-lookup"><span data-stu-id="2943f-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="2943f-110">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="2943f-110">Child Elements</span></span>

<span data-ttu-id="2943f-111">Нет.</span><span class="sxs-lookup"><span data-stu-id="2943f-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="2943f-112">Родительские элементы</span><span class="sxs-lookup"><span data-stu-id="2943f-112">Parent Elements</span></span>

|<span data-ttu-id="2943f-113">Элемент</span><span class="sxs-lookup"><span data-stu-id="2943f-113">Element</span></span>|<span data-ttu-id="2943f-114">Описание</span><span class="sxs-lookup"><span data-stu-id="2943f-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="2943f-115">Элемент GroupBy для представления (формат)</span><span class="sxs-lookup"><span data-stu-id="2943f-115">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)|<span data-ttu-id="2943f-116">Определяет, как отображается группа объектов .NET.</span><span class="sxs-lookup"><span data-stu-id="2943f-116">Defines how a group of .NET objects is displayed.</span></span>|

## <a name="text-value"></a><span data-ttu-id="2943f-117">Текстовое значение</span><span class="sxs-lookup"><span data-stu-id="2943f-117">Text Value</span></span>

<span data-ttu-id="2943f-118">Укажите оцениваемый скрипт.</span><span class="sxs-lookup"><span data-stu-id="2943f-118">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="2943f-119">Замечания</span><span class="sxs-lookup"><span data-stu-id="2943f-119">Remarks</span></span>

<span data-ttu-id="2943f-120">PowerShell запускает новую группу при каждом изменении значения этого сценария.</span><span class="sxs-lookup"><span data-stu-id="2943f-120">PowerShell starts a new group whenever the value of this script changes.</span></span>

<span data-ttu-id="2943f-121">Если этот элемент указан, нельзя указать элемент [PropertyName](propertyname-element-for-groupby-format.md) для запуска новой группы.</span><span class="sxs-lookup"><span data-stu-id="2943f-121">When this element is specified, you cannot specify the [PropertyName](propertyname-element-for-groupby-format.md) element to start a new group.</span></span>

## <a name="see-also"></a><span data-ttu-id="2943f-122">См. также:</span><span class="sxs-lookup"><span data-stu-id="2943f-122">See Also</span></span>

[<span data-ttu-id="2943f-123">Элемент PropertyName для GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="2943f-123">PropertyName Element for GroupBy (Format)</span></span>](propertyname-element-for-groupby-format.md)

[<span data-ttu-id="2943f-124">Элемент GroupBy для представления (формат)</span><span class="sxs-lookup"><span data-stu-id="2943f-124">GroupBy Element for View (Format)</span></span>](groupby-element-for-view-format.md)

[<span data-ttu-id="2943f-125">Написание файла форматирования PowerShell</span><span class="sxs-lookup"><span data-stu-id="2943f-125">Writing a PowerShell Formatting File</span></span>](writing-a-powershell-formatting-file.md)