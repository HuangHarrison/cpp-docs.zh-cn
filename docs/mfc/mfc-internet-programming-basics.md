---
title: MFC Internet 编程基础知识
ms.date: 11/19/2018
helpviewer_keywords:
- ISAPI extensions, programming with ISAPI
- Internet applications [MFC]
- ISAPI
- ActiveX controls [MFC], Internet
- programming [MFC], Internet
- Web applications [MFC], MFC classes
- ISAPI filters [MFC], programming with ISAPI
- Internet applications [MFC], ActiveX controls
- Internet applications [MFC], writing
- Internet applications [MFC], Active technology
- Active technology [MFC]
- Internet content [MFC]
- WinInet classes [MFC]
ms.assetid: 6df2dfd0-6e3f-4587-9d01-2a32f00f8a6f
ms.openlocfilehash: b41ce97a9b5efe6ad84c543f5c49dd091557b3a8
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88846311"
---
# <a name="mfc-internet-programming-basics"></a>MFC Internet 编程基础知识

Microsoft 提供了许多 Api 用于对客户端和服务器应用程序进行编程。 许多新应用程序是针对 Internet 编写的，随着技术、浏览器功能和安全选项的更改，将编写新类型的应用程序。 浏览器在客户端计算机上运行，提供对万维网的访问，并显示包含文本、图形、ActiveX 控件和文档的 HTML 页面。 服务器提供 FTP、HTTP 和 gopher 服务，并使用 CGI 运行服务器扩展应用程序。 你的自定义应用程序可以检索信息并在 Internet 上提供数据。

>[!IMPORTANT]
> ActiveX 是一种不能用于新开发的旧技术。 有关详细信息，请参阅 [ActiveX 控件](activex-controls.md)。

![客户端和服务器应用程序](../mfc/media/vc38bq1.gif "客户端和服务器应用程序")

MFC 提供支持 Internet 编程的类。 可以使用 [COleControl](reference/colecontrol-class.md) 和 [CDOCOBJECTSERVER](reference/cdocobjectserver-class.md) 以及相关 MFC 类编写 ActiveX 控件和活动文档。 你可以使用 MFC 类（如 [CInternetSession](reference/cinternetsession-class.md)、 [CFtpConnection](reference/cftpconnection-class.md)和 [CAsyncMonikerFile](reference/casyncmonikerfile-class.md) ）来检索使用 INTERNET 协议（如 FTP、HTTP 和 gopher）的文件和信息。

## <a name="in-this-section"></a>本节内容

- [与 Internet 相关的 MFC 类](internet-related-mfc-classes.md)

- [按主题的 Internet 信息](internet-information-by-topic.md)

- [按任务的 Internet 信息](internet-information-by-task.md)

- [Internet 上的活动技术](active-technology-on-the-internet.md)

- [WinInet 基础知识](wininet-basics.md)

- [HTML 基础知识](html-basics.md)

## <a name="related-sections"></a>相关章节

- [Internet 上的 ActiveX 控件](activex-controls-on-the-internet.md)

- [Internet 上的异步名字对象](asynchronous-monikers-on-the-internet.md)

- [ (WinInet) 的 Win32 Internet 扩展 ](win32-internet-extensions-wininet.md)

- [MFC Internet 编程任务](mfc-internet-programming-tasks.md)

- [应用程序设计选择](application-design-choices.md)

- [编写 MFC 应用程序](writing-mfc-applications.md)

- [测试 Internet 应用程序](testing-internet-applications.md)

- [Internet 安全性](internet-security-cpp.md)

- [ATL 支持 DHTML 控件](../atl/atl-support-for-dhtml-controls.md)

## <a name="websites-for-more-information"></a><a name="_core_web_sites_for_more_information"></a> 网站获取详细信息

有关 Microsoft Internet 技术的详细信息，请参阅 [联网和 Internet](/windows/win32/networking)。

[万维网联合会 (W3C) ](https://go.microsoft.com/fwlink/p/?linkid=37125)发布 HTML、HTTP、CGI 和其他万维网技术的规范。

## <a name="more-internet-help"></a><a name="_core_more_internet_help"></a> 更多 internet 帮助

Windows SDK 的 OLE 部分包含有关 OLE 编程的其他信息。 此信息提供有关直接使用 Win32 WinInet 函数而不是通过 MFC 类的详细信息。 它还包含有关 Internet 技术的概述信息。
