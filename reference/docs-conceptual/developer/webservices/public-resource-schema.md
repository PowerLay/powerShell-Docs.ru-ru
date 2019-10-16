---
title: Схема общих ресурсов | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e67298ee-a773-4402-8afb-d97ad0e030e5
caps.latest.revision: 4
ms.openlocfilehash: c7e20ff0f36e8cab2d414ff2e5924b3359ad9c60
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72366273"
---
# <a name="public-resource-schema"></a><span data-ttu-id="86192-102">Общедоступная схема ресурсов</span><span class="sxs-lookup"><span data-stu-id="86192-102">Public Resource Schema</span></span>

<span data-ttu-id="86192-103">Управление OData использует MOF для определения ресурсов и их свойств.</span><span class="sxs-lookup"><span data-stu-id="86192-103">Management OData uses MOF to define resources and their properties.</span></span> <span data-ttu-id="86192-104">Свойства сущности OData управления непосредственно соответствуют свойствам управляемого типа, возвращаемого базовым командлетом.</span><span class="sxs-lookup"><span data-stu-id="86192-104">The properties of a Management OData entity correspond directly to the properties of the managed type returned by the underlying cmdlet.</span></span>

## <a name="defining-a-resource"></a><span data-ttu-id="86192-105">Определение ресурса</span><span class="sxs-lookup"><span data-stu-id="86192-105">Defining a resource</span></span>

<span data-ttu-id="86192-106">Каждый ресурс соответствует объекту, возвращенному командлетом Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86192-106">Each resource corresponds to an object returned by a Windows PowerShell cmdlet.</span></span> <span data-ttu-id="86192-107">В MOF-файле общедоступного ресурса вы определяете ресурс, объявляя класс.</span><span class="sxs-lookup"><span data-stu-id="86192-107">In the public resource MOF file, you define a resource by declaring a class.</span></span> <span data-ttu-id="86192-108">Класс состоит из свойств, соответствующих свойствам объекта.</span><span class="sxs-lookup"><span data-stu-id="86192-108">The class consists of properties that correspond to the properties of the object.</span></span> <span data-ttu-id="86192-109">Например, в следующем примере класс [System. Diagnostics. Process](/dotnet/api/System.Diagnostics.Process) представлен следующим MOF.</span><span class="sxs-lookup"><span data-stu-id="86192-109">For example, in the following example, the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) class is represented by the following MOF.</span></span>

```csharp
class PswsTest_Process
{
    [Key] SInt32 Id;
    [Required] SInt32 BasePriority;
    [Required] SInt32 HandleCount;
    [Required] string MachineName;
    [Required] SInt32 MainWindowHandle;

    ...
};
```

<span data-ttu-id="86192-110">Каждому имени свойства предшествует тип данных.</span><span class="sxs-lookup"><span data-stu-id="86192-110">Each property name is preceded by a data type.</span></span> <span data-ttu-id="86192-111">Типы данных в этом примере соответствуют примитивным типам данных CLR в .NET Framework, но свойства также могут быть ссылками на другие ресурсы или сложные типы, которые описаны далее.</span><span class="sxs-lookup"><span data-stu-id="86192-111">The data types in this example correspond to primitive CLR data types in the .NET Frameworks, but properties can also be references to other resources or complex types, which are both described later.</span></span>

<span data-ttu-id="86192-112">Квалификатор `Key` указывает, что свойство используется для уникальной идентификации экземпляра ресурса.</span><span class="sxs-lookup"><span data-stu-id="86192-112">The `Key` qualifier indicates that a property is used to uniquely identify a resource instance.</span></span> <span data-ttu-id="86192-113">Ресурс может иметь более одного ключа.</span><span class="sxs-lookup"><span data-stu-id="86192-113">A resource can have more than one key.</span></span>

<span data-ttu-id="86192-114">Квалификатор `Required` указывает, что свойство является обязательным.</span><span class="sxs-lookup"><span data-stu-id="86192-114">The `Required` qualifier indicates that the property is required.</span></span> <span data-ttu-id="86192-115">Если свойство помечено квалификатором `Key`, оно считается обязательным, а квалификатор `Required` не требуется.</span><span class="sxs-lookup"><span data-stu-id="86192-115">If a property is labeled with the `Key` qualifier, it is considered to be required, and the `Required` qualifier is not necessary.</span></span>

