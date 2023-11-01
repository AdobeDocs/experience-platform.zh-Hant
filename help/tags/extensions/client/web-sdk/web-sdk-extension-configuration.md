---
title: 設定Web SDK標籤擴充功能
description: 瞭解如何在標籤UI中設定Experience Platform Web SDK標籤擴充功能。
exl-id: 22425daa-10bd-4f06-92de-dff9f48ef16e
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 10%

---

# 設定Web SDK標籤擴充功能

此 [!DNL Web SDK] 標籤擴充功能會透過Experience PlatformEdge Network，將資料從Web屬性傳送至Adobe Experience Cloud。

擴充功能可讓您將資料串流至Platform、同步身分、處理客戶同意訊號，以及自動收集內容資料。

本檔案說明如何在標籤UI中設定標籤擴充功能。

## 安裝Web SDK標籤擴充功能 {#install}

Web SDK標籤擴充功能需要安裝屬性。 如果您尚未這麼做，請參閱以下檔案： [建立標籤屬性](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

建立屬性後，請開啟屬性並選取 **[!UICONTROL 擴充功能]** 標籤。

選取 **[!UICONTROL 目錄]** 標籤。 從可用擴充功能的清單中，找到 [!DNL Web SDK] 擴充功能並選取 **[!UICONTROL 安裝]**.

![此影像顯示已選取Web SDK擴充功能的標籤UI](assets/web-sdk-install.png)

選取後 **[!UICONTROL 安裝]**，您必須設定Web SDK標籤擴充功能並儲存設定。

>[!NOTE]
>
>標籤擴充功能只會在儲存設定後安裝。 請參閱下一節以瞭解如何設定標籤擴充功能。

## 設定執行個體設定 {#general}

頁面頂端的設定選項可告知Adobe Experience Platform將資料路由到何處，以及要在伺服器上使用哪些設定。

![此影像顯示標籤UI中Web SDK標籤擴充功能的一般設定](assets/web-sdk-ext-general.png)

* **[!UICONTROL 名稱]**：Adobe Experience Platform Web SDK擴充功能支援頁面上的多個例項。 此名稱可用來透過標籤設定，將資料傳送至多個組織。 執行個體名稱預設為 `alloy`. 不過您可將例項名稱變更為任何有效的 JavaScript 物件名稱。
* **[!UICONTROL IMS組織ID]**：您要在Adobe傳送資料的組織ID。 大部分時間都會使用自動填入的預設值。 頁面上有多個例項時，請找到您要傳送資料的第二個組織，以該組織的值填入此欄位。
* **[!UICONTROL 邊緣網域]**：擴充功能傳送及接收資料的網域。 Adobe建議對此擴充功能使用第一方網域(CNAME)。 預設的第三方網域適用於開發環境，但不適用於生產環境。若需設定第一方 CNAME 的相關說明，請參閱[此處](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hant)。

## 設定資料流設定 {#datastreams}

此段落可讓您選取三個可用環境（生產、測試和開發）中每一個都應該使用的資料串流。

當請求傳送至Edge Network時，會使用資料串流ID來參考伺服器端設定。 您可以更新設定，而無須在網站上變更程式碼。

請參閱以下指南： [資料串流](../../../../datastreams/overview.md) 以瞭解如何設定資料串流。

您可以從可用的下拉式功能表中選擇資料串流，或選取 **[!UICONTROL 輸入值]** 並輸入每個環境的自訂資料串流ID。

![此影像顯示標籤UI中Web SDK標籤擴充功能的資料流設定](assets/web-sdk-ext-datastreams.png)

## 設定隱私權設定 {#privacy}

本節可讓您設定Web SDK如何處理來自您網站的使用者同意訊號。 具體來說，如果沒有提供其他明確的同意偏好設定，這可讓您選取使用者假設的預設同意等級。

預設同意層級不會儲存到使用者設定檔。

![此影像顯示標籤UI中Web SDK標籤擴充功能的隱私權設定](assets/web-sdk-ext-privacy.png)

| [!UICONTROL 預設同意層級] | 說明 |
| --- | --- |
| [!UICONTROL 在] | 收集在使用者提供同意偏好設定之前發生的事件。 |
| [!UICONTROL 輸出] | 捨棄在使用者提供同意偏好設定之前發生的事件。 |
| [!UICONTROL 擱置中] | 在使用者提供同意偏好設定之前發生的佇列事件。 提供同意偏好設定時，系統會根據提供的偏好設定收集或捨棄事件。 |
| [!UICONTROL 資料元素提供] | 預設同意層級是由您定義的個別資料元素所決定。 使用此選項時，您必須使用提供的下拉式選單指定資料元素。 |

>[!TIP]
>
>使用 **[!UICONTROL 輸出]** 或 **[!UICONTROL 擱置中]** 如果您的業務營運需要明確的使用者同意。

## 設定身分設定 {#identity}

本節可讓您定義Web SDK在處理使用者身分識別時的行為。

![此影像顯示標籤UI中Web SDK標籤擴充功能的身分設定](assets/web-sdk-ext-identity.png)

* **[!UICONTROL 從VisitorAPI移轉ECID]**：此選項預設為啟用。 啟用此功能後，SDK可讀取 `AMCV` 和 `s_ecid` Cookie並設定 `AMCV` 使用的Cookie [!DNL Visitor.js]. 移轉至Web SDK時，此功能很重要，因為有些頁面可能仍使用 [!DNL Visitor.js]. 此選項可讓SDK繼續使用相同程式碼 [!DNL ECID] 因此不會將使用者識別為兩個不同的使用者。
* **[!UICONTROL 使用第三方Cookie]**：啟用此選項後，Web SDK會嘗試將使用者識別碼儲存在第三方Cookie中。 如果成功，則會在使用者瀏覽多個網域時將其識別為單一使用者，而不是在每個網域上將其識別為個別使用者。 如果已啟用此選項，如果瀏覽器不支援第三方Cookie或使用者已設定不允許第三方Cookie，SDK仍可能無法將使用者識別碼儲存在第三方Cookie中。 在此情況下，SDK只會將識別碼儲存在第一方網域中。

## 設定個人化設定 {#personalization}

此區段可讓您設定在載入個人化內容時如何隱藏頁面的某些部分。

您可以在預先隱藏樣式編輯器中指定要隱藏的元素。 接著，您可以複製提供的預設預先隱藏程式碼片段，並將其貼到中 `<head>` 您網站的 [!DNL HTML] 程式碼。

![此影像顯示標籤UI中Web SDK標籤擴充功能的個人化設定](assets/web-sdk-ext-personalization.png)

* **[!UICONTROL 將Target從at.js移轉至Web SDK]**：使用此選項來啟用 [!DNL Web SDK] 以讀取及寫入舊版 `mbox` 和 `mboxEdgeCluster` at.js使用的Cookie `1.x` 或 `2.x` 程式庫。 這可協助您在從使用Web SDK的頁面移至使用at.js的頁面時，保留訪客設定檔 `1.x` 或 `2.x` 資料庫或反之。

## 設定資料收集設定 {#data-collection}

![此影像顯示標籤UI中Web SDK標籤擴充功能的資料收集設定](assets/web-sdk-ext-collection.png)

* **[!UICONTROL 回呼函式]**：擴充功能中提供的回呼函式也稱為 [`onBeforeEventSend` 函式](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=zh-Hant) 在程式庫中。 此函式可讓您在事件傳送至Edge Network之前，先全域修改事件。 如需如何使用此函式的詳細資訊，請參閱 [此處](../../../../edge/fundamentals/tracking-events.md#modifying-events-globally).
* **[!UICONTROL 啟用點選資料收集]**：Web SDK可以自動收集您的連結點選資訊。 依預設，此功能已啟用，但可使用此選項加以停用。 如果連結包含下列其中一個下載運算式，也會標示為下載連結： [!UICONTROL 下載連結限定詞] 文字方塊。 Adobe提供您一些預設的下載連結限定詞。 您可以視需要加以編輯。
* **[!UICONTROL 自動收集的內容資料]**：依預設，Web SDK會收集關於裝置、Web、環境和地標內容的特定內容資料。 如果您想檢視Adobe收集的資訊清單，可以找到 [此處](../../../../edge/data-collection/automatic-information.md). 如果您不想要收集這些資料，或只想要收集某些類別的資料，請選取「 」 **[!UICONTROL 特定內容資訊]** 並選取您要收集的資料。

## 設定資料流覆寫 {#datastream-overrides}

資料流覆寫可讓您定義資料流的額外設定，這些設定會透過 Web SDK 傳遞到 Edge Network。

這可協助您觸發和預設行為不同的資料流行為，且無須建立新的資料流或修改現有設定。

資料流設定覆寫的流程包含兩個步驟：

1. 首先，您必須在[資料流設定頁面](../../../../datastreams/configure.md)中定義您的資料流設定覆寫。
2. 接著，您必須透過 Web SDK 命令或使用 Web SDK 標記擴充功能將覆寫傳送至 Edge Network。

檢視資料流 [設定覆寫檔案](../../../../datastreams/overrides.md) 以取得有關如何覆寫資料流設定的詳細說明。

除了透過Web SDK命令傳遞覆寫之外，您也可以在下面顯示的標籤擴充功能畫面中設定覆寫。

>[!IMPORTANT]
>
> 資料流覆寫必須根據環境進行設定。 開發、測試和生產環境都有不同的覆寫。 您可以使用下方畫面中顯示的專用選項，複製設定值。

![此影像顯示Web SDK標籤擴充功能頁面中的資料流設定覆寫。](assets/datastream-overrides.png)

## 設定進階設定

使用 **[!UICONTROL 邊緣基底路徑]** 欄位。 這應該不需要更新，但在您參與Beta或Alpha的情況下，Adobe可能會要求您變更此欄位。

![此影像顯示Web SDK標籤擴充功能頁面中的進階設定。](assets/advanced-settings.png)
