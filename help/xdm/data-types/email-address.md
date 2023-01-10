---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；電子郵件地址；xdm:emailAddress；電子郵件；電子郵件地址；資料類型；資料類型；
solution: Experience Platform
title: 電子郵件地址資料類型
description: 本檔案概述「電子郵件地址XDM」資料類型。
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---

# [!UICONTROL 電子郵件地址] 資料類型

[!UICONTROL 電子郵件地址] 是標準的Experience Data Model(XDM)資料類型，可說明電子郵件地址的詳細資訊。

<img src="../images/data-types/email-address.png" width="450" /><br />

| 屬性 | 說明 |
| --- | --- |
| `address` | RFC2822及後續標準中通常定義的電子郵件技術地址(例如 `name@domain.com`)。<br><br>在XDM中，電子郵件地址必須包含有效的頂層網域，才能通過驗證。 請參閱下列內容 [檔案](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) ，以獲取由Internet Assigned Numbers Authority(IANA)定義的有效頂級域的完整清單。 |
| `label` | 可用的其他顯示資訊。 例如，如果電子郵件的Microsoft Outlook豐富地址顯示為 `John Smith smithjr@company.uk`, `John Smith` 會放在此欄位中。 |
| `primary` | 指出這是否為個人的主要電子郵件地址。 設定檔只能有一個 `primary` 指定時間點的電子郵件地址。 |
| `status` | 指出目前是否可使用電子郵件地址 |
| `statusReason` | 目前的說明 `status`. |
| `type` | 帳戶與人員的關聯方式(例如 `work` 或 `personal`)。 |

{style=&quot;table-layout:auto&quot;}


如需電子郵件地址資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
