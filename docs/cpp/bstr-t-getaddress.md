---
title: _bstr_t::GetAddress
ms.date: 11/04/2016
f1_keywords:
- _bstr_t::GetAddress
helpviewer_keywords:
- GetAddress method [C++]
ms.assetid: 09bc9180-867e-4ee5-b22a-8339dc663142
ms.openlocfilehash: ca78bd1b607ba4a86bbc824887a7ec767cd5476e
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2020
ms.locfileid: "80181247"
---
# <a name="_bstr_tgetaddress"></a>_bstr_t::GetAddress

**Microsoft 专用**

释放所有现有字符串并返回一个新分配的字符串的地址。

## <a name="syntax"></a>语法

```
BSTR* GetAddress( );
```

## <a name="return-value"></a>返回值

指向由 `BSTR` 包装的 `_bstr_t` 的指针。

## <a name="remarks"></a>备注

**GetAddress**影响所有共享 `BSTR`的 `_bstr_t` 对象。 多个 `_bstr_t` 可以通过使用复制构造函数和**运算符 =** 来共享 `BSTR`。

## <a name="example"></a>示例

有关使用**GetAddress**的示例，请参阅[_Bstr_t：： Assign](../cpp/bstr-t-assign.md) 。

**结束 Microsoft 专用**

## <a name="see-also"></a>另请参阅

[_bstr_t 类](../cpp/bstr-t-class.md)
