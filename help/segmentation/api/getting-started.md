---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；API；
solution: Experience Platform
title: Segmentation Service API快速入門
description: 下列檔案提供成功使用分段API所需瞭解的其他資訊。
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 18%

---

# Segmentation Service API快速入門 {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] 可讓您透過Adobe Experience Platform中的區段定義或其他來源，從您的 [!DNL Real-Time Customer Profile] 資料。

開發人員指南需要您實際瞭解各種 [!DNL Experience Platform] 與使用有關的服務 [!DNL Segmentation Service].

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：可讓您從建立對象 [!DNL Real-Time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：[!DNL Experience Platform] 據以組織客戶體驗資料的標準化框架。為善用分段，請確保您的資料已根據 [資料模型化的最佳實務](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，協助開發及改進數位體驗應用程式。

以下小節提供您需瞭解的其他資訊，才能成功使用 [!DNL Segmentation] API。

## 讀取範例 API 呼叫

此 [!DNL Segmentation Service] API檔案提供API呼叫範例，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需文件中用於範例 API 呼叫的慣例相關資訊，請參閱 [ 疑難排解指南中的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)如何讀取範例 API 呼叫[!DNL Experience Platform]一節。

## 必要的標頭

此API檔案也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] 端點。 完成驗證教學課程，在中提供每個所需標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 會隔離至特定的虛擬沙箱。 所有要求至 [!DNL Platform] API需要標頭，用以指定將執行作業的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需在中使用沙箱的詳細資訊 [!DNL Experience Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

## 後續步驟

使用進行呼叫 [!DNL Segmentation Service] API，使用左側導覽或在 [開發人員指南概觀](./overview.md)
