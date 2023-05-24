---
keywords: 目的地；問題；常問問題；常見問題目標常見問題
title: 常見問答
description: 關於Adobe Experience Platform目的地最常問問題的解答
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# 常見問答 {#faq}

## 總覽 {#overview}

本文檔提供有關Adobe Experience Platform目的地的常見問題解答。 有關與其他相關的問題和故障排除 [!DNL Platform] 服務，包括所有 [!DNL Platform] API，請參閱 [Experience Platform故障排除指南](../landing/troubleshooting.md)。

## 一般目標問題 {#general}

**為什麼在Experience PlatformUI和導出的CSV檔案中看到不同的配置檔案計數？**

這是正常行為，因為Experience Platform執行分割的方式。

流分段在一天中更新流段的配置檔案計數，而批分段每24小時更新一次批段的配置檔案計數。

當段導出計畫與分段計畫不同時，UI和導出的配置檔案計數 [!DNL CSV] 檔案將不同，特別是在流段方面。

查看 [分段服務文檔](../segmentation/home.md) 的子菜單。

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**在激活觀眾之前，我需要做什麼 [!DNL Facebook Custom Audiences]?**

在將受眾段發送到 [!DNL Facebook]，確保滿足以下要求：

* 您 [!DNL Facebook] 用戶帳戶必須具有 **[!DNL Manage campaigns]** 已為您計畫使用的Ad帳戶啟用權限。
* 的 **Adobe Experience Cloud** 必須將業務帳戶添加為廣告合作夥伴 [!DNL Facebook Ad Account]。 使用 `business ID=206617933627973`. 請參閱 [將合作夥伴添加到您的業務經理](https://www.facebook.com/business/help/1717412048538897) 在Facebook文檔中。
   >[!IMPORTANT]
   >
   > 為Adobe Experience Cloud配置權限時，必須啟用 **管理市場活動** 權限。 這是進行 [!DNL Adobe Experience Platform] 整合的必要權限。
* 閱讀並簽名 [!DNL Facebook Custom Audiences] 服務條款。 若要完成此操作，請前往 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID]。

**是否需要將任何應用或像素添加到我 [!DNL Facebook] 廣告客戶？**

不可以。 由於這不是基於像素的整合，因此無需向您的廣告商帳戶添加任何像素。

**facebook要多久才能處理Adobe Experience Platform的資訊？**

截至2021年3月， [!DNL Facebook Custom Audiences] 處理從 [!DNL Platform]。

**我能用 [!DNL Facebook Custom Audiences] 針對其他受眾 [!DNL Facebook] 應用，例如 [!DNL Instagram]?**

您可以使用 [!DNL Facebook Custom Audiences] 目的地，針對Facebook家族支援的應用程式 [!DNL Facebook Custom Audiences]，包括 [!DNL Facebook]。 [!DNL Instagram]。 [!DNL Audience Network], [!DNL Messenger]。 廣告商要在其上運行廣告的應用的選擇在中的放置級別上表示 [!DNL Facebook Ads Manager]。

**這和 [!DNL Facebook Custom Audiences] 連接和 [!DNL Facebook Pixel] 分機？**

的 [!DNL Facebook Custom Audiences] 連接使用 [!DNL Platform] 向觀眾發送時的身份 [!DNL Facebook]，也請參見Wiki頁。 [[!DNL Facebook Pixel] 連接](../destinations/catalog/advertising/facebook-pixel.md) 使用 [!DNL Facebook] 整合在網站中的像素。

這兩項整合相輔相成，您可以同時使用兩者來確保受眾涵蓋範圍更廣。例如，您可以 [!DNL Facebook Pixel] 未建立帳戶的潛在客戶網站訪問者的擴展，而 [!DNL Facebook Custom Audiences] 可幫助您瞄準現有客戶，基於 [!DNL Platform] 身份。

**Adobe Experience Platform與 [!DNL Facebook Custom Audiences] 支援在用戶不再有資格訪問時取消其訪問對象資格？**

是，整合支援將用戶從 [!DNL Facebook Custom Audiences] 當他們不再合格時。

**在將受眾資料發送到之前，應如何對其進行散列 [!DNL Facebook]?**

[!DNL Facebook] 要求未清除發送個人身份資訊(PII)。 因此，觀眾被激活 [!DNL Facebook] 可以鎖住 *散* 標識符，如電子郵件地址或電話號碼。

有關ID匹配要求的詳細說明，請參見 [ID匹配要求](catalog/social/facebook.md#id-matching-requirements)。

**我可以在 [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] 支援激活以下標識：丟失的電子郵件，丟失的電話號碼， [!DNL GAID]。 [!DNL IDFA]和自定義外部ID。

**我是否可以在平台UI中為單獨的Facebook帳戶建立多個Facebook目標？**

可以。facebook的Experience Platform目的地是Facebook的一個廣告賬戶。 您可以為公司中的每個Facebook廣告帳戶建立單獨的Facebook目標。 關注 [目標連接教程](/help/destinations/ui/connect-destination.md) 並連接到平台UI中每個新的Facebook目標的單獨Facebook帳戶。 您可以連接的Facebook廣告帳戶數沒有限制。

## Google Customer Match {#google-customer-match}

**將段導出到Google客戶匹配時，為什麼在Google介面的段名稱末尾附加了額外的數字？**

Google要求段名唯一。 你看到的數字 [UNIX時間戳](https://www.unixtimestamp.com/) 如果將同一段映射到多個Google目標，則會附加這些段名以保持段名唯一。

## linkedIn與觀眾 {#linkedin}

**是否需要將任何應用或像素添加到我 [!DNL LinkedIn] 廣告客戶？**

不可以。 由於這不是基於像素的整合，因此無需向您的廣告商帳戶添加任何像素。

**在激活觀眾之前，我需要做什麼 [!DNL LinkedIn Matched Audiences]?**

在使用 [!UICONTROL linkedIn對陣觀眾] 目標，確保 [!DNL LinkedIn Campaign Manager] 帳戶 [!DNL Creative Manager] 權限級別或更高。

瞭解如何編輯 [!DNL LinkedIn Campaign Manager] 用戶權限，請參閱 [添加、編輯和刪除廣告帳戶上的用戶權限](https://www.linkedin.com/help/lms/answer/5753) 在LinkedIn檔案里。

**在將受眾資料發送到之前，應如何對其進行散列 [!DNL LinkedIn]?**

[!DNL LinkedIn] 要求未清除發送個人身份資訊(PII)。 因此，觀眾被激活 [!DNL LinkedIn] 可以鎖住 *散* 標識符，如電子郵件地址或電話號碼。

有關ID匹配要求的詳細說明，請參見 [ID匹配要求](catalog/social/linkedin.md#id-matching-requirements)。

**我可以在 [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] 支援激活以下標識：大量郵件， [!DNL GAID], [!DNL IDFA]。
