---
title: 编译器警告（等级 1）C4946
ms.date: 11/04/2016
f1_keywords:
- C4946
helpviewer_keywords:
- C4946
ms.assetid: b85cbef0-e053-4de6-9b14-7b0f82d40495
ms.openlocfilehash: 3b829eb7cdd0adc58a3ddb225115a4b188a2336f
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2020
ms.locfileid: "80199067"
---
# <a name="compiler-warning-level-1-c4946"></a>编译器警告（等级 1）C4946

reinterpret_cast 在相关类之间使用:“class1”和“class2”

不要使用[reinterpret_cast](../../cpp/reinterpret-cast-operator.md)在相关类型之间强制转换。 请改用[static_cast](../../cpp/static-cast-operator.md) ，对于多态类型，请使用[dynamic_cast](../../cpp/dynamic-cast-operator.md)。

默认情况下，此警告处于关闭状态。 有关详细信息，请参阅 [Compiler Warnings That Are Off by Default](../../preprocessor/compiler-warnings-that-are-off-by-default.md)。

以下代码示例生成 C4946：

```cpp
// C4946.cpp
// compile with: /W1
#pragma warning (default : 4946)
class a {
public:
   a() : m(0) {}
   int m;
};

class b : public virtual a {
};

class b2 : public virtual a {
};

class c : public b, public b2 {
};

int main() {
   c* pC = new c;
   a* pA = reinterpret_cast<a*>(pC);   // C4946
   // try the following line instead
   // a* pA = static_cast<a*>(pC);
}
```
