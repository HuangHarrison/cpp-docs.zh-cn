---
title: Pragma 指令和 __pragma 关键字
ms.date: 08/29/2019
f1_keywords:
- '#pragma'
helpviewer_keywords:
- '#pragma directives, C/C++'
- __pragma keyword
- pragma directives, C/C++
- pragmas, C/C++
- preprocessor
- pragmas
- preprocessor, pragmas
- pragma directives (#pragma)
ms.assetid: 9867b438-ac64-4e10-973f-c3955209873f
ms.openlocfilehash: 786f76d9f7fd2eee73c6b1d009186bf93ea0c667
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88842684"
---
# <a name="pragma-directives-and-the-__pragma-keyword"></a>Pragma 指令和 __pragma 关键字

杂注指令指定计算机或操作系统特定的编译器功能。 **__Pragma**关键字，它是特定于 Microsoft 编译器的，可让你在宏定义中编码杂注指令。

## <a name="syntax"></a>语法

> **#pragma** *标记-字符串*\
> **__pragma (** *标记-字符串* **) **

## <a name="remarks"></a>注解

C 和 C++ 的每个实现均支持某些对其主机或操作系统唯一的功能。 例如，某些程序必须对内存中的数据位置进行精确控制，或控制某些函数接收参数的方式。 **#Pragma**指令为每个编译器提供了一种提供计算机和操作系统特定功能的方法，同时保持与 c 和 c + + 语言的总体兼容性。

杂注是计算机或操作系统特定于定义的，并且对于每个编译器通常是不同的。 杂注可用于条件指令，提供新的预处理器功能，或向编译器提供实现定义的信息。

*标记字符串*是提供特定编译器指令和参数（如果有）的一系列字符。 数字符号 (**#**) 必须是包含杂注的行上的第一个非空白字符。 空白字符可以分隔数字符号和词 "pragma"。 **#Pragma**后，编写转换器可分析为预处理令牌的任何文本。 **#Pragma**的参数受宏展开的限制。

编译器在找到它无法识别的杂注时发出警告并继续编译。

Microsoft C 和 C++ 编译器识别以下杂注：

:::row:::
   :::column span="":::
      [`alloc_text`](../preprocessor/alloc-text.md)\
      [`auto_inline`](../preprocessor/auto-inline.md)\
      [`bss_seg`](../preprocessor/bss-seg.md)\
      [`check_stack`](../preprocessor/check-stack.md)\
      [`code_seg`](../preprocessor/code-seg.md)\
      [`comment`](../preprocessor/comment-c-cpp.md)\
      [`component`](../preprocessor/component.md)\
      [`conform`](../preprocessor/conform.md)<sup>1</sup>\
      [`const_seg`](../preprocessor/const-seg.md)\
      [`data_seg`](../preprocessor/data-seg.md)\
      [`deprecated`](../preprocessor/deprecated-c-cpp.md)
   :::column-end:::
   :::column span="":::
      [`detect_mismatch`](../preprocessor/detect-mismatch.md)\
      [`fenv_access`](../preprocessor/fenv-access.md)\
      [`float_control`](../preprocessor/float-control.md)\
      [`fp_contract`](../preprocessor/fp-contract.md)\
      [`function`](../preprocessor/function-c-cpp.md)\
      [`hdrstop`](../preprocessor/hdrstop.md)\
      [`include_alias`](../preprocessor/include-alias.md)\
      [`init_seg`](../preprocessor/init-seg.md)<sup>1</sup>\
      [`inline_depth`](../preprocessor/inline-depth.md)\
      [`inline_recursion`](../preprocessor/inline-recursion.md)
   :::column-end:::
   :::column span="":::
      [`intrinsic`](../preprocessor/intrinsic.md)\
      [`loop`](../preprocessor/loop.md)<sup>1</sup>\
      [`make_public`](../preprocessor/make-public.md)\
      [`managed`](../preprocessor/managed-unmanaged.md)\
      [`message`](../preprocessor/message.md)\
      [`omp`](../preprocessor/omp.md)\
      [`once`](../preprocessor/once.md)\
      [`optimize`](../preprocessor/optimize.md)\
      [`pack`](../preprocessor/pack.md)\
      [`pointers_to_members`](../preprocessor/pointers-to-members.md)<sup>1</sup>
   :::column-end:::
   :::column span="":::
      [`pop_macro`](../preprocessor/pop-macro.md)\
      [`push_macro`](../preprocessor/push-macro.md)\
      [`region`，endregion](../preprocessor/region-endregion.md)\
      [`runtime_checks`](../preprocessor/runtime-checks.md)\
      [`section`](../preprocessor/section.md)\
      [`setlocale`](../preprocessor/setlocale.md)\
      [`strict_gs_check`](../preprocessor/strict-gs-check.md)\
      [`unmanaged`](../preprocessor/managed-unmanaged.md)\
      [`vtordisp`](../preprocessor/vtordisp.md)<sup>1</sup>\
      [`warning`](../preprocessor/warning.md)
   :::column-end:::
:::row-end:::

<sup>1</sup> 仅由 c + + 编译器支持。

## <a name="pragmas-and-compiler-options"></a>杂注和编译器选项

某些杂注提供与编译器选项相同的功能。 在源代码中遇到杂注时，将重写编译器选项所指定的行为。 例如，如果指定 [了/zp8](../build/reference/zp-struct-member-alignment.md)，则可以用 [pack](../preprocessor/pack.md)的代码的特定部分重写此编译器设置：

```cmd
cl /Zp8 some_file.cpp
```

```cpp
// some_file.cpp - packing is 8
// ...
#pragma pack(push, 1) - packing is now 1
// ...
#pragma pack(pop) - packing is 8 again
// ...
```

## <a name="the-__pragma-keyword"></a>__Pragma ( # A1 关键字

编译器还支持特定于 Microsoft 的 **__pragma** 关键字，该关键字具有与 **#pragma** 指令相同的功能。 不同之处在于， **__pragma** 关键字在宏定义中是以内联方式使用的。 **#Pragma**指令不可用于宏定义中，因为编译器会将指令中的数字符号 )  ( 字符解释为[字符串化运算符 ( # ) ](../preprocessor/stringizing-operator-hash.md)。

下面的代码示例演示如何在宏中使用 **__pragma** 关键字。 此代码摘自“编译器 COM 支持示例”中的 ACDUAL 示例中的 mfcdual.h 头：

```cpp
#define CATCH_ALL_DUAL \
CATCH(COleException, e) \
{ \
_hr = e->m_sc; \
} \
AND_CATCH_ALL(e) \
{ \
__pragma(warning(push)) \
__pragma(warning(disable:6246)) /*disable _ctlState prefast warning*/ \
AFX_MANAGE_STATE(pThis->m_pModuleState); \
__pragma(warning(pop)) \
_hr = DualHandleException(_riidSource, e); \
} \
END_CATCH_ALL \
return _hr; \
```

## <a name="see-also"></a>另请参阅

[C/c + + 预处理器参考](../preprocessor/c-cpp-preprocessor-reference.md)\
[C 杂注](../c-language/c-pragmas.md)\
[关键字](../cpp/keywords-cpp.md)
