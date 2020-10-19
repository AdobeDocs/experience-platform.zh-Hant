---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;emailAddress;xdm:emailAddress;email;email address;datatype;data-type;data type;
solution: Experience Platform
title: 電子郵件地址資料類型
topic: overview
description: 本文檔概述「電子郵件地址XDM」資料類型。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---


# [!UICONTROL 電子郵件地址] ，資料類型

[!UICONTROL 電子郵件地址] (Email address)是一種標準的XDM資料類型，用於說明電子郵件地址的詳細資訊。

<img src="../images/data-types/email-address.png" width="450" /><br />

| 屬性 | 說明 |
| --- | --- |
| `address` | RFC2822和後續標準(例如 `name@domain.com`)中通常定義的電子郵件技術地址。 |
| `label` | 其他可用的顯示資訊。 例如，如果電子郵件顯示Microsoft Outlook豐富地址， `John Smith smithjr@company.uk`則 `John Smith` 會放在此欄位中。 |
| `primary` | 指出這是否為個人的主要電子郵件地址。 描述檔在指定時 `primary` 間點只能有一個電子郵件地址。 |
| `status` | 指出目前是否可使用電子郵件地址 |
| `statusReason` | 當前的說明 `status`。 |
| `type` | 帳戶與人員(例如 `work` 或 `personal`)的關聯。 |


有關電子郵件地址資料類型的詳細資訊，請參閱公用XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)