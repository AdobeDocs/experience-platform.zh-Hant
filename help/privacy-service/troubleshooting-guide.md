---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service故障排除指南
topic-legacy: troubleshooting
description: 本檔案提供有關Privacy Service的常見問題解答，以及API中常見錯誤的相關資訊。
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---

# [!DNL Privacy Service] 疑難排解指南

Adobe Experience Platform[!DNL Privacy Service]提供REST風格的API和使用者介面，協助公司管理客戶資料隱私權要求。 有了[!DNL Privacy Service]，您可以提交存取和刪除私人或個人客戶資料的請求，以利自動符合組織和法律的隱私權規範。

本檔案提供有關[!DNL Privacy Service]的常見問題解答，以及API中常見錯誤的相關資訊。

## 在API中提出隱私權要求時，使用者ID和使用者ID之間有何不同？{#user-ids}

為了在API中建立新的隱私權工作，請求的JSON裝載必須包含`users`陣列，列出適用於隱私權要求的每個使用者的特定資訊。 `users`陣列中的每個項目都是代表特定用戶的對象，由其`key`值標識。

反過來，每個用戶對象（或`key`）都包含其自己的`userIDs`陣列。 此陣列列出該特定用戶&#x200B;**的特定ID值**。

請考慮以下示例`users`陣列：

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

陣列包含兩個物件，代表個別使用者以其`key`值（&quot;DavidSmith&quot;和&quot;user12345&quot;）所識別。 「DavidSmith」只有一個列出的ID（其電子郵件地址），而「user12345」有兩個（其電子郵件地址和ECID）。

有關提供用戶身份資訊的詳細資訊，請參閱[隱私請求身份資料指南](identity-data.md)。


## 我可以使用[!DNL Privacy Service]清除意外傳送至[!DNL Platform]的資料嗎？

Adobe不支援使用[!DNL Privacy Service]來清除意外提交到產品的資料。 [!DNL Privacy Service] 旨在協助您履行資料主體（或消費者）存取或刪除要求的義務。這些要求會對時間產生敏感影響，並且會根據適用的隱私權法完成。 提交不屬於資料主體／消費者訪問或刪除請求會影響所有[!DNL Privacy Service]客戶以及[!DNL Privacy Service]支援適當法律時間表的能力。

請連絡您的客戶經理(CDM)，以協調並提供一定程度的努力，以移除任何PII或資料問題。

## 我要如何取得隱私權要求或工作狀態的相關資訊？

您可以使用[!DNL Privacy Service] API或使用者介面來擷取特定工作的詳細資訊。

### 使用API

要使用[!DNL Privacy Service] API檢索特定作業的狀態，請使用請求路徑中作業的ID向根(`GET /`)端點發出請求。 如需詳細資訊，請參閱[!DNL Privacy Service]開發人員指南中檢查工作狀態的[一節。](api/privacy-jobs.md#check-the-status-of-a-job)

### 使用UI

所有作用中的工作請求都列在[!DNL Privacy Service] UI儀表板的&#x200B;**[!UICONTROL Job Requests]**&#x200B;介面工具集中。 每個作業請求的狀態顯示在&#x200B;**[!UICONTROL Status]**&#x200B;列下。 有關在UI中查看作業請求的詳細資訊，請參閱[Privacy Service使用手冊](ui/user-guide.md)。

## 如何下載完成的隱私權工作結果？

[!DNL Privacy Service] API和使用者介面都提供以ZIP格式下載完成工作結果的方法。

### 使用API

使用要在請求路徑中下載其結果的作業的ID，向[!DNL Privacy Service] API中的根(`GET /`)端點發出請求。 如果作業狀態完成，API會在回應主體中包含`downloadURL`屬性。 此屬性包含URL，您可將其貼入瀏覽器的位址列，以下載ZIP檔案。

如需詳細資訊，請參閱[!DNL Privacy Service]開發人員指南中[依其ID](api/privacy-jobs.md#check-the-status-of-a-job)尋找工作的章節。

### 使用UI

在[!DNL Privacy Service] UI儀表板上，從&#x200B;**作業請求**&#x200B;介面工具集中找到要下載的作業。 選擇作業的ID以開啟「作業詳細資訊」頁。 從這裡，選擇右上角的&#x200B;**Download**&#x200B;以下載ZIP檔案。 有關詳細步驟，請參閱[Privacy Service使用手冊](ui/user-guide.md)。

## 常見錯誤訊息

下表概述了[!DNL Privacy Service]中的一些常見錯誤，並提供了有助於解決各自問題的說明。

| 錯誤訊息 | 說明 |
| --- | --- |
| 找不到用戶ID。 | 無法找到請求中提供的某些使用者ID，且已略過。 請確定您在請求裝載中使用正確的命名空間和ID值。 如需更詳細的說明，請參閱[提供身分資料](./identity-data.md)的檔案。 |
| 無效的命名空間 | 提供的使用者ID識別名稱空間無效。 請參閱[!DNL Privacy Service]開發人員指南附錄中[標準身分名稱空間](./api/appendix.md#standard-namespaces)一節，以取得已接受的名稱空間清單。 如果您使用自訂命名空間，請確定您正在將ID的`type`屬性設定為&quot;custom&quot;。 |
| 部分完成 | 工作已成功完成，但有些資料不適用於指定的請求，且已略過。 |
| 資料不是必要格式。 | 指定應用程式的一或多個資料值格式錯誤。 請查看工作詳細資訊以取得詳細資訊。 |
| 尚未布建IMS組織。 | 當您的IMS組織尚未布建[!DNL Privacy Service]時，會出現此訊息。 如需詳細資訊，請洽詢您的管理員。 |
| 存取權和權限是必要的。 | 要使用[!DNL Privacy Service]，需要存取權和權限。 請連絡您的管理員以取得存取權。 |
| 上傳和封存存取資料時發生問題。 | 發生此錯誤時，請重新上傳存取資料並再試一次。 |
| 已超出當前文檔速率限制的工作量。 | 發生此錯誤時，請降低提交率，然後重試。 |
