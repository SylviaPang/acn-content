---
title: "Web APP 如何实现反向代理转发功能"
description: "本文介绍了 Azure App Service 如何实现对指定的 URL 进行反向代理转发"
author: zhangyannan-yuki
resourceTags: 'App Service Web, Nginx Reverse Proxy'
ms.service: app-service-web
wacn.topic: aog
ms.topic: article
ms.author: v-tawe
ms.date: 10/31/2017
wacn.date: 10/31/2017
---

# Web APP 如何实现反向代理转发功能

本文介绍了 Azure App Service 如何实现对指定的 URL 进行反向代理转发的功能。

## 操作步骤

1. 创建了 2 个 Web 应用以 PHP 和 Java 语言为例，此处 URL 分别为：`http://testreverseproxyphp.chinacloudsites.cn/` 和`http://testreverseproxyjava.chinacloudsites.cn/`。

    2 个 URL 的返回结果如下：

    ![01](media/aog-app-service-web-howto-realize-reverse-proxy-and-forward-function/01.jpg)

    ![02](media/aog-app-service-web-howto-realize-reverse-proxy-and-forward-function/02.jpg)

2.	在 `http://testreverseproxyphp.chinacloudsites.cn/` 这个网站 `site` 目录下加上 `applicationHost.xdt`。

    ![03](media/aog-app-service-web-howto-realize-reverse-proxy-and-forward-function/03.jpg)

    内容如下：

    ```XML
    <?xml version="1.0"?>
    <configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
        <system.webServer>
            <proxy xdt:Transform="InsertIfMissing" enabled="true" preserveHostHeader="false" reverseRewriteHostInResponseHeaders="false" />
        </system.webServer>
    </configuration>
    ```

3. 在管理门户重启网站。

4. 同时也在 `http://testreverseproxyphp.chinacloudsites.cn/` 网站的 **site** -> **wwwroot** 目录下，加上 web.config 文件。

    ![04](media/aog-app-service-web-howto-realize-reverse-proxy-and-forward-function/04.jpg)

    内容如下：

    ```XML
    <configuration>  
    <system.webServer>  
    <rewrite>  
    <rules>  
    <rule name="Proxy" stopProcessing="true">  
    <match url="^proxy/?(.*)" />  
    <action type="Rewrite" url="http://testreverseproxyjava.chinacloudsites.cn/{R:1}" />  
    </rule>  
    </rules>  
    </rewrite>  
    </system.webServer>  
    </configuration>
    ```
    其中的 `rule name="Proxy"`，这个 Proxy 可以自定义。

    配置好之后，回到管理门户重启网站。

5. 测试结果，当访问 `http://testreverseproxyphp.chinacloudsites.cn/` 这个网站时，返回的是 PHP 页面，访问 `http://testreverseproxyphp.chinacloudsites.cn/proxy` 时返回的是 Java 页面，实现转发功能。

    ![05](media/aog-app-service-web-howto-realize-reverse-proxy-and-forward-function/05.jpg)