---
title: 疑難排解
description: 瞭解如何在使用Adobe Experience Platform邊緣網路伺服器API時排除錯誤
seo-description: Learn how to troubleshoot errors when using the Adobe Experience Platform Edge Network Server API
keywords: 邊緣網路；網關；api;troubleshoot;errors;griffon;
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 1%

---


# 疑難排解

Adobe Experience Platform邊緣網路伺服器API允許您從服務中捕獲調試資訊，因為您的事件是通過邊緣網路資料收集管道處理的。

同一機構 [Experience Platform調試器](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) 使您能夠調試基於API的實現。

使用 [格里芬項目](https://aep-sdks.gitbook.io/docs/beta/project-griffon)，您可以建立調試會話ID，在邊緣網路請求中可以進一步使用該ID來跟蹤事件。

