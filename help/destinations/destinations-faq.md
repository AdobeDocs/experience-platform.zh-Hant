---
keywords: 目的地；問題；常見問題；faq；目的地常見問題
title: 常見問答
description: 關於Adobe Experience Platform目的地最常見問題的解答
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: dff460f0b0d365d3d643744544642d9f9488e18a
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 2%

---

# 常見問答 {#faq}

## 概觀 {#overview}

本檔案提供有關Adobe Experience Platform目的地的常見問題解答。 關於其他相關問題和疑難排解 [!DNL Platform] 服務，包括所有遇到的 [!DNL Platform] API，請參閱 [Experience Platform疑難排解指南](../landing/troubleshooting.md).

## 一般目的地問題 {#general}

### 為什麼在Experience Platform UI和匯出的CSV檔案中會看到不同的設定檔計數？

+++答案由於Experience Platform執行分段的方式，這是正常行為。

串流細分會更新一整天串流對象的設定檔計數，而批次細分則會每24小時更新批次對象的設定檔計數一次。

當對象匯出排程與分段排程不同時，UI與匯出的設定檔會計算 [!DNL CSV] 檔案會有所不同，尤其是針對串流對象。

請參閱 [分段服務檔案](../segmentation/home.md) 以取得更多詳細資料。
+++

### 為何ID在停用並重新啟用更新對象至相同目的地時，會看到低匹配率？

+++回答

從串流目的地停用和取消受眾並不會在受眾重新啟用至相同串流目的地時觸發回填。

**範例**

您對串流目的地啟用了包含10個設定檔的受眾。

啟用對象後，您會意識到您想要變更對象設定，因此您停用對象並變更其母體條件，導致對象母體為100個設定檔。

您將更新的對象重新啟用到相同的目的地，但由於沒有觸發回填，因此您的目的地不會收到額外的90個設定檔。

**解決方案**

為確保所有設定檔都傳送至您的目的地，您必須使用新設定建立新的對象，然後將其啟用至您的目的地。

+++

### 從目的地移除對象時，是否有任何傳送至目的地的訊號指出對象已移除？

+++回答

否，Experience Platform目的地和目標系統的客戶執行個體之間沒有相依性。 在接收端，目標系統看到的唯一指示是它停止接收該對象資料。

+++

<!--
## [!DNL Experience Cloud Audiences] {#eca-faq}

### What are the differences between the Experience Cloud Audiences and Adobe Target destinations?

+++Answer

See the table below for a feature comparison between the Experience Cloud Audiences and Adobe Target destinations.

||Experience Cloud Audiences|Adobe Target|
|---|---|---|
| **Supported Experience Cloud apps** | Supports audience activation to Audience Manager, Adobe Target, Adobe Analytics, Advertising Cloud, Marketo, Adobe Campaign | Supports audience activation only to Adobe Target |
| **Supports audience activation** | ✓ | ✓ |
| **Supports attribute activation** | X | ✓ |
| **Latency** | Profiles begin activating in 6 hours. Full population is visible in 48 hours​. |Depends on implementation​ type. <ul><li>Web SDK enables same-page/next-page​ personalization.</li><li>AT.js enables next-session personalization.</li></ul> |
| **DULE support** | ✓ | ✓ |
| **Marketing actions support** | ✓ | ✓ |
| **Supported IDs** | [!DNL ECID], [!DNL GAID], [!DNL IDFA], [!DNL email_lc_sha256] | Any ID type |
| **Sandbox support** | One sandbox | Multiple sandboxes |
| **Consent support** | X | Yes. Requires Privacy & Security Shield. |
| **Edge segmentation support** | Supports activation of edge audiences. Does not support edge segmentation. | Supports edge segmentation and activation of edge audiences. |
| **Supported audiences** | All types of audiences  | Edge merge policy required for activation.|

+++

-->

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### 我需要做什麼才能在中啟用對象 [!DNL Facebook Custom Audiences]？

+++回答在您傳送對象到之前 [!DNL Facebook]，確定您符合下列需求：

* 您的 [!DNL Facebook] 使用者帳戶必須具有 **[!DNL Manage campaigns]** 已為您計畫使用的廣告帳戶啟用許可權。
* 此 **Adobe Experience Cloud** 企業帳戶必須新增為廣告合作夥伴，才能在您的 [!DNL Facebook Ad Account]. 使用 `business ID=206617933627973`。另請參閱 [新增合作夥伴至您的Business Manager](https://www.facebook.com/business/help/1717412048538897) 詳細資訊，請參閱Facebook檔案。

  >[!IMPORTANT]
  >
  > 設定Adobe Experience Cloud的許可權時，您必須啟用 **管理行銷活動** 許可權。 這是進行 [!DNL Adobe Experience Platform] 整合的必要權限。
* 閱讀並簽署 [!DNL Facebook Custom Audiences] 服務條款。 若要完成此操作，請前往 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID]。
+++

### 我需要將任何應用程式或畫素新增到我的 [!DNL Facebook] 廣告商帳戶？

