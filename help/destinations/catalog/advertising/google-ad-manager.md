---
keywords: google廣告管理員；google廣告；doubleclick；DoubleClick AdX；DoubleClick；Google廣告管理員；Google廣告管理員；DFP
title: Google廣告管理員連線
description: Google Ad Manager （舊稱為DoubleClick for Publishers或DoubleClick AdX）是Google的廣告服務平台，可讓發佈者透過視訊和行動應用程式管理其網站上的廣告顯示。
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 4%

---

# [!DNL Google Ad Manager] 連線

## 概觀 {#overview}

[!DNL Google Ad Manager]，先前稱為 [!DNL DoubleClick for Publishers] (DFP)或 [!DNL DoubleClick AdX]是一個廣告服務平台，來自 [!DNL Google] 這可讓發佈者透過視訊和行動應用程式，管理在其網站上顯示的廣告。

## 目的地詳情 {#specifics}

請注意以下專屬於您的詳細資訊 [!DNL Google Ad Manager] 目的地：

* 啟用的對象是以程式設計方式建立於 [!DNL Google] 平台。
* [!DNL Platform] 目前不包含可驗證成功啟用的測量量度。 請參考Google中的對象計數，以驗證整合併瞭解對象目標定位大小。
* 將對象對應至之後 [!DNL Google Ad Manager] 目的地，對象名稱會立即出現在 [!DNL Google Ad Manager] 使用者介面。
* 區段母體需要24到48小時才能顯示於 [!DNL Google Ad Manager]. 此外，對象的對象人數必須至少為50個設定檔，才能顯示在 [!DNL Google Ad Manager]. 大小小於50個設定檔的對象將不會填入 [!DNL Google Ad Manager].

## 支援的身分 {#supported-identities}

[!DNL Google Ad Manager] 支援下表所述的身分啟用。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 當您的來源身分是GAID名稱空間時，請選取此目標身分。 |
| IDFA | [!DNL Apple ID for Advertisers] | 當您的來源身分是IDFA名稱空間時，請選取此目標身分。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也稱為 [!DNL Device ID]. 38位數的裝置ID，Audience Manager會與每個與其互動的裝置建立關聯。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hant) 以加州的目標使用者，以及所有其他使用者的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 使用此ID來鎖定加州以外的使用者。 |
| RIDA | 適用於廣告的Roku ID。 此ID可唯一識別Roku裝置。 |  |
| MAID | Microsoft廣告ID。 此ID可唯一識別執行Windows 10的裝置。 |  |
| Amazon Fire TV ID | 此ID可唯一識別Amazon Fire電視。 |  |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以匯出至此目的地的所有對象。

此目的地支援啟用透過Experience Platform產生的所有對象 [分段服務](../../../segmentation/home.md).

*此外*，此目的地也支援下表所述的對象啟用。

| 對象型別 | 說明 |
---------|----------|
| 自訂上傳 | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在將對象的所有成員匯出至Google目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

如果您打算使用建立您的第一個目的地 [!DNL Google Ad Manager] 且尚未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 若是過去的Experience CloudID服務(使用Audience Manager或其他應用程式)，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已設定 [!DNL Google] Audience Manager中的整合，也就是您設定的ID同步會移轉到Platform。

### 允許清單 {#allow-listing}

必須先將列入允許清單，才能設定您的第一個 [!DNL Google Ad Manager] Platform中的目的地。 在建立目的地之前，請務必完成下述允許清單程式。

1. 請依照中所述的步驟操作。 [Google Ad Manager檔案](https://support.google.com/admanager/answer/3289669?hl=en) 將Adobe新增為連結資料管理平台(DMP)。
2. 在 [!DNL Google Ad Manager] 介面，前往 **[!UICONTROL 管理員]** > **[!UICONTROL 全域設定]** > **[!UICONTROL 網路設定]**，並啟用 **[!UICONTROL API存取]** 滑桿。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 連線引數 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="將對象 ID 附加到對象名稱"
>abstract="選取此選項可讓 Google Ad Manager 中的對象名稱包含來自 Experience Platform 的對象 ID，如下所示：`Audience Name (Audience ID)`"

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊給此目的地：

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 說明]**：選填。 例如，您可以提及要將此目的地用於哪個行銷活動。
* **[!UICONTROL 帳戶ID]**：輸入您的 [!DNL Audience Link ID] 從您的 [!DNL Google] 帳戶。 這是與您的關聯的特定識別碼 [!DNL Google Ad Manager] 網路(不是您的 [!DNL Network code])。 您可以在下方找到此專案 **[!UICONTROL 管理員>全域設定]** 在 [!DNL Google Ad Manager] 介面。
* **[!UICONTROL 帳戶型別]**：根據您使用Google的帳戶，選取選項：
   * 使用 `DFP by Google` 的 [!DNL DoubleClick] 發佈者專用
   * 使用 `AdX buyer` 的 [!DNL Google AdX]
* **[!UICONTROL 將對象ID附加至對象名稱]**：選取此選項，讓Google Ad Manager中的對象名稱包含Experience Platform中的對象ID，如下所示： `Audience Name (Audience ID)`.

>[!NOTE]
>
>設定時 [!DNL Google Ad Manager] 目的地，請使用您的 [!DNL Google Account Manager] 或Adobe代表以瞭解您的帳戶型別。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟用此目的地的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用受眾資料至串流受眾匯出目的地](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

## 匯出的資料 {#exported-data}

驗證資料是否已成功匯出至 [!DNL Google Ad Manager] 目的地，請檢視您的 [!DNL Google Ad Manager] 帳戶。 如果成功啟用，系統會將對象填入您的帳戶。

## 疑難排解 {#troubleshooting}

如果您在使用此目的地時遇到任何錯誤，且需要聯絡Adobe或Google，請隨時保留下列ID。

這些是Adobe的Google帳戶ID：

* **[!UICONTROL 帳戶ID]**：87933855
* **[!UICONTROL 客戶ID]**：89690775