---
keywords: Experience Platform; home；熱門主題；分段；分段；分段服務；api;
solution: Experience Platform
title: 分段服務API快速入門
topic-legacy: developer guide
description: 以下檔案提供您需要知道的其他資訊，以便成功使用區段API。
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 分段服務API {#getting-started}快速入門

Adobe Experience Platform[!DNL Segmentation Service]可讓您建立區段，並從[!DNL Real-time Customer Profile]資料產生Adobe Experience Platform的觀眾。

開發人員指南需要對使用[!DNL Segmentation Service]時涉及的各種[!DNL Experience Platform]服務有良好的瞭解。

- [[!DNL Segmentation]](../home.md):可讓您從資料建立受眾 [!DNL Real-time Customer Profile] 細分。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
- [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，才能成功使用[!DNL Segmentation] API。

## 讀取範例API呼叫

[!DNL Segmentation Service] API檔案提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

## 必要的標題

API檔案也要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫[!DNL Platform]端點。 完成驗證教學課程可為[!DNL Experience Platform] API呼叫中的每個必要標題提供值，如下所示：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定執行操作的沙盒的名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需在[!DNL Experience Platform]中使用沙盒的詳細資訊，請參閱[沙盒概觀檔案](../../sandboxes/home.md)。

## 後續步驟

若要使用[!DNL Segmentation Service] API進行呼叫，請使用左側導覽或在[開發人員指南總覽](./overview.md)中選取其中一個可用的端點指南
