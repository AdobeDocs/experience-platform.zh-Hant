---
keywords: Experience Platform；首頁；熱門主題；分段；分段服務；api;
solution: Experience Platform
title: 區段服務API快速入門
description: 下列檔案提供您需要了解的其他資訊，以便順利使用分段API。
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# 區段服務API快速入門 {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] 可讓您在Adobe Experience Platform中建立區段，並透過 [!DNL Real-Time Customer Profile] 資料。

開發人員指南需要妥善了解 [!DNL Experience Platform] 與使用 [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md):可讓您從 [!DNL Real-Time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。 為了最能善用區段，請確定您的資料已根據 [資料模型最佳實務](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便成功使用 [!DNL Segmentation] API。

## 讀取範例API呼叫

此 [!DNL Segmentation Service] API檔案提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

## 必要標題

API檔案也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] 端點。 完成驗證教學課程，可提供 [!DNL Experience Platform] API呼叫，如下所示：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要進行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需使用沙箱的詳細資訊，請參閱 [!DNL Experience Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

## 後續步驟

若要使用進行呼叫 [!DNL Segmentation Service] API，請使用左側導覽或在 [開發人員指南概觀](./overview.md)
