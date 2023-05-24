---
title: 為擴展建立Exchange清單
description: 瞭解如何將擴展添加到Adobe Experience Platform的公共目錄中。
exl-id: 0395fc99-5e2b-46d6-a067-f8f167733e02
source-git-commit: fcc586034317fb31122721fa9754b580c761a1da
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 24%

---

# 建立擴展的交換清單

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

Adobe Experience Platform有一個統一目錄，用戶可以在該目錄中查看可安裝的標籤擴展。 此目錄在產品中可用，包含三種類型的擴展：

1. **公共擴展**:這些擴展是為任何用戶生產而設計的。
1. **專用擴展**:這些是為生產而設計的已完成擴展，但是由您公司中的其他用戶開發的，並且僅適用於您公司中的用戶。
1. **開發擴展**:這些擴展正在積極開發中，僅在您公司內可用，並且僅在特定指定為「開發」屬性的屬性上可用。

除了產品目錄中的擴展，公共擴展還在 [Experience CloudExchange應用市場](https://exchange.adobe.com/apps/browse/ec)。

這些清單使擴展開發人員能夠發佈功能說明、提供指向其他支援和文檔的連結，以及向可能不瞭解您的公司或擴展功能的潛在用戶進行市場擴展。 在此市場中，您的分機將有一個公共清單，該清單可在用戶未通過平台身份驗證的情況下查看。 對於公共擴展，建立此Exchange清單是必需步驟。

>[!TIP]
>
>發佈Exchange清單時，會自動將連結添加到清單內容中，使您的客戶和潛在客戶能夠按一下並 `Connect with publisher` 的子菜單。 您的聯繫人電子郵件地址不顯示，因為這些郵件將由Exchange系統轉發給您。

如果您沒有公司可以上傳和test您的分機包，則應註冊Exchange程式並開始清單。 這將觸發建立公司帳戶（需要一段時間，完成後您將收到一封電子郵件），您可以使用該帳戶上載和test擴展。 同樣，只有公共擴展才需要Exchange清單。

如果您已經擁有公司帳戶，或者您不需要Exchange清單（僅限私人分機），則可以跳過此步驟的其餘部分，繼續 [上傳並測試擴展](./upload-and-test.md)。

## 建立清單

>[!NOTE]
>
>以下過程詳細說明了在AdobeExchange程式中建立應用程式清單的過程。 這是用於Adobe Experience Platform各種整合和擴展的術語。

![Experience CloudApp Manager連結位置](../images/getting-started/app-mgr-link.png)

1. 登入 [Exchange 合作夥伴網站](https://partners.adobe.com/tw/exchangeprogram/experiencecloud)。登錄後，選擇 **應用程式管理器** 連結。
1. 選擇 **建立新應用程式** ，然後選擇 **建立新應用** 或選擇適用的模板。
1. 提供您的清單資訊。有關App Manager的詳細資訊，請簽出完整 [文章](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931)。 列出資訊應非常清楚擴展功能的作用，以及擴展功能的用處。 清單用作您的應用的營銷空間。 使用清晰的說明、到站點登錄頁的連結、幫助文檔或支援電子郵件地址的連結等，在此處升級您的分機。 儘管擴展視圖中的空間有限，但Exchange清單仍提供了推廣您的擴展和公司的機會。 以下是改進推廣工作的建議：
   - **應用表徵圖**  — 確保Exchange清單的表徵圖具有適當的尺寸（png為512 x 512）或jpg為1:1縱橫比。

      >[!NOTE]
      >
      >這是與擴展代碼中使用的檔案格式不同的檔案格式。 擴充功能本身將包含 svg 檔案作為[圖示](../manifest.md)。

   - **特色影像**  — 使用可獨立顯示並顯示您的品牌和突出顯示您的應用程式的影像，以獲得關注。 「特色圖片」是指某人共用Exchange清單連結或在社交媒體上發佈有關該清單的連結時顯示的圖片。 因此，它需要成為您品牌的模型表示。
   - **App Publisher 的標誌** - 這是您的公司標誌，請確保圖示具有適當尺寸；png 格式請使用 1280 x 720，jpg 格式請使用 2560 x 1440 (16:9)。
   - **配置說明**  — 告知客戶如何配置您的Adobe Experience Platform分機。 確保在您的 [配置視圖](../configuration.md) 在屬性中安裝擴展後立即顯示。
   - **標記** - 在編輯清單的第一個頁面上，請務必在「自訂標記」欄位中加入 &quot;Launch&quot; 這個字。這將使您的清單顯示在Exchange市場中的標籤搜索中：
      ![](../images/getting-started/custom-tags.jpg)
   - **沙箱**  — 您通過沙盒帳戶訪問Adobe解決方案，在沙盒帳戶中，您可以訪問完全正常運行的Adobe Experience Platform版本。 您會在建立應用程式清單時要求這些沙箱帳戶。在 **連接** 部分選擇適用於您建立的應用程式（標籤擴展）的特定連接，以及 **保存**，如果需要，將生成沙盒請求。
1. 提交清單。 Adobe Exchange 團隊將審閱您的應用程式，並在需要更新時提供意見回應。如果標籤 **立即發佈** 複選框，在您提交清單時，該清單將在批准後立即發佈。 如果以後要發佈應用程式，請不選中該複選框。當您的分機清單被批准時，藍色 **發佈** 按鈕將出現在您的應用（擴展）清單頁面中。

### 建立有效的清單

請看 [應用程式提交准則](https://partners.adobe.com/tw/exchangeprogram/experiencecloud/build/ec-exchange.html) 有關如何建立最吸引人的清單的詳細資訊。

#### 提交您的 Exchange 清單後

提交之後，Adobe Exchange 團隊將審閱應用程式，然後核准應用程式，或回覆指出可能需要的修改。此程序在應用程式提交指導方針中有詳細說明。

如果您無法登入 Exchange 網站，請依照[計畫註冊指南](https://partners.adobe.com/tw/content/mcp/us/en/home/reg-guide.html)中的指示，確定您的電子郵件已註冊到 Exchange 計畫中。每個用戶都必須將其電子郵件與公司的合作夥伴帳戶關聯。 有關此流程的問題可通過電子郵件發送給 <ExchangeHelpEC@adobe.com>。

#### 在通過初審後更新 Exchange 清單

如果您需更新擴充功能，或只需要更新 Exchange 清單，請登入[合作夥伴入口網站](https://partners.adobe.com/tw/exchangeprogram/experiencecloud)，然後選取您名稱旁邊的 App Manager 按鈕。接著，請選取您的應用程式，並依照初次用來建立清單的前述流程操作。重新提交後，Adobe Exchange 團隊將審閱變更，然後核准變更，或回覆指出可能需要的修改。

## 將擴展包連結到清單

在您的清單獲得批准並公開後，我們建議您提供以下連結： `exchange_url` 的 `extension.json` 檔案。  這將在標籤擴展目錄中建立「更多資訊」連結，以便產品中的用戶可以找到您的清單及其附加資訊。
