---
title: 无服务器体系结构的无服务器应用
description: 各种体系结构和应用程序所支持的无服务器体系结构，包括 web 应用、 移动和 IoT 的探索。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: ea944a172154a1cff2b8f830cb8fc3fa24a15028
ms.sourcegitcommit: 4c158beee818c408d45a9609bfc06f209a523e22
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "49369661"
---
# <a name="serverless-architecture"></a>无服务器体系结构

有许多方法使用无服务器体系结构。 这一章介绍了集成无服务器的常见体系结构的示例。 它还介绍了可能会带来额外挑战或实现无服务器时需要额外考虑的问题。 最后，设计的几个示例都是提供说明不同的无服务器的使用方案。

无服务器主机通常使用现有的基于容器的或 PaaS 层来管理无服务器的实例。 例如，基于 Azure Functions [Azure 应用服务](https://docs.microsoft.com/azure/app-service/)。 应用服务用于横向扩展实例和管理执行 Azure Functions 代码的运行时。 对于基于 Windows 的函数，作为 PaaS 和可扩展的主机运行带.NET 运行时。 对于基于 Linux 的函数，主机会利用容器。

![Azure Functions 体系结构](./media/azure-functions-architecture.png)

WebJobs 核心提供用于函数的执行上下文。 语言运行时运行脚本、 执行库和承载目标语言的框架。 例如，使用 Node.js 运行 JavaScript 函数，.NET Framework 用于运行 C# 函数中。 您将了解有关本章后面的语言和平台选项的详细信息。

某些项目可能受益于对无服务器采用"全面的"方法。 应用程序非常依赖微服务可能会实现所有微服务都使用无服务器技术。 大多数应用而言是混合环境中，以下的 N 层设计和使用无服务器的组件的意义，因为组件是模块化且可独立缩放。 为了帮助理解这些情况下，此部分将指导完成一些使用无服务器的常见体系结构示例。

## <a name="full-serverless-back-end"></a>完全无服务器的后端

尤其是新生成时，非常适合于多种类型的情况下，完全无服务器的后端或"绿色字段"应用程序。 具有较大的表面区域的 Api 的应用程序可能受益于实现的无服务器函数为每个 API。 基于微服务体系结构的应用程序是可作为一个完整的无服务器的后端实现的另一个示例。 微服务通过各种协议相互通信。 特定的方案包括：

* 基于 API 的 SaaS 产品 (示例： 财务付款处理器)。
* 消息驱动应用程序 (示例： 设备监视解决方案)。
* 应用关注服务之间的集成 (示例： 航班预订应用程序)。
* 定期运行进程 (示例： 基于计时器的数据库清除)。
* 应用侧重于数据转换 (示例： 导入文件上传触发)。
* 提取转换和加载 (ETL) 过程。

有更高版本中本文档介绍的其他、 更具体用例。

## <a name="monoliths-and-starving-the-beast"></a>庞大的单体结构并在"耗尽怪兽"

常见的难题将现有单一式应用程序到云迁移。 至少风险的方法是"提升和转移"到虚拟机上完全。 许多服务提供商更喜欢使用这个机会，将迁移以实现其基本代码的现代化。 迁移的可行方法被调用"耗尽怪兽"。 在此方案中，迁移单体结构，"按原样"开始使用。 然后，所选的服务会得到改进。 在某些情况下，该服务的签名等同于原始： 它只托管为函数。 客户端已更新为使用新的服务而不是整体应用程序终结点。 在此期间，如数据库复制的步骤使微服务来托管其自己的存储，即使事务仍由单体结构。 最终，所有客户端迁移到新服务。 单体结构"会耗尽"（其服务不再称为） 直到替换所有功能。 组合的无服务器和代理可以通过此迁移的很多方便。

![无服务器的整体应用程序迁移](./media/serverless-monolith-migration.png)

若要了解有关这种方法的详细信息，请观看视频：[将应用迁移到使用无服务器 Azure Functions 在云中](https://channel9.msdn.com/Events/Connect/2017/E102)。

## <a name="web-apps"></a>Web 应用

Web 应用程序很适合无服务器应用程序。 目前有两种常用方法到 web 应用： 服务器驱动的和客户端驱动 （如单页面应用程序或 SPA）。 服务器驱动的 web 应用程序通常使用中间件层发出 API 调用，以呈现 web UI。 SPA 应用程序直接从浏览器进行 REST API 调用。 在这两种情况下，无服务器通过提供必要的业务逻辑可以适应中间件或 REST API 请求。 常见的体系结构是以建立静态的轻型 web 服务器。 单页面应用程序 (SPA) 是 HTML、 CSS、 JavaScript 和其他浏览器资产。 然后，web 应用连接到微服务后端。

## <a name="mobile-back-ends"></a>移动后端

无服务器应用的事件驱动模式，使其作为移动后端的理想之选。 移动设备触发的事件和无服务器代码执行来满足请求。 利用无服务器模型使开发人员能够增强业务逻辑，而无需部署完整的应用程序更新。 无服务器方法还使团队能够共享终结点和并行工作。

移动开发人员可以构建业务逻辑，而不会成为在服务器端的专家。 传统上，移动应用连接到的本地服务。 构建服务层需要了解服务器平台和编程范例。 开发人员结合操作预配的服务器，然后相应地对其进行配置。 有时数天或甚至数周时间都花在生成的部署管道。 所有这些难题进行寻址的无服务器。

无服务器提取服务器端依赖项，并使开发人员可以专注于业务逻辑。 例如，移动开发人员构建使用 JavaScript 框架的应用可以生成无服务器函数使用 JavaScript 以及。 无服务器的主机管理操作系统的 Node.js 实例来承载代码、 包依赖项和的详细信息。 开发人员提供一组简单的输入和标准模板的输出。 它们然后可以专注于构建和测试业务逻辑。 因此您可以使用现有技能来构建移动应用后端逻辑，而无需了解新的平台或成为"服务器端开发人员。"

![无服务器移动后端](./media/serverless-mobile-backend.png)

大多数云提供商提供的基于 mobile 的无服务器产品，用于简化整个移动开发生命周期。 产品可能会自动预配的数据库，以保留数据、 处理 DevOps 问题、 提供基于云的生成和测试框架和脚本使用开发人员的业务流程的能力首选语言。 以移动为中心的无服务器方法可以简化过程。 无服务器中删除预配、 配置和维护移动后端服务器的巨大开销。

## <a name="internet-of-things-iot"></a>物联网 (IoT)

IoT 是指它们联网在一起的物理对象。 它们有时简称为"已连接的设备"或"智能设备"。 从汽车和自动贩卖机的所有内容可能会连接并发送到如温度和湿度传感器数据的各种从清单信息。 在企业中，IoT 提供了通过监控和自动化的业务流程改进。 IoT 数据可能用于控制在大型仓库气候或跟踪通过供应链的清单。 IoT 可以感测化工溢出，并在检测到烟雾时调用消防部门。

超大批量的设备和信息通常决定了事件驱动的体系结构到路由和处理消息。 无服务器的原因是一个理想的解决方案：

* 启用增加的数量增加设备和数据。
* 适合于添加新的终结点以支持新的设备和传感器。
* 便于独立的版本控制，因此开发人员可以更新特定设备的业务逻辑，而无需部署整个系统。
* 复原能力并减少停机时间。

IoT 普适性相结合为它带来了多个无服务器产品，重点介绍专门 IoT 问题，如[Azure IoT 中心](https://docs.microsoft.com/azure/iot-hub)。 无服务器自动执行任务，例如设备注册、 策略实施、 跟踪和甚至部署到设备的代码*边缘*。 边缘是指类似于传感器和传动装置连接到，但不是活动部分 Internet 的设备。

>[!div class="step-by-step"]
[上一页](architecture-approaches.md)
[下一页](serverless-architecture-considerations.md)
