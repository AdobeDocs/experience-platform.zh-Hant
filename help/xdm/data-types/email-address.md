---
keywords: Experience Platform;home；熱門主題；架構；Schema;XDM;fields;schemas;emailAddress;xdm:emailAddress;email;email address;datatype;datatype；資料類型；
solution: Experience Platform
title: 電子郵件地址資料類型
topic: overview
description: 本文檔概述「電子郵件地址XDM」資料類型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---


# [!UICONTROL 電子郵件] 地址資料類型

[!UICONTROL 電子] 郵件地址是一種標準的XDM資料類型，它描述了電子郵件地址的詳細資訊。

<img src="../images/data-types/email-address.png" width="450" /><br />

| 屬性 | 說明 |
| --- | --- |
| `address` | RFC2822和後續標準中通常定義的電子郵件技術地址（例如`name@domain.com`）。 |
| `label` | 其他可用的顯示資訊。 例如，如果電子郵件的Microsoft Outlook富地址顯示為`John Smith smithjr@company.uk`，則`John Smith`將放在此欄位中。 |
| `primary` | 指出這是否為個人的主要電子郵件地址。 一個配置檔案在給定時間點只能有一個`primary`電子郵件地址。 |
| `status` | 指出目前是否可使用電子郵件地址 |
| `statusReason` | 當前`status`的說明。 |
| `type` | 帳戶與人員的關聯方式（例如`work`或`personal`）。 |


有關電子郵件地址資料類型的詳細資訊，請參閱公用XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)