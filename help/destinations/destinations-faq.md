---
keywords: 目的地；問題；常問的問題；常見問答；目的地常見問答集
title: 目標常見問答集
seo-title: 目標常見問答集
description: 關於Adobe Experience Platform目的地的常見問題解答
seo-description: 關於Adobe Experience Platform目的地的常見問題解答
source-git-commit: 117f0f82adb764cedaa048e718cd72fa033845a0
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 5%

---


# 目標常見問答集 {#faq}

## [!DNL Facebook Custom Audiences] (#facebook常見問答)

**在啟動受眾之前，我需要做什麼 [!DNL Facebook Custom Audiences]?**

在將對象區段傳送至[!DNL Facebook]之前，請確定您符合下列需求：

* 您的[!DNL Facebook]使用者帳戶必須已針對您計畫使用的廣告帳戶啟用&#x200B;**[!DNL Manage campaigns]**&#x200B;權限。
* **Adobe Experience Cloud**&#x200B;商業帳戶必須新增為[!DNL Facebook Ad Account]的廣告合作夥伴。 使用 `business ID=206617933627973`。如需詳細資訊，請參閱Facebook檔案中的[將合作夥伴新增至您的業務經理](https://www.facebook.com/business/help/1717412048538897)。
   >[!IMPORTANT]
   >
   > 設定Adobe Experience Cloud的權限時，您必須啟用「管理促銷活動&#x200B;**」權限。**&#x200B;這是進行 [!DNL Adobe Experience Platform] 整合的必要權限。
* 閱讀並簽署[!DNL Facebook Custom Audiences]服務條款。 若要完成此操作，請前往 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID]。

**我是否需要新增任何應用程式或像素至我的廣 [!DNL Facebook] 告商帳戶？**

否。由於這並非以像素為基礎的整合，因此您不需要新增任何像素至廣告商帳戶。

**facebook需要多久才能處理Adobe Experience Platform的資訊？**

自2021年3月起，[!DNL Facebook Custom Audiences]需要最多一小時來處理從[!DNL Platform]收到的資訊。

**我可以用於其 [!DNL Facebook Custom Audiences] 他應用程式中的受 [!DNL Facebook] 眾定位，例如 [!DNL Instagram]?**

您可以使用[!DNL Facebook Custom Audiences]目標，針對[!DNL Facebook Custom Audiences]支援的Facebook應用程式系列，包括[!DNL Facebook]、[!DNL Instagram]、[!DNL Audience Network]和[!DNL Messenger]的對象定位。 廣告商要在[!DNL Facebook Ads Manager]的位置層級中指出要執行促銷活動的應用程式的選擇。

**連線和擴充功能之 [!DNL Facebook Custom Audiences] 間有何 [!DNL Facebook Pixel] 差異？**

[!DNL Facebook Custom Audiences]連線在傳送對象至[!DNL Facebook]時使用[!DNL Platform]身分，而[[!DNL Facebook Pixel] 連線](../destinations/catalog/advertising/facebook-pixel.md)則使用整合在網站中的[!DNL Facebook]像素。

這兩項整合相輔相成，您可以同時使用兩者來確保受眾涵蓋範圍更廣。例如，您可以使用[!DNL Facebook Pixel]擴充功能來探索尚未建立帳戶的網站訪客，而[!DNL Facebook Custom Audiences]可協助您根據[!DNL Platform]身分來定位現有客戶。

**Adobe Experience Platform是否與支援 [!DNL Facebook Custom Audiences] 整合，讓使用者在不再符合使用者資格時，無法與受眾取得資格？**

是的，整合支援在使用者不再符合資格時，從[!DNL Facebook Custom Audiences]移除使用者。

**我應如何在將受眾資料傳送至之前先加以雜湊 [!DNL Facebook]?**

[!DNL Facebook] 要求不會傳送任何個人識別資訊(PII)。因此，激活至[!DNL Facebook]的觀眾可以鍵入&#x200B;*雜湊*&#x200B;標識符，如電子郵件地址或電話號碼。

有關ID匹配要求的詳細說明，請參閱[ID匹配要求](catalog/social/facebook.md#id-matching-requirements)。

**我可以啟用哪些身分識別 [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] 支援啟用下列身分：雜湊的電子郵件、雜湊的電 [!DNL GAID]話號碼 [!DNL IDFA]和自訂外部ID。

## linkedIn對象匹配 {#linkedin}

**我是否需要新增任何應用程式或像素至我的廣 [!DNL LinkedIn] 告商帳戶？**

否。由於這並非以像素為基礎的整合，因此您不需要新增任何像素至廣告商帳戶。

**在啟動受眾之前，我需要做什麼 [!DNL LinkedIn Matched Audiences]?**

在您使用[!UICONTROL LinkedIn符合的對象]目標之前，請確定您的[!DNL LinkedIn Campaign Manager]帳戶具有[!DNL Creative Manager]權限層級或更高。

要瞭解如何編輯[!DNL LinkedIn Campaign Manager]用戶權限，請參閱LinkedIn文檔中的[添加、編輯和刪除廣告帳戶的用戶權限。](https://www.linkedin.com/help/lms/answer/5753)

**我應如何在將受眾資料傳送至之前先加以雜湊 [!DNL LinkedIn]?**

[!DNL LinkedIn] 要求不會傳送任何個人識別資訊(PII)。因此，激活至[!DNL LinkedIn]的觀眾可以鍵入&#x200B;*雜湊*&#x200B;標識符，如電子郵件地址或電話號碼。

有關ID匹配要求的詳細說明，請參閱[ID匹配要求](catalog/social/linkedin.md#id-matching-requirements)。

**我可以啟用哪些身分識別 [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] 支援啟用下列身分：雜湊的電子 [!DNL GAID]郵件和 [!DNL IDFA]。
