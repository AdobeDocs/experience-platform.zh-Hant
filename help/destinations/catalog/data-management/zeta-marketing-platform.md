---
title: Zeta行銷平台
description: Zeta Marketing Platform (ZMP)是雲端型系統，由智慧（專屬資料和AI）提供支援，協助您更有效率地贏取、成長及留住客戶。
hide: true
hidefromtoc: true
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 1%

---


# Zeta行銷平台 {#zeta-marketing-platform}

## 概觀 {#overview}

Zeta Marketing Platform (ZMP)是雲端型系統，由智慧（專屬資料和AI）提供支援，協助您更有效率地贏取、成長及留住客戶。 如需詳細資訊，請參閱[Zeta Global](https://zetaglobal.com/)。

透過Adobe Experience Platform提供的Zeta Marketing Platform聯結器，您可以順暢地將對象從Experience Platform同步至ZMP。

>[!IMPORTANT]
>
>目的地聯結器和檔案頁面是由&#x200B;*Zeta全域*&#x200B;團隊建立和維護的。 若有任何查詢或更新要求，請透過[連絡我們](https://zetaglobal.com/about/contact-us/)連絡團隊。

## 使用案例 {#use-cases}

### 建立受眾區段 {#use-case-build-audiences}

行銷人員想要建立獨一無二的訪客個人資料，找出他們最寶貴的區段，並在Zeta Marketing Platform支援的任何數位頻道中使用。 他們想要建立消費者個人資料的真實360度檢視，建置並啟用有意義的對象。 如需Zeta行銷平台支援哪些管道的詳細資訊，請參閱[這裡](https://zetaglobal.com/platform/integrations/)。

### 使用廣告鎖定使用者 {#use-case-target-users}

廣告商的目標是透過ZetaDemand Side Platform(DSP)鎖定特定受眾內的使用者，因為這些使用者會與他們的品牌互動。 如需Zeta DSP的詳細資訊，請按一下[這裡](https://knowledgebase.zetaglobal.com/programmatic-user-guide/)。

## 先決條件 {#prerequisites}

### Zeta行銷平台必要條件

* 在您設定與Zeta Marketing Platform目的地的新連線之前，必須在Zeta Marketing Platform帳戶中建立空白的客戶清單。 您必須選擇其中一個客戶清單作為指定目標，以接收您計畫傳送的Adobe Experience Platform對象。 您可以依照指示[這裡](https://knowledgebase.zetaglobal.com/zmp/creating-audiences#CreatingAudiences-CreatingaCustomerList)，在ZMP中建立空的客戶清單。
* 雖然Adobe Experience Platform允許針對特定ZMP目的地執行個體啟用多個對象，但每個ZMP目的地執行個體都必須只接收一個Experience Platform對象。 若要從Experience Platform處理多個受眾，請為每個受眾建立其他ZMP目的地例項，並從下拉式清單中選取不同的客戶清單。 此方法可確保不會覆寫Target ZMP對象。 如需詳細資訊，請參閱[填寫目的地詳細資料](#destination-details)。
* 使用下列認證來設定目的地：
   * 使用者名稱： **api**
   * 密碼：您的ZMP REST API金鑰。 您可以登入您的ZMP帳戶並瀏覽至&#x200B;**設定** > **整合** > **金鑰與應用程式**&#x200B;區段，以找到您的REST API金鑰。 如需詳細資訊，請參閱[ZMP檔案](https://knowledgebase.zetaglobal.com/zmp/integrations)。

## 支援的身分 {#supported-identities}

[!DNL Zeta Marketing Platform]支援啟用下表中描述的自訂使用者ID。 如需詳細資訊，請參閱[身分](/help/identity-service/features/namespaces.md)。

>[!IMPORTANT]
> Zeta Marketing Platform目的地需要您將來源身分名稱空間對應到ZMP `uid`目標身分。 這有助於Zeta行銷平台專門區分每個設定檔。

| 目標身分 | 說明 | 考量事項 | 附註 |
---------|----------|----------|----------|
| uid | ZMP用來區別客戶個人檔案的唯一ID | 強制 | 如果您想要使用唯一的設定檔的電子郵件地址來識別它們，請選擇`Email`標準身分名稱空間。 或者，如果客戶設定檔沒有電子郵件，您可以選擇將自訂名稱空間對應到`uid`。 |
| email_md5_id | 電子郵件MD5代表每個客戶設定檔 | 選填 | 當您想要使用電子郵件MD5值唯一識別客戶設定檔時，請選擇此目標身分。 由於Platform無法將純文字轉換為MD5，因此Experience Platform中的電子郵件地址必須是MD5格式。 在此案例中，將`uid` （必要）設為相同的電子郵件MD5值或其他適當的身分名稱空間。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform[細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | X | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

>[!NOTE]
> 新增或移除Platform對象中的個別成員後，系統會將更新傳送至ZMP，以確保目標客戶清單會據此同步。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據區段評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

* **[!UICONTROL 使用者名稱]**： `api`
* **[!UICONTROL 密碼]**：您的ZMP REST API金鑰。 您可以登入您的ZMP帳戶並瀏覽至&#x200B;**設定** > **整合** > **金鑰與應用程式**&#x200B;區段，以找到您的REST API金鑰。 如需詳細資訊，請參閱[ZMP檔案](https://knowledgebase.zetaglobal.com/zmp/integrations)。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![顯示ZMP組態的影像](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-configure-new-destination.png)
* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL ZMP帳戶網站ID]**：您要將對象傳送至的ZMP **網站ID**。 您可以瀏覽至&#x200B;**設定** > **整合** > **金鑰與應用程式**&#x200B;區段，以檢視您的網站ID。 在[這裡](https://knowledgebase.zetaglobal.com/zmp/integrations)可找到更多資訊。
* **[!UICONTROL ZMP區段]**：您ZMP網站ID帳戶中要與Platform對象一起更新的客戶清單區段。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 管理目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[啟用串流區段匯出目的地的設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md)，以取得啟用此目的地的對象區段的指示。

### 對應屬性和身分 {#map}

以下是將設定檔匯出至[!DNL Zeta Marketing Platform]時的正確身分對應範例。

選取來源欄位：
* 選取在Adobe Experience Platform和[!DNL Zeta Marketing Platform]中唯一識別設定檔的來源識別名稱空間（自訂或標準，例如`Email`）。
* 選取需要匯出到[!DNL Zeta Marketing Platform]並更新的任何XDM來源設定檔屬性。

選取目標欄位：
* （必要）選取`uid`作為您對應來源身分名稱空間的目標身分。
* （選擇性）選取`email_md5_id`作為目標身分，您將代表電子郵件md5值的來源身分名稱空間對應至該身分。 由於Platform無法將純文字轉換為MD5，因此Experience Platform中的電子郵件地址必須是MD5格式
* 視需要選取任何其他目標對應。

![身分對應](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-mapping-example.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

從Experience Platform到Zeta Marketing Platform的成功受眾啟用會更新ZMP中的目標客戶清單。 目標客戶清單中的計數和範例設定檔將等於成功啟用的身分數量。

ZMP中的![客戶清單](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-customer-list-in-zmp.png)

從Experience Platform啟用的每個對象成員也會顯示在ZMP的&#x200B;**對象** > **人員**&#x200B;底下。 您也能在「單一客戶」檢視中檢視設定檔所屬的&#x200B;**客戶清單**&#x200B;區段，如下所示。

![SingleCustomerViewInZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-single-customer-view-in-zmp.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

* [Zeta知識庫](https://knowledgebase.zetaglobal.com/zmp/)
