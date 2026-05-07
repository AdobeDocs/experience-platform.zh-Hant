---
title: Salesforce Service Cloud Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Salesforce Service Cloud連線至Adobe Experience Platform。
exl-id: 9bebbc00-55b3-4aec-9357-4127c05844e2
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# [!DNL Salesforce Service Cloud]

[!DNL Salesforce Service Cloud]是客戶成功平台，旨在自動化服務工作流程，並簡化公司與其客戶之間的溝通。 它將來自各種管道（例如電子郵件、電話、社群媒體和即時聊天）的請求整合到統一的代理主控台中。 如此一來，支援團隊就能透過360度檢視客戶歷程來管理「案例」，確保無論客戶提出何種要求，回應都能個人化且有效率。

您可以在Adobe Experience Platform來源中使用[!DNL Salesforce Service Cloud]來源聯結器來連線您的[!DNL Salesforce Service Cloud]帳戶，並將您的資料帶到Experience Platform服務中使用。

閱讀本檔案以瞭解如何設定您的[!DNL Salesforce Service Cloud]帳戶並將其連結至Experience Platform。

## 先決條件 {#prerequisites}

請參閱本節，瞭解在成功連線至Experience Platform之前必須完成的先決條件設定。

### IP位址允許清單 {#allowlist}

將來源連線至Experience Platform之前，您必須先將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址以連線至Experience Platform](../../ip-address-allow-list.md)的指南以瞭解詳細資訊。

### 收集必要的認證 {#credentials}

您必須提供下列認證的值，才能使用OAuth2使用者端認證連線您的[!DNL Salesforce Service Cloud]帳戶。

| 認證 | 說明 |
| --- | --- |
| 環境 URL | [!DNL Salesforce Service Cloud]來源執行個體的網址。 |
| 用戶端 ID | 使用者端ID會與使用者端密碼搭配使用，作為OAuth2驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式透過向[!DNL Salesforce Service Cloud]識別您的應用程式，以代表您的帳戶運作。 |
| 用戶端密碼 | 使用者端密碼會與使用者端ID搭配使用，做為OAuth2驗證的一部分。 使用者端ID和使用者端密碼可讓您的應用程式透過向[!DNL Salesforce Service Cloud]識別您的應用程式，以代表您的帳戶運作。 |
| API 版本 | 您正在使用的[!DNL Salesforce Service Cloud]執行個體的REST API版本。 API版本的值必須使用小數點格式化。 例如，如果您使用API版本`52`，則必須以`52.0`的形式輸入值。 如果此欄位留空，Experience Platform會自動使用最新可用版本。 |

如需針對[!DNL Salesforce Service Cloud]使用OAuth的詳細資訊，請參閱OAuth授權流程[&#128279;](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5)的[!DNL Salesforce Service Cloud] 指南。

## 使用API連線[!DNL Salesforce Service Cloud]至Experience Platform

- [使用流量服務API建立Salesforce Service雲端基本連線](../../tutorials/api/create/customer-success/salesforce-service-cloud.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API建立客戶成功來源的資料流](../../tutorials/api/collect/customer-success.md)

## 使用UI連線[!DNL Salesforce Service Cloud]至Experience Platform

- [在UI中建立Salesforce Service雲端來源連線](../../tutorials/ui/create/customer-success/salesforce-service-cloud.md)
- [在UI中建立客戶成功來源連線的資料流](../../tutorials/ui/dataflow/customer-success.md)
