---
keywords: Experience Platform；首頁；熱門主題；DULE;dule
solution: Experience Platform
title: 策略服務API入門
description: 策略服務API允許您建立和管理與Adobe Experience Platform資料治理相關的各種資源。 本文檔介紹了在嘗試調用策略服務API之前需要瞭解的核心概念。
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 入門 [!DNL Policy Service] API

的 [!DNL Policy Service] API允許您建立和管理與Adobe Experience Platform資料治理相關的各種資源。 本文檔介紹了在嘗試呼叫至 [!DNL Policy Service] API。

## 先決條件

使用開發人員指南需要瞭解各種 [!DNL Experience Platform] 與Data Governance功能協作的服務。 開始使用 [!DNL Policy Service API]，請查看以下服務的文檔：

* [資料治理](../home.md):框架 [!DNL Experience Platform] 強制實施資料使用合規性。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 讀取示例API調用

的 [!DNL Policy Service] API文檔提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

## 必需的標題

API文檔還要求您完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功撥打 [!DNL Platform] 端點。 完成身份驗證教程將提供中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]包括屬於「資料管理」的「資料管理」，將與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

* `Content-Type: application/json`

## 核心資源與定製資源

在 [!DNL Policy Service] API，所有策略和營銷操作都稱為 `core` 或 `custom` 資源。

`core` 資源是由Adobe定義和維護的， `custom` 資源是由您的組織建立和維護的資源，因此對您的組織來說是唯一和可見的。 因此，列出和查找操作(`GET`)是唯一允許的操作 `core` 資源，而列出、查找和更新操作(`POST`。 `PUT`。 `PATCH`, `DELETE`)可用 `custom` 資源。

## 後續步驟

要開始使用策略服務API進行調用，請選擇可用終結點指南之一。