+++答案否。 由於這不是以畫素為基礎的整合，因此不需要將任何畫素新增至您的廣告商帳戶。
+++

### facebook需要多久才能處理來自Adobe Experience Platform的資訊？

+++截至2021年3月的答案， [!DNL Facebook Custom Audiences] 最多需要一小時來處理從收到的資訊 [!DNL Platform].
+++

### 我可以使用 [!DNL Facebook Custom Audiences] 針對其他中的對象目標定位 [!DNL Facebook] 應用程式，例如 [!DNL Instagram]？

+++Amswer您可以使用 [!DNL Facebook Custom Audiences] facebook所支援應用程式系列中的受眾鎖定目標 [!DNL Facebook Custom Audiences]，包括 [!DNL Facebook]， [!DNL Instagram]， [!DNL Audience Network]、和 [!DNL Messenger]. 廣告商想要在哪個應用程式上執行行銷活動，會在中的版位層級顯示 [!DNL Facebook Ads Manager].
+++

### 兩者之間有何差異？ [!DNL Facebook Custom Audiences] 連線和 [!DNL Facebook Pixel] 副檔名？

+++回答 [!DNL Facebook Custom Audiences] 連線使用 [!DNL Platform] 將受眾傳送至時的身分 [!DNL Facebook]，而 [[!DNL Facebook Pixel] 連線](../destinations/catalog/advertising/facebook-pixel.md) 使用 [!DNL Facebook] 畫素已整合至網站。

這兩項整合相輔相成，您可以同時使用兩者來確保受眾涵蓋範圍更廣。例如，您可以使用 [!DNL Facebook Pixel] 尚未建立帳戶的潛在網站訪客擴充功能，而 [!DNL Facebook Custom Audiences] 可協助您根據以下專案鎖定現有客戶 [!DNL Platform] 身分。
+++

### Adobe Experience Platform是否與整合 [!DNL Facebook Custom Audiences] 當使用者不再符合受眾資格時，支援將他們從受眾中取消資格?**

+++回答是，整合支援將使用者從 [!DNL Facebook Custom Audiences] 不再符合資格時。
+++

### 在傳送對象資料到之前，應如何先將對象資料雜湊化？ [!DNL Facebook]？

+++回答
[!DNL Facebook] 需要未明確傳送任何個人識別資訊(PII)。 因此，啟用的對象 [!DNL Facebook] 鍵可關閉 *雜湊* 識別碼，例如電子郵件地址或電話號碼。

