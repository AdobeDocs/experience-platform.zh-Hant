---
title: LiveRamp — 散發連線
description: 瞭解如何使用LiveRamp - Distribution聯結器將先前上線到LiveRamp的受眾啟用到其他廣告目的地。
hide: true
hidefromtoc: true
source-git-commit: 324f662dcc9718df6c81c47874c6b30235a74601
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 40%

---


# [!DNL LiveRamp - Distribution] 連線 {#liveramp-onboarding}

此 [!DNL LiveRamp - Distribution] 連線可讓您在行動裝置、網路、顯示和連線的電視媒體中，啟用從Experience Platform到高階發佈者的對象。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由LiveRamp建立和維護。 如有任何查詢或更新要求，請直接連絡LiveRamp [此處](mailto:example@email.com).

## 支援的目的地 {#supported-destinations}

[!DNL LiveRamp - Distribution] 目前支援對下列平台進行對象啟用：

* [!DNL 4C Insights]
* [!DNL Acast]
* [!DNL Amobee]
* [!DNL Ampersand.tv]
* [!DNL Captify]
* [!DNL Cardlytics]
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [!DNL iHeartMedia]
* [!DNL Index Exchange]
* [!DNL Magnite CTV Platform]
* [!DNL Magnite DV+ (Rubicon Project)]
* [!DNL One Fox]
* [!DNL Pandora]
* [!DNL Reddit]
* [[!DNL Roku]](#roku)
* [!DNL Spotify]
* [!DNL Taboola]
* [!DNL TargetSpot]
* [!DNL Teads]
* [!DNL WB Discovery]

## 使用案例 {#use-cases}

為了協助您更清楚瞭解您應如何及何時使用 [!DNL LiveRamp - Distribution] 目的地，以下是Adobe Experience Platform客戶可以使用此目的地解決的範例使用案例。

運動服裝零售商的行銷團隊使用 [LiveRamp — 入門](liveramp-onboarding.md) 將對象從Experience Platform傳送至其LiveRamp帳戶的連線。

透過 [!DNL LiveRamp - Distribution] 連線他們現在可以觸發將已上線對象啟動至本頁面頂端提及的目的地，因此可將目標定位為行動裝置、開放網頁、社交和網路上的使用者， [!DNL CTV] 平台。

## 將對象上線到LiveRamp {#onboarding}

在透過啟用對象之前 [!DNL LiveRamp - Distribution] 連線，使用 [LiveRamp — 入門](liveramp-onboarding.md) 將您的Experience Platform對象匯出至LiveRamp的連線。

將對象上線至LiveRamp後，請從繼續啟動工作流程。 [連線到目的地](#connect) 步驟。

## 連線到目的地 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_identifier_settings"
>title="識別碼設定"
>abstract="選取您的目標所支援的識別碼。有關每個目標所支援的識別碼完整清單，請參閱本文件。"

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證LiveRamp {#authenticate}

若要向目的地進行驗證，請填寫必填欄位並選取 **[!UICONTROL 連線到目的地]**.

![顯示目的地連線畫面的Platform UI影像。l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-new-connection.png)

* **[!UICONTROL 權杖URL]**：您的LiveRamp權杖URL。
* **[!UICONTROL LiveRamp組織ID]**：您的LiveRamp帳戶的組織ID。
* **[!UICONTROL 使用者名稱]**：您的LiveRamp帳戶使用者名稱。
* **[!UICONTROL 密碼]**：您的LiveRamp帳戶密碼。

### 設定目的地詳細資料 {#destination-details}

成功連線至您的LiveRamp帳戶後，請輸入連線至您要啟用對象的目標所需的資訊。

![顯示目的地詳細資訊畫面的Platform UI影像。l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-destination-details.png)

* **[!UICONTROL 名稱]**：填寫目的地連線的偏好名稱。
* **[!UICONTROL 說明]**：輸入目的地的說明。 使用說明來協助您輕鬆識別此目的地的用途。
* **[!UICONTROL 目的地]**：使用下拉式功能表選取您要啟用對象的目的地。 您在這裡選取的目的地，會直接影響您在 [目的地特定設定](#destination-settings) 畫面。
* **[!UICONTROL 整合]**：選取您要用於目的地的整合帳戶。
* **[!UICONTROL 識別碼]**：選取目的地支援的識別碼。 目前，下拉式功能表中已預先填入所有目的地支援的識別碼。

## 目的地特定設定 {#destination-settings}

每個目的地 [支援](#supported-destinations) 作者： [!DNL LiveRamp - Onboarding] 需要您填寫特定的組態選項。

如需如何設定每個目的地的詳細指引，請參閱以下各節。

### [!DNL 4C Insights] {#insights}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_4cinsights_profile_id"
>title="4C 品牌設定檔 ID"
>abstract="輸入與您的 4C 品牌設定檔相關的數值 ID。如果您沒有此 ID，請聯絡您的 4C 用戶端服務代表。"

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

### [!DNL Acast] {#acast}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_acast_client"
>title="用戶端名稱"
>abstract="依您希望對目標合作夥伴顯示的廣告商帳戶名稱。使用您的公司名稱。請勿使用空格或特殊字元。"

### [!DNL Amobee] {#amobee}

### [!DNL Ampersand.tv] {#ampersand-tv}

### [!DNL Captify] {#captify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_captify_client"
>title="用戶端名稱"
>abstract="依您希望對目標合作夥伴顯示的廣告商帳戶名稱。使用您的公司名稱。請勿使用空格或特殊字元。"

### [!DNL Cardlytics] {#cardlytics}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_cardlytics_client"
>title="用戶端名稱"
>abstract="依您希望對目標合作夥伴顯示的廣告商帳戶名稱。使用您的公司名稱。請勿使用空格或特殊字元。"

### [!DNL Disney (Hulu/ESPN/ABC)] {#disney}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_agreement"
>title="廣告商資料目標條款合約"
>abstract="輸入 `I AGREE` 確認 Disney 廣告商資料條款的認可與合約。"

<!-- 
>additional-url="https://www.disneyadvertising.com/ADVERTISER-DATA-DESTINATION-TERMS/" text="Read the agreement" -->

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_client"
>title="用戶端名稱"
>abstract="依您希望對目標合作夥伴顯示的廣告商帳戶名稱。使用您的公司名稱。請勿使用空格或特殊字元。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_email"
>title="您的電子郵件地址"
>abstract="輸入與個人相連結的電子郵件地址。該電子郵件地址做為廣告商資料條款合約的簽名。必要時，也會使用該電子郵件地址與您聯絡。"

若要設定目的地的詳細資料，請填寫下列欄位。

![平台UI影像，其中顯示Disney目的地的客戶資料欄位。](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-disney-fields.png)

* **[!UICONTROL 廣告商資料目的地條款合約]**：輸入 `I AGREE` 確認對迪士尼廣告商資料條款的認可與同意。
* **[!UICONTROL 使用者端名稱]**：輸入您要向目的地合作夥伴顯示的公司名稱。
* **[!UICONTROL 電子郵件地址]**：輸入繫結至個人的電子郵件地址。 該電子郵件地址做為廣告商資料條款合約的簽名。

### [!DNL iHeartMedia] {#iheartmedia}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_iheartmedia_client"
>title="用戶端名稱"
>abstract="依您希望對目標合作夥伴顯示的廣告商帳戶名稱。使用您的公司名稱。請勿使用空格或特殊字元。"

### [!DNL Index Exchange] {#index-exchange}

### [!DNL Magnite CTV Platform] {#magnite}

### [!DNL Magnite DV+ (Rubicon Project)] {#magnite-dv}

### [!DNL One Fox] {#fox}

### [!DNL Pandora] {#pandora}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_data_provider_name"
>title="資料提供者名稱"
>abstract="您希望對 Pandora 顯示的公司名稱。該名稱最多可以包含 40 個小寫字母和英數字元 (例如 My_Company)。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_rep_email"
>title="客戶代表電子郵件地址"
>abstract="Pandora 客戶代表的電子郵件地址。該地址用於傳送類型更新。若要輸入多個地址，請用逗號分隔。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_email"
>title="電子郵件地址"
>abstract="該地址用於傳送類型更新。若要輸入多個地址，請用逗號分隔。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_account_name"
>title="帳戶名稱"
>abstract="您的 Pandora 帳戶名稱。如果不確定您的帳戶名稱是什麼，請聯絡您的 Pandora 客戶代表。請勿使用空格或特殊字元。"

### [!DNL Reddit] {#reddit}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_id"
>title="Reddit 廣告商 ID"
>abstract="您的 Reddit 廣告商 ID。必須以「t2_」或「a2_」開頭。如果您不知道自己的廣告商 ID，請聯絡您的 Reddit 代表。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_name"
>title="Reddit 廣告商名稱"
>abstract="您的 Reddit 廣告商名稱。請勿使用空格或特殊字元。"

### Roku {#roku}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_email"
>title="Roku 帳戶電子郵件地址"
>abstract="輸入與您的 Roku 帳戶相連結的電子郵件地址。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_representative_email"
>title="Roku 客戶代表電子郵件地址"
>abstract="輸入您的 Roku 客戶代表的電子郵件地址。該地址用於傳送類型更新。若要輸入多個地址，請用逗號分隔。"

若要設定目的地的詳細資料，請填寫下列欄位。

![顯示Roku目的地支援之識別碼的平台UI影像。](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-roku-fields.png)

* **[!UICONTROL Roku帳戶電子郵件地址]**：輸入與您的Roku帳戶相關聯的電子郵件地址。
* **[!UICONTROL Roku客戶代表電子郵件地址]**：輸入您Roku客戶代表的電子郵件地址。 若要輸入多個地址，請用逗號分隔。

### [!DNL Spotify] {#spotify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_client"
>title="用戶端名稱"
>abstract="依您希望對目標合作夥伴顯示的廣告商帳戶名稱。使用您的公司名稱。請勿使用空格或特殊字元。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_account_token"
>title="帳戶語彙基元"
>abstract="通知 Spotify 連結資料之處，以及通過驗證可使用此工作流程的一個英數標別碼。請聯絡您的 Spotify 客戶經理以取得此語彙基元。"

### [!DNL Taboola] {#taboola}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_rep_email"
>title="客戶經理電子郵件地址"
>abstract="您的 Taboola 客戶經理的電子郵件地址。"

### [!DNL TargetSpot] {#targetspot}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_targetspot_client"
>title="用戶端名稱"
>abstract="依您希望對目標合作夥伴顯示的廣告商帳戶名稱。使用您的公司名稱。請勿使用空格或特殊字元。"

### [!DNL Teads] {#teads}

### [!DNL WB Discovery] {#wb-discovery}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_wb_client"
>title="用戶端名稱"
>abstract="依您希望對目標合作夥伴顯示的廣告商帳戶名稱。使用您的公司名稱。請勿使用空格或特殊字元。"

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需有關警示的詳細資訊，請閱讀以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟用此目的地的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

此 [!DNL LiveRamp - Distribution] 連線會啟用已透過上線至您LiveRamp帳戶的對象。 [LiveRamp — 入門](liveramp-onboarding.md) 連線。

若要成功啟用您的對象，在此步驟中，您必須選取 **相同對象** 您之前已上線到LiveRamp的檔案。

>[!IMPORTANT]
>
>選取先前未上線至LiveRamp的受眾，不會觸發新受眾的上線。

## 匯出的資料/驗證資料匯出 {#exported-data}

若要驗證及監控對象的啟用情況，請登入您的LiveRamp帳戶並檢查啟用量度。

如果您對受眾啟用有任何疑問，請聯絡您的LiveRamp客戶代表。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，讀取 [資料控管概觀](/help/data-governance/home.md).

## 其他資源 {#additional-resources}

如需如何設定 [!DNL LiveRamp - Onboarding] 儲存，請參閱 [正式檔案](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
