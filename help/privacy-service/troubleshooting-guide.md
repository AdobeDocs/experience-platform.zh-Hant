---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 隱私權服務常見問答集
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 64cb2de507921fcb4aaade67132024a3fc0d3dee

---


# 隱私權服務常見問答集

本檔案提供有關Adobe Experience Platform Privacy Service常見問題的解答。

隱私權服務提供REST風格的API和使用者介面，可協助公司管理客戶資料隱私權要求。 透過隱私權服務，您可以提交存取和刪除私人或個人客戶資料的要求，以利自動符合組織和法律的隱私權規定。

## 在API中提出隱私權要求時，使用者ID和使用者ID之間有何不同？ {#user-ids}

為了在API中建立新的隱私權工作，請求的JSON裝載必須包含一個陣列，列出隱私權要求所套用之每位使用者的特定資訊。 `users` 陣列中的每個項 `users` 目都是一個對象，它表示由其值標識的特定用 `key` 戶。

反過來，每個用戶對象(或 `key`)都包含其自己的 `userIDs` 陣列。 此陣列會列出該特定 **使用者的特定ID值**。

Consider the following example `users` array:

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

陣列包含兩個物件，代表個別使用者 `key` 的值（&quot;DavidSmith&quot;和&quot;user12345&quot;）。 「DavidSmith」只有一個列出的ID（其電子郵件地址），而「user12345」有兩個（其電子郵件地址和ECID）。

如需提供使用者身分資訊的詳細資訊，請參閱隱私權要求 [身分資料指南](identity-data.md)。


## 我是否可以使用隱私權服務來清除意外傳送至平台的資料？

Adobe不支援使用隱私權服務來清除意外提交至產品的資料。 隱私權服務旨在協助您履行資料主體（或消費者）存取或刪除要求的義務。 這些要求會對時間產生敏感影響，並且會根據適用的隱私權法完成。 提交非資料主體／消費者存取或刪除請求會影響所有隱私權服務客戶以及隱私權服務支援適當法律時間表的能力。

請連絡您的客戶經理(CDM)，以協調並提供一定程度的努力，以移除任何PII或資料問題。

## 我要如何取得隱私權要求或工作狀態的相關資訊？

您可以使用隱私權服務API或使用者介面來擷取特定工作的詳細資訊。

### 使用API

若要使用隱私服務API擷取特定工作的狀態，請使用請求路徑中的工作ID，向根(`GET /`)端點提出請求。 如需詳細資訊，請參閱「隱私 [服務開發人員指南」中](api/privacy-jobs.md#check-the-status-of-a-job) ，有關檢查工作狀態的章節。

### 使用UI

所有作用中的工作請求都會列在「隱私 **服務** 」UI控制面板的「工作請求」介面工具集中。 每個作業請求的狀態會顯示在「狀 **態** 」欄下。 如需在UI中檢視工作要求的詳細資訊，請參閱隱私 [服務使用指南](ui/user-guide.md)。

## 如何下載完成的隱私權工作結果？

隱私權服務API和使用者介面都提供以ZIP格式下載完成工作結果的方法。

### 使用API

使用您要在請求路徑中下載其結果之工作的ID，向隱私權服務API中的根(`GET /`)端點提出請求。 如果作業狀態完成，API會在回應內文 `downloadURL` 中包含屬性。 此屬性包含URL，您可將其貼入瀏覽器的位址列，以下載ZIP檔案。

如需詳細資訊，請參閱「隱私 [服務開發人員指南」中](api/privacy-jobs.md#check-the-status-of-a-job) ,「依照工作ID尋找工作」一節。

### 使用UI

在「隱私權服務UI」控制面板上，從「工作請求」介面工具集中尋找您要下 **載的工作** 。 按一下作業的ID以開啟「作業詳細 _資訊_ 」頁。 在這裡，按 **一下右上角** 「下載」，下載ZIP檔案。 如需詳細 [步驟，請參閱隱私服務](ui/user-guide.md) 使用指南。