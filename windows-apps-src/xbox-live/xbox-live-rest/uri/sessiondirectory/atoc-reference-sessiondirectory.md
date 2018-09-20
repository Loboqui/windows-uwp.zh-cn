---
title: 会话目录 URI
assetID: e3ba951d-b21f-0014-c358-2603d549d118
permalink: en-us/docs/xboxlive/rest/atoc-reference-sessiondirectory.html
author: KevinAsgari
description: " 会话目录 URI"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: b03c55b827b083c050451c12c1fe48834d7ae186
ms.sourcegitcommit: 68fcac3288d5698a13dbcbd57f51b30592f24860
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2018
ms.locfileid: "4054906"
---
# <a name="session-directory-uris"></a>会话目录 URI

本部分提供了从 Xbox Live 服务的多人游戏会话目录 (MPSD) 的详细信息的统一资源标识符 (URI) 地址和关联的超文本传输协议 (HTTP) 方法。


> [!NOTE] 
> 仅适用于游戏的 Xbox 360 上、 在 Windows Phone 设备上，或在 Xbox.com 上运行的游戏可以使用会话目录 Uri。  


  * [域](#ID4EUB)
  * [服务版本](#ID4EZB)
  * [系统对象和属性](#ID4EAC)
  * [句柄](#ID4EBE)

<a id="ID4EUB"></a>


## <a name="domain"></a>域
sessiondirectory.xboxlive.com  
<a id="ID4EZB"></a>


## <a name="service-version"></a>服务版本

这些 REST Uri 的调用方必须为 X-Xbl-合同的版本，HTTP 标头，指定的服务版本的娱乐发现服务 (EDS) 传递值 104/105 或更高版本。

<a id="ID4EAC"></a>


## <a name="system-objects-and-properties"></a>系统对象和属性

用于配置的其会话和模板，MPSD 使用多个会话 JSON 对象符合该目录会强制执行和解释的固定架构。 在调用期间为支持各种会话目录 Uri 的方法，这些对象验证和合并，具体取决于受支持的架构。 与多人游戏配置相关联的主要 JSON 对象是：

   *  [MultiplayerActivityDetails (JSON)](../../json/json-multiplayeractivitydetails.md)
   *  [MultiplayerSession (JSON)](../../json/json-multiplayersession.md)
   *  [MultiplayerSessionReference (JSON)](../../json/json-multiplayersessionreference.md)
   *  [MultiplayerSessionRequest (JSON)](../../json/json-multiplayersessionrequest.md)


特别是与游戏相关的关联的 JSON 对象是：

   *  [GameMessage (JSON)](../../json/json-gamemessage.md)
   *  [GameResult (JSON)](../../json/json-gameresult.md)
   *  [GameSession (JSON)](../../json/json-gamesession.md)
   *  [GameSessionSummary (JSON)](../../json/json-gamesessionsummary.md)


<a id="ID4EBE"></a>


## <a name="handles"></a>句柄

2015 多人游戏只能，可以通过会话句柄访问会话。 添加了多个 Uri 以提供功能以支持句柄。  
<a id="ID4EFE"></a>


## <a name="in-this-section"></a>本部分内容

[/handles](uri-handles.md)

&nbsp;&nbsp;支持 POST 操作来设置用户的当前活动显示在 Xbox One 仪表板的用户体验，并邀请会话成员，如果所需的会话。

[/handles/{handleId}](uri-handleshandleid.md)

&nbsp;&nbsp;支持会话句柄标识符指定的删除和 GET 的操作。

[/handles/{handleId}/session](uri-handleshandleidsession.md)

&nbsp;&nbsp;支持 PUT 和获取对会话的操作，使用句柄取消引用。

[/handles/query](uri-handlesquery.md)

&nbsp;&nbsp;支持创建会话句柄查询 POST 操作。

[/serviceconfigs/{scid}/batch](uri-serviceconfigsscidbatch.md)

&nbsp;&nbsp;支持在服务配置标识符级别为批处理查询 POST 操作。

[/serviceconfigs/{scid}/sessions](uri-serviceconfigsscidsessions.md)

&nbsp;&nbsp;支持获取操作来检索一组会话文档。

[/serviceconfigs/{scid}/sessiontemplates](uri-serviceconfigsscidsessiontemplates.md)

&nbsp;&nbsp;支持获取操作来检索一组的 MPSD 会话模板。

[/serviceconfigs/{scid}/sessiontemplates/{sessionTemplateName}](uri-serviceconfigsscidsessiontemplatessessiontemplatename.md)

&nbsp;&nbsp;支持获取操作来检索一组会话模板名称。

[/serviceconfigs/{scid}/sessiontemplates/{sessionTemplateName}/batch](uri-serviceconfigscidsessiontemplatessessiontemplatenamebatch.md)

&nbsp;&nbsp;支持 POST 操作在会话模板级别创建批处理的查询。

[/serviceconfigs/{scid}/sessiontemplates/{sessionTemplateName}/sessions](uri-serviceconfigsscidsessiontemplatessessiontemplatenamesessions.md)

&nbsp;&nbsp;支持获取操作来检索一组指定的模板名称的会话模板。

[/serviceconfigs/{scid}/sessiontemplates/{sessionTemplateName}/sessions/{sessionName}](uri-serviceconfigsscidsessiontemplatessessiontemplatenamesessionssessionname.md)

&nbsp;&nbsp;支持创建和检索会话的 PUT 和 GET 操作。

[/serviceconfigs/{scid}/sessiontemplates/{sessionTemplateName}/sessions/{sessionName}/members/{index}](uri-serviceconfigsscidsessiontemplatessessiontemplatenamesessionnamemembersindex.md)

&nbsp;&nbsp;支持删除操作，以删除指定的会话成员。

[/serviceconfigs/{scid}/sessiontemplates/{sessionTemplateName}/sessions/{sessionName}/members/me](uri-serviceconfigsscidsessiontemplatessessiontemplatenamesessionssessionnamemembersme.md)

&nbsp;&nbsp;支持删除操作，删除会话成员。

[/serviceconfigs/{scid}/sessiontemplates/{sessionTemplateName}/sessions/{sessionName}/servers/{server-name}](uri-serviceconfigsscidsessiontemplatessessiontemplatenamesessionnamemembersservername.md)

&nbsp;&nbsp;支持删除操作，以删除指定的会话的服务器。

<a id="ID4ESF"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4EUF"></a>

   [匹配 URI](../matchtickets/atoc-reference-matchtickets.md)


<a id="ID4E1F"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[统一资源标识符 (URI) 参考](../atoc-xboxlivews-reference-uris.md)