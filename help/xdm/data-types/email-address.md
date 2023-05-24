---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；欄位；模式；模式；電子郵件地址；xdm:emailAddress;e-mail address;e-mail address;datatype；資料類型；
solution: Experience Platform
title: 電子郵件地址資料類型
description: 本文檔概述了電子郵件地址XDM資料類型。
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# [!UICONTROL 電子郵件地址] 資料類型

[!UICONTROL 電子郵件地址] 是一個標準的體驗資料模型(XDM)資料類型，它描述了電子郵件地址的詳細資訊。

<img src="../images/data-types/email-address.png" width="450" /><br />

| 屬性 | 說明 |
| --- | --- |
| `address` | RFC2822和後續標準中通常定義的電子郵件技術地址(例如， `name@domain.com`)。<br><br>在XDM中，電子郵件地址必須包含有效的頂級域才能通過驗證。 請參閱以下內容 [文檔](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) 的子目錄。 |
| `label` | 可能可用的其他顯示資訊。 例如，如果電子郵件的Outlook地址顯示為Microsoft `John Smith smithjr@company.uk`。 `John Smith` 將被放在此欄位中。 |
| `primary` | 指示這是否是個人的主要電子郵件地址。 配置檔案只能有一個 `primary` 指定時間點的電子郵件地址。 |
| `status` | 指示當前是否可以使用電子郵件地址 |
| `statusReason` | 當前的說明 `status`。 |
| `type` | 帳戶與人員(如 `work` 或 `personal`)。 |

{style="table-layout:auto"}


有關電子郵件地址資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
