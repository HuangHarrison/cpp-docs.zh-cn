---
title: CComCompositeControl 类
ms.date: 11/04/2016
f1_keywords:
- CComCompositeControl
- ATLCTL/ATL::CComCompositeControl
- ATLCTL/ATL::CComCompositeControl::CComCompositeControl
- ATLCTL/ATL::CComCompositeControl::AdviseSinkMap
- ATLCTL/ATL::CComCompositeControl::CalcExtent
- ATLCTL/ATL::CComCompositeControl::Create
- ATLCTL/ATL::CComCompositeControl::CreateControlWindow
- ATLCTL/ATL::CComCompositeControl::SetBackgroundColorFromAmbient
- ATLCTL/ATL::CComCompositeControl::m_hbrBackground
- ATLCTL/ATL::CComCompositeControl::m_hWndFocus
helpviewer_keywords:
- CComCompositeControl class
- composite controls, CComCompositeControl class
ms.assetid: 1304b931-27e8-4fbc-be8e-bb226ad887fb
ms.openlocfilehash: a37386c40f119c855dcb8584a72ce85c48a66381
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88834734"
---
# <a name="ccomcompositecontrol-class"></a>CComCompositeControl 类

此类提供实现复合控件所需的方法。

> [!IMPORTANT]
> 此类及其成员不能用于在 Windows 运行时中执行的应用程序。

## <a name="syntax"></a>语法

```
template <class T>
class CComCompositeControl : public CComControl<T,CAxDialogImpl<T>>
```

#### <a name="parameters"></a>参数

*T*<br/>
从 [CComObjectRoot](../../atl/reference/ccomobjectroot-class.md) 或 [CComObjectRootEx](../../atl/reference/ccomobjectrootex-class.md)派生的类，以及要支持用于复合控件的任何其他接口。

## <a name="members"></a>成员

### <a name="public-constructors"></a>公共构造函数

