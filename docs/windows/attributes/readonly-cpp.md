---
title: 'readonly (c + + COM 特性) '
ms.date: 10/02/2018
f1_keywords:
- vc-attr.readonly
helpviewer_keywords:
- readonly attribute
ms.assetid: 1246cadd-5304-43a9-beea-51153d12704d
ms.openlocfilehash: ea2b0a46d34fc415a3b9eca97b92cda764fc7d42
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88839798"
---
# <a name="readonly-c"></a>readonly (C++)

禁止分配给数据成员。

## <a name="syntax"></a>语法

```cpp
[readonly]
```

## <a name="remarks"></a>备注

**readonly** C++ 属性具有与 [readonly](/windows/win32/Midl/readonly) MIDL 属性相同的功能。

如果要禁止修改方法参数，则使用 [in](in-cpp.md) 属性。

## <a name="example"></a>示例

下面的代码演示的 **readonly** 属性的用法：

```cpp
// cpp_attr_ref_readonly.cpp
// compile with: /LD
[idl_quote("midl_pragma warning(disable:2461)")];
#include "unknwn.h"
[module(name="ATLFIRELib")];

[dispinterface, uuid(11111111-1111-1111-1111-111111111111)]
__interface IFireTabCtrl
{
   [readonly, id(1)] int i();
};
```

## <a name="requirements"></a>要求

| 特性上下文 | 值 |
|-|-|
|**适用于**|接口方法|
|**且**|否|
|**必需属性**|无|
|**无效的特性**|无|

有关特性上下文的详细信息，请参见 [特性上下文](cpp-attributes-com-net.md#contexts)。

## <a name="see-also"></a>另请参阅

[IDL 特性](idl-attributes.md)<br/>
[数据成员特性](data-member-attributes.md)
