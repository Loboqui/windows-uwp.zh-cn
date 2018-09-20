---
title: GET (/users/xuid({xuid})/scids/{scid}/stats/{statname)/people/{all|favorite})
assetID: 942cf0d7-f988-0495-cf28-cdac608b8109
permalink: en-us/docs/xboxlive/rest/uri-usersxuidscidstatnamepeopleget.html
author: KevinAsgari
description: " GET (/users/xuid({xuid})/scids/{scid}/stats/{statname)/people/{all|favorite})"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏, uwp, windows 10, xbox one
ms.localizationpriority: medium
ms.openlocfilehash: c62703d43197962e313e364df2cdc3650bd2a792
ms.sourcegitcommit: 68fcac3288d5698a13dbcbd57f51b30592f24860
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2018
ms.locfileid: "4061146"
---
# <a name="get-usersxuidxuidscidsscidstatsstatnamepeopleallfavorite"></a>GET (/users/xuid({xuid})/scids/{scid}/stats/{statname)/people/{all|favorite})
返回在社交排行榜的统计数据值 （分数） 为当前用户的任一所有已知的联系人或仅通过该用户指定为常用联系人的联系人的排名。
这些 Uri 的域是`leaderboards.xboxlive.com`。

  * [备注](#ID4EV)
  * [URI 参数](#ID4EAB)
  * [查询字符串参数](#ID4ELB)
  * [授权](#ID4EQD)
  * [需的请求标头](#ID4EGE)
  * [可选的请求标头](#ID4EXF)
  * [请求正文](#ID4ETG)
  * [HTTP 状态代码](#ID4ECEAC)
  * [所需的响应标头](#ID4E1HAC)
  * [可选的响应标头](#ID4EDJAC)
  * [响应正文](#ID4EDKAC)

<a id="ID4EV"></a>


## <a name="remarks"></a>备注

排行榜 Api 都是只读的因此 （通过 HTTPS) 仅支持获取动词命令。 它们反映排名和排序的"页"派生通过数据平台编写的单个用户统计数据的编制了索引的玩家统计数据。 完整的排行榜索引可能会相当大，并将永远不会要求调用方看到一个完整，因此此 URI 支持多个允许调用方是哪种类型的视图其想要针对的排行榜，请参阅有关特定的查询字符串参数。

获取操作不会修改任何资源，因此如果执行一次或多次，这将产生相同的结果。

<a id="ID4EAB"></a>


## <a name="uri-parameters"></a>URI 参数

| 参数| 类型| 说明|
| --- | --- | --- |
| xuid| 字符串| 用户的标识符。|
| scid| 字符串| 服务配置，其中包含要访问的资源的标识符。|
| statname| 字符串| 正在访问的用户统计数据资源的唯一标识符。|
| 全部|收藏夹| 枚举| 是否要排名统计数据值 （分数） 为当前用户的所有已知的联系人或仅通过该用户指定为常用联系人的联系人。|

<a id="ID4ELB"></a>


## <a name="query-string-parameters"></a>查询字符串参数

| 参数| 类型| 说明|
| --- | --- | --- | --- | --- | --- |
| maxItems| 32 位无符号的整数| 排行榜要返回的记录的结果页中的最大数量。 如果未指定，默认数量将返回 (10)。 MaxItems 的最大值是仍未定义的但我们想要避免大型数据集，所以此值应该可能的最大设置的 UI 可以处理每个调用调谐器。 |
| skipToRank| 32 位无符号的整数| 返回结果与指定的排行榜排名启动的页面。 结果的其余部分将按排名排序顺序。 此查询字符串可以返回到后续查询以获取"下一步"的结果页返回延续令牌可以馈送。 |
| skipToUser| 字符串| 返回排行榜结果周围的指定玩家 xuid，无论该用户的排名或分数的页面。 该页面将按指定用户在页面的预定义视图，最后位置或统计数据的排行榜视图中间百分点等级进行排序。 没有任何<b>continuationToken</b>提供此类查询。 |
| ContinuationToken| 字符串| 如果上一个调用返回<b>continuationToken</b>，然后调用方可以传递回该令牌"按原样"查询字符串以获取结果的下一页。 |
| 排序| 字符串| 指定是否排名从低到高值顺序 （"升序"） 的玩家的列表或高到低值顺序 （"降序"）。 这是一个可选参数。默认值为降序顺序。|

<a id="ID4EQD"></a>


## <a name="authorization"></a>授权

Xuid 授权是必需的。

授权逻辑是出于内容隔离和访问控制方案实现的。

排行榜和用户的统计数据可以读取的所有平台上的客户端，前提是调用方提交他们的请求的有效 XSTS 令牌。 写入到数据平台支持的客户端 （显然） 受到。

游戏开发人员可以将统计数据标记为打开或 XDP 或开发人员中心使用限制。 排行榜是开放的统计信息。 打开统计信息可以访问 Smartglass，以及 iOS、 Android、 Windows、 Windows Phone 和 web 应用程序，只要用户有权沙盒。 通过 XDP 或开发人员中心管理到沙盒的用户身份验证。

<a id="ID4EGE"></a>


## <a name="required-request-headers"></a>需的请求标头

| 标题| 说明|
| --- | --- | --- | --- | --- | --- | --- | --- |
| 授权| 字符串。 HTTP 身份验证的身份验证凭据。 示例值:"XBL3.0 x =&lt;userhash >;&lt;令牌 >"。|
| Content-Type| 字符串。 请求正文的 MIME 类型。 示例值:"应用程序/json"。|
| X RequestedServiceVersion| 生成此请求应定向到 Xbox LIVE 的服务的名称/数。 请求仅为路由到服务验证该标头，身份验证令牌中的声明的有效性后等。 默认值： 1。|
| 接受| 字符串。 可接受的内容类型值。 示例值:"应用程序/json"。|

<a id="ID4EXF"></a>


## <a name="optional-request-headers"></a>可选的请求标头

| 标题| 说明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| If-None-Match| 字符串。 实体标记-如果客户端支持缓存使用。 示例值:"686897696a7c876b7e"。|

<a id="ID4ETG"></a>


## <a name="request-body"></a>请求正文

若要最大化的任何调用方的能力，以了解其正确显示重新获取数据，每位用户每个统计数据值将在其中它应显示，和格式化以匹配接受的语言中指定的区域设置格式的字符串作为返回在请求中的标头。 为该排行榜 statname 将还返回本地化"显示名称"。

<a id="ID4E2G"></a>


### <a name="required-members"></a>所需的成员

| 成员| 说明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| <b>pagingInfo</b>| 部分| 可选。 在页面中的最后一项的排名低于 totalItems 时返回。 本部分还不会返回时请求中指定 skipToUser。|
| ContinuationToken| 字符串| 必需。 指定要返回到"continuationToken"查询参数，以获取该 URI 的下一页结果，如果所需的源的值。 如果没有 pagingInfo 返回则没有"下一页"要获取的数据。|
| totalItems| 64 位无符号的整数| 必需。 排行榜中的条目的总数。|
| <b>leaderboardInfo</b>| 部分| 必需。 始终返回。 包含有关请求排行榜的元数据。|
| 显示名称| 字符串| 必需。 预定义的排行榜的本地化的显示名称。 示例值:"总捕获的标志"。|
| totalCount| 字符串| 必需。 排行榜中的条目的总数。|
| 列| array| 必需。|
| 显示名称| 字符串| 必需。 对应于排行榜中的列。|
| statName| 字符串| 必需。 对应于排行榜中的列。|
| type| 字符串| 必需。 对应于排行榜中的列。|
| <b>用户列表</b>| 部分| 必需。 始终返回。 包含请求的排行榜的实际的用户评分。|
| 玩家代号| 字符串| 必需。 对应于用户在排行榜条目。|
| xuid| 32 位有符号的整数| 必需。 对应于用户在排行榜条目。|
| 百分比| 字符串| 必需。 对应于用户在排行榜条目。|
| 排名| 字符串| 必需。 对应于用户在排行榜条目。|
| 值| array| 必需。 每个以逗号分隔的值对应于排行榜中的列。|

<a id="ID4ECEAC"></a>


## <a name="http-status-codes"></a>HTTP 状态代码

该服务返回的状态代码之一此部分中使用此方法对此资源进行的请求的响应。 有关使用 Xbox Live 服务的标准 HTTP 状态代码的完整列表，请参阅[标准 HTTP 状态代码](../../additional/httpstatuscodes.md)。

| 代码| 原因短语| 说明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 200| “确定”| 已成功检索会话。|
| 304| 未修改|  |
| 400| 错误请求| | 服务可能不理解格式不正确的请求。 通常是一个无效的参数。|
| 401| 未授权| | 请求要求用户身份验证。|
| 403| 已禁止| 为用户或服务不允许该请求。|
| 404| 找不到| 找不到指定的资源。|
| 406| 不允许| 资源版本不受支持;应拒绝 MVC 层。|
| 408| 请求超时| 服务可能不理解格式不正确的请求。 通常是一个无效的参数。|

<a id="ID4E1HAC"></a>


## <a name="required-response-headers"></a>所需的响应标头

| 标头| 类型| 说明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Content-Type| 字符串| 该响应正文的 mime 类型。 示例值:"应用程序/json"。|
| Content-Length| 字符串| 在响应中发送的字节数。 示例值:"232"。|

<a id="ID4EDJAC"></a>


## <a name="optional-response-headers"></a>可选的响应标头

| 标头| 类型| 说明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ETag| 字符串| 用于缓存优化。 示例值:"686897696a7c876b7e"。|

<a id="ID4EDKAC"></a>


## <a name="response-body"></a>响应正文

社交排行榜，没有分页请求：

https://leaderboards.xboxlive.com/users/xuid(2533274916402282)/scids/c1ba92a9-0000-0000-0000-000000000000/stats/EnemyDefeats/people/all?sort=descending

<a id="ID4ENKAC"></a>


### <a name="sample-response"></a>示例响应


```cpp
{
    "pagingInfo": null,
    "leaderboardInfo": {
        "displayName": "Kills",
        "totalCount": 3,
        "columns": [
            {
                "displayName": "Kills",
                "statName": "enemydefeats",
                "type": "integer"
            }
        ]
    },
    "userList": [
        {
            "gamertag":"xxxSniper39",
            "xuid":"1234567890123555",
            "percentile":1.0,
            "rank":1,
            "values": [
                "47"
            ]
        },
        {
            "gamertag":"WarriorSaint",
            "xuid":"2533274916402282",
            "percentile":0.66,
            "rank":2,
            "values": [
                "42"
            ]
        },
        {
            "gamertag":"WhockaWhocka",
            "xuid":"1234567890123666",
            "percentile":0.33,
            "rank":3,
            "values": [
                "12"
            ]
        }
    ]
}

```


<a id="ID4EXKAC"></a>


## <a name="see-also"></a>另请参阅

<a id="ID4EZKAC"></a>


##### <a name="parent"></a>Parent 的子磁盘）

[/ 用户/xuid ({xuid}) /scids/ {scid} /stats/ {statname) /people/ {all\ | 最喜爱}](uri-usersxuidscidstatnamepeople.md)