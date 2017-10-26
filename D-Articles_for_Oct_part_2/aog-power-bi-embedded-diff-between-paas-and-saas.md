---
title: Power BI PaaS 和 SaaS 的 Embed 服务区别
description: Power BI PaaS 和 SaaS 的 Embed 服务区别
service: ''
resource: Power BI Embedded
author: kustbilla
displayOrder: ''
selfHelpType: ''
supportTopicIds: ''
productPesIds: ''
resourceTags: 'Power BI Embedded, Power BI Desktop'
cloudEnvironments: MoonCake

ms.service: power-bi-embedded
wacn.topic: aog
ms.topic: article
ms.author: weihuan
ms.date: 10/25/2017
wacn.date: 10/25/2017
---

# Power BI PaaS 和 SaaS 的 Embed 服务区别

众所周知，Power BI 有 SaaS 和 PaaS 之分，其中 Power BI PaaS 指的是 Power BI Embedded 服务，而 Power BI SaaS 通常指的是 Power BI 桌面版和网页版等产品。以下是 [Power BI Embedded 官网](https://docs.azure.cn/zh-cn/power-bi-embedded/power-bi-embedded-faq)上对 Power BI Embedded(PaaS) 与 Power BI 服务(SaaS)之间的关系：

> ## Power BI Embedded 与 Power BI 服务有什么关系？
> Power BI Embedded 和 Power BI 服务是单独的产品/服务。 Power BI Embedded 采取基于消费的计费模式，通过 Azure 门户部署并且旨在使 ISV 能够将数据可视化元素嵌入到应用程序中，供其客户使用。 Power BI 服务通过 O365 门户进行计费和部署，是一个独立通用的 BI 产品/服务，主要供企业内部使用。 若要了解 Power BI 服务的详细信息，请参阅 [www.powerbi.com](www.powerbi.com)。
 
然而，许多人不知道的是，和 Power BI PaaS 类似，Power BI SaaS 也存在和嵌入(Embed)相关的服务，二者都是通过 HTTP 调用 REST API，从而实现所需内容的内嵌和展示。以下归纳了一些二者的区别，方便读者参考：

1. **REST API 和官方示例**

    * Power BI PaaS

        REST API: https://msdn.microsoft.com/library/azure/mt711507.aspx<br>
        官方示例: https://github.com/Azure-Samples/power-bi-embedded-integrate-report-into-web-app/

    * Power BI SaaS

        REST API: https://msdn.microsoft.com/en-us/library/mt147898.aspx<br>
        官方示例: https://github.com/Microsoft/PowerBI-developer-samples

2. **常用 URL**

    * Power BI PaaS

        Power BI API URL: https://api.powerbi.cn<br>
        Power BI API Endpoint: https://WABI-MC-BJB-redirect.analysis.chinacloudapi.cn<br>
        Azure Resource Manager API Endpoint: https://management.chinacloudapi.cn<br>
        Azure Resource Manager Resource: https://management.core.chinacloudapi.cn<br>
        Authentication Url: https://login.chinacloudapi.cn<br>
        Tenants Url: https://management.chinacloudapi.cn/tenants?api-version=2016-06-01<br>
        Default Embed URL: https://embedded.powerbi.cn/appTokenReportEmbed

    * Power BI SaaS

        Authority URL: https://login.chinacloudapi.cn/common/oauth2/authorize<br>
        Resource URL: https://analysis.wchinacloudapi.cn/powerbi/api<br>
        API URL: https://api.powerbi.cn<br>
        Embed URL Base: https://app.powerbi.cn<br>

3. 所调用的内容及是否需要什么账号

    * Power BI PaaS

        所调用的是上传至 Azure 账号的 Power BI Embedded 工作区集合的 pbix 文件，因此需要 Azure 账号。而 pbix 文件是在 Power BI 桌面版上制作，因此无需 Power BI 账号。

    * Power BI SaaS

        所调用的是 Power BI 网页版(Power BI Service)上的 Dashboard, Report 或者 Tile 等 内容，因此是需要 Power BI 账号的。