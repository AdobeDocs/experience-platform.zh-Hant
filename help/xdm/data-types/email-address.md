---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；電子郵件地址；xdm：emailAddress；電子郵件；電子郵件地址；資料型別；資料型別；
solution: Experience Platform
title: 電子郵件地址資料型別
description: 瞭解電子郵件地址XDM資料型別。
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# [!UICONTROL 電子郵件地址]資料型別

[!UICONTROL 電子郵件地址]是標準的體驗資料模型(XDM)資料型別，說明電子郵件地址的詳細資訊。

<img src="../images/data-types/email-address.png" width="450" /><br />

| 屬性 | 說明 |
| --- | --- |
| `address` | RFC2822和後續標準（例如，`name@domain.com`）中通常定義的電子郵件技術位址。<br><br>在XDM中，電子郵件地址必須包含有效的上層網域才能通過驗證。 請參閱下列[檔案](https://data.iana.org/TLD/tlds-alpha-by-domain.txt)，以取得網際網路指定號碼授權單位(IANA)所定義的有效上層網域完整清單。 |
| `label` | 可能提供的其他顯示資訊。 例如，如果電子郵件的Microsoft Outlook Rich Address顯示為`John Smith smithjr@company.uk`，則會將`John Smith`置於此欄位中。 |
| `primary` | 指出這是否為個人的主要電子郵件地址。 設定檔在特定時間只能有一個`primary`電子郵件地址。 |
| `status` | 指出目前是否可以使用電子郵件地址 |
| `statusReason` | 目前`status`的說明。 |
| `type` | 帳戶與個人的關聯方式（例如`work`或`personal`）。 |

{style="table-layout:auto"}


如需電子郵件地址資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
