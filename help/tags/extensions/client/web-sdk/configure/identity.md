---
title: 身分識別設定
description: 定義標記擴充功能識別訪客的方式。
exl-id: 12e707f4-c37b-4c02-bfec-5ef7b98c2d3b
source-git-commit: b292b9243816b1eed7fd3939096ddc30d6be0606
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 10%

---

# 身分識別設定 {#identity}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_identity"
>title="身分識別"
>abstract="定義標記擴充功能識別訪客的方式。"

此設定區段可讓您定義處理使用者識別時的網頁SDK行為。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下捲動至&#x200B;**[!UICONTROL Identity]**&#x200B;區段。

![此影像顯示標籤UI中Web SDK標籤擴充功能的身分設定](../assets/web-sdk-ext-identity.png)

提供下列選項：

## [!UICONTROL Migrate ECID from VisitorAPI]

允許Web SDK讀取`AMCV`和`s_ecid` Cookie並設定`AMCV`所使用`Visitor.js` Cookie的核取方塊。 從使用`VisitorAPI.js`的資料庫移轉至Web SDK時，此功能很重要，因為有些頁面可能仍在使用`Visitor.js`。 此選項可讓SDK繼續使用相同的ECID，這樣就不會將使用者識別為兩個不同的使用者。 此核取方塊的JavaScript資料庫等同於[`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md)。

## [!UICONTROL Use third-party cookies]

啟用此選項後，Web SDK會嘗試將使用者識別碼儲存在第三方Cookie中。 如果成功，則會在使用者瀏覽多個網域時將其識別為單一使用者，而不是在每個網域上將其識別為個別使用者。 如果已啟用此選項，如果瀏覽器不支援第三方Cookie或使用者已設定不允許第三方Cookie，則SDK可能仍無法將使用者識別碼儲存在第三方Cookie中。 在此情況下，SDK只會將識別碼儲存在第一方網域中。 此核取方塊的JavaScript資料庫等同於[`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md)。
