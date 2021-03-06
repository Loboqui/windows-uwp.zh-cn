---
title: 三角形插值
description: 在渲染期间，管道会在每个三角形中插入顶点数据。
ms.assetid: 1A76DD78-CED7-42BE-BA81-B9050CD3AF9B
keywords:
- 三角形插值
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: e8017cd75ed3dfd4129d6c15d668648792cc8d0a
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57592902"
---
# <a name="triangle-interpolation"></a>三角形插值


在渲染期间，管道会在每个三角形中插入顶点数据。 顶点数据可以是各种各样的数据并可以包括（但不限于）：漫射颜色、反射颜色、漫射 alpha（三角形不透明度）、反射 alpha 和雾化系数。 对于可编程的顶点管道，雾系数取自雾注册。 对于固定函数顶点管道，雾系数取自反射 alpha。

对于某些顶点数据，内插取决于当前阴影模式，如下所示：

| 阴影模式 | 描述                                                                                                                                                                 |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 平面         | 仅在平面阴影模式下内插雾系数。 对于所有其他内插值，将在整个面中应用三角形中第一个顶点的颜色。 |
| 高氏      | 将在所有三个顶点之间执行线性内插。                                                                                                               |

 

漫射颜色和反射颜色的处理方式不同，具体取决于颜色模式。 在 RGB 颜色模式中，系统将在内插中使用红色、绿色和蓝色组件。

颜色的 alpha 组件将被视为单独的内插值，因为设备驱动程序可通过两种不同的方式实施透明：使用纹理混合或点彩。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>相关主题


[坐标系统和几何结构](coordinate-systems-and-geometry.md)

 

 




