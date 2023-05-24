---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service故障排除指南
description: 本文檔提供有關Privacy Service的常見問題解答以及有關API中常見錯誤的資訊。
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 1%

---

# [!DNL Privacy Service] 故障排除指南

Adobe Experience Platform [!DNL Privacy Service] 提供REST風格的API和用戶介面，幫助公司管理客戶資料隱私請求。 與 [!DNL Privacy Service]，您可以提交訪問和刪除私人或個人客戶資料的請求，以便自動遵守組織和法律隱私法規。

本文檔提供有關 [!DNL Privacy Service]，以及有關API中常見錯誤的資訊。

## 在API中發出隱私請求時，用戶和用戶ID之間有何區別？ {#user-ids}

要在API中建立新的隱私作業，請求的JSON負載必須包含 `users` 陣列，該陣列列出隱私請求所應用的每個用戶的特定資訊。 中的每個項 `users` 陣列是表示特定用戶的對象，由其標識 `key` 值。

反過來，每個用戶對象(或 `key`)包含 `userIDs` 陣列。 此陣列列出特定ID值 **那個特定用戶**。

請考慮以下示例 `users` 陣列：

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

該陣列包含兩個對象，表示由其標識的單個用戶 `key` 值（「DavidSmith」和「user12345」）。 「DavidSmith」只有一個列出的ID（其電子郵件地址），而「user12345」有兩個（其電子郵件地址和ECID）。

有關提供用戶身份資訊的詳細資訊，請參閱上的指南 [隱私請求的標識資料](identity-data.md)。


## 我能用 [!DNL Privacy Service] 清除意外發送到 [!DNL Platform]?

Adobe不支援使用 [!DNL Privacy Service] 清除意外提交到產品的資料。 [!DNL Privacy Service] 旨在幫助您履行對資料主題（或消費者）訪問或刪除請求的義務。 不支援或不允許使用Privacy Service進行資料清理或維護。

隱私請求是時間敏感的，並且完成與適用隱私法相關。 提交不屬於資料主題/用戶訪問或刪除請求會影響所有 [!DNL Privacy Service] 客戶和 [!DNL Privacy Service] 以支援適當的法律時限。 現在已設定硬性每日上載限制，以幫助防止濫用服務。

請與您的Adobe客戶團隊聯繫，以協調並提供刪除任何PII或資料問題的工作級別。

## 如何獲取有關我的隱私請求或工作狀態的資訊？

您可以使用 [!DNL Privacy Service] API或用戶介面。

### 使用 API

使用 [!DNL Privacy Service] API，向根請求(`GET /`)終結點，使用請求路徑中作業的ID。 有關詳細資訊，請參閱 [檢查作業的狀態](api/privacy-jobs.md#check-the-status-of-a-job) 的 [!DNL Privacy Service] API指南。

### 使用UI

所有活動作業請求都列在 **[!UICONTROL 作業請求]** 小部件 [!DNL Privacy Service] UI儀表板。 每個作業請求的狀態顯示在 **[!UICONTROL 狀態]** 的雙曲餘切值。 有關在UI中查看作業請求的詳細資訊，請參閱 [Privacy Service使用手冊](ui/user-guide.md)。

## 如何下載已完成隱私作業的結果？

的 [!DNL Privacy Service] API和用戶介面都提供了以ZIP格式下載已完成作業結果的方法。

### 使用 API

向根請求(`GET /`)端點 [!DNL Privacy Service] API，使用要在請求路徑中下載其結果的作業的ID。 如果作業狀態已完成，則API將包括 `downloadURL` 屬性。 此屬性包含一個URL，您可以將其貼上到瀏覽器的地址欄中以下載ZIP檔案。

有關詳細資訊，請參閱 [用身份證找工作](api/privacy-jobs.md#check-the-status-of-a-job) 的 [!DNL Privacy Service] API指南。

### 使用UI

在 [!DNL Privacy Service] UI儀表板，從 **作業請求** 小部件。 選擇作業的ID以開啟「作業詳細資料」頁。 從此處，選擇 **下載** 下載ZIP檔案。 查看 [Privacy Service使用手冊](ui/user-guide.md) 的子菜單。

## 常見錯誤訊息

下表概述了中的一些常見錯誤 [!DNL Privacy Service]，並提供說明以幫助解決各自的問題。

| 錯誤訊息 | 說明 |
| --- | --- |
| 找不到用戶ID。 | 找不到請求中提供的某些用戶ID，已跳過。 確保在請求負載中使用了正確的命名空間和ID值。 查看上的文檔 [提供身份資料](./identity-data.md) 來解釋。 |
| 命名空間無效 | 為用戶ID提供的標識命名空間無效。 請參閱 [標準標識命名空間](./api/appendix.md#standard-namespaces) 的 [!DNL Privacy Service] API指南附錄，用於獲取接受的命名空間清單。 如果使用的是自定義命名空間，請確保正在設定 `type` 屬性到「自定義」。 |
| 部分完成 | 作業已成功完成，但某些資料不適用於給定請求並已跳過。 |
| 資料不是必需的格式。 | 指定應用程式的一個或多個資料值格式不正確。 有關詳細資訊，請檢查作業詳細資訊。 |
| 尚未設定IMS組織。 | 未為您的組織設定此消息時 [!DNL Privacy Service]。 有關詳細資訊，請與管理員聯繫。 |
| 需要訪問權限。 | 需要訪問權限才能使用 [!DNL Privacy Service]。 請與管理員聯繫以獲取訪問權限。 |
| 上載和存檔訪問資料時出現問題。 | 發生此錯誤時，請重新上載訪問資料並重試。 |
| 已超出當前文檔速率限制的工作量。 | 發生此錯誤時，請降低提交率，然後重試。 |
