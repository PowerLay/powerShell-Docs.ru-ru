---
title: Элемент PropertyName для SelectionCondition для EntrySelectedBy для WideEntry (формат) | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 340abb12-6df1-42f4-bdae-b0509c90952c
caps.latest.revision: 11
ms.openlocfilehash: 196877b97db9ed0592e357486c1318dc1e7efd31
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56860420"
---
# <a name="propertyname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format"></a><span data-ttu-id="0f35f-102">Элемент PropertyName для элемента SelectionCondition для элемента EntrySelectedBy для элемента WideEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="0f35f-102">PropertyName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>

<span data-ttu-id="0f35f-103">Задает свойство .NET, которое активирует условие.</span><span class="sxs-lookup"><span data-stu-id="0f35f-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="0f35f-104">Если этому свойству присвоено присутствует или когда оно оценивается как `true`условие выполняется, и используется определение.</span><span class="sxs-lookup"><span data-stu-id="0f35f-104">When this property is present or when it evaluates to `true`, the condition is met, and the definition is used.</span></span>

<span data-ttu-id="0f35f-105">Элемент (формат) элемент ViewDefinitions (формат) представление элемента (формат) элемент WideControl (формат) элемент WideEntries (формат) элемент WideEntry (формат) EntrySelectedBy элемент конфигурации для элемент SelectionCondition WideEntry (формат) для EntrySelectedBy элемента PropertyName WideEntry (формат) для SelectionCondition для EntrySelectedBy для WideEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="0f35f-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) SelectionCondition Element for EntrySelectedBy for WideEntry (Format) PropertyName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0f35f-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="0f35f-106">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

```csharp

```

## <a name="attributes-and-elements"></a><span data-ttu-id="0f35f-107">Атрибуты и элементы</span><span class="sxs-lookup"><span data-stu-id="0f35f-107">Attributes and Elements</span></span>

<span data-ttu-id="0f35f-108">Ниже описаны атрибуты, дочерние элементы и родительский элемент `PropertyName` элемент.</span><span class="sxs-lookup"><span data-stu-id="0f35f-108">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="0f35f-109">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="0f35f-109">Attributes</span></span>

<span data-ttu-id="0f35f-110">Нет.</span><span class="sxs-lookup"><span data-stu-id="0f35f-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0f35f-111">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="0f35f-111">Child Elements</span></span>

<span data-ttu-id="0f35f-112">Нет.</span><span class="sxs-lookup"><span data-stu-id="0f35f-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="0f35f-113">Родительские элементы</span><span class="sxs-lookup"><span data-stu-id="0f35f-113">Parent Elements</span></span>

|<span data-ttu-id="0f35f-114">Элемент</span><span class="sxs-lookup"><span data-stu-id="0f35f-114">Element</span></span>|<span data-ttu-id="0f35f-115">Описание</span><span class="sxs-lookup"><span data-stu-id="0f35f-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0f35f-116">Элемент SelectionCondition для EntrySelectedBy для WideEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="0f35f-116">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|<span data-ttu-id="0f35f-117">Определяет условие, которое должен существовать для данного определения для использования.</span><span class="sxs-lookup"><span data-stu-id="0f35f-117">Defines the condition that must exist for this definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="0f35f-118">Текстовое значение</span><span class="sxs-lookup"><span data-stu-id="0f35f-118">Text Value</span></span>

<span data-ttu-id="0f35f-119">Укажите имя свойства .NET.</span><span class="sxs-lookup"><span data-stu-id="0f35f-119">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="0f35f-120">Замечания</span><span class="sxs-lookup"><span data-stu-id="0f35f-120">Remarks</span></span>

<span data-ttu-id="0f35f-121">Условию выбора необходимо указать по крайней мере для одного имени свойства или сценарий для оценки, но нельзя указать одновременно.</span><span class="sxs-lookup"><span data-stu-id="0f35f-121">The selection condition must specify at least one property name or a script to evaluate, but cannot specify both.</span></span> <span data-ttu-id="0f35f-122">Дополнительные сведения об использовании условий выборки см. в разделе [определение условий при отображении данных](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="0f35f-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="0f35f-123">Дополнительные сведения о других компонентах широкое представление, см. в разделе [широкое представление](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="0f35f-123">For more information about other components of a wide view, see [Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0f35f-124">См. также</span><span class="sxs-lookup"><span data-stu-id="0f35f-124">See Also</span></span>

[<span data-ttu-id="0f35f-125">Создание широкое представление</span><span class="sxs-lookup"><span data-stu-id="0f35f-125">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="0f35f-126">Определение условия при отображении данных</span><span class="sxs-lookup"><span data-stu-id="0f35f-126">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="0f35f-127">Элемент ScriptBlock для SelectionCondition для EntrySelectedBy для WideEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="0f35f-127">ScriptBlock Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="0f35f-128">Элемент SelectionCondition для EntrySelectedBy для WideEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="0f35f-128">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="0f35f-129">Запись файла форматирования PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f35f-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)