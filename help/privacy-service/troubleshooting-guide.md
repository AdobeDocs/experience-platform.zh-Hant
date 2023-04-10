---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service疑難排解指南
description: 本檔案提供Privacy Service常見問題的解答，以及API中常見錯誤的相關資訊。
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 1%

---

# [!DNL Privacy Service] 疑難排解指南

Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和使用者介面，協助公司管理客戶資料隱私權請求。 使用 [!DNL Privacy Service]，您可以提交存取和刪除私人或個人客戶資料的請求，協助您自動遵守組織和法律隱私權法規。

本檔案提供關於 [!DNL Privacy Service]，以及API中常見錯誤的相關資訊。

## 在API中提出隱私權要求時，使用者與使用者ID有何不同？ {#user-ids}

若要在API中建立新的隱私權工作，要求的JSON裝載必須包含 `users` 陣列，列出隱私權要求所套用之每個使用者的特定資訊。 中的每個項目 `users` 陣列是代表特定使用者的物件，以 `key` 值。

接著，每個使用者物件(或 `key`)包含自己的 `userIDs` 陣列。 此陣列列出特定ID值 **針對某個特定用戶**.

請考量下列範例 `users` 陣列：

```json
"users": [
  {
    "key": "DavidSmith",
    "action": ["access"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "dsmith@acme.com",
        "type": "standard"
      }
    ]
  },
  {
    "key": "user12345",
    "action": ["access", "delete"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "ajones@acme.com",
        "type": "standard"
      },
      {
        "namespace": "ECID",
        "type": "standard",
        "value":  "443636576799758681021090721276",
        "isDeletedClientSide": false
      }
    ]
  }
]
```

陣列包含兩個物件，分別代表個別使用者所識別的使用者 `key` 值(「DavidSmith」和「user12345」)。 「DavidSmith」只有一個列出的ID（其電子郵件地址），而「user12345」有兩個（其電子郵件地址和ECID）。

有關提供用戶身份資訊的詳細資訊，請參閱 [隱私權要求的身分資料](identity-data.md).


## 我可以使用 [!DNL Privacy Service] 清除意外傳送至的資料 [!DNL Platform]?

Adobe不支援使用 [!DNL Privacy Service] 用於清除意外提交至產品的資料。 [!DNL Privacy Service] 旨在協助您履行資料主體（或消費者）存取或刪除請求的義務。 不支援或不允許使用Privacy Service進行資料清理或維護。

隱私權要求會區分大小寫，且會根據適用的隱私權法完成。 提交非資料主體/消費者存取或刪除請求會影響所有 [!DNL Privacy Service] 客戶和 [!DNL Privacy Service] 支援適當的法律時間表。 現已設定硬式每日上傳限制，以協助防止濫用服務。

請連絡您的Adobe客戶團隊，協調並著手移除任何PII或資料問題。

## 如何取得隱私權要求或工作狀態的相關資訊？

您可以使用 [!DNL Privacy Service] API或使用者介面。

### 使用 API

使用 [!DNL Privacy Service] API，向根(`GET /`)端點，在請求路徑中使用工作的ID。 如需詳細資訊，請參閱 [檢查作業的狀態](api/privacy-jobs.md#check-the-status-of-a-job) 在 [!DNL Privacy Service] API指南。

### 使用UI

所有作用中的作業請求都列在 **[!UICONTROL 工作請求]** 介面工具集 [!DNL Privacy Service] UI控制面板。 每個作業請求的狀態會顯示在 **[!UICONTROL 狀態]** 欄。 如需在UI中檢視工作請求的詳細資訊，請參閱 [Privacy Service使用手冊](ui/user-guide.md).

## 如何下載已完成的隱私權工作結果？

此 [!DNL Privacy Service] API和使用者介面都提供以ZIP格式下載已完成作業結果的方法。

### 使用 API

向根(`GET /`)端點 [!DNL Privacy Service] API，使用您要在請求路徑中下載結果之作業的ID。 如果工作狀態完成，API將包含 `downloadURL` 屬性。 此屬性包含URL，您可將其貼入瀏覽器的位址列以下載ZIP檔案。

如需詳細資訊，請參閱 [用身份證查找工作](api/privacy-jobs.md#check-the-status-of-a-job) 在 [!DNL Privacy Service] API指南。

### 使用UI

在 [!DNL Privacy Service] UI控制面板，從 **工作請求** 介面工具集。 選擇作業的ID以開啟「作業詳細資訊」頁。 從此處，選擇 **下載** 下載ZIP檔案。 請參閱 [Privacy Service使用手冊](ui/user-guide.md) 以取得更詳細的步驟。

## 常見錯誤訊息

下表概述 [!DNL Privacy Service]，並附上說明以協助解決其各自的問題。

| 錯誤訊息 | 說明 |
| --- | --- |
| 找不到用戶ID。 | 找不到請求中提供的某些使用者ID，且已略過。 請確定您在要求裝載中使用正確的命名空間和ID值。 請參閱 [提供身分資料](./identity-data.md) 以取得更詳細的說明。 |
| 命名空間無效 | 提供的用戶ID標識命名空間無效。 請參閱 [標準身分命名空間](./api/appendix.md#standard-namespaces) 在 [!DNL Privacy Service] API指南附錄，以取得接受的命名空間清單。 如果您使用自訂命名空間，請確定您正在設定ID的 `type` 屬性轉換為「自訂」。 |
| 部分完成 | 作業已成功完成，但某些資料不適用於給定請求，已跳過。 |
| 資料不是必要格式。 | 指定應用程式的一個或多個資料值的格式不正確。 如需詳細資訊，請查看作業詳細資訊。 |
| 尚未布建IMS組織。 | 未針對布建您的IMS組織時，就會出現此訊息 [!DNL Privacy Service]. 如需詳細資訊，請聯絡您的管理員。 |
| 需要存取和權限。 | 必須有存取權和權限才能使用 [!DNL Privacy Service]. 請連絡您的管理員以取得存取權。 |
| 上載和歸檔訪問資料時出現問題。 | 發生此錯誤時，請重新上傳存取資料，然後重試。 |
| 已超出當前文檔速率限制的工作量。 | 發生此錯誤時，請降低提交率，然後重試。 |
