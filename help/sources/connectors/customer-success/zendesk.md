---
title: Zendesk Source Connector概述
description: 瞭解如何使用API或使用者介面將Zendesk連線至Adobe Experience Platform。
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# [!DNL Zendesk]

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商客戶成功應用程式擷取資料。 對客戶成功提供者的支援包括[!DNL Zendesk]。

此Adobe Experience Platform [來源](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=zh-Hant)利用[Zendesk搜尋API >匯出搜尋結果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results)，將使用者資訊從Zendesk傳回Experience Platform以進行進一步處理。

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 驗證您的[!DNL Zendesk]帳戶

[!DNL Zendesk]使用持有人權杖作為驗證機制來與[!DNL Zendesk] API通訊。

本節概述驗證[!DNL Zendesk]帳戶所需完成的先決條件步驟。

* 驗證您[!DNL Zendesk]帳戶的第一步是確定您有[!DNL Zendesk]支援帳戶。 如果您還沒有帳戶，請參閱[[!DNL Zendesk] 註冊頁面](https://www.zendesk.com/register/)來註冊並建立您的Zendesk帳戶。
* 成功註冊後，請瀏覽至[[!DNL Zendesk] 網站](https://www.zendesk.com/login/)並提供您的&#x200B;**子網域**。
* 接著，選取「**[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**」。
* 最後，從&#x200B;**[!DNL API token]**&#x200B;區段擷取您的API Token。

![Zendesk API權杖](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

如需如何擷取子網域的資訊，請參閱[[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->)。 如需有關產生API權杖的資訊，請參閱產生新API權杖的[[!DNL Zendesk] 指南](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>)。

以下檔案提供如何使用API或使用者介面將[!DNL Zendesk]連線至Experience Platform的資訊：

## 使用API連線[!DNL Zendesk]至Experience Platform

* [使用Flow Service API為 [!DNL Zendesk] 建立來源連線和資料流](../../tutorials/api/create/customer-success/zendesk.md)

## 使用UI連線[!DNL Zendesk]至Experience Platform

* [在使用者介面中建立 [!DNL Zendesk ]來源連線](../../tutorials/ui/create/customer-success/zendesk.md)
* [在UI中建立客戶成功來源連線的資料流](../../tutorials/ui/dataflow/customer-success.md)
