---
keywords: 目的地；問題；常問的問題；常見問題集；目的地常見問題集
title: 常見問題集
seo-title: 常見問題集
description: 關於Adobe Experience Platform目的地最常問問題的回答
seo-description: 關於Adobe Experience Platform目的地最常問問題的回答
source-git-commit: 47b3ef28281e3480e8b194486845f4fb4326b7d4
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 6%

---


# 常見問題集 {#faq}

## 概述 {#overview}

本檔案提供Adobe Experience Platform目的地相關常見問題的解答。 有關其他[!DNL Platform]服務的問題和故障排除，包括在所有[!DNL Platform] API中遇到的問題，請參閱[Experience Platform故障排除指南](../landing/troubleshooting.md)。

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**在中啟用對象之前，需要做什麼 [!DNL Facebook Custom Audiences]?**

將對象區段傳送至[!DNL Facebook]之前，請確定您符合下列需求：

* 您的[!DNL Facebook]使用者帳戶必須為您打算使用的Ad帳戶啟用&#x200B;**[!DNL Manage campaigns]**&#x200B;權限。
* 必須將&#x200B;**Adobe Experience Cloud**&#x200B;商業帳戶新增為[!DNL Facebook Ad Account]中的廣告合作夥伴。 使用 `business ID=206617933627973`。如需詳細資訊，請參閱Facebook檔案中的[將合作夥伴新增至您的Business Manager](https://www.facebook.com/business/help/1717412048538897) 。
   >[!IMPORTANT]
   >
   > 設定Adobe Experience Cloud的權限時，您必須啟用&#x200B;**管理促銷活動**&#x200B;權限。 這是進行 [!DNL Adobe Experience Platform] 整合的必要權限。
* 閱讀並簽署[!DNL Facebook Custom Audiences]服務條款。 若要完成此操作，請前往 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID]。

**我是否需要將任何應用程式或像素新增至廣 [!DNL Facebook] 告商帳戶？**

否。由於這不是以像素為基礎的整合，因此不需要新增任何像素至廣告商帳戶。

**facebook需要多久才能處理來自Adobe Experience Platform的資訊？**

自2021年3月起，[!DNL Facebook Custom Audiences]最多需要一小時來處理從[!DNL Platform]收到的資訊。

**我可以在其 [!DNL Facebook Custom Audiences] 他應用程式（例如）中 [!DNL Facebook] 用於對象鎖定 [!DNL Instagram]目標嗎？**

您可以在[!DNL Facebook Custom Audiences]所支援的Facebook應用程式系列中，使用[!DNL Facebook Custom Audiences]目標定位對象，包括[!DNL Facebook]、[!DNL Instagram]、[!DNL Audience Network]和[!DNL Messenger]。 [!DNL Facebook Ads Manager]中的版位層級會指出廣告商要在其上執行行銷活動的應用程式選擇。

**連線和擴充功能之 [!DNL Facebook Custom Audiences] 間有何 [!DNL Facebook Pixel] 差異？**

[!DNL Facebook Custom Audiences]連線在將對象傳送至[!DNL Facebook]時使用[!DNL Platform]身分，而[[!DNL Facebook Pixel] 連線](../destinations/catalog/advertising/facebook-pixel.md)則使用整合在網站中的[!DNL Facebook]像素。

這兩項整合相輔相成，您可以同時使用兩者來確保受眾涵蓋範圍更廣。例如，您可以使用[!DNL Facebook Pixel]擴充功能來探索尚未建立帳戶的網站訪客，而[!DNL Facebook Custom Audiences]可協助您根據[!DNL Platform]身分來鎖定現有客戶。

**Adobe Experience Platform與支援的整合 [!DNL Facebook Custom Audiences] 會在使用者不再符合受眾資格時，讓使用者不符合受眾資格嗎？**

是的，整合支援在使用者不再符合資格時，從[!DNL Facebook Custom Audiences]中移除使用者。

**如何先雜湊對象資料再將其傳送至 [!DNL Facebook]?**

[!DNL Facebook] 需要清楚傳送任何個人識別資訊(PII)。因此，對[!DNL Facebook]啟動的對象可以被去除&#x200B;*雜湊*&#x200B;識別碼，例如電子郵件地址或電話號碼。

有關ID匹配要求的詳細說明，請參閱[ID匹配要求](catalog/social/facebook.md#id-matching-requirements)。

**我可以在中啟用何種身分識 [!DNL Facebook Custom Audiences]別？**

[!DNL Facebook Custom Audiences] 支援啟用下列身分：雜湊電子郵件、雜湊電話號碼、  [!DNL GAID]、 [!DNL IDFA]以及自訂外部ID。

## linkedIn相符的對象 {#linkedin}

**我是否需要將任何應用程式或像素新增至廣 [!DNL LinkedIn] 告商帳戶？**

否。由於這不是以像素為基礎的整合，因此不需要新增任何像素至廣告商帳戶。

**在中啟用對象之前，需要做什麼 [!DNL LinkedIn Matched Audiences]?**

在使用[!UICONTROL LinkedIn相符對象]目的地之前，請確定您的[!DNL LinkedIn Campaign Manager]帳戶具有[!DNL Creative Manager]權限層級或更高。

若要了解如何編輯您的[!DNL LinkedIn Campaign Manager]使用者權限，請參閱LinkedIn檔案中的[新增、編輯及移除Advertising帳戶的使用者權限](https://www.linkedin.com/help/lms/answer/5753)。

**如何先雜湊對象資料再將其傳送至 [!DNL LinkedIn]?**

[!DNL LinkedIn] 需要清楚傳送任何個人識別資訊(PII)。因此，對[!DNL LinkedIn]啟動的對象可以被去除&#x200B;*雜湊*&#x200B;識別碼，例如電子郵件地址或電話號碼。

有關ID匹配要求的詳細說明，請參閱[ID匹配要求](catalog/social/linkedin.md#id-matching-requirements)。

**我可以在中啟用何種身分識 [!DNL LinkedIn]別？**

[!DNL LinkedIn Matched Audiences] 支援啟用下列身分：雜湊電子郵件 [!DNL GAID]、和 [!DNL IDFA]。
