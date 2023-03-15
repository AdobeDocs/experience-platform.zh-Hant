---
keywords: Experience Platform；首頁；熱門主題；Zendesk;zendesk
solution: Experience Platform
title: Zendesk源連接器概述
description: 了解如何使用API或使用者介面將Zendesk連線至Adobe Experience Platform。
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 61b694ca5fbd3548243663b3f1bff06aaca72434
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---

# （測試版） [!DNL Zendesk]

>[!NOTE]
>
>此 [!DNL Zendesk] 來源為測試版。 請參閱 [來源概觀](../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

Experience Platform支援從協力廠商客戶成功應用程式擷取資料。 客戶成功提供者的支援包括 [!DNL Zendesk].

這個Adobe Experience Platform [來源](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=zh-Hant) 利用 [Zendesk Search API >導出搜索結果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) 這會從Zendesk將使用者資訊傳回Experience Platform，以便進一步處理。

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 驗證您的 [!DNL Zendesk] 帳戶

[!DNL Zendesk] 使用承載令牌作為與通信的驗證機制 [!DNL Zendesk] API。

本節概述為了驗證您的 [!DNL Zendesk] 帳戶。

* 驗證您的 [!DNL Zendesk] 帳戶是確保您 [!DNL Zendesk] 支援帳戶。 如果您還沒有看到 [[!DNL Zendesk] 註冊頁面](https://www.zendesk.com/register/) 註冊並建立Zendesk帳戶。
* 成功註冊後，請導覽至 [[!DNL Zendesk] 網站](https://www.zendesk.com/login/) 提供 **子網域**.
* 下一步，選擇 **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* 最後，從 **[!DNL API token]** 區段。

![Zendesk API代號](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

請參閱 [[!DNL Zendesk documentation on subdomains]](https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain-) 以取得如何擷取子網域的資訊。 如需產生API代號的詳細資訊，請參閱 [[!DNL Zendesk] 產生新API代號的指南](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token).

以下檔案提供如何連線的資訊 [!DNL Zendesk] 若要使用API或使用者介面來建立平台：

## Connect [!DNL Zendesk] 使用API到平台

* [為建立源連接和資料流 [!DNL Zendesk] 使用流量服務API](../../tutorials/api/create/customer-success/zendesk.md)

## Connect [!DNL Zendesk] 使用UI設為Platform

* [建立 [!DNL Zendesk ]UI中的源連接](../../tutorials/ui/create/customer-success/zendesk.md)
* [在UI中為客戶成功源連接建立資料流](../../tutorials/ui/dataflow/customer-success.md)
