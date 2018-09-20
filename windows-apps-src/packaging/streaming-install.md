---
author: laurenhughes
ms.assetid: df4d227c-21f9-4f99-9e95-3305b149d9c5
title: UWP 应用流式安装
description: 借助通用 Windows 平台 (UWP) 应用流式安装，可指定希望 Microsoft Store 首先下载应用的哪些部分。 当首先下载了该应用的基本文件后，用户就可以启动该应用并与其进行交互，而应用的其余部分则会在后台完成下载。
ms.author: lahugh
ms.date: 04/05/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: 安装 windows 10，uwp，流安装 uwp 应用程序流式处理
ms.localizationpriority: medium
ms.openlocfilehash: 087226cad4bcf7ea0294d8878564c345d6cfb9d0
ms.sourcegitcommit: 897a111e8fc5d38d483800288ad01c523e924ef4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2018
ms.locfileid: "304517"
---
# <a name="uwp-app-streaming-install"></a>UWP 应用流式安装
借助通用 Windows 平台 (UWP) 应用流式安装，可指定希望 Microsoft Store 首先下载应用的哪些部分。 当首先下载了该应用的基本文件后，用户就可以启动该应用并与其进行交互，而应用的其余部分则会在后台完成下载。 

若要使用 UWP 安装应用程序流式处理您需要将您的应用程序文件划分为节。 若要执行此操作，将创建内容组映射，这是一个 XML 文件，打包与您的应用程序，允许您设置下载优先级和顺序。 请参阅下面的详细信息链接的主题。

有关向应用程序流式处理安装 UWP UWP 应用程序的完整指南，查看此[博客系列](https://blogs.msdn.microsoft.com/appinstaller/2017/03/15/uwp-streaming-app-installation/)。

| 主题 | 说明 | 
|-------|-------------|
| [创建和转换源内容组映射](create-cgm.md) | 为让通用 Windows 平台 (UWP) 应用做好添加 UWP 应用流式安装的准备，需要创建内容组映射。 本文介绍有关创建和转换内容组映射的具体信息，同时提供一些相关提示和技巧。 |