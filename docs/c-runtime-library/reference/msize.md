---
title: _msize
ms.date: 4/2/2020
api_name:
- _msize
- _o__msize
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-heap-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- msize
- _msize
helpviewer_keywords:
- memory blocks
- msize function
- _msize function
ms.assetid: 02b1f89e-d0d7-4f12-938a-9eeba48a0f88
ms.openlocfilehash: cc8eef0d28f649340715edbf4b1ebdfea85c2ff2
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82914610"
---
# <a name="_msize"></a>_msize

返回在堆中分配的存储块的大小。

## <a name="syntax"></a>语法

```C
size_t _msize(
   void *memblock
);
```

### <a name="parameters"></a>参数

*memblock*<br/>
指向内存块的指针。

## <a name="return-value"></a>返回值

**_msize**返回无符号整数形式的大小（以字节为单位）。

## <a name="remarks"></a>备注

**_Msize**函数返回通过调用**calloc**、 **malloc**或**realloc**分配的内存块的大小（以字节为单位）。

当应用程序与调试版的 C 运行时库链接时， **_msize**解析为[_msize_dbg](msize-dbg.md)。 有关在调试过程中如何托管堆的详细信息，请参阅 [CRT 调试堆](/visualstudio/debugger/crt-debug-heap-details)。

此函数验证其参数。 如果*memblock*为 null 指针， **_msize**将调用无效参数处理程序，如[参数验证](../../c-runtime-library/parameter-validation.md)中所述。 如果处理错误，函数会将**errno**设置为**EINVAL** ，并返回-1。

默认情况下，此函数的全局状态的作用域限定为应用程序。 若要更改此项，请参阅[CRT 中的全局状态](../global-state.md)。

## <a name="requirements"></a>要求

|例程|必需的标头|
|-------------|---------------------|
|**_msize**|\<malloc.h>|

有关兼容性的详细信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="libraries"></a>库

[C 运行时库](../../c-runtime-library/crt-library-features.md)的所有版本。

## <a name="example"></a>示例

请参阅 [realloc](realloc.md) 的示例。

## <a name="see-also"></a>另请参阅

[内存分配](../../c-runtime-library/memory-allocation.md)<br/>
[calloc](calloc.md)<br/>
[_expand](expand.md)<br/>
[malloc](malloc.md)<br/>
[realloc](realloc.md)<br/>
