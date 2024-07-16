---
title: 為擴充功能建立Exchange清單
description: 瞭解如何將擴充功能新增至Adobe Experience Platform中的公開目錄。
exl-id: 0395fc99-5e2b-46d6-a067-f8f167733e02
source-git-commit: fcc586034317fb31122721fa9754b580c761a1da
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 20%

---

# 為擴充功能建立Exchange清單

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../term-updates.md)，以取得術語變更的彙總參考資料。

Adobe Experience Platform有一個統一的目錄，使用者可以在其中檢視可用於安裝的標籤擴充功能。 此目錄可在產品中使用，並包含三種型別的擴充功能：

1. **公用擴充功能**：這些是專為任何使用者生產使用而設計的完整擴充功能。
1. **私人擴充功能**：這些是專為生產而設計的完整擴充功能，但由貴公司中的其他使用者開發，僅供貴公司內的使用者使用。
1. **開發擴充功能**：這些擴充功能正在開發中，只能在貴公司內使用，而且只能在特別指定為開發屬性的屬性上使用。

除了產品目錄中的擴充功能之外，公用擴充功能也會在[Experience CloudExchange應用程式市集](https://exchange.adobe.com/apps/browse/ec)中列出專案。

這些清單可讓擴充功能開發人員張貼功能說明、提供其他支援和檔案的連結，以及將擴充功能行銷給可能還不熟悉您的公司或擴充功能的潛在使用者。 在此Marketplace中，您的擴充功能將有公開清單可供檢視，且使用者不需經過Platform驗證。 對於公開擴充功能，建立此Exchange清單是必要步驟。

>[!TIP]
>
>發佈Exchange清單時，系統會自動將連結新增至清單內容，讓您的客戶和潛在客戶可以按一下「 」和「`Connect with publisher`」，以取得有關您產品和服務的詳細資訊。 不會顯示您的連絡人電子郵件地址，因為這些訊息會由Exchange系統轉寄給您。

若沒有公司可上傳及測試您的擴充功能套件，您應註冊Exchange計畫並開始加入清單。 這將觸發公司帳戶的建立（需要一些時間，完成後，您會收到一封電子郵件），您可將其用於上傳和測試擴充功能。 同樣地，Exchange清單只適用於公開擴充功能。

如果您已有公司帳戶，或您不需要Exchange清單（僅限私人擴充功能），您可以略過此步驟的其餘部分，並繼續[上傳及測試您的擴充功能](./upload-and-test.md)。

## 建立清單

>[!NOTE]
>
>下列程式詳細說明如何在Adobe Exchange程式中建立應用程式清單。 這是Adobe Experience Platform中各種整合和擴充功能的用語。

![Experience Cloud應用程式管理員連結位置](../images/getting-started/app-mgr-link.png)

1. 登入 [Exchange 合作夥伴網站](https://partners.adobe.com/tw/exchangeprogram/experiencecloud)。登入後，選取您名稱旁邊的&#x200B;**應用程式管理員**&#x200B;連結。
1. 選取&#x200B;**建立新應用程式**&#x200B;索引標籤，然後為自訂解決方案選取&#x200B;**建立新應用程式**，或選取適用的範本。
1. 提供您的清單資訊。如需App Manager的詳細資訊，請參閱完整的[文章](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931)。 清單資訊應清楚說明擴充功能的功用及其功用。 清單可作為您應用程式的行銷空間。 透過清楚的說明、網站登陸頁面的連結、說明檔案的連結或支援電子郵件地址等，在這裡推廣您的擴充功能。 雖然擴充功能檢視的空間有限，但Exchange清單仍提供機會，可同時推廣您的擴充功能和公司。 以下是改善擴充功能促銷活動的建議：
   - **應用程式圖示** — 請確定Exchange清單的圖示具有適當尺寸；png請使用512 x 512，jpg請使用1:1外觀比例。
     >[!NOTE]
     >
     >這是與擴充功能程式碼所用不同的檔案格式。 擴充功能本身將包含 svg 檔案作為[圖示](../manifest.md)。

   - **精選影像** — 使用可獨立顯示您的品牌並突顯您的應用程式的影像，以吸引您的注意。 「精選影像」是當某人分享您的Exchange清單連結或在社群媒體上發佈相關文章時所顯示的影像。 因此，它必須是您品牌的模型表示法。
   - **App Publisher 的標誌** - 這是您的公司標誌，請確保圖示具有適當尺寸；png 格式請使用 1280 x 720，jpg 格式請使用 2560 x 1440 (16:9)。
   - **設定指示** — 告知客戶如何設定您的Adobe Experience Platform擴充功能。 請確定他們在屬性中安裝您的擴充功能後立即顯示您的[組態檢視](../configuration.md)時，瞭解所有必要的設定和後續步驟。
   - **標記** - 在編輯清單的第一個頁面上，請務必在「自訂標記」欄位中加入 &quot;Launch&quot; 這個字。這會使您的清單顯示在Exchange Marketplace的標籤搜尋中：
     ![](../images/getting-started/custom-tags.jpg)
   - **沙箱** — 您對Adobe解決方案的存取是透過沙箱帳戶進行，您可在此帳戶中存取完整功能版本的Adobe Experience Platform。 您會在建立應用程式清單時要求這些沙箱帳戶。在「**連線**」區段中，選取您所建立的應用程式（標籤延伸模組）適用的特定連線，當您點選「**儲存**」時，就會視需要產生沙箱要求。
1. 提交您的清單。 Adobe Exchange 團隊將審閱您的應用程式，並在需要更新時提供意見回應。如果您在提交清單時勾選了&#x200B;**立即發佈**&#x200B;核取方塊，則會在核准後立即發佈。 如果您希望稍後再發佈應用程式，請取消勾選核取方塊。 當您的擴充功能清單通過核準時，應用程式（擴充功能）清單頁面會在其旁邊顯示一個藍色的&#x200B;**Publish**&#x200B;按鈕。

### 建立有效的清單

請檢視[應用程式提交指導方針](https://partners.adobe.com/tw/exchangeprogram/experiencecloud/build/ec-exchange.html)，以取得有關如何建立最吸引人的清單的詳細資訊。

#### 提交您的 Exchange 清單後

提交之後，Adobe Exchange 團隊將審閱應用程式，然後核准應用程式，或回覆指出可能需要的修改。此程式在應用程式提交指導方針中有詳細說明。

如果您無法登入 Exchange 網站，請依照[計畫註冊指南](https://partners.adobe.com/tw/content/mcp/us/en/home/reg-guide.html)中的指示，確定您的電子郵件已註冊到 Exchange 計畫中。每位使用者都必須將其電子郵件與公司的合作夥伴帳戶建立關聯。 您可以透過電子郵件將此程式的問題導向至<ExchangeHelpEC@adobe.com>。

#### 在通過初審後更新 Exchange 清單

如果您需更新擴充功能，或只需要更新 Exchange 清單，請登入[合作夥伴入口網站](https://partners.adobe.com/tw/exchangeprogram/experiencecloud)，然後選取您名稱旁邊的 App Manager 按鈕。接著，請選取您的應用程式，並依照初次用來建立清單的前述流程操作。重新提交後，Adobe Exchange 團隊將審閱變更，然後核准變更，或回覆指出可能需要的修改。

## 將您的擴充功能套件連結至清單

您的清單獲得核准且可供公開使用後，建議您在擴充功能套件中，於`extension.json`檔案的`exchange_url`欄位中提供公開清單的連結。  這會在標籤擴充功能目錄中建立「更多資訊」連結，方便產品內的使用者找到您的清單及其額外資訊。
