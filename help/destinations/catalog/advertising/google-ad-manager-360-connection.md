---
title: （測試版） [!DNL Google Ad Manager 360] 連接
description: Google Ad Manager 360是Google的廣告服務平台，可讓發佈商管理其網站上、透過視訊和行動應用程式的廣告顯示。
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: 5174c65970aa8df9bc3f2c8d612c26c72c20e81f
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 4%

---

# （測試版） [!DNL Google Ad Manager 360] 連接

## 總覽 {#overview}

此 [!DNL Google Ad Manager 360] 連線可啟用批次上傳 [!DNL publisher provided identifiers] (PPID)輸入 [!DNL Google Ad Manager 360]，透過 [!DNL Google Cloud Storage].

如需發佈者提供之識別碼在Google Ad Manager 360中如何運作的詳細資訊，請參閱 [官方Google檔案](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>此目的地目前為測試版，僅適用於有限數量的客戶。 若要要求存取 [!DNL Google Ad Manager 360] 連線，請連絡您的Adobe代表，並提供 [!DNL organization ID].

此 [!DNL Google Ad Manager 360] 目的地匯出 [!DNL CSV] 檔案 [!DNL Google Cloud Storage] 桶。 一旦匯出 [!DNL CSV] 檔案，您必須將它們匯入 [!DNL Google Ad Manager 360] 帳戶。

## 目的地細節 {#specifics}

請注意下列 [!DNL Google Ad Manager 360] 目的地。

* 已啟用的對象是以程式設計方式在Google平台中建立，並填入CSV檔案中。

## 支援的身分 {#supported-identities}

[!DNL This integration] 支援啟用下表所述的身分。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | 選取此目標身分以傳送對象至 [!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要依「 」的「選取設定檔屬性」畫面中的選取，匯出區段的所有成員，以及適用的結構欄位（例如PPID） [目的地啟動工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以3、6、8、12或24小時為增量將檔案匯出至下游平台。 深入了解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

### 允許清單 {#allow-listing}

在設定第一個 [!DNL Google Ad Manager 360] 目標。 建立目的地之前，請務必完成下述的允許清單程式。

>[!NOTE]
>
>此規則的例外是現有 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 客戶。 如果您已Audience Manager建立連線至此Google目的地，則不需要再次執行允許清單程式，您可以繼續執行後續步驟。

1. 請依照 [Google Ad Manager檔案](https://support.google.com/admanager/answer/3289669?hl=en) 將Adobe新增為連結的資料管理平台(DMP)。
2. 在 [!DNL Google Ad Manager] 介面，轉到 **[!UICONTROL 管理]** > **[!UICONTROL 全域設定]** > **[!UICONTROL 網路設定]**，並啟用 **[!UICONTROL API存取]** 滑桿。


## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). 在目標設定工作流程中，填寫下列兩節中列出的欄位。

### 驗證到目標 {#authenticate}

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

* **[!UICONTROL 訪問密鑰ID]**:61個字元的英數字串，用於驗證您的 [!DNL Google Cloud Storage] 帳戶至Platform。
* **[!UICONTROL 秘密訪問密鑰]**:用於驗證您的 [!DNL Google Cloud Storage] 帳戶至Platform。

如需這些值的詳細資訊，請參閱 [Google雲端儲存HMAC金鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 指南。 有關如何生成您自己的訪問密鑰ID和秘密訪問密鑰的步驟，請參閱 [[!DNL Google Cloud Storage] 來源概觀](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### 填寫目的地詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="將區段 ID 附加到區段名稱"
>abstract="選取此選項可讓 Google Ad Manager 360 中的區段名稱包含來自 Experience Platform 的區段 ID，如下所示：`Segment Name (Segment ID)`"

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
* **[!UICONTROL 說明]**:選填。 例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 資料夾路徑]**:輸入要承載導出檔案的目標資料夾的路徑。
* **[!UICONTROL 貯體名稱]**:輸入 [!DNL Google Cloud Storage] 此目的地所使用的貯體。
* **[!UICONTROL 帳戶ID]**:輸入 [!DNL Audience Link ID] 從 [!DNL Google] 帳戶。 這是與 [!DNL Google Ad Manager] 網路(不是 [!DNL Network code])。 您可以在 **[!UICONTROL 「管理員>全域設定」]** 在 [!DNL Google Ad Manager] 介面。
* **[!UICONTROL 帳戶類型]**:根據您的 [!DNL Google] 帳戶：
   * 使用 `AdX buyer` for [!DNL Google AdX]
   * 使用 `DFP by Google` for [!DNL DoubleClick] 適用於發佈者
* **[!UICONTROL 將區段ID附加至區段名稱]**:選取此選項，讓Google Ad Manager 360中的區段名稱包含來自Experience Platform的區段ID，如下所示： `Segment Name (Segment ID)`.

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

在身分對應步驟中，您會看到下列預先填入的對應：

| 預先填入的對應 | 說明 |
|---------|----------|
| `ECID` -> `ppid` | 這是唯一可由使用者編輯的預先填入對應。 您可以從Platform選取任何屬性或身分識別命名空間，並將其對應至 `ppid`. |
| `metadata.segment.alias` -> `list_id` | 將Experience Platform區段名稱對應至Google平台中的區段ID。 |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | 告知Google平台何時從區段中移除不合格的使用者。 |

需要這些對應 [!DNL Google Ad Manager 360] 和由Adobe Experience Platform自動建立， [!DNL Google Ad Manager 360] 連線。

![顯示Google Ad Manager 360對應步驟的UI影像。](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## 匯出的資料 {#exported-data}

若要確認資料是否已成功匯出，請檢查 [!DNL Google Cloud Storage] 儲存貯體，並確認匯出的檔案包含預期的設定檔母體。

## 疑難排解 {#troubleshooting}

如果您在使用此目的地時遇到任何錯誤，且需要聯絡Adobe或Google，請保留下列ID。

這些是Adobe的Google帳戶ID:

* **[!UICONTROL 帳戶ID]**:87933855
* **[!UICONTROL 客戶ID]**:89690775