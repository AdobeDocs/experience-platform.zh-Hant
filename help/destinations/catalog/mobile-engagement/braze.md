---
keywords: 行動；佈雷茲；報文傳送；
title: Braze連接
description: Braze是一個全面的客戶參與平台，可為客戶與其喜愛的品牌之間提供相關且難忘的體驗。
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 1%

---

# [!DNL Braze] 連接

## 總覽 {#overview}

此 [!DNL Braze] 目的地可協助您將設定檔資料傳送至 [!DNL Braze].

[!DNL Braze] 是全方位的客戶互動平台，可為客戶與其喜愛的品牌之間提供相關且難忘的體驗。

若要將設定檔資料傳送至 [!DNL Braze]，您必須先連線至目的地。

## 目的地細節 {#specifics}

請注意下列 [!DNL Braze] 目的地：

* [!DNL Adobe Experience Platform] 區段會匯出至 [!DNL Braze] 在 `AdobeExperiencePlatformSegments` 屬性。

>[!NOTE]
>
>請記住，將其他自訂屬性傳送至 [!DNL Braze] 可能會導致 [!DNL Braze] 資料點耗用量。 請諮詢您的 [!DNL Braze] 帳戶管理員，再傳送其他自訂屬性。

## 使用案例 {#use-cases}

身為行銷人員，我想要將目標鎖定在行動參與目的地的使用者，並內建區段 [!DNL Adobe Experience Platform]. 此外，我也想根據訪客的屬性，為他們提供個人化體驗 [!DNL Adobe Experience Platform] 設定檔，當區段和設定檔在 [!DNL Adobe Experience Platform].

## 支援的身分 {#supported-identities}

[!DNL Braze] 支援啟用下表所述的身分。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| external_id | 自訂 [!DNL Braze] 支援任何身分對應的識別碼。 | 您可以傳送任何 [身分](../../../identity-service/namespaces.md) 到 [!DNL Braze] 目的地，只要您將其對應至 [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要匯出區段的所有成員，以及所需的結構欄位(例如：根據您的欄位對應，以電子郵件地址、電話號碼、姓氏)和/或身分識別。[!DNL Adobe Experience Platform] 區段會匯出至 [!DNL Braze] 在 `AdobeExperiencePlatformSegments` 屬性。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

### 驗證到目標 {#authenticate}

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

* **[!UICONTROL Braze帳戶代號]**:這是您的 [!DNL Braze] [!DNL API] 鍵。 您可以找到有關如何獲取 [!DNL API] 索引鍵： [REST API金鑰概觀](https://www.braze.com/docs/api/api_key/).

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:輸入一個名稱，以便您將來識別此目標。
* **[!UICONTROL 說明]**:輸入說明，以便您在未來識別此目的地。
* **[!UICONTROL 端點執行個體]**:詢問 [!DNL Braze] 代表您應使用的端點執行個體。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 對應考量事項 {#mapping-considerations}

若要正確傳送對象資料，請從 [!DNL Adobe Experience Platform] 到 [!DNL Braze] 目的地，您必須執行欄位對應步驟。

對應包括在 [!DNL Experience Data Model] (XDM)您 [!DNL Platform] 帳戶，以及目標目的地的對應等效項目。

若要正確將XDM欄位對應至 [!DNL Braze] 目標欄位，請遵循下列步驟：

在 [!UICONTROL 對應] 步驟，按一下 **[!UICONTROL 新增對應]**.

![Braze目標添加映射](../../assets/catalog/mobile-engagement/braze/mapping.png)

在 [!UICONTROL 源欄位] 區段，按一下空白欄位旁的箭頭按鈕。

![佈雷茲目標源映射](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

在 [!UICONTROL 選擇源欄位] 視窗中，您可以在兩個XDM欄位類別中進行選擇：
* [!UICONTROL 選擇屬性]:使用此選項將特定欄位從XDM架構對應至 [!DNL Braze] 屬性。

![佈雷茲目標映射源屬性](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL 選取身分命名空間]:使用此選項來對應 [!DNL Platform] 身分命名空間 [!DNL Braze] 命名空間。

![佈雷茲目標映射源命名空間](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

選擇源欄位，然後按一下 **[!UICONTROL 選擇]**.

在 [!UICONTROL 目標欄位] 區段，按一下欄位右側的對應圖示。

![佈雷茲目標對應](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

在 [!UICONTROL 選擇目標欄位] 窗口中，您可以在兩個目標欄位之間進行選擇：
* [!UICONTROL 選取身分命名空間]:使用此選項可映射 [!DNL Platform] 識別命名空間 [!DNL Braze] 身分識別命名空間。
* [!UICONTROL 選取自訂屬性]:使用此選項將XDM屬性對應至自訂 [!DNL Braze] 您在 [!DNL Braze] 帳戶。 <br> 您也可以使用此選項，將現有的XDM屬性重新命名為 [!DNL Braze]. 例如，對應 `lastName` 自訂的XDM屬性 `Last_Name` 屬性 [!DNL Braze]，將建立 `Last_Name` 屬性 [!DNL Braze]，如果尚未存在，請對應 `lastName` XDM屬性。

![佈雷茲目標對應欄位](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

選擇您的目標欄位，然後按一下 **[!UICONTROL 選擇]**.

您現在應該會在清單中看到欄位對應。

![Braze目標映射完成](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

若要新增更多對應，請重複先前的步驟。

## 對應範例 {#mapping-example}

假設您的XDM設定檔結構和 [!DNL Braze] 例項包含下列屬性和身分：

|  | XDM設定檔結構 | [!DNL Braze] 例項 |
|---|---|---|
| 屬性 | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>名字</code></li><li>LastName</code></li><li>電話號碼</code></li></ul> |
| 身分 | <ul><li>電子郵件</code></li><li>Google廣告ID(GAID)</code></li><li>Apple Id For Advertisers(IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

正確的對應如下所示：

![佈雷茲目標對應範例](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## 匯出的資料 {#exported-data}

驗證資料是否已成功導出到 [!DNL Braze] 目的地，檢查 [!DNL Braze] 帳戶。 [!DNL Adobe Experience Platform] 區段會匯出至 [!DNL Braze] 在 `AdobeExperiencePlatformSegments` 屬性。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強化資料控管，請參閱 [資料控管概觀](../../../data-governance/home.md).