### <a name="complex-data-types"></a><span data-ttu-id="86192-116">Сложные типы данных</span><span class="sxs-lookup"><span data-stu-id="86192-116">Complex data types</span></span>

<span data-ttu-id="86192-117">Свойства сущностей могут иметь сложные типы данных.</span><span class="sxs-lookup"><span data-stu-id="86192-117">Properties of entities can have complex data types.</span></span> <span data-ttu-id="86192-118">Сложные типы данных — это типы, которые состоят из других типов, аналогично структурам в языке программирования C.</span><span class="sxs-lookup"><span data-stu-id="86192-118">Complex data types are types that are made up of other types, similar to structs in the C programming language.</span></span> <span data-ttu-id="86192-119">Сложный тип объявляется в MOF-файле как класс с квалификатором `ComplexType`, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="86192-119">A complex type is declared in the MOF file as a class with the `ComplexType` qualifier, as in the following example.</span></span>

```csharp
[ComplexType]
class PswsTest_ProcessModule
{
    String ModuleName;
    String FileName;
};
```

<span data-ttu-id="86192-120">Чтобы объявить свойство сущности как сложный тип, объявите его как тип `string` с квалификатором `EmbeddedInstance`, включая имя сложного типа.</span><span class="sxs-lookup"><span data-stu-id="86192-120">To declare an entity property as a complex type, you declare it as a `string` type with the `EmbeddedInstance` qualifier, including the name of the complex type.</span></span> <span data-ttu-id="86192-121">В следующем примере показано объявление свойства типа `PswsTest_ProcessModule`, объявленного в предыдущем примере.</span><span class="sxs-lookup"><span data-stu-id="86192-121">The following example shows the declaration of a property of the `PswsTest_ProcessModule` type declared in the previous example.</span></span>

```csharp
[Required, EmbeddedInstance("PswsTest_ProcessModule")] String Modules[];
```

### <a name="associating-entities"></a><span data-ttu-id="86192-122">Связывание сущностей</span><span class="sxs-lookup"><span data-stu-id="86192-122">Associating entities</span></span>

<span data-ttu-id="86192-123">Связать две сущности можно с помощью квалификаторов Association и АссоЦиатионкласс.</span><span class="sxs-lookup"><span data-stu-id="86192-123">You can associate two entities by using the Association and AssociationClass qualifiers.</span></span> <span data-ttu-id="86192-124">Дополнительные сведения см. в разделе [Сопоставление сущностей OData управления](./associating-management-odata-entities.md).</span><span class="sxs-lookup"><span data-stu-id="86192-124">For more information, see [Associating Management OData Entities](./associating-management-odata-entities.md).</span></span>

### <a name="derived-types"></a><span data-ttu-id="86192-125">Производные типы</span><span class="sxs-lookup"><span data-stu-id="86192-125">Derived types</span></span>

<span data-ttu-id="86192-126">Тип можно получить из другого типа.</span><span class="sxs-lookup"><span data-stu-id="86192-126">You can derive a type from another type.</span></span> <span data-ttu-id="86192-127">Производный тип наследует все свойства типа, от которого он является производным, помимо явно производных свойств.</span><span class="sxs-lookup"><span data-stu-id="86192-127">The derived type inherits all of the properties of the type from which it derives in addition to any properties explicitly derived.</span></span> <span data-ttu-id="86192-128">В следующем примере показано объявление типа, а затем объявление двух типов, производных от этого типа.</span><span class="sxs-lookup"><span data-stu-id="86192-128">The following example shows a type declaration and then a declaration of two types derived from that type.</span></span>

```csharp
Class Product {

    [Key] String ProductName;

};

Class DairyProduct : Product {

    Uint16 PercentFat;
};
Class POPProduct : Product {

    Boolean IsCarbonated;
};
```