---
title: 為擴充功能建立Exchange清單
description: 了解如何將您的擴充功能新增至Adobe Experience Platform中的公開目錄。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 28%

---

# 為擴充功能建立Exchange清單

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

Adobe Experience Platform有單一統一目錄，供使用者檢視可供安裝的標籤擴充功能。 此目錄可在產品中使用，並包含三種類型的擴充功能：

1. **公用擴充功能**:這些是完整的擴充功能，專為任何使用者生產而設計。
1. **私人擴充功能**:這些是專為生產環境而設計的完整擴充功能，但是由公司中的其他使用者開發，且僅供公司內的使用者使用。
1. **開發擴充功能**:這些擴充功能處於作用中開發狀態，僅可在您的公司內使用，且僅可在指定為開發屬性的屬性上使用。

與產品目錄中的擴充功能不同，有些擴充功能也會在[Experience CloudExchange Marketplace](https://exchange.adobe.com/experiencecloud.experience-platform-launch.html#product)中顯示清單。

這些清單可讓擴充功能開發人員發佈功能說明、提供其他支援和檔案的連結，以及將擴充功能行銷給可能不了解您公司或擴充功能的潛在使用者。 在此Marketplace中，您的擴充功能會有公開清單可供檢視，且使用者不需要通過Platform驗證。  許多開發人員認為，開發Exchange清單是有益的，但這並非必要步驟。

如果您沒有公司可上傳和測試您的擴充功能套件，您應註冊Exchange計畫並開始列出。  這會觸發公司帳戶的建立（這需要一些時間，當完成時您會收到電子郵件），您可以用來上傳和測試您的擴充功能。  你不必把上市公之於眾。

如果您已有公司帳戶，或如果您不打算完成清單，則可以略過此步驟的其餘部分，然後繼續[上傳並測試您的擴充功能](./upload-and-test.md)。

## 建立清單

>[!NOTE]
>
>以下流程詳細說明了在Adobe交換程式中建立應用程式清單的過程。 這是用於Adobe Experience Platform中各種整合和擴充功能的辭彙。

![Experience CloudApp Manager連結位置](../images/getting-started/app-mgr-link.png)

1. 登入 [Exchange 合作夥伴網站](https://partners.adobe.com/tw/exchangeprogram/experiencecloud)。登入後，請選取您名稱旁的&#x200B;**App Manager**&#x200B;連結。
1. 選擇&#x200B;**建立新應用程式**&#x200B;頁簽，然後選擇&#x200B;**建立新應用程式**&#x200B;以自定義解決方案，或選擇適用的模板。
1. 提供您的清單資訊。如需 App Manager 的詳細資訊，請參閱完整[文章](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931)。清單資訊應清楚說明擴充功能的用途及其用途。 清單可作為應用程式的行銷空間。 使用清楚的說明、網站登陸頁面的連結、說明檔案的連結或支援電子郵件地址等，在這裡促銷您的擴充功能。 雖然擴充功能檢視的空間有限，但Exchange清單仍提供機會，可推廣您的擴充功能和公司。 以下是改善擴充功能的建議：
   - **應用程式圖示** - 請確保 Exchange 清單的圖示具有適當尺寸；png 請使用 512 x 512，jpg 請使用 1:1 外觀比例。

   >[!NOTE]
   >
   >這是與您在擴充功能程式碼中使用的檔案格式不同。 擴充功能本身將包含 svg 檔案作為[圖示](../manifest.md)。
   - **精選影像**  — 使用獨一無二且能顯示您的品牌和突顯應用程式的影像，吸引眾人目光。 「精選影像」是當某人分享您的Exchange清單連結或在社交媒體上發佈相關貼文時顯示的影像。 因此，它必須是您品牌的模型表示。
   - **App Publisher 的標誌** - 這是您的公司標誌，請確保圖示具有適當尺寸；png 格式請使用 1280 x 720，jpg 格式請使用 2560 x 1440 (16:9)。
   - **設定指示**  — 通知客戶如何設定您的Adobe Experience Platform擴充功能。請確定他們在屬性中安裝您的擴充功能後而隨即看到[組態檢視](../configuration.md)時，了解必須執行哪些必要設定和後續步驟。
   - **標記** - 在編輯清單的第一個頁面上，請務必在「自訂標記」欄位中加入 &quot;Launch&quot; 這個字。這樣，您的清單就會顯示在Exchange市集中標籤的搜尋中：
      ![](../images/getting-started/custom-tags.jpg)
   - **沙箱**  — 您必須透過沙箱帳戶，才能存取完整運作的Adobe Experience Platform版本，才能存取Adobe解決方案。您會在建立應用程式清單時要求這些沙箱帳戶。在&#x200B;**連線**&#x200B;區段中，選取您所建立的應用程式（您的標籤擴充功能）適用的特定連線，當您點擊&#x200B;**儲存**&#x200B;時，就會視需要產生沙箱請求。
1. 提交您的清單。 Adobe Exchange 團隊將審閱您的應用程式，並在需要更新時提供意見回應。如果您在提交清單時勾選了「立即發佈&#x200B;**」核取方塊，則清單在獲得核准後會立即發佈。**&#x200B;如果您想稍後發佈應用程式，請取消勾選核取方塊。當您的擴充功能清單獲核准後，應用程式（擴充功能）清單頁面上的擴充功能旁會出現藍色的&#x200B;**Publish**&#x200B;按鈕。

### 建立有效的清單

請參閱[應用程式提交指導方針](https://partners.adobe.com/tw/exchangeprogram/experiencecloud/build/ec-exchange.html) ，深入了解如何建立最吸引人的清單。

#### 提交您的 Exchange 清單後

提交之後，Adobe Exchange 團隊將審閱應用程式，然後核准應用程式，或回覆指出可能需要的修改。此程序在應用程式提交指導方針中有詳細說明。

如果您無法登入 Exchange 網站，請依照[計畫註冊指南](https://partners.adobe.com/tw/content/mcp/us/en/home/reg-guide.html)中的指示，確定您的電子郵件已註冊到 Exchange 計畫中。每位使用者必須將其電子郵件與其公司的合作夥伴帳戶建立關聯。 有關此程式的問題可透過電子郵件傳送至<ExchangeHelpEC@adobe.com>。

#### 在通過初審後更新 Exchange 清單

如果您需更新擴充功能，或只需要更新 Exchange 清單，請登入[合作夥伴入口網站](https://partners.adobe.com/exchangeprogram/experiencecloud)，然後選取您名稱旁邊的 App Manager 按鈕。接著，請選取您的應用程式，並依照初次用來建立清單的前述流程操作。重新提交後，Adobe Exchange 團隊將審閱變更，然後核准變更，或回覆指出可能需要的修改。

## 將您的擴充功能套件連結至清單

在您的清單獲得核准並可供公開後，我們建議您在擴充功能套件內`extension.json`檔案的`exchange_url`欄位中，提供公開清單的連結。  這會在標籤擴充功能目錄中建立「更多資訊」連結，讓產品中的使用者可以找到您的清單，並取得額外資訊。
