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

Zeta Marketing Platform (ZMP)是雲端型系統，由智慧（專屬資料和AI）提供支援，協助您更有效率地贏取、成長及留住客戶。 如需詳細資訊，請參閱 [Zeta全域](https://zetaglobal.com/).

透過Adobe Experience Platform提供的Zeta Marketing Platform聯結器，您可以順暢地將對象從Experience Platform同步至ZMP。

>[!IMPORTANT]
>
>目的地聯結器和檔案頁面是由 *Zeta全域* 團隊。 如有任何查詢或更新要求，請聯絡團隊： [聯絡我們](https://zetaglobal.com/about/contact-us/).

## 使用案例 {#use-cases}

### 建立受眾區段 {#use-case-build-audiences}

行銷人員想要建立獨一無二的訪客個人資料，找出他們最寶貴的區段，並在Zeta Marketing Platform支援的任何數位頻道中使用。 他們想要建立消費者個人資料的真實360度檢視，建置並啟用有意義的對象。 如需Zeta行銷平台支援哪些管道的詳細資訊，請參閱 [此處](https://zetaglobal.com/platform/integrations/).

### 使用廣告鎖定使用者 {#use-case-target-users}

廣告商的目標是透過ZetaDemand Side Platform(DSP)鎖定特定受眾內的使用者，因為這些使用者會與他們的品牌互動。 如需Zeta DSP的詳細資訊，請按一下 [此處](https://knowledgebase.zetaglobal.com/programmatic-user-guide/).

## 先決條件 {#prerequisites}

### Zeta行銷平台必要條件

* 在您設定與Zeta Marketing Platform目的地的新連線之前，必須在Zeta Marketing Platform帳戶中建立空白的客戶清單。 您必須選擇其中一個客戶清單作為指定目標，以接收您計畫傳送的Adobe Experience Platform對象。 您可以依照指示在ZMP中建立空的客戶清單 [此處](https://knowledgebase.zetaglobal.com/zmp/creating-audiences#CreatingAudiences-CreatingaCustomerList).
* 雖然Adobe Experience Platform允許針對特定ZMP目的地執行個體啟用多個對象，但每個ZMP目的地執行個體都必須只接收一個Experience Platform對象。 若要從Experience Platform處理多個受眾，請為每個受眾建立其他ZMP目的地例項，並從下拉式清單中選取不同的客戶清單。 此方法可確保不會覆寫Target ZMP對象。 另請參閱 [填寫目的地詳細資料](#destination-details) 以取得更多詳細資料。
* 使用下列認證來設定目的地：
   * 使用者名稱： **api**
   * 密碼：您的ZMP REST API金鑰。 您可以登入ZMP帳戶並導覽至，找到您的REST API金鑰 **設定** > **整合** > **按鍵與應用程式** 區段。 請參閱 [ZMP檔案](https://knowledgebase.zetaglobal.com/zmp/integrations) 以取得更多詳細資料。

## 支援的身分 {#supported-identities}

[!DNL Zeta Marketing Platform] 支援自訂使用者ID的啟用，如下表所述。 如需詳細資訊，請參閱 [身分](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
> Zeta行銷平台目的地需要您將來源身分名稱空間對應到ZMP `uid` 目標身分。 這有助於Zeta行銷平台專門區分每個設定檔。

| 目標身分 | 說明 | 考量事項 | 附註 |
---------|----------|----------|----------|
| uid | ZMP用來區別客戶個人檔案的唯一ID | 強制 | 選擇 `Email` 標準身分名稱空間。 或者，您可以選擇將自訂名稱空間對應至 `uid` 如果客戶設定檔沒有電子郵件。 |
| email_md5_id | 電子郵件MD5代表每個客戶設定檔 | 選填 | 當您想要使用電子郵件MD5值唯一識別客戶設定檔時，請選擇此目標身分。 由於Platform無法將純文字轉換為MD5，因此Experience Platform中的電子郵件地址必須是MD5格式。 在此案例中，設定 `uid` （必要）至相同的電子郵件MD5值或其他適當的身分名稱空間。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | X | 受眾 [已匯入](../../../segmentation/ui/audience-portal.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

>[!NOTE]
> 新增或移除Platform對象中的個別成員後，系統會將更新傳送至ZMP，以確保目標客戶清單會據此同步。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據區段評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要向目的地進行驗證，請填寫必填欄位並選取 **[!UICONTROL 連線到目的地]**.

* **[!UICONTROL 使用者名稱]**： `api`
* **[!UICONTROL 密碼]**：您的ZMP REST API金鑰。 您可以登入ZMP帳戶並導覽至，找到您的REST API金鑰 **設定** > **整合** > **按鍵與應用程式** 區段。 請參閱 [ZMP檔案](https://knowledgebase.zetaglobal.com/zmp/integrations) 以取得更多詳細資料。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![顯示ZMP設定的影像](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-configure-new-destination.png)
* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL ZMP帳戶網站ID]**：您的ZMP **網站ID** 您要將受眾傳送至何處。 您可以導覽至「 」以檢視您的網站ID **設定** > **整合** > **按鍵與應用程式** 區段。 可以找到更多資訊 [此處](https://knowledgebase.zetaglobal.com/zmp/integrations).
* **[!UICONTROL ZMP區段]**：您ZMP Site Id帳戶中要與Platform對象一起更新的客戶清單區段。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

讀取 [對串流區段匯出目的地啟用設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 對應屬性和身分 {#map}

以下是將設定檔匯出到時的正確身分對應範例 [!DNL Zeta Marketing Platform].

選取來源欄位：
* 選取來源身分名稱空間(自訂或標準，例如 `Email`)可唯一識別Adobe Experience Platform中的設定檔，以及 [!DNL Zeta Marketing Platform].
* 選取需要匯出到的任何XDM來源設定檔屬性，並更新於 [!DNL Zeta Marketing Platform].

選取目標欄位：
* （必要）選取 `uid` 作為目標身分，您會將來源身分名稱空間對應至該身分。
* （選用）選取 `email_md5_id` 作為目標身分，您會將代表電子郵件md5值的來源身分名稱空間對應至該身分。 由於Platform無法將純文字轉換為MD5，因此Experience Platform中的電子郵件地址必須是MD5格式
* 視需要選取任何其他目標對應。

![身分對應](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-mapping-example.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

從Experience Platform到Zeta Marketing Platform的成功受眾啟用會更新ZMP中的目標客戶清單。 目標客戶清單中的計數和範例設定檔將等於成功啟用的身分數量。

![ZMP中的客戶清單](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-customer-list-in-zmp.png)

從Experience Platform啟用的每個對象成員也會顯示在下 **受眾** > **人員** 在ZMP中。 您也可以檢視 **客戶清單** 設定檔在「單一客戶」檢視中所屬的區段，如下所示。

![SingleCustomerViewInZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-single-customer-view-in-zmp.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，讀取 [資料控管概觀](/help/data-governance/home.md).

## 其他資源 {#additional-resources}

* [Zeta知識庫](https://knowledgebase.zetaglobal.com/zmp/)
