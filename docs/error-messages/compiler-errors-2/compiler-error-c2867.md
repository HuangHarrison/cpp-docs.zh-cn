---
title: 编译器错误 C2867
ms.date: 11/04/2016
f1_keywords:
- C2867
helpviewer_keywords:
- C2867
ms.assetid: 63be26b2-d9ab-4f3d-a8b7-981ce3e4d6b9
ms.openlocfilehash: 66d71d87fbb8e5dce495803f1251565bb14d23f8
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87212639"
---
# <a name="compiler-error-c2867"></a>编译器错误 C2867

"identifier"：不是命名空间

**`using`** 指令应用于命名空间以外的内容。

下面的示例生成 C2867：

```cpp
// C2867.cpp
// compile with: /c
namespace N {
   class X {};
}
using namespace N::X;   // C2867
```
