---
ms.assetid: b556a245-6359-4ddc-a4bd-76f9873ab694
description: 使用 Microsoft Store 分析 API 中的此方法，可获取应用中的错误堆栈跟踪。
title: 获取应用中的错误的堆栈跟踪
ms.date: 06/05/2018
ms.topic: article
keywords: windows 10, uwp, Microsoft Store 服务, Microsoft Store 分析 API, 堆栈跟踪, 错误
ms.localizationpriority: medium
ms.openlocfilehash: ceffc7622f756eb17c8475208852e013df814554
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57627452"
---
# <a name="get-the-stack-trace-for-an-error-in-your-app"></a>获取应用中的错误的堆栈跟踪

使用 Microsoft Store 分析 API 中的此方法，可获取应用中的错误堆栈跟踪。 此方法仅可以下载过去 30 天内发生的应用错误的堆栈跟踪。 堆栈跟踪也会出现在**故障**一部分[运行状况报告](../publish/health-report.md)在合作伙伴中心。

在可以使用此方法之前，必须首先使用[获取应用中的错误的详细信息](get-details-for-an-error-in-your-app.md)方法来检索与想要检索堆栈跟踪的错误相关联的 CAB 文件 ID。

## <a name="prerequisites"></a>必备条件


若要使用此方法，首先需要执行以下操作：

* 完成 Microsoft Store 分析 API 的所有[先决条件](access-analytics-data-using-windows-store-services.md#prerequisites)（如果尚未这样做）。
* [获取 Azure AD 访问令牌](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)，以供在此方法的请求标头中使用。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。
* 获取与想要检索堆栈跟踪的错误相关联的 CAB 文件的 ID。 若要获取此 ID，请使用[获取应用中的错误的详细信息](get-details-for-an-error-in-your-app.md)方法来检索应用中特定错误的详细信息，并使用该方法的响应正文中的 **cabId** 值。

## <a name="request"></a>请求


### <a name="request-syntax"></a>请求语法

| 方法 | 请求 URI                                                          |
|--------|----------------------------------------------------------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/stacktrace``` |


### <a name="request-header"></a>请求头

| 标头        | 在任务栏的搜索框中键入   | 描述                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** *token*&lt;&gt;。 |


### <a name="request-parameters"></a>请求参数

| 参数        | 在任务栏的搜索框中键入   |  描述      |  必需  |
|---------------|--------|---------------|------|
| applicationId | 字符串 | 要获取堆栈跟踪的应用的应用商店 ID。 Store ID 位于[应用程序标识页](../publish/view-app-identity-details.md)在合作伙伴中心。 存储 ID 的一个示例是 9WZDNCRFJ3Q8。 |  是  |
| cabId | 字符串 | 获取与想要检索堆栈跟踪的错误相关联的 CAB 文件的唯一 ID。 若要获取此 ID，请使用[获取应用中的错误的详细信息](get-details-for-an-error-in-your-app.md)方法来检索应用中特定错误的详细信息，并使用该方法的响应正文中的 **cabId** 值。 |  是  |

 
### <a name="request-example"></a>请求示例

以下示例演示了如何使用此方法获取堆栈跟踪。 将 *applicationId* 值替换为你的应用的存储 ID。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/stacktrace?applicationId=9NBLGGGZ5QDR&cabId=1336373323853 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应


### <a name="response-body"></a>响应正文

| 值      | 在任务栏的搜索框中键入    | 描述                  |
|------------|---------|--------------------------------|
| 值      | 数组   | 一组对象，其中每个包含堆栈跟踪数据的一个帧。 有关每个对象中的数据的详细信息，请参阅以下[堆栈跟踪值](#stack-trace-values)部分。 |
| @nextLink  | 字符串  | 如果存在数据的其他页，此字符串中包含的 URI 可用于请求下一页数据。 例如，当请求的 **top** 参数设置为 10，但查询的错误超过 10 行时，就会返回此值。 |
| TotalCount | 整数 | 查询的数据结果中的行总数。          |


### <a name="stack-trace-values"></a>堆栈跟踪值

*Value* 数组中的元素包含以下值。

| 值           | 在任务栏的搜索框中键入    | 描述      |
|-----------------|---------|----------------|
| level            | 字符串  |  此元素在调用堆栈中表示的帧编号。  |
| image   | 字符串  |   可执行文件或库映像的名称，包含在此堆栈帧中调用的函数。           |
| function | 字符串  |  在此堆栈帧中调用的函数名称。 仅当应用包含可执行文件或库的符号时才可用。              |
| offset     | 字符串  |  相对于函数开始的当前指令的字节偏移量。      |


### <a name="response-example"></a>响应示例

以下示例举例说明此请求的 JSON 响应正文。

```json
{
  "Value": [
    {
      "level": "0",
      "image": "Contoso.ContosoApp",
      "function": "Contoso.ContosoApp.MainPage.DoWork",
      "offset": "0x25C"
    }
    {
      "level": "1",
      "image": "Contoso.ContosoApp",
      "function": "Contoso.ContosoApp.MainPage.Initialize",
      "offset": "0x26"
    }
    {
      "level": "2",
      "image": "Contoso.ContosoApp",
      "function": "Contoso.ContosoApp.Start",
      "offset": "0x66"
    }
  ],
  "@nextLink": null,
  "TotalCount": 3
}

```

## <a name="related-topics"></a>相关主题

* [运行状况报告](../publish/health-report.md)
* [使用 Microsoft Store 服务的访问分析数据](access-analytics-data-using-windows-store-services.md)
* [获取错误报告数据](get-error-reporting-data.md)
* [获取应用程序中错误的详细信息](get-details-for-an-error-in-your-app.md)
* [下载您的应用程序中的错误的 CAB 文件](download-the-cab-file-for-an-error-in-your-app.md)
