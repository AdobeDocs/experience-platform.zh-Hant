---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；電子郵件地址；xdm:emailAddress；電子郵件；電子郵件地址；資料類型；資料類型；
solution: Experience Platform
title: 電子郵件地址資料類型
topic-legacy: overview
description: 本檔案概述「電子郵件地址XDM」資料類型。
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 2%

---

# [!UICONTROL 電子郵件] 地址資料類型

[!UICONTROL 電子] 郵件地址是一種標準XDM資料類型，可說明電子郵件地址的詳細資訊。

<img src="../images/data-types/email-address.png" width="450" /><br />

| 屬性 | 說明 |
| --- | --- |
| `address` | RFC2822及後續標準中通常定義的電子郵件技術地址（例如`name@domain.com`）。 |
| `label` | 可用的其他顯示資訊。 例如，如果電子郵件的Microsoft Outlook富地址顯示為`John Smith smithjr@company.uk`，則`John Smith`將放在此欄位中。 |
| `primary` | 指出這是否為個人的主要電子郵件地址。 設定檔在指定時間點只能有一個`primary`電子郵件地址。 |
| `status` | 指出目前是否可使用電子郵件地址 |
| `statusReason` | 當前`status`的說明。 |
| `type` | 帳戶與人員的相關方式（例如`work`或`personal`）。 |

{style=&quot;table-layout:auto&quot;}


如需電子郵件地址資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
