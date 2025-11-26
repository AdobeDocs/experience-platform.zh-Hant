---
title: Acxiom Real ID受眾連線
description: 使用 [!DNL Acxiom Real ID Audience Connection] 目的地以 [!DNL Acxiom's Real ID] 技術增強受眾，並啟用多個平台的受眾，例如 [!DNL Altice]、 [!DNL Ampersand]、 [!DNL Comcast]等。
badge: label="Beta" type="Informative"
exl-id: 5f1f0f7f-ac46-42bd-8002-be50fab5a76b
source-git-commit: fda542e62c448788099d63951277278a146fdfc8
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 5%

---

# [!DNL Acxiom Real ID Audience Connection]目標

>[!NOTE]
>
>[!DNL Acxiom Real ID Audience Connection]目的地是測試版。 此目的地聯結器和檔案頁面是由[!DNL Acxiom]團隊建立和維護。 若有任何查詢或更新要求，請直接在[這裡](mailto:acxiom-adobe-help@acxiom.com)聯絡Acxiom。

使用 [!DNL Acxiom Real ID Audience Connection] 目標搭配 [!DNL Acxiom's][Real ID](https://www.acxiom.com/real-id/real-id/) 技術來強化客群，並在多個平台上 (例如 [!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast] 等) 啟用客群。

本教學課程提供使用[!DNL Acxiom Real ID Audience Connection]使用者介面建立[!DNL Adobe Experience Platform]目的地聯結器的指示。 此聯結器用於建立受眾，並將受眾發佈至選取的目的地。

## 使用案例 {#use-cases}

此聯結器支援將Acxiom真實身分識別作為識別碼載入到Real-Time CDP中的使用者端。 為協助您更清楚瞭解您應如何及何時使用[!DNL Acxiom Real ID Audience Connection]目的地，以下是[!DNL Adobe Experience Platform]客戶可以使用此聯結器解決的範例使用案例。

### 將對象從Experience Platform傳送至您的Acxiom帳戶 {#send-audiences}

如果您是行銷專業人員，想要將對象從[!DNL Experience Platform]傳送至您的[!DNL Acxiom]帳戶，以進行跨管道贏取，請使用此目的地聯結器。

例如，某個全球金融服務品牌的行銷營運部門對於透過多個廣告平台進行跨頻道客戶贏取感興趣。 他們可以使用[!DNL Acxiom Real ID Audience Connection]目的地聯結器將對象從[!DNL Experience Platform]傳送至[!DNL Acxiom]、使用[!DNL Acxiom's Real ID]技術增強對象，以及將對象啟用至多個平台，例如[!DNL Altice]、[!DNL Ampersand]、[!DNL Comcast]等。


## 先決條件 {#prerequisites}

* **確認使用條款：**&#x200B;您必須閱讀並簽署[!DNL Acxiom Real ID Audience Connection]使用條款合約，才能設定新的[!DNL Acxiom's]目的地。 執行銷售訂單完成後，您將會收到合約的連結。 在您簽署合約之前，不會在Experience Platform目的地目錄中看到[!DNL Acxiom Real ID Audience Connection]目的地卡片。 在您接受並簽署合約後，[!DNL Adobe]將完成您的上線程式，您將會看到[!DNL Acxiom Real ID Audience Connection]目的地卡。
* **知道您的Adobe組織識別碼：**&#x200B;需要您的[!DNL Adobe]組織識別碼才能完成您的使用者合約條款。 如需如何[!DNL Adobe's]檢視組織ID *的詳細資訊，請參閱Experience Cloud中的* [組織](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)主題。
* **取得[!DNL Acxiom's Real ID]產品的授權：**&#x200B;取得授權後，請在Real-Time CDP中提供Acxiom的真實ID。 如需詳細資訊，請參閱[Acxiom資料增強功能](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/data-partner/acxiom-data-enhancement)。


## 支援的身分 {#supported-identities}

[!DNL Acxiom's Real ID Audience Connection]目的地支援下表所述的身分啟用。 深入瞭解[身分](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/identity/features/namespaces)。

| 目標身分 | 說明 | 考量事項 |
|---------------|----------------|----------------|
| 真實ID | [!DNL Acxiom Real ID] | 當您的來源身分識別是Acxiom Real ID名稱空間時，請選取此目標身分。 |
| extern_id | 自訂使用者ID | 當您的來源身分是自訂名稱空間時，請選取此目標身分。 |

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------------|----------------|----------------|
| 細分服務 | ✓ | 透過Experience Platform [細分服務](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/segmentation/home)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-portal#import-audience)至Experience Platform。 |


## 支援的目的地 {#supported-destinations}

[!DNL Acxiom's Real ID Audience Connection]目的地目前支援下列平台的對象啟用。

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## 連線到目標 {#connect}

為了您的方便，系統會在幕後自動處理對[!DNL Acxiom's Real ID Audience Connection]目的地的驗證。

## 目的地特定設定 {#destination-settings}

有些[!DNL Acxiom Real ID Audience Connection]目的地需要其他資訊。 以下各節提供如何設定這些選項的詳細指引。

### [!DNL LG Ads] {#lg-ads}

若要設定目的地的詳細資料，請填寫下列欄位。

* **區段類別**：您的區段所屬的目標類別或垂直。 範例：金融服務、汽車、健康等。

![LG廣告目的地詳細資料](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_lg_ads_destination_details.png)


## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}



讀取[啟用批次設定檔匯出目的地的對象資料](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)，以取得啟用此目的地對象的指示。

>[!NOTE]
>
>[!DNL Acxiom Real ID Audience Connection]目的地僅支援完整檔案匯出。


### 對應屬性和身分 {#map}

若要讓[!DNL Acxiom Real ID Audience Connection]目的地正確接收對象資料，您必須從Experience Platform將來源欄位對應至正確的[!DNL Acxiom Real ID Audience Connection]目標欄位。

[!DNL Acxiom Real ID Audience Connection]僅允許對應到下列目標欄位。

| 欄位名稱 | 說明 | 必填 |
|--------------------|------------|--------| 
| 真實ID | 實數ID是Acxiom專屬身分解析圖形中的唯一36位元組英數字元識別碼(ID)，類似於關聯式資料庫的主索引鍵。 這是代表個人、家庭或地址的識別碼。 | 是 |



在&#x200B;**[!UICONTROL Source Field]**&#x200B;欄中，輸入您要對應至對應目標欄位的來源屬性名稱，或選取箭頭圖示以開啟&#x200B;**[!UICONTROL  Select source field]**&#x200B;畫面。 然後，選取&#x200B;**[!UICONTROL Next]**。
![對應熒幕](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_mapping_screen.png)


如果您未使用[!DNL Adobe's]標準結構描述，請參閱[查詢服務UI指南](../../../query-service/ui/overview.md)檔案，以瞭解如何使用查詢服務將您的欄位名稱填入[!DNL Adobe]標準結構描述的資訊。


### 審閱 {#review}

完成上述所有步驟後，您就有機會先檢閱目的地連線狀態和對象詳細資訊，然後再啟用（發佈）該功能。 您選取的對象將顯示在清單底部。 每個對象都會是對[!DNL Acxiom Real ID Audience Connection] API的個別呼叫。

如果您對結果滿意，請選取&#x200B;**[!UICONTROL Finish]**&#x200B;以啟用您的目的地。

![檢閱您的對象](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_review_audience.png)


## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)。

## 疑難排解 {#troubleshooting}

如果目的地代表找不到您的對象，請連絡您的[!DNL Adobe]代表以尋求協助。

您需要提供下列資訊給您的[!DNL Adobe]代表：

* 客群名稱
* 目的地名稱
* 對象啟用日期
* 匯出的檔案名稱

## 後續步驟 {#next-steps}

依照本教學課程中的指示，您已成功將對象啟動至選取的目的地平台。 接下來，請聯絡您的目的地平台代表，以開始設定您的行銷活動。
