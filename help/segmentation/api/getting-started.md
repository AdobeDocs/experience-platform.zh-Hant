---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；api;
solution: Experience Platform
title: 使用分段服務API入門
description: 以下文檔提供了需要瞭解的其他資訊，以便成功使用分段API。
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# 分段服務API入門 {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] 允許您在Adobe Experience Platform構建節目段，並通過 [!DNL Real-Time Customer Profile] 資料。

開發人員指南要求對各種 [!DNL Experience Platform] 使用涉及的服務 [!DNL Segmentation Service]。

- [[!DNL Segmentation]](../home.md):允許您從 [!DNL Real-Time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。 為最好地利用分段，請確保根據 [資料建模的最佳做法](../../xdm/schema/best-practices.md)。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了您需要瞭解的其他資訊，以便成功使用 [!DNL Segmentation] API。

## 讀取示例API調用

的 [!DNL Segmentation Service] API文檔提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

## 必需的標題

API文檔還要求您完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功撥打 [!DNL Platform] 端點。 完成身份驗證教程將提供中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在其中進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關使用沙箱的詳細資訊，請參閱 [!DNL Experience Platform]，請參見 [箱概述文檔](../../sandboxes/home.md)。

## 後續步驟

使用 [!DNL Segmentation Service] API，使用左側導航或在 [開發人員指南](./overview.md)
