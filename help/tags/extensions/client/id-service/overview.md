---
title: Adobe Experience Cloud Identity Service擴充功能概觀
description: 瞭解Adobe Experience Platform中的Adobe Experience Cloud Identity Service標籤擴充功能。
exl-id: 9bfcb666-a3f1-46ad-8678-2c63738da2b2
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 81%

---

# Adobe Experience Cloud Identity Service擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

請使用此參考資料來瞭解有關設定Adobe Experience Cloud ID擴充功能的資訊，以及使用此擴充功能建立規則時可用的選項。

使用此擴充功能整合 Experience Cloud Identity 服務與您的屬性。使用 Experience Cloud Identity 服務，您可以為網站訪客建立並儲存唯一的永久性識別碼。

## 設定 Experience Cloud ID 擴充功能

本節提供設定 Experience Cloud ID 擴充功能時可用選項的參考資料。

如果尚未安裝Experience CloudID擴充功能，請開啟您的屬性，然後選取「 」 **[!UICONTROL 擴充功能>目錄]**，將游標暫留在Experience CloudID擴充功能上，然後選取「 」 **[!UICONTROL 安裝]**.

若要設定擴充功能，請開啟「擴充功能」標籤、將游標暫留在擴充功能上方，然後選取「 」 **[!UICONTROL 設定]**.

![](../../../images/optin.jpg)

下列組態選項可供使用：

### Experience Cloud 組織 ID

您 Experience Cloud 組織的 ID。

此 ID 是 24 個字元的英數字串，後面接著 `@AdobeOrg`。如果您不認得此 ID，請連絡客戶服務。

### 排除特定路徑

如果 URL 符合任何指定的路徑，則 Experience Cloud ID 不會載入。

(選用) 若這是規則運算式，請啟用 Regex。

選取 **[!UICONTROL 新增]** 以排除其他路徑。

### 加入宣告

「加入宣告」選項可決定是否要求訪客在您的網站上同意使用 Adobe 服務，包括是否要建立追蹤訪客活動的 Cookie。

「加入宣告」是所有平台解決方案用戶端程式庫的集中式參考點，能決定訪客瀏覽您的網站時，系統能否在使用者的裝置或瀏覽器上建立 Cookie。「加入宣告」不支援收集或儲存使用者的同意偏好設定。

**要啟用「加入宣告」功能嗎？**

選取的選項會決定網站是否等待訪客同意，以追蹤訪客在您網站上的活動。

共有 3 個選項：

* **否：**&#x200B;不等待訪客同意網站追蹤其活動。如果您未選取任何選項，此為預設行為。
* **是：**&#x200B;等待訪客同意網站追蹤其活動。
* **使用函數在執行階段中判斷：**&#x200B;利用程式在執行階段中判斷值是 true 或 false。如果您選取此選項，則可使用「選取資料元素」欄位。選取可指定是否等待訪客同意的資料元素。此資料元素會解析為布林值。例如，您可以選取資料元素，根據訪客是否位於歐盟國家/地區來提供加入宣告選項。

**是否啟用「加入宣告儲存」？**

如果您啟用此功能，使用者的同意宣告會儲存至您網域的第一方 Cookie。如果您未啟用此功能，同意設定會保留在您的 CMP 或您管理的 Cookie 中。

**「加入宣告」Cookie 網域？**

這項選用設定可指定在啟用儲存功能的情況下，系統儲存「加入宣告」Cookie 的網域。您可以輸入網域，或選取包含網域的資料元素。

**「加入宣告儲存」的到期日？**

指定在啟用儲存功能的情況下，「加入宣告」Cookie 的到期時間 (以秒為單位)。

輸入數字，然後從下拉式清單中選取時間單位，例如，輸入2並選取 **[!UICONTROL 周]**. 預設值為 13 個月。

**權限？**

將先前的同意宣告傳送至「加入宣告」程式庫。選取包含同意宣告的資料元素。元素類型必須是物件或 JSON 字串。覆寫「加入宣告預先核准」。

範例：

`"{"aa":true,"aam":true,"ecid":true}"`

**加入宣告預先核准？**

定義訪客未設定偏好設定時，要核准或拒絕的類別。從載入頁面的當下開始，系統會假定選取的解決方案為同意。元素類型必須是物件或 JSON 字串 (範例：`{aam: true}`)。

### 變數

將名稱值配對設定為 Experience Cloud ID 例項屬性。使用下拉式選單選取變數，然後輸入或選取值。如需各個變數的相關資訊，請參閱 [Experience CloudIdentity Service檔案](https://experiencecloud.adobe.com/resources/help/zh_TW/mcvid/mcvid-overview.html).

## Experience Cloud ID 擴充功能動作類型

本節說明 Experience Cloud ID 擴充功能中可用的動作類型。

### 動作類型

#### 設定客戶 ID

設定一或多個客戶 ID。

1. 輸入整合代碼。

   整合程式碼應該包含在 Audience Manager 或客戶屬性中設定為資料來源的值。

1. 選取值。

   此值應為使用者 ID。資料元素最適合用於動態值，例如來自用戶端專屬內部系統的 ID。

1. 選取驗證狀態。

   可選擇下列選項：

   * 未知
   * 已驗證
   * 已登出

1. （選用）選取 **[!UICONTROL 新增]** 以設定更多客戶ID。
1. 選取&#x200B;**[!UICONTROL 「保留變更」]**。
