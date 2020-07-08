---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 即時客戶個人檔案API快速入門
topic: guide
translation-type: tm+mt
source-git-commit: d1656635b6d082ce99f1df4e175d8dd69a63a43a
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# 即時客戶個人檔案API快速入門 {#getting-started}

使用Real-time Customer Profile API，您可以對Profile資源執行基本的CRUD操作，如配置計算屬性、訪問實體、導出Profile資料以及刪除不需要的資料集或批。

使用開發人員指南時，需要對使用描述檔資料時涉及的各種Adobe Experience Platform服務有正確的瞭解。 在開始使用即時客戶設定檔API之前，請先檢閱下列服務的檔案：

* [即時客戶個人檔案](../home.md): 根據來自多個來源的匯整資料，即時提供統一的客戶個人檔案。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): 跨裝置和系統橋接身分，以更全面地瞭解客戶及其行為。
* [Adobe Experience Platform細分服務](../../segmentation/home.md): 可讓您從即時客戶個人檔案資料建立受眾細分。
* [體驗資料模型(XDM)](../../xdm/home.md): 平台組織客戶體驗資料的標準化架構。
* [沙盒](../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便成功呼叫描述檔API端點。

## 讀取範例API呼叫

即時客戶設定檔API檔案提供範例API呼叫，以示範如何正確格式化請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

## 必要的標題

API檔案也要求您完成驗證教學課 [程](../../tutorials/authentication.md) ，才能成功呼叫平台端點。 完成驗證教學課程時，會針對Experience Platform API呼叫中的每個必要標題提供值，如下所示：

* 授權： 生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 對平台API的請求需要一個標題，該標題指定要在中執行操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

請求正文中包含裝載的所有請求（例如POST、PUT和PATCH呼叫）都必須包含標 `Content-Type` 題。 在呼叫參數中提供每個呼叫的接受值。

## 後續步驟

若要開始使用即時客戶設定檔API進行呼叫，請選取其中一個可用的端點指南。