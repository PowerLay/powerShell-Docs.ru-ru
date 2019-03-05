---
title: Элемент PropertyName для WideItem для WideControl (формат) | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3d91d0e6-bf18-4587-b651-db66849e5df5
caps.latest.revision: 6
ms.openlocfilehash: 326880834cd82ab826aadc409cd7a8f21cd36824
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56860960"
---
# <a name="propertyname-element-for-wideitem-for-widecontrol-format"></a><span data-ttu-id="0c675-102">Элемент PropertyName для элемента WideItem для элемента WideControl (формат)</span><span class="sxs-lookup"><span data-stu-id="0c675-102">PropertyName Element for WideItem for WideControl (Format)</span></span>

<span data-ttu-id="0c675-103">Задает свойство объекта, значение которого отображается в широком представлении.</span><span class="sxs-lookup"><span data-stu-id="0c675-103">Specifies the property of the object whose value is displayed in the wide view.</span></span>

<span data-ttu-id="0c675-104">Элемент (формат) элемент ViewDefinitions (формат) представление элемента (формат) элемент WideControl (формат) элемент WideEntries (формат) элемент WideEntry (формат) элемент WideItem (формат) PropertyName элемент конфигурации для WideItem (формат)</span><span class="sxs-lookup"><span data-stu-id="0c675-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) WideItem Element (Format) PropertyName Element for WideItem (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0c675-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="0c675-105">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0c675-106">Атрибуты и элементы</span><span class="sxs-lookup"><span data-stu-id="0c675-106">Attributes and Elements</span></span>

<span data-ttu-id="0c675-107">В следующих разделах атрибуты, дочерние элементы и родительский элемент `PropertyName` элемент.</span><span class="sxs-lookup"><span data-stu-id="0c675-107">The following sections describe the attributes, child elements, and parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="0c675-108">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="0c675-108">Attributes</span></span>

<span data-ttu-id="0c675-109">Нет.</span><span class="sxs-lookup"><span data-stu-id="0c675-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0c675-110">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="0c675-110">Child Elements</span></span>

<span data-ttu-id="0c675-111">Нет.</span><span class="sxs-lookup"><span data-stu-id="0c675-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="0c675-112">Родительские элементы</span><span class="sxs-lookup"><span data-stu-id="0c675-112">Parent Elements</span></span>

|<span data-ttu-id="0c675-113">Элемент</span><span class="sxs-lookup"><span data-stu-id="0c675-113">Element</span></span>|<span data-ttu-id="0c675-114">Описание</span><span class="sxs-lookup"><span data-stu-id="0c675-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0c675-115">Элемент WideItem (формат)</span><span class="sxs-lookup"><span data-stu-id="0c675-115">WideItem Element (Format)</span></span>](./wideitem-element-for-widecontrol-format.md)|<span data-ttu-id="0c675-116">Определяет свойство или скрипта, значение которого отображается в широком представлении.</span><span class="sxs-lookup"><span data-stu-id="0c675-116">Defines the property or script whose value is displayed in the wide view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="0c675-117">Текстовое значение</span><span class="sxs-lookup"><span data-stu-id="0c675-117">Text Value</span></span>

<span data-ttu-id="0c675-118">Укажите имя свойства, значение которого отображается.</span><span class="sxs-lookup"><span data-stu-id="0c675-118">Specify the name of the property whose value is displayed.</span></span>

## <a name="remarks"></a><span data-ttu-id="0c675-119">Замечания</span><span class="sxs-lookup"><span data-stu-id="0c675-119">Remarks</span></span>

<span data-ttu-id="0c675-120">Дополнительные сведения о компонентах широкое представление, см. в разделе [Создание широкое представление](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="0c675-120">For more information about the components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="0c675-121">Пример</span><span class="sxs-lookup"><span data-stu-id="0c675-121">Example</span></span>

<span data-ttu-id="0c675-122">В этом примере показано широкое представление, которое отображает значение свойства ProcessName [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) объекта.</span><span class="sxs-lookup"><span data-stu-id="0c675-122">This example shows a wide view that displays the value of the ProcessName property of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

```xml
View>
  <Name>process</Name>
  <ViewSelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </ViewSelectedBy>
  <WideControl>
    <WideEntries>
      <WideEntry>
        <WideItem>
          <PropertyName>ProcessName</PropertyName>
        </WideItem>
      </WideEntry>
    </WideEntries>
  </WideControl>
</View>

```

## <a name="see-also"></a><span data-ttu-id="0c675-123">См. также</span><span class="sxs-lookup"><span data-stu-id="0c675-123">See Also</span></span>

[<span data-ttu-id="0c675-124">Элемент WideItem (формат)</span><span class="sxs-lookup"><span data-stu-id="0c675-124">WideItem Element (Format)</span></span>](./wideitem-element-for-widecontrol-format.md)

[<span data-ttu-id="0c675-125">Создание широкое представление</span><span class="sxs-lookup"><span data-stu-id="0c675-125">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="0c675-126">Запись файла форматирования PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c675-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)