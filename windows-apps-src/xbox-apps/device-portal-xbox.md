---
ms.assetid: bf0a8b01-79f1-4944-9d78-9741e235dbe9
title: 适用于 Xbox 的 Device Portal
description: 了解如何启用适用于 Xbox One 的 Device Portal。
ms.date: 04/09/2019
ms.topic: article
keywords: windows 10，uwp，设备门户
ms.localizationpriority: medium
ms.openlocfilehash: db0d2955f01fcae04a85c57a6dc28a32c561553a
ms.sourcegitcommit: 139717a79af648a9231821bdfcaf69d8a1e6e894
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67713845"
---
# <a name="device-portal-for-xbox"></a>适用于 Xbox 的 Device Portal

## <a name="set-up-device-portal-on-xbox"></a>在 Xbox 上设置 Device Portal

以下步骤显示如何启用 Xbox 设备门户，从而为你提供对你的开发 Xbox 的远程访问。

1. 打开“开发人员主页”。 默认情况下，该主页应在你启动开发 Xbox 时打开，但你也可以从主屏幕打开它。

    ![Device Portal DevHome](images/device-portal-xbox-1.png)

2. 在开发人员主页中，在**主页**选项卡上的**远程访问**下，选择**远程访问设置**。

    ![设备门户 RemoteManagement 工具](images/device-portal-xbox-15.png)

3. 选中**启用 Xbox 设备门户** 设置。

4. 在**身份验证**下，选择**设置用户名和密码**。 输入用于从浏览器对开发套件的访问进行身份验证的**用户名**和**密码**，然后**保存**它们。

5. **关闭** **远程访问**页面，并在**主页**选项卡上，记下**远程访问**下列出的 URL。

6. 在浏览器中输入 URL，然后使用已配置的凭据登录。

7. 你将收到有关已提供的证书的警告，与下图中的内容类似。 在 Microsoft Edge 中，单击**详细信息**，然后**转到网页**以访问 Xbox 设备门户。 在弹出的对话框中，输入您之前在 Xbox 中输入的用户名和密码。

    ![Device Portal 证书错误](images/device-portal-xbox-3.png)

## <a name="device-portal-pages"></a>Device Portal 页面

Xbox 设备门户提供了一组与 Windows 设备门户上可用的页面类似的标准页面以及唯一的多个页面。 有关前者的详细说明，请参阅 [Windows 设备门户概述](../debug-test-perf/device-portal.md)。 以下部分介绍对 Xbox 设备门户是唯一的页面。

### <a name="home"></a>主页

与 Windows 设备门户的**应用管理器**页面类似，Xbox 设备门户的**主页**显示**我的游戏和应用**下已安装的游戏和应用列表。 您可以单击某个游戏或应用的名称查看有关它的更多详细信息，如**包系列名称**。 在**操作**下拉列表中，你可以对游戏或应用执行操作，如**启动**它。

在 **Xbox Live 测试帐户**下，你可以管理与 Xbox 关联的帐户。 你可以添加用户和来宾帐户、创建新用户、用户登录和注销以及删除帐户。

![主页](images/device-portal-xbox-16.png)

### <a name="xbox-live-game-saves"></a>Xbox Live（游戏保存）

Windows 设备门户和 Xbox 设备门户均有一个 **Xbox Live** 页面。 但是，Xbox 设备门户有一个独特的部分 **Xbox Live 游戏保存**，在此部分中，你可以保存已在 Xbox 上安装的游戏的数据。 输入与标题和游戏保存关联的**服务配置 ID (SCID)** （有关更多信息，请参阅 [Xbox Live 服务配置](https://docs.microsoft.com/gaming/xbox-live/xbox-live-service-configuration.md#get-your-ids)）、**成员名(MSA)** 和**包系列名称(PFN)** ，浏览**输入文件(.json 或 .xml)** ，然后选择其中一个按钮（**重置**、**导入**、**导出**和**删除** ）来操作保存数据。

在**生成**部分中，你可以生成虚拟数据并保存到指定的输入文件中。 只需输入**容器(默认为 2 个)** 、**Blob (默认为 3 个)** 和 **Blob 大小(默认为 1024)** ，然后选择**生成**。

![Xbox Live](images/device-portal-xbox-17.png)

### <a name="http-monitor"></a>HTTP 监视器

HTTP 监视器允许你当其在你的 Xbox One 上运行时查看你的应用或游戏中已解密的 HTTP 和 HTTPS 流量。

![HTTP 监视器](images/device-portal-xbox-18.png)

若要启用它，在 Xbox One 上打开开发人员主页，转到**设置**选项卡，然后在 **HTTP 监视器设置**框中，选中**启用 HTTP 监视器**。

![适用于开发人员主页：网络](images/device-portal-xbox-14.png)

启用此项后，在 Xbox 设备门户中，你可以通过选择相应按钮来对 HTTP 和 HTTPS 流量执行**停止**、**清除**和**保存到文件**操作。

### <a name="network-fiddler-tracing"></a>网络(Fiddler 跟踪)

Xbox 设备门户中的**网络**页面与 Windows 设备门户中的**网络**页面几乎相同，唯一不同是 **Fiddler 跟踪**功能，这是 Xbox 设备门户的独特功能。 这允许你在电脑上运行 Fiddler 记录和检查你的 Xbox One 与 Internet 之间的 HTTP 和 HTTPS 流量。 有关更多信息，请参阅[在针对 UWP 进行开发时如何将 Fiddler 用于 Xbox One](../xbox-apps/uwp-fiddler.md)。

![网络](images/device-portal-xbox-19.png)

### <a name="media-capture"></a>媒体捕获

在**媒体捕获**页面上，你可以选择**捕获屏幕截图**来拍摄 Xbox One 的屏幕截图。 在执行此操作后，你的浏览器将提示你下载该文件。 如果你想要以 HDR 拍摄屏幕截图（如果控制台支持它），则可以选中**首选 HDR**。

![媒体捕获](images/device-portal-xbox-12.png)

### <a name="settings"></a>设置

在**设置**页面上，你可以查看和编辑 Xbox One 的多个设置。 在顶部，你可以选择**导入**以从文件中导入设置，然后选择**导出**以将当前设置导出至 .txt 文件。 导入设置可实现更轻松批量编辑，尤其是在配置多个控制台时。 若要创建要导入的设置文件，将设置更改为你希望其形成的方式，然后导出设置。 然后，可以使用此文件为其他控制台快速轻松地导入设置。

以下几个部分具有要查看和/或编辑的不同设置，如下所述。

![设置](images/device-portal-xbox-20.png)

![设置](images/device-portal-xbox-21.png)

#### <a name="device-information"></a>设备信息

* **设备名称**:设备的名称。 若要编辑，在框中更改该名称，然后选择**保存**。

* **OS 版本**:只读的。 操作系统的版本号。

* **OS 版本**:只读的。 主要版本操作系统的名称。

* **Xbox Live 设备 ID**:只读的。

* **控制台 ID**:只读的。

* **序列号**:只读的。

* **控制台类型**:只读的。 Xbox One 设备的类型（Xbox One、Xbox One S 或 Xbox One X）。

* **开发人员模式**:只读的。 设备所处的开发人员模式。

#### <a name="audio-settings"></a>音频设置

* **音频位流格式**:音频数据的格式。

* **HDMI 音频**:通过 HDMI 端口的音频的类型。

* **耳机格式**:通过耳机的音频格式。

* **光学音频**:通过光学端口的音频的类型。

* **使用 HDMI 或光学音频耳机**:如果将耳机连接通过 HDMI 或光盘，请选中此框。

#### <a name="display-settings"></a>显示设置

* **颜色深度**:为一个像素的每个颜色组件使用的位的数目。

* **颜色空间**:色域供显示。

* **显示分辨率**:显示的分辨率。

* **显示连接**:连接到显示的类型。

* **允许高动态范围 (HDR)** :启用 HDR 上显示。 仅适用于兼容的屏幕。

* **允许 4k**:使 4k 分辨率的显示器上。 仅适用于兼容的屏幕。

* **允许变量刷新速率 (VRR)** :启用 VRR 上显示。 仅适用于兼容的屏幕。

#### <a name="kinect-settings"></a>Kinect 设置

Kinect 传感器必须连接到控制台才能更改以下这些设置。

* **启用 Kinect**:启用附加的 Kinect 传感器。

* **在应用更改时重新加载强制 Kinect**:无论何时运行不同的应用或游戏，重新加载附加的 Kinect 传感器。

#### <a name="localization-settings"></a>本地化设置

* **地理区域**:设备设置为在地理区域。 必须为特定的 2 个字符国家/地区代码（例如，**US** 表示美国）。

* **首选语言**:设备设置为语言。

* **时区**:设备设置为的时区。

#### <a name="network-settings"></a>网络设置

* **无线广播设置**:无线设备 （如无线 LAN 的某些方面是否打开或关闭） 的设置。

#### <a name="power-settings"></a>电源设置

* **当处于空闲状态时，dim 屏幕 （分钟） 后的**:设备的此时间内处于空闲状态后，屏幕会变暗。 设置为 **0** 表示屏幕永远不会变暗。

* **如果处于空闲状态，请关闭后**:在空闲此段时间后，设备将关闭。

* **电源模式**:设备的电源模式。 有关更多信息，请参阅[有关节能和随开即用电源模式](https://support.xbox.com/xbox-one/console/learn-about-power-modes)。

* **自动启动控制台时连接到电源**:当连接到电源时，将自动开启设备。

#### <a name="preference-settings"></a>首选项设置

* **默认主页体验**:主屏幕将显示在设备开启时的设置。

* **允许来自 Xbox 应用程序的连接**:另一台设备 （如 Windows 10 电脑） 上的 Xbox 应用可以连接到此控制台。

* **默认情况下将视为游戏的 UWP 应用**:游戏和应用程序获取 Xbox 上分配给它们的不同资源。 如果选中此框，所有 UWP 程序包将标识为游戏，并因此获取更多资源。

#### <a name="user-settings"></a>用户设置

* **自动登录用户**:中选定的用户在设备开启时自动登录。

* **自动登录用户控制器**:自动将特定的控制器类型与特定用户相关联。

#### <a name="xbox-live-sandbox"></a>Xbox Live 沙盒

在这里，你可以更改设备所在的 Xbox Live 沙盒。 在框中输入沙盒的名称，然后选择**更改**。

### <a name="scratch"></a>Scratch

这是一个空白工作区，你可以根据自己的喜好自定义它。 你可以使用菜单（单击左上角的菜单按钮）添加工具（选择**将工具添加到工作区**，然后选择要添加的工具，然后选择**添加**）。 请注意，你可以使用此菜单将工具添加到任何工作区，以及自行管理工作区。

![将工具添加到工作区](images/device-portal-xbox-13.png)

### <a name="game-event-data"></a>游戏事件数据

上**游戏事件数据**页上，您可以查看流的实时关系图中的当前记录在 Xbox One 上的事件跟踪 Windows (ETW) 游戏事件数。 如果有记录在系统上的游戏事件，您还可以查看详细信息 （事件名称、 事件匹配项和游戏标题） 描述数据在图表下方的数据表中的每个事件。 表才可用，如果有记录的事件。

![游戏事件数据](images/device-portal-xbox-22.PNG)

## <a name="see-also"></a>请参阅

* [Windows Device Portal 概述](../debug-test-perf/device-portal.md)
* [设备门户 core API 参考](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-api-core)