如需ID比對需求的詳細說明，請參閱 [ID比對要求](catalog/social/facebook.md#id-matching-requirements).
+++

### 我可以在哪一種身分啟用 [!DNL Facebook Custom Audiences]？

+++回答
[!DNL Facebook Custom Audiences] 支援啟用下列身分：雜湊電子郵件、雜湊電話號碼、 [!DNL GAID]， [!DNL IDFA]，以及自訂外部ID。
+++

### 我可以為個別的Facebook帳戶在Platform UI中建立多個Facebook目的地嗎？

+++回答是。 Experience Platform中的Facebook目的地與Facebook中的廣告帳戶之比是1:1。 您可以為公司中的每個Facebook廣告帳戶建立個別的Facebook目的地。 請遵循 [目的地連線教學課程](/help/destinations/ui/connect-destination.md) 並在Platform UI中為每個新Facebook目的地連線至個別的Facebook帳戶。 您可以連線的Facebook廣告帳戶數量沒有限制。
+++

## Google Customer Match {#google-customer-match}

### 將對象匯出至Google Customer Match時，為什麼在Google介面的對象名稱結尾會附加額外的數字？

+++回答Google需要對象名稱必須是唯一的。 您看到的數字是 [UNIX時間戳記](https://www.unixtimestamp.com/) 如果您將相同的對象對應至多個Google目的地，則會附加這些對象，以保持對象名稱不重複。
+++

## linkedIn相符的受眾 {#linkedin}

### 我需要將任何應用程式或畫素新增到我的 [!DNL LinkedIn] 廣告商帳戶？

+++答案否。 由於這不是以畫素為基礎的整合，因此不需要將任何畫素新增至您的廣告商帳戶。
+++

### 我需要做什麼才能在中啟用對象 [!DNL LinkedIn Matched Audiences]？

+++使用前請先回答 [!UICONTROL linkedIn相符的受眾] 目的地，確認您的 [!DNL LinkedIn Campaign Manager] 帳戶具有 [!DNL Creative Manager] 許可權層級或更高。

若要瞭解如何編輯您的 [!DNL LinkedIn Campaign Manager] 使用者許可權，請參閱 [新增、編輯和移除Advertising帳戶的使用者許可權](https://www.linkedin.com/help/lms/answer/5753) (位於LinkedIn檔案中)。
+++

### 在傳送對象資料到之前，應如何先將對象資料雜湊化？ [!DNL LinkedIn]？

+++回答
[!DNL LinkedIn] 需要未明確傳送任何個人識別資訊(PII)。 因此，啟用的對象 [!DNL LinkedIn] 鍵可關閉 *雜湊* 識別碼，例如電子郵件地址或電話號碼。

如需ID比對需求的詳細說明，請參閱 [ID比對要求](catalog/social/linkedin.md#id-matching-requirements).
+++

### 我可以在哪一種身分啟用 [!DNL LinkedIn]？

+++回答
[!DNL LinkedIn Matched Audiences] 支援啟用下列身分：雜湊電子郵件、 [!DNL GAID]、和 [!DNL IDFA].

+++

## 透過Adobe Target和自訂個人化目的地實現相同頁面和下一頁個人化 {#same-next-page-personalization}

### 我是否需要使用Experience Platform Web SDK傳送對象和屬性至Adobe Target？

+++答案否， [Web SDK](../edge/home.md) 不一定要啟用對象，才可以 [Adobe Target](catalog/personalization/adobe-target-connection.md).

但是，如果 [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html) 已使用（而非Web SDK），僅支援下一次工作階段個人化。

的 [相同頁面和下一頁個人化](ui/activate-edge-personalization-destinations.md) 使用案例，您必須使用 [Web SDK](../edge/home.md) 或 [Edge Network伺服器API](../server-api/overview.md). 請參閱以下檔案： [啟用對象至邊緣目的地](ui/activate-edge-personalization-destinations.md) 以取得更多實作詳細資訊。
+++

### 我可以從Real-time Customer Data Platform傳送至Adobe Target或自訂個人化目的地的屬性數量是否有限制？

+++回答「是」，在Adobe Target或自訂個人化目的地啟用受眾時，同頁和下一頁個人化使用案例支援每個沙箱最多30個屬性。 請參閱中有關啟動護欄的詳細資訊 [護欄檔案](guardrails.md#edge-destinations-activation).
+++

### 啟動支援哪些型別的屬性（例如陣列、地圖等）？

+++回答目前，僅支援靜態的單值屬性，例如 `person.name.firstName`. 目前不支援陣列屬性。
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### 我在Experience Platform中建立對象後，需要多久才能供邊緣細分使用案例使用？

+++回答對象定義會傳播至 [Edge Network](../edge/home.md) 最多一小時。 但是，如果對象在這第一個小時內啟動，可能會錯過一些符合對象資格的訪客。
+++

### 我可以在哪裡檢視Adobe Target中已啟用的屬性？

+++回應屬性可用於Target中，位置如下： [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) 和 [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html) 選件。
+++

### 我可以建立沒有資料串流的目的地，然後在稍後將資料串流新增到相同目的地嗎？

+++答案目前不支援透過目的地UI進行此作業。 如果您需要這方面的協助，請洽詢您的Adobe代表。
+++

### 如果我刪除Adobe Target目的地，會發生什麼事？

+++答案當您刪除目的地時，對應至目的地的所有對象和屬性都會從Adobe Target中刪除，而也會從Edge Network中移除。
+++

### 整合是否可以使用Edge Network Server API運作？

+++回答是，Edge Network Server API可與自訂個人化目的地搭配使用。 由於設定檔屬性可能包含敏感資料，為了保護此資料，自訂個人化目的地需要您使用Edge Network Server API來收集資料。 此外，所有API呼叫都必須在 [已驗證的內容](../server-api/authentication.md).
+++

### 我只能有一個邊緣主動的合併原則。 我可以建立使用不同合併原則的受眾，並且仍將其當作串流受眾傳送給Adobe Target嗎？

+++答案否。 您要對Adobe Target啟用的所有對象都必須使用active-on-edge [合併原則](../profile/merge-policies/ui-guide.md).
+++

### 資料使用標籤和實作(DULE)和同意原則是否已強制執行？

+++回答是。 此 [資料控管和同意原則](../data-governance/home.md) 已建立並與所選行銷動作相關聯的屬性，將控管所選屬性的啟動。
+++

### 為 [!DNL Adobe Target] 和 [!DNL Custom Personalization] 目的地 [!DNL HIPAA]是否符合？

+++回答
[!DNL Adobe Target] 不是 [!DNL HIPPA] — 相容於 [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/solutions/industries/healthcare.html). 客戶應就以下事項與自己的法律團隊確認 [!DNL HIPPA] — 在透過使用邊緣個人化之前對自訂最佳化通道整備 [!DNL Adobe Target] 或 [!DNL Custom Personalization] 目的地。

若是需要大規模套用同意原則管理的使用案例，客戶必須購買 [!DNL Adobe Privacy & Security Shield]. [!DNL Adobe Privacy & Security Shield] 功能是以進階功能套件形式出售，不得另行購買。

此服務包括客戶管理的金鑰和提升的臨界值，以管理客戶資料生命週期。

此 [!DNL Adobe Target] 和 [!DNL Custom Personalization] 目的地會與整合 [Experience Platform資料使用標籤](../data-governance/labels/overview.md) 和 [同意原則執行服務](../data-governance/enforcement/overview.md). 這些功能可供所有客戶使用。




+++

