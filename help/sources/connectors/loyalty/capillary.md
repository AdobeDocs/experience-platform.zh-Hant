---
title: Capillary Streaming Events概述
description: 瞭解如何將資料從Capillary串流至Experience Platform。
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: bd5611b23740f16e41048f3bc65f62312593a075
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 4%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>[!DNL Capillary Streaming Events]來源是測試版。 閱讀來源概觀中的[條款與條件](../../home.md#terms-and-conditions)，以取得有關使用測試版標籤之來源的詳細資訊。

[!DNL Capillary Technologies]是領先的忠誠度和參與平台，受到全球300多個品牌的信任。 使用[!DNL Capillary Streaming Events]來源讓您的企業可以順暢地從[!DNL Capillary]將客戶設定檔、忠誠度資料和交易事件串流到Adobe Experience Platform。 連線您的[!DNL Capillary]來源以啟用即時個人化、進階對象細分和全通路行銷活動策劃。

將[!DNL Capillary]與Experience Platform整合後，您可以：

* 即時同步&#x200B;**忠誠度點數、層級和獎勵**。
* 將&#x200B;**異動資料**&#x200B;傳送到Experience Platform以進行分析和啟用。
* 運用Real-Time CDP、Experience Platform和Adobe Journey Optimizer進行細分、歷程協調和個人化。

## 先決條件

在將[!DNL Capillary]連線至Adobe Experience Platform之前，請確定您擁有：

* 有效的&#x200B;**Adobe組織ID**&#x200B;和啟用Experience Platform沙箱的存取權。
* **[!DNL Capillary]來源認證** （使用者端識別碼與使用者端密碼）。
* 在Adobe Admin Console中建立來源和資料流的必要許可權。

### 收集必要的認證

您必須提供下列認證的值，才能將您的[!DNL Capillary]帳戶連線至Experience Platform：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| 用戶端 ID | [!DNL Capillary]來源的使用者端識別碼。 | `321c8a8fee0d4a06838d46f9d3109e8a` |
| 使用者端密碼 | 以使用者端ID發行的使用者端密碼 | `xxxxxxxxxxxxxxxxxx` |
| 組織 ID | 您的Adobe組織ID | `0A7D42FC5DB9D3360A495FD3@AdobeOrg` |

如需有關產生存取權杖的詳細資訊，請參閱[Adobe驗證指南](https://developer.adobe.com/developer-console/docs/guides/authentication/)。

### 產生存取權杖

接下來，使用您的使用者端ID和使用者端密碼，從Adobe產生存取權杖。

**要求**

```shell
curl -X POST 'https://ims-na1.adobelogin.com/ims/token' \
  -d 'client_id={CLIENT_ID}' \
  -d 'client_secret={CLIENT_SECRET}' \
  -d 'grant_type=client_credentials' \
  -d 'scope=openid AdobeID read_organizations additional_info.projectedProductContext session'
```

**回應**

```json
{
  "access_token": "eyJhbGciOi...",
  "token_type": "bearer",
  "expires_in": 86399994
}
```

## 後續步驟

完成[!DNL Capillary]的先決條件設定後，請閱讀以下檔案以瞭解如何連線帳戶並開始將資料從[!DNL Capillary]串流至Experience Platform。

* [使用API連線 [!DNL Capillary Streaming Events] 至Experience Platform](../../tutorials/api/create/loyalty/capillary.md)
* [使用UI連線 [!DNL Capillary Streaming Events] 至Experience Platform](../../tutorials/ui/create/loyalty/capillary.md)
