---
title: 多人游戏会话状态代码
author: KevinAsgari
description: 介绍在请求多人游戏会话时从 Xbox Live 服务返回的状态代码。
ms.assetid: 4ab320d6-8050-41a9-9f00-faaad3b128fd
ms.author: kevinasg
ms.date: 04/04/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: xbox live, xbox, 游戏 uwp, windows 10, xbox one, 多人游戏 2015, 状态代码, 会话
ms.localizationpriority: medium
ms.openlocfilehash: 39320e9bf051c0cb2fd1c9936cd5472f46d6d38e
ms.sourcegitcommit: 68fcac3288d5698a13dbcbd57f51b30592f24860
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2018
ms.locfileid: "4060016"
---
# <a name="multiplayer-session-status-codes"></a>多人游戏会话状态代码

本主题列出了与会话有关的多人游戏状态代码。

| 注意                                                                                                         |
|---------------------------------------------------------------------------------------------------------------------------|
| 返回会话的 4xx 状态代码始终返回整个会话，即使 URI 指向会话元素。 |


| 状态代码 | 字符串              | 内容类型     | 正文    | 描述 |
|----|
| 200         | 正常                  | 应用程序/json | 会话 | 成功读取 (GET) 或更新 (PUT)。                                                                                                                                                                                                                                                                                                             |
| 201         | 已创建             | 应用程序/json | 会话 | 成功创建。                                                                                                                                                                                                                                                                                                                                 |
| 202         | 已接受            | 文本/无格式       | 无    | 已接受请求，但尚未完成。                                                                                                                                                                                                                                                                                             |
| 204         | 无内容          |                  |         | 在会话的 GET 中，会话不存在。 在会话元素的 GET 中，会话存在但元素不存在。 在会话的 PUT 中，会话由于 PUT 操作被删除。 在会话元素的 PUT 或 DELETE 中，当操作开始时会话存在，但会话或元素已不再存在。 |
| 304         | 未修改        |                  |         | 在标头为 If-None-Match 的 GET 中，会话未更改。                                                                                                                                                                                                                                                                                        |
| 400         | 错误请求         | 文本/无格式       | 消息 | 请求被假设为在第一次检查时无效。 其缺少必填字段或 JSON 文件格式不正确。 正文包括其他详细信息。                                                                                                                                                                                        |
| 403         | 已禁止           | 文本/无格式       | 消息 | 请求在某些上下文中可能有效，但对于其上下文无效。 授权已失败。                                                                                                                                                                                                                                                |
|             |                     | 应用程序/json | 会话 | 会话无法由用户更新，但可以读取。                                                                                                                                                                                                                                                                                           |
| 404         | 找不到           | 文本/无格式       | 消息 | 会话无法被访问，因为 URI 无效；句柄 SCID 或会话模板无法找到；hopper 无法找到；会话元素无法访问，因为会话不存在；或针对会话的元素查找无效。                                                                                 |
| 405         | 不允许的方法  | 文本/无格式       | 消息 | 请求 URI 看似正确，但谓词是错误的。 例如，当需要 PUT 操作时，请求是针对 POST 操作的。                                                                                                                                                                                                                 |
| 409         | 冲突            | 文本/无格式       | 消息 | 会话无法更新，因为请求与会话不兼容。 例如，请求中的常量与会话或会话模板中的常量冲突，或调用方以外的成员被添加到大型会话或被从中删除。                                                                         |
| 412         | 前置条件失败 |                  |         | If-Match 标头或 If-None-Match 标头（对于 GET 以外的操作）无法达到满意要求。                                                                                                                                                                                                                                           |
|             |                     | 应用程序/json | 会话 | If-Match 标头无法在现有会话的 PUT 或 DELETE 操作中达到满意要求。 返回会话的当前状态以及当前的 ETag 值。                                                                                                                                                                      |
| 429 | 请求太多 | 应用程序/json | 消息 | 服务调用由于超出细化速率限制而被阻止。 有关详细信息，请参阅[细化速率限制](../../using-xbox-live/best-practices/fine-grained-rate-limiting.md)。 |
| 503         | 服务不可用 | 文本/无格式       | 无    | 服务已重载，应稍后重试请求。 此代码包括客户端应服从的 Retry-After 标头。                                                                                                                                                                                                              |