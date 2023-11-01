---
title: Marketo Engage目的地
description: Marketo Engage是唯一適用於行銷、廣告、分析和商業的端對端客戶體驗管理(CXM)解決方案。 它可讓您自動化並管理從CRM銷售機會管理和客戶參與到帳戶式行銷和收入歸因的活動。
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 1%

---

# Marketo Engage目的地 {#beta-marketo-engage-destination}

## 目的地變更記錄檔 {#changelog}

>[!IMPORTANT]
>
>隨著 [增強型Marketo V2目的地聯結器](/help/release-notes/2022/july-2022.md#destinations)，您現在會在目的地目錄中看到兩張Marketo卡片。
>* 如果您已將資料啟用至 **[!UICONTROL Marketo V1]** 目的地：請建立新的資料流至 **[!UICONTROL Marketo V2]** 目的地並刪除現有的資料流 **[!UICONTROL Marketo V1]** 2023年2月前到達目的地。 截至該日， **[!UICONTROL Marketo V1]** 將移除目的地卡片。
>* 如果您尚未建立任何資料流至 **[!UICONTROL Marketo V1]** 目的地，請使用新的 **[!UICONTROL Marketo V2]** 卡片，用來連線及匯出資料至Marketo。

![並排檢視中的兩個Marketo目的地卡片影像。](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Marketo V2目的地的改良專案包括：

* 在 **[!UICONTROL 排程區段]** 啟動工作流程的步驟，在Marketo V1中，您需要手動新增 **對應ID** 以成功將資料匯出至Marketo。 Marketo V2不再需要此手動步驟。
* 在 **[!UICONTROL 對應]** 啟動工作流程的步驟中，在Marketo V1中，您僅能將XDM欄位對應到Marketo中的三個目標欄位： `firstName`， `lastName`、和 `companyName`. 透過Marketo V2版本，您現在可以將XDM欄位對應至Marketo中的更多欄位。 如需詳細資訊，請閱讀 [支援的屬性](#supported-attributes) 區段。

## 概觀 {#overview}

[!DNL Marketo Engage] 是唯一適用於行銷、廣告、分析和商務的端對端客戶體驗管理(CXM)解決方案。 它可讓您自動化並管理從CRM銷售機會管理和客戶參與到帳戶式行銷和收入歸因的活動。

目的地可讓行銷人員將在Adobe Experience Platform中建立的對象推送至Marketo，以便顯示為靜態清單。

## 支援的身分和屬性 {#supported-identities-attributes}

>[!NOTE]
>
>在 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) （在啟用目標工作流程中），它是 *強制* 對應身分和 *可選* 以對應屬性。 從「身分名稱空間」標籤對應電子郵件和/或ECID是確保人員在Marketo中相符的最重要事項。 對應電子郵件可確保最高的符合率。

### 支援的身分 {#supported-identities}

| 目標身分 | 說明 |
|---|---|
| ECID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 請參閱以下檔案： [ECID](/help/identity-service/ecid.md) 以取得詳細資訊。 |
| 電子郵件 | 代表電子郵件地址的名稱空間。 這種型別的名稱空間通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 |

{style="table-layout:auto"}

### 支援的屬性 {#supported-attributes}

您可以將屬性從「Experience Platform」對應至貴組織在Marketo中可以存取的任何屬性。 在Marketo中，您可以使用 [說明API要求](https://developers.marketo.com/rest-api/lead-database/leads/#describe) 以擷取貴組織有權存取的屬性欄位。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在匯出某個對象的所有成員，而這些成員具有在檔案庫中使用的識別碼（電子郵件、ECID）。 [!DNL Marketo Engage] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 設定目的地並啟用對象 {#set-up}

>[!IMPORTANT]
> 
>* 若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions).
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

如需如何設定目的地和啟用對象的詳細指示，請閱讀 [將Adobe Experience Platform對象推送至Marketo靜態清單](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) (位於Marketo檔案中)。

以下影片也會示範設定Marketo目的地和啟用對象的步驟。

>[!IMPORTANT]
>
>此影片並未完整反映目前的功能。 如需最新資訊，請參閱以上連結的指南。 視訊的下列部分已過時：
> 
>* 您應在Experience Platform UI中使用的目的地卡片是 **[!UICONTROL Marketo V2]**.
>* 影片未顯示新的 **[!UICONTROL 個人建立]** 連線到目標工作流程中的選取器欄位。
>* 影片中叫用的兩個限制不再適用。 除了錄製影片時支援的對象成員資格資訊之外，您現在可以對應許多其他設定檔屬性欄位。 您也可以將尚未存在於Marketo靜態清單中的受眾成員匯出至Marketo，這些受眾成員將會新增至清單中。
>* 在 **[!UICONTROL 排程對象步驟]** Marketo在啟動工作流程中，您需要手動新增 **[!UICONTROL 對應ID]** 以成功將資料匯出至Marketo。 Marketo V2不再需要此手動步驟。

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料治理總覽](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant).

<!--

## Activate audiences to this destination {#activate}

See [Activate audience data to streaming audience export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audiences to this destination.

-->