|“属性”|说明|
|----------|-----------------|
|[CComCompositeControl::CComCompositeControl](#ccomcompositecontrol)|构造函数。|
|[CComCompositeControl：： ~ CComCompositeControl](#dtor)|析构函数。|

### <a name="public-methods"></a>公共方法

|“属性”|说明|
|----------|-----------------|
|[CComCompositeControl::AdviseSinkMap](#advisesinkmap)|调用此方法可通知或 unadvise 复合控件承载的所有控件。|
|[CComCompositeControl::CalcExtent](#calcextent)|调用此方法可计算用于承载复合控件的对话框资源的 HIMETRIC 单位的大小。|
|[CComCompositeControl：： Create](#create)|调用此方法可为复合控件创建控件窗口。|
|[CComCompositeControl::CreateControlWindow](#createcontrolwindow)|调用此方法以创建控件窗口并建议任何承载的控件。|
|[CComCompositeControl::SetBackgroundColorFromAmbient](#setbackgroundcolorfromambient)|调用此方法可使用容器的背景色设置复合控件的背景色。|

### <a name="public-data-members"></a>公共数据成员

|名称|说明|
|----------|-----------------|
|[CComCompositeControl：： m_hbrBackground](#m_hbrbackground)|背景画笔。|
|[CComCompositeControl：： m_hWndFocus](#m_hwndfocus)|当前具有焦点的窗口的句柄。|

## <a name="remarks"></a>注解

派生自类的类 `CComCompositeControl` 继承 ActiveX 复合控件的功能。 派生自的 ActiveX 控件 `CComCompositeControl` 由标准对话框承载。 这些类型的控件称为复合控件，因为它们能够承载 (本机 Windows 控件和 ActiveX 控件) 的其他控件。

`CComCompositeControl` 通过查找子类中的枚举数据成员，标识用于创建复合控件的对话框资源。 此子类的成员 IDD 设置为将用作控件窗口的对话框资源的资源 ID。 下面是派生自的类应包含的数据成员的一个示例， `CComCompositeControl` 用于标识要用于控件窗口的对话框资源：

[!code-cpp[NVC_ATL_COM#13](../../atl/codesnippet/cpp/ccomcompositecontrol-class_1.h)]

> [!NOTE]
> 复合控件始终是有窗口控件，不过它们可以包含无窗口控件。

由派生类实现的控件 `CComCompositeControl` 具有内置的默认跳格行为。 如果控件在包含应用程序中通过选项卡式接收焦点，则连续按 TAB 键将导致焦点遍历所有复合控件的包含控件，然后将其移出复合控件，并将其移到容器的 TAB 键顺序中的下一项。 承载的控件的 tab 键顺序由对话框资源确定，确定 tab 键的出现顺序。

> [!NOTE]
> 为了使加速器能够正常运行 `CComCompositeControl` ，必须在创建控件时加载快捷键对应表，将句柄和加速器数传递回 [IOleControlImpl：： GetControlInfo](../../atl/reference/iolecontrolimpl-class.md#getcontrolinfo)，最后在释放控件时销毁该表。

## <a name="example"></a>示例

[!code-cpp[NVC_ATL_COM#14](../../atl/codesnippet/cpp/ccomcompositecontrol-class_2.h)]

## <a name="inheritance-hierarchy"></a>继承层次结构

`WinBase`

[CComControlBase](../../atl/reference/ccomcontrolbase-class.md)

[CComControl](../../atl/reference/ccomcontrol-class.md)

`CComCompositeControl`

## <a name="requirements"></a>要求

**标头：** atlctl

## <a name="ccomcompositecontroladvisesinkmap"></a><a name="advisesinkmap"></a> CComCompositeControl::AdviseSinkMap

调用此方法可通知或 unadvise 复合控件承载的所有控件。

```
HRESULT AdviseSinkMap(bool bAdvise);
```

### <a name="parameters"></a>参数

*bAdvise*<br/>
如果建议所有控件，则为 True;否则为 false。

### <a name="return-value"></a>返回值

| 值 | 说明 |
|--|--|
| `S_OK` | 事件接收器映射中的所有控件都已成功连接或断开与其事件源的连接。 |
| `E_FAIL` | 并非事件接收器映射中的所有控件都可以成功连接或断开与其事件源的连接。 |
| `E_POINTER` | 此错误通常表示控件的事件接收器映射中的条目出现问题，或在或基类中使用的模板自变量出现 `IDispEventImpl` 问题 `IDispEventSimpleImpl` 。 |
| `CONNECT_E_ADVISELIMIT` | 该连接点已经达到其连接极限，无法再进行接受了。 |
| `CONNECT_E_CANNOTCONNECT` | 接收器不支持此连接点所需的接口。 |
| `CONNECT_E_NOCONNECTION` | Cookie 值不表示有效的连接。 此错误通常表示控件的事件接收器映射中的条目出现问题，或在或基类中使用的模板自变量出现 `IDispEventImpl` 问题 `IDispEventSimpleImpl` 。 |

### <a name="remarks"></a>注解

此方法的基实现在事件接收器映射中搜索各个条目。 然后，它将建议或 unadvises 连接到事件接收器映射的接收器条目所描述的 COM 对象。 此成员方法还依赖于这样一个事实：派生类从的一个实例继承，以 `IDispEventImpl` 对接收器映射中要通知或 unadvised 的每个控件继承。

## <a name="ccomcompositecontrolcalcextent"></a><a name="calcextent"></a> CComCompositeControl::CalcExtent

调用此方法可计算用于承载复合控件的对话框资源的 HIMETRIC 单位的大小。

```
BOOL CalcExtent(SIZE& size);
```

### <a name="parameters"></a>参数

*大小*<br/>
对要 `SIZE` 通过此方法填充的结构的引用。

### <a name="return-value"></a>返回值

如果控件由对话框承载，则为 TRUE;否则为 FALSE。

### <a name="remarks"></a>注解

大小在 *size* 参数中返回。

## <a name="ccomcompositecontrolcreate"></a><a name="create"></a> CComCompositeControl：： Create

调用此方法可为复合控件创建控件窗口。

```
HWND Create(
    HWND hWndParent,
    RECT& /* rcPos */,
    LPARAM dwInitParam = NULL);
```

### <a name="parameters"></a>参数

*hWndParent*<br/>
控件的父窗口的句柄。

*rcPos*<br/>
保留。

*dwInitParam*<br/>
控件创建期间要传递到控件的数据。 作为 *dwInitParam* 传递的数据将显示为 [WM_INITDIALOG](/windows/win32/dlgbox/wm-initdialog) 消息的 LPARAM 参数，该参数将在创建时发送到复合控件。

### <a name="return-value"></a>返回值

新创建的复合控件对话框的句柄。

### <a name="remarks"></a>注解

通常在就地激活控件过程中调用此方法。

## <a name="ccomcompositecontrolccomcompositecontrol"></a><a name="ccomcompositecontrol"></a> CComCompositeControl::CComCompositeControl

构造函数。

```
CComCompositeControl();
```

### <a name="remarks"></a>注解

将 [CComCompositeControl：： m_hbrBackground](#m_hbrbackground) 和 [CComCompositeControl：： m_hWndFocus](#m_hwndfocus) 数据成员初始化为 NULL。

## <a name="ccomcompositecontrolccomcompositecontrol"></a><a name="dtor"></a> CComCompositeControl：： ~ CComCompositeControl

析构函数。

```
~CComCompositeControl();
```

### <a name="remarks"></a>注解

删除后台对象（如果存在）。

## <a name="ccomcompositecontrolcreatecontrolwindow"></a><a name="createcontrolwindow"></a> CComCompositeControl::CreateControlWindow

调用此方法可创建控件窗口并建议任何承载的控件。

```
virtual HWND CreateControlWindow(
    HWND hWndParent,
    RECT& rcPos);
```

### <a name="parameters"></a>参数

*hWndParent*<br/>
控件的父窗口的句柄。

*rcPos*<br/>
复合控件在相对于 *hWndParent*的工作区坐标中的位置矩形。

### <a name="return-value"></a>返回值

返回新创建的复合控件对话框的句柄。

### <a name="remarks"></a>注解

此方法调用 [CComCompositeControl：： Create](#create) 和 [CComCompositeControl：： AdviseSinkMap](#advisesinkmap)。

## <a name="ccomcompositecontrolm_hbrbackground"></a><a name="m_hbrbackground"></a> CComCompositeControl：： m_hbrBackground

背景画笔。

```
HBRUSH m_hbrBackground;
```

## <a name="ccomcompositecontrolm_hwndfocus"></a><a name="m_hwndfocus"></a> CComCompositeControl：： m_hWndFocus

当前具有焦点的窗口的句柄。

```
HWND m_hWndFocus;
```

## <a name="ccomcompositecontrolsetbackgroundcolorfromambient"></a><a name="setbackgroundcolorfromambient"></a> CComCompositeControl::SetBackgroundColorFromAmbient

调用此方法可使用容器的背景色设置复合控件的背景色。

```
HRESULT SetBackgroundColorFromAmbient();
```

### <a name="return-value"></a>返回值

如果成功，则返回 S_OK; 否则返回错误 HRESULT。

## <a name="see-also"></a>另请参阅

[CComControl 类](../../atl/reference/ccomcontrol-class.md)<br/>
[复合控件基础知识](../../atl/atl-composite-control-fundamentals.md)<br/>
[类概述](../../atl/atl-class-overview.md)
