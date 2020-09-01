---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;api;
solution: Experience Platform
title: 區段服務開發人員指南
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Adobe Experience Platform可 [!DNL Segmentation Service] 讓您在Adobe Experience Platform中從資料建立細分並產生受 [!DNL Real-time Customer Profile] 眾。

開發人員指南需要對使用中涉及的各 [!DNL Experience Platform] 種服務有良好的認識 [!DNL Segmentation Service]。

- [[!DNL分段]](../home.md):可讓您從資料建立受眾 [!DNL Real-time Customer Profile] 區段。
- [[!DNL體驗資料模型(XDM)系統]](../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
- [[!DNL即時客戶基本資料]](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
- [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您成功使用 [!DNL Segmentation] API時需要知道的其他資訊。

## 讀取範例API呼叫

API文 [!DNL Segmentation Service] 件提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

## 必要的標題

API檔案也要求您完成驗證教學 [課程](../../tutorials/authentication.md) ，才能成功呼叫端點 [!DNL Platform] 。 完成驗證教學課程可提供 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權： `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題指定執行操作的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需有關在中使用沙盒的詳細資訊，請 [!DNL Experience Platform]參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

## 後續步驟

若要使用 [!DNL Segmentation Service] API進行呼叫，請使用左側導覽或開發人員指南總覽，選取其中一個可用 [的端點指南](./overview.md)