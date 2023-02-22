---
title: 為擴充功能建立Exchange清單
description: 了解如何將您的擴充功能新增至Adobe Experience Platform中的公開目錄。
exl-id: 0395fc99-5e2b-46d6-a067-f8f167733e02
source-git-commit: fcc586034317fb31122721fa9754b580c761a1da
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 24%

---

# 為擴充功能建立Exchange清單

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

Adobe Experience Platform有單一統一目錄，供使用者檢視可供安裝的標籤擴充功能。 此目錄可在產品中使用，並包含三種類型的擴充功能：

1. **公用擴充功能**:這些是完整的擴充功能，專為任何使用者生產而設計。
1. **私人擴充功能**:這些是專為生產環境而設計的完整擴充功能，但是由公司中的其他使用者開發，且僅供公司內的使用者使用。
1. **開發擴充功能**:這些擴充功能處於作用中開發狀態，僅可在您的公司內使用，且僅可在指定為開發屬性的屬性上使用。

除了產品目錄中的擴充功能，公開擴充功能也會在 [Experience CloudExchange應用程式市集](https://exchange.adobe.com/apps/browse/ec).

這些清單可讓擴充功能開發人員發佈功能說明、提供其他支援和檔案的連結，以及將擴充功能行銷給可能不了解您公司或擴充功能的潛在使用者。 在此Marketplace中，您的擴充功能會有公開清單可供檢視，且使用者不需要通過Platform驗證。 對於公開擴充功能，建立此Exchange清單是必要步驟。

>[!TIP]
>
>當您的Exchange清單發佈時，會自動將連結新增至清單內容，讓您的客戶和潛在客戶可點按和 `Connect with publisher` 以取得有關您的產品和服務的詳細資訊。 您的聯繫人電子郵件地址未顯示，因為這些郵件將由Exchange系統轉發給您。

如果您沒有公司可上傳和測試您的擴充功能套件，您應註冊Exchange計畫並開始列出。 這會觸發公司帳戶的建立（這需要一些時間，當完成時您會收到電子郵件），您可以用來上傳和測試您的擴充功能。 同樣地，Exchange清單僅對於公開擴充功能是必要的。

如果您已有公司帳戶，或您不需要Exchange清單（僅限私人擴充功能），則可略過此步驟的其餘部分，然後繼續 [上傳和測試您的擴充功能](./upload-and-test.md).

## 建立清單

>[!NOTE]
>
>以下流程詳細說明了在Adobe交換程式中建立應用程式清單的過程。 這是用於Adobe Experience Platform中各種整合和擴充功能的辭彙。

![Experience CloudApp Manager連結位置](../images/getting-started/app-mgr-link.png)

1. 登入 [Exchange 合作夥伴網站](https://partners.adobe.com/tw/exchangeprogram/experiencecloud)。登入後，選取 **App Manager** 連結至您的名稱旁。
1. 選取 **建立新應用程式** ，然後選取 **建立新應用程式** ，或選取適用的範本。
1. 提供您的清單資訊。如需App Manager的詳細資訊，請查看完整 [文章](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931). 清單資訊應清楚說明擴充功能的用途及其用途。 清單可作為應用程式的行銷空間。 使用清楚的說明、網站登陸頁面的連結、說明檔案的連結或支援電子郵件地址等，在這裡促銷您的擴充功能。 雖然擴充功能檢視的空間有限，但Exchange清單仍提供機會，可推廣您的擴充功能和公司。 以下是改善擴充功能的建議：
   - **應用程式圖示**  — 確保Exchange清單的表徵圖具有適當尺寸；png請使用512 x 512,jpg請使用1:1外觀比例。

      >[!NOTE]
      >
      >這是與您在擴充功能程式碼中使用的檔案格式不同。 擴充功能本身將包含 svg 檔案作為[圖示](../manifest.md)。

   - **精選影像**  — 使用可獨立顯示您的品牌並突顯應用程式的影像，吸引注意。 「精選影像」是當某人分享您的Exchange清單連結或在社交媒體上發佈相關貼文時顯示的影像。 因此，它必須是您品牌的模型表示。
   - **App Publisher 的標誌** - 這是您的公司標誌，請確保圖示具有適當尺寸；png 格式請使用 1280 x 720，jpg 格式請使用 2560 x 1440 (16:9)。
   - **設定指示**  — 通知客戶如何設定您的Adobe Experience Platform擴充功能。 請確定他們了解任何必要的設定，以及您 [組態檢視](../configuration.md) 在屬性中安裝您的擴充功能後，立即顯示。
   - **標記** - 在編輯清單的第一個頁面上，請務必在「自訂標記」欄位中加入 &quot;Launch&quot; 這個字。這樣，您的清單就會顯示在Exchange市集中標籤的搜尋中：
      ![](../images/getting-started/custom-tags.jpg)
   - **沙箱**  — 您需透過沙箱帳戶存取「Adobe解決方案」，即可在其中存取完整運作的Adobe Experience Platform版本。 您會在建立應用程式清單時要求這些沙箱帳戶。在 **連線** 區段選取您建立的應用程式（您的標籤擴充功能）以及您點擊時適用的特定連線 **儲存**，則會視需要產生沙箱要求。
1. 提交您的清單。 Adobe Exchange 團隊將審閱您的應用程式，並在需要更新時提供意見回應。如果您將 **立即發佈** 核取方塊，清單會在您提交時立即發佈，經核准。 如果您想稍後發佈應用程式，請取消勾選核取方塊。當您的擴充功能清單獲核準時，會顯示藍色 **發佈** 按鈕會顯示在您的應用程式（擴充功能）清單頁面上。

### 建立有效的清單

請看 [應用程式提交指導方針](https://partners.adobe.com/tw/exchangeprogram/experiencecloud/build/ec-exchange.html) 以取得如何建立最吸引人清單的詳細資訊。

#### 提交您的 Exchange 清單後

提交之後，Adobe Exchange 團隊將審閱應用程式，然後核准應用程式，或回覆指出可能需要的修改。此程序在應用程式提交指導方針中有詳細說明。

如果您無法登入 Exchange 網站，請依照[計畫註冊指南](https://partners.adobe.com/tw/content/mcp/us/en/home/reg-guide.html)中的指示，確定您的電子郵件已註冊到 Exchange 計畫中。每位使用者必須將其電子郵件與其公司的合作夥伴帳戶建立關聯。 有關此程式的問題可透過電子郵件傳送至 <ExchangeHelpEC@adobe.com>.

#### 在通過初審後更新 Exchange 清單

如果您需更新擴充功能，或只需要更新 Exchange 清單，請登入[合作夥伴入口網站](https://partners.adobe.com/tw/exchangeprogram/experiencecloud)，然後選取您名稱旁邊的 App Manager 按鈕。接著，請選取您的應用程式，並依照初次用來建立清單的前述流程操作。重新提交後，Adobe Exchange 團隊將審閱變更，然後核准變更，或回覆指出可能需要的修改。

## 將您的擴充功能套件連結至清單

在您的清單獲得核准並可供公開後，我們建議您提供以下項目的公開清單連結： `exchange_url` 欄位 `extension.json` 檔案。  這會在標籤擴充功能目錄中建立「更多資訊」連結，讓產品中的使用者可以找到您的清單，並取得額外資訊。
