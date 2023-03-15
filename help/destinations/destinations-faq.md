---
keywords: 目的地；問題；常問的問題；常見問題集；目的地常見問題集
title: 常見問答
description: 關於Adobe Experience Platform目的地最常問問題的回答
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# 常見問答 {#faq}

## 總覽 {#overview}

本檔案提供Adobe Experience Platform目的地相關常見問題的解答。 以了解與其他 [!DNL Platform] 服務，包括所有 [!DNL Platform] API請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

## 一般目的地問題 {#general}

**為何在Experience PlatformUI和匯出的CSV檔案中看到不同的設定檔計數？**

這是正常行為，因為Experience Platform執行分段的方式。

串流區段會全天更新串流區段的設定檔計數，而批次區段則會每24小時更新一次批次區段的設定檔計數。

當區段匯出排程與區段排程不同時，UI和匯出的設定檔會計數 [!DNL CSV] 檔案會不同，尤其是當涉及串流區段時。

請參閱 [區段服務檔案](../segmentation/home.md) 以取得更多詳細資訊。

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**在啟用對象之前，我需要做什麼 [!DNL Facebook Custom Audiences]?**

將受眾區段傳送至之前 [!DNL Facebook]，請確定您符合下列需求：

* 您的 [!DNL Facebook] 使用者帳戶必須具有 **[!DNL Manage campaigns]** 已為您打算使用的廣告帳戶啟用權限。
* 此 **Adobe Experience Cloud** 業務帳戶必須新增為您 [!DNL Facebook Ad Account]. 使用 `business ID=206617933627973`. 請參閱 [將合作夥伴添加到您的業務經理](https://www.facebook.com/business/help/1717412048538897) 在Facebook檔案中取得詳細資訊。
   >[!IMPORTANT]
   >
   > 設定Adobe Experience Cloud的權限時，您必須啟用 **管理行銷活動** 權限。 這是進行 [!DNL Adobe Experience Platform] 整合的必要權限。
* 閱讀並簽署 [!DNL Facebook Custom Audiences] 服務條款。 若要完成此操作，請前往 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID]。

**是否需要將任何應用程式或像素新增至 [!DNL Facebook] 廣告商帳戶？**

不可以。 由於這不是以像素為基礎的整合，因此不需要新增任何像素至廣告商帳戶。

**facebook需要多久才能處理來自Adobe Experience Platform的資訊？**

截至2021年3月， [!DNL Facebook Custom Audiences] 最多需要一小時來處理從 [!DNL Platform].

**我可以使用 [!DNL Facebook Custom Audiences] 適用於其他 [!DNL Facebook] 應用程式，如 [!DNL Instagram]?**

您可以使用 [!DNL Facebook Custom Audiences] 目的地鎖定受支援Facebook應用程式系列中受 [!DNL Facebook Custom Audiences]，包括 [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]，和 [!DNL Messenger]. 廣告商要在上執行行銷活動的應用程式，會在 [!DNL Facebook Ads Manager].

**兩者的差異為何 [!DNL Facebook Custom Audiences] 連線與 [!DNL Facebook Pixel] 擴充功能？**

此 [!DNL Facebook Custom Audiences] 連線使用 [!DNL Platform] 將對象傳送至 [!DNL Facebook]，而 [[!DNL Facebook Pixel] 連接](../destinations/catalog/advertising/facebook-pixel.md) 使用 [!DNL Facebook] 整合在網站中的像素。

這兩項整合相輔相成，您可以同時使用兩者來確保受眾涵蓋範圍更廣。例如，您可以使用 [!DNL Facebook Pixel] 未建立帳戶的探礦網站訪客擴充功能，但 [!DNL Facebook Custom Audiences] 可協助您鎖定現有客戶，根據 [!DNL Platform] 身份。

**Adobe Experience Platform與 [!DNL Facebook Custom Audiences] 支援在使用者不再符合受眾資格時取消其受眾的資格？**

是的，整合支援將使用者從 [!DNL Facebook Custom Audiences] 當他們不再符合資格時。

**如何先雜湊對象資料，再將其傳送至 [!DNL Facebook]?**

[!DNL Facebook] 需要清楚傳送任何個人識別資訊(PII)。 因此，對象已啟動至 [!DNL Facebook] 可以砍掉 *雜湊* 識別碼，例如電子郵件地址或電話號碼。

如需ID比對需求的詳細說明，請參閱 [ID比對需求](catalog/social/facebook.md#id-matching-requirements).

**我可以在 [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] 支援啟用下列身分：雜湊電子郵件，雜湊電話號碼， [!DNL GAID], [!DNL IDFA]、和自訂外部ID。

**我可以在Platform UI中為不同的Facebook帳戶建立多個Facebook目的地嗎？**

可以。Experience Platform中的Facebook目的地為Facebook中廣告帳戶的1:1。 您可以為公司中的每個Facebook廣告帳戶建立個別的Facebook目的地。 關注 [目的地連線教學課程](/help/destinations/ui/connect-destination.md) 並針對Platform UI中的每個新Facebook目的地，連線至個別的Facebook帳戶。 您可以連線的Facebook和帳戶數沒有限制。

## Google Customer Match {#google-customer-match}

**將區段匯出至Google客戶比對時，為何在Google介面中看到區段名稱結尾附加了額外的數字？**

Google要求區段名稱必須是唯一的。 您看到的數字是 [UNIX時間戳記](https://www.unixtimestamp.com/) 如果您將相同的區段對應至多個Google目的地，則會附加這些區段名稱以保持唯一。

## linkedIn相符的對象 {#linkedin}

**是否需要將任何應用程式或像素新增至 [!DNL LinkedIn] 廣告商帳戶？**

不可以。 由於這不是以像素為基礎的整合，因此不需要新增任何像素至廣告商帳戶。

**在啟用對象之前，我需要做什麼 [!DNL LinkedIn Matched Audiences]?**

您可以使用 [!UICONTROL linkedIn相符的對象] 目的地，請確定 [!DNL LinkedIn Campaign Manager] 帳戶具有 [!DNL Creative Manager] 權限層級或更高。

了解如何編輯 [!DNL LinkedIn Campaign Manager] 使用者權限，請參閱 [新增、編輯及移除Advertising帳戶的使用者權限](https://www.linkedin.com/help/lms/answer/5753) 在LinkedIn檔案中。

**如何先雜湊對象資料，再將其傳送至 [!DNL LinkedIn]?**

[!DNL LinkedIn] 需要清楚傳送任何個人識別資訊(PII)。 因此，對象已啟動至 [!DNL LinkedIn] 可以砍掉 *雜湊* 識別碼，例如電子郵件地址或電話號碼。

如需ID比對需求的詳細說明，請參閱 [ID比對需求](catalog/social/linkedin.md#id-matching-requirements).

**我可以在 [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] 支援啟用下列身分：雜湊電子郵件， [!DNL GAID]，和 [!DNL IDFA].
