---
title: 从另一个记录集填充列表框（MFC 数据访问）
ms.date: 11/04/2016
helpviewer_keywords:
- record views, filling list boxes
- list boxes, filling from second recordset
- recordsets [C++], filling list boxes or combo boxes
- CComboBox class, filling object from second rowset
- ODBC recordsets [C++], filling list boxes or combo boxes
- combo boxes [C++], filling from second recordset
- CListCtrl class, filling from second recordset
ms.assetid: 360c0834-da6b-4dc0-bcea-80e9acd611f0
ms.openlocfilehash: 8664e98c6668568918cc0e6504a38119d2e71428
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81336923"
---
# <a name="filling-a-list-box-from-a-second-recordset--mfc-data-access"></a>从另一个记录集填充列表框（MFC 数据访问）

默认情况下，记录视图与其字段映射到记录视图控件的单个记录集对象有关。 有时，你可能需要在记录视图中放置列表框或组合框控件，并使用来自另一个记录集对象的值填充。 用户可以使用列表框选择要在记录视图中显示的新类别信息。 本主题将介绍此操作的方法和时间。

> [!TIP]
> 请注意，从数据源填充组合框或列表框速度可能比较慢。 请采取措施，防止试图从具有大量记录的记录集填充控件。

本主题的模型由填充窗体控件的主要记录集组成，而辅助记录集则填充列表框或组合框。 选择列表框中的字符串将导致你的程序根据所选的类型重新查询主要记录集。 以下过程使用的是组合框，但同样也适用于列表框。

#### <a name="to-fill-a-combo-box-or-list-box-from-a-second-recordset"></a>要从另一个记录集填充组合框或列表框

1. 创建记录集对象[（CRecordset](../mfc/reference/crecordset-class.md)）。

1. 获取组合框控件的指向[CComboBox](../mfc/reference/ccombobox-class.md)对象的指针。

1. 清空组合框以前的所有内容。

1. 移动记录集中的所有记录，调用[CComboBox：：添加](../mfc/reference/ccombobox-class.md#addstring)要添加到组合框中的当前记录中的每个字符串的 String。

1. 初始化组合框中的选择。

```cpp
void CSectionForm::OnInitialUpdate()
{
    // ...

    // Fill the combo box with all of the courses
    CENROLLDoc* pDoc = GetDocument();
    if (!pDoc->m_courseSet.Open())
        return;

    // ...

    m_ctlCourseList.ResetContent();
    if (pDoc->m_courseSet.IsOpen())
    {
        while (!pDoc->m_courseSet.IsEOF() )
        {
            m_ctlCourseList.AddString(
                pDoc->m_courseSet.m_CourseID);
            pDoc->m_courseSet.MoveNext();
        }
    }
    m_ctlCourseList.SetCurSel(0);
}
```

此函数使用另一个记录集 `m_courseSet`，该记录集含有所提供的所有课程的记录和一个存储在记录视图类中的 `CComboBox` 控件 `m_ctlCourseList`。

此函数可从文档获取 `m_courseSet` 并将其打开。 然后清空 `m_ctlCourseList` 并浏览 `m_courseSet`。 对于每一条记录，函数都会调用组合框的 `AddString` 成员函数来添加记录的课程 ID 值。 最后，代码设置组合框选择。

## <a name="see-also"></a>另请参阅

[记录视图（MFC 数据访问）](../data/record-views-mfc-data-access.md)<br/>
[ODBC 驱动程序列表](../data/odbc/odbc-driver-list.md)
