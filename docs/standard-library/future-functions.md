---
title: '&lt;future&gt; 函数'
ms.date: 11/04/2016
f1_keywords:
- future/std::async
- future/std::future_category
- future/std::make_error_code
- future/std::make_error_condition
- future/std::swap
ms.assetid: 1e3acc1e-736a-42dc-ade2-b2fe69aa96bc
helpviewer_keywords:
- std::async [C++]
- std::future_category [C++]
- std::make_error_code [C++]
- std::make_error_condition [C++]
- std::swap [C++]
ms.openlocfilehash: d419984243d3970533f30814fe0ff451199afb34
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88837965"
---
# <a name="ltfuturegt-functions"></a>&lt;future&gt; 函数

[异步](#async)\
[future_category](#future_category)\
[make_error_code](#make_error_code)\
[make_error_condition](#make_error_condition)\
[购](#swap)|

## <a name="async"></a><a name="async"></a> 异步

表示一个异步提供程序**。

```cpp
template <class Fn, class... ArgTypes>
future<typename result_of<Fn(ArgTypes...)>::type>
    async(Fn&& fn, ArgTypes&&... args);

template <class Fn, class... ArgTypes>
future<typename result_of<Fn(ArgTypes...)>::type>
    async(launch policy, Fn&& fn, ArgTypes&&... args);
```

### <a name="parameters"></a>参数

*政策*\
一个 [launch](../standard-library/future-enums.md#launch) 值。

### <a name="remarks"></a>注解

缩写的定义：

|缩写|说明|
|-|-|
|*dfn*|调用 `decay_copy(forward<Fn>(fn))` 的结果。|
|*dargs*|调用 `decay_copy(forward<ArgsTypes>(args...))` 的结果。|
|*Ty*|`result_of<Fn(ArgTypes...)>::type` 类型。|

第一个模板函数返回 `async(launch::any, fn, args...)`。

第二个函数返回一个 `future<Ty>` 对象，其关联的异步状态** 包含一个结果以及 dfn** 和 dargs** 的值和一个用于管理单独的执行线程的线程对象。

除非 `decay<Fn>::type` 是一种不同于 launch 的类型，否则第二个函数将不参与重载解析。

C + + 标准表明，如果 policy 为启动：： async，函数将创建一个新线程。 但是 Microsoft 实现当前不符合要求。 它从 Windows ThreadPool 获取其线程，在某些情况下，可能会提供回收的线程而不是新线程。 这意味着 `launch::async` 策略实际实现为 `launch::async|launch::deferred` 。  基于 ThreadPool 的实现的另一个含义是无法保证线程在线程完成时，将销毁线程本地变量。 如果回收线程并将其提供给新调用 `async` ，则旧变量仍存在。 因此，建议不要将线程本地变量用于 `async` 。

如果 *策略* 为 `launch::deferred` ，则函数会将其关联异步状态标记为包含一个 *延迟函数* 并返回。 对任何等待关联异步状态生效的非计时函数的第一次调用都将通过计算 `INVOKE(dfn, dargs..., Ty)` 来调用延迟函数。

任何情况下，在通过引发异常或正常返回完成 `INVOKE(dfn, dargs..., Ty)` 的计算之前，`future` 对象的关联异步状态不会设置为** 就绪。 如果引发了异常，则关联异步状态的结果为异常，否则为计算返回的任何值。

> [!NOTE]
> 对于一个附加到以 `std::async` 开头的任务的 `future`（或最后一个 [shared_future](../standard-library/shared-future-class.md)），如果任务尚未完成，则析构函数将阻塞；即，如果此线程尚未调用 `.get()` 或 `.wait()` 且任务仍在进行，则析构函数将阻塞。 如果从 `future` 中获得的 `std::async` 移出局部范围，则使用它的其他代码必须知道其析构函数可能在共享状态变成已就绪时阻塞。

伪函数 `INVOKE` 是在中定义的 [\<functional>](../standard-library/functional.md) 。

## <a name="future_category"></a><a name="future_category"></a> future_category

返回一个描述与 `future` 对象相关联错误特征的 [error_category](../standard-library/error-category-class.md) 对象的引用。

```cpp
const error_category& future_category() noexcept;
```

## <a name="make_error_code"></a><a name="make_error_code"></a> make_error_code

创建一个 [error_code](../standard-library/error-code-class.md) 以及一个描述 [future](../standard-library/future-class.md) 错误特征的 [error_category](../standard-library/error-category-class.md) 对象。

```cpp
inline error_code make_error_code(future_errc Errno) noexcept;
```

### <a name="parameters"></a>参数

*Errno*\
一个标识已报告错误的 [future_errc](../standard-library/future-enums.md#future_errc) 值。

### <a name="return-value"></a>返回值

`error_code(static_cast<int>(Errno), future_category());`

## <a name="make_error_condition"></a><a name="make_error_condition"></a> make_error_condition

创建一个 [error_condition](../standard-library/error-condition-class.md) 以及一个描述 [future](../standard-library/future-class.md) 错误特征的 [error_category](../standard-library/error-category-class.md) 对象。

```cpp
inline error_condition make_error_condition(future_errc Errno) noexcept;
```

### <a name="parameters"></a>参数

*Errno*\
一个标识已报告错误的 [future_errc](../standard-library/future-enums.md#future_errc) 值。

### <a name="return-value"></a>返回值

`error_condition(static_cast<int>(Errno), future_category());`

## <a name="swap"></a><a name="swap"></a> 购

将一个 `promise` 对象的关联异步状态** 与另一对象的关联异步状态交换。

```cpp
template <class Ty>
void swap(promise<Ty>& Left, promise<Ty>& Right) noexcept;

template <class Ty, class... ArgTypes>
void swap(packaged_task<Ty(ArgTypes...)>& Left, packaged_task<Ty(ArgTypes...)>& Right) noexcept;
```

### <a name="parameters"></a>参数

*左中*\
左 `promise` 对象。

*然后*\
正确的 `promise` 对象。

## <a name="see-also"></a>另请参阅

[\<future>](../standard-library/future.md)
