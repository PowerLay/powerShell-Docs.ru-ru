---
title: Элемент PropertyName для SelectionCondition для EntrySelectedBy для ListControl (формат) | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 71c3f1f6-6fe2-42f1-8260-6974d3871748
caps.latest.revision: 11
ms.openlocfilehash: f857f5944b9e971215a06d6f5c39f7c22c6cf99f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56853300"
---
# <a name="propertyname-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format"></a><span data-ttu-id="7af18-102">Элемент PropertyName для элемента SelectionCondition для элемента EntrySelectedBy для элемента ListControl (формат)</span><span class="sxs-lookup"><span data-stu-id="7af18-102">PropertyName Element for SelectionCondition for EntrySelectedBy for ListControl (Format)</span></span>

<span data-ttu-id="7af18-103">Задает свойство .NET, которое активирует условие.</span><span class="sxs-lookup"><span data-stu-id="7af18-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="7af18-104">Если этому свойству присвоено присутствует или когда оно оценивается как `true`условие выполняется, и используется элемент списка.</span><span class="sxs-lookup"><span data-stu-id="7af18-104">When this property is present or when it evaluates to `true`, the condition is met, and the list entry is used.</span></span>

<span data-ttu-id="7af18-105">Элемент (формат) элемент ViewDefinitions (формат) представление элемент (формат) элемента ListControl (формат) элемент ListEntries (формат) элемент ListEntry (формат) EntrySelectedBy элемент конфигурации для элемента SelectionCondition ListEntry (формат) для EntrySelectedBy элемента PropertyName ListEntry (формат) для SelectionCondition для EmtrySelectedBy для ListEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="7af18-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element (Format) EntrySelectedBy Element for ListEntry (Format) SelectionCondition Element for EntrySelectedBy for ListEntry (Format) PropertyName Element for SelectionCondition for EmtrySelectedBy for ListEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="7af18-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="7af18-106">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="7af18-107">Атрибуты и элементы</span><span class="sxs-lookup"><span data-stu-id="7af18-107">Attributes and Elements</span></span>

<span data-ttu-id="7af18-108">Ниже описаны атрибуты, дочерние элементы и родительский элемент `PropertyName` элемент.</span><span class="sxs-lookup"><span data-stu-id="7af18-108">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="7af18-109">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="7af18-109">Attributes</span></span>

<span data-ttu-id="7af18-110">Нет.</span><span class="sxs-lookup"><span data-stu-id="7af18-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="7af18-111">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="7af18-111">Child Elements</span></span>

<span data-ttu-id="7af18-112">Нет.</span><span class="sxs-lookup"><span data-stu-id="7af18-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="7af18-113">Родительские элементы</span><span class="sxs-lookup"><span data-stu-id="7af18-113">Parent Elements</span></span>

|<span data-ttu-id="7af18-114">Элемент</span><span class="sxs-lookup"><span data-stu-id="7af18-114">Element</span></span>|<span data-ttu-id="7af18-115">Описание</span><span class="sxs-lookup"><span data-stu-id="7af18-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7af18-116">Элемент SelectionCondition для EntrySelectedBy для ListEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="7af18-116">SelectionCondition Element for EntrySelectedBy for ListEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="7af18-117">Определяет условие, которое должен существовать для записи в этом списке для использования.</span><span class="sxs-lookup"><span data-stu-id="7af18-117">Defines the condition that must exist for this list entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="7af18-118">Текстовое значение</span><span class="sxs-lookup"><span data-stu-id="7af18-118">Text Value</span></span>

<span data-ttu-id="7af18-119">Укажите имя свойства .NET.</span><span class="sxs-lookup"><span data-stu-id="7af18-119">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="7af18-120">Замечания</span><span class="sxs-lookup"><span data-stu-id="7af18-120">Remarks</span></span>

<span data-ttu-id="7af18-121">Условию выбора необходимо указать по крайней мере для одного имени свойства или блок скрипта, но нельзя указать одновременно.</span><span class="sxs-lookup"><span data-stu-id="7af18-121">The selection condition must specify at least one property name or a script block, but cannot specify both.</span></span> <span data-ttu-id="7af18-122">Дополнительные сведения об использовании условий выборки см. в разделе [определение условий для, когда операция отчета или элемента используется](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="7af18-122">For more information about how to use selection conditions, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="7af18-123">Дополнительные сведения о других компонентах представления списка, см. в разделе [Создание представления списка](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="7af18-123">For more information about other components of a list view, see [Creating List View](./creating-a-list-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7af18-124">См. также</span><span class="sxs-lookup"><span data-stu-id="7af18-124">See Also</span></span>

[<span data-ttu-id="7af18-125">Создание представления списка</span><span class="sxs-lookup"><span data-stu-id="7af18-125">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="7af18-126">Определение условия для данных, когда отображается</span><span class="sxs-lookup"><span data-stu-id="7af18-126">Defining Conditions for When Data is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="7af18-127">Элемент ListEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="7af18-127">ListEntry Element (Format)</span></span>](./listentry-element-for-listcontrol-format.md)

[<span data-ttu-id="7af18-128">Элемент ScriptBlock для SelectionCondition для EntrySelectedBy для ListEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="7af18-128">ScriptBlock Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="7af18-129">Запись файла форматирования PowerShell</span><span class="sxs-lookup"><span data-stu-id="7af18-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)