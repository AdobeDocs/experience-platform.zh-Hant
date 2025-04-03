---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；API；
solution: Experience Platform
title: Segmentation Service API快速入門
description: 下列檔案提供成功使用分段API所需瞭解的其他資訊。
role: Developer
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 7%

---

# Segmentation Service API快速入門 {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service]可讓您從[!DNL Real-Time Customer Profile]資料，透過Adobe Experience Platform中的區段定義或其他來源建立對象。

開發人員指南需要您實際瞭解使用[!DNL Segmentation Service]時涉及的各種[!DNL Experience Platform]服務。

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：可讓您從[!DNL Real-Time Customer Profile]資料建立對象。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。 若要充分利用「細分」，請確定您的資料已根據[資料模型最佳實務](../../xdm/schema/best-practices.md)被擷取為設定檔和事件。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能成功使用[!DNL Segmentation] API。

## 讀取範例 API 呼叫

[!DNL Segmentation Service] API檔案提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

## 必要的標頭

API檔案也要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫[!DNL Experience Platform]端點。 完成驗證教學課程會提供[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的所有請求都需要一個標頭，以指定將執行操作的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需在[!DNL Experience Platform]中使用沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

## 後續步驟

若要使用[!DNL Segmentation Service] API進行呼叫，請使用左側導覽或在[開發人員指南概觀](./overview.md)中，選取其中一個可用的端點指南
