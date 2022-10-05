---
title: Marketo Engage目標
description: Marketo Engage是唯一適用於行銷、廣告、分析和商務的端對端客戶體驗管理(CXM)解決方案。 它可讓您自動化和管理活動，從CRM銷售機會管理、客戶參與，到以帳戶為基礎的行銷和收入歸因。
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 9f305ee7824bd8790dec57ccbd2d9462ccfa8b49
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 2%

---

# Marketo Engage目標 {#beta-marketo-engage-destination}

## 目標更改日誌 {#changelog}

>[!IMPORTANT]
>
>隨著 [增強的Marketo V2目的地連接器](/help/release-notes/2022/july-2022.md#destinations)，您現在會在目的地目錄中看到兩個Marketo卡。
>* 如果您已在 **[!UICONTROL Marketo V1]** 目的地：請建立新資料流到 **[!UICONTROL Marketo V2]** 目標資料流並將其刪除 **[!UICONTROL Marketo V1]** 目的地。 截至該日， **[!UICONTROL Marketo V1]** 目的地卡將會移除。
>* 如果您尚未建立任何資料流至 **[!UICONTROL Marketo V1]** 目的地，請使用新 **[!UICONTROL Marketo V2]** 卡片，以連線並匯出資料至Marketo。


![以並排檢視顯示的兩個Marketo目的地卡片影像。](/help/destinations/assets/catalog/adobe/marketo-side-by-side-view.png)

Marketo V2目的地的改良功能包括：

* 在 **[!UICONTROL 排程區段]** 在Marketo V1中，您需要手動新增 **對應ID** 成功將資料匯出至Marketo。 Marketo V2不再需要此手動步驟。
* 在 **[!UICONTROL 對應]** 啟動工作流程的步驟中，在Marketo V1中，您可以將XDM欄位對應至Marketo中的僅三個目標欄位： `firstName`, `lastName`，和 `companyName`. 透過Marketo V2版本，您現在可以將XDM欄位對應至Marketo中的更多欄位。 如需詳細資訊，請閱讀 [支援的屬性](#supported-attributes) 下文一節。

## 總覽 {#overview}

[!DNL Marketo Engage] 是唯一適用於行銷、廣告、分析和商務的端對端客戶體驗管理(CXM)解決方案。 它可讓您自動化和管理活動，從CRM銷售機會管理、客戶參與，到以帳戶為基礎的行銷和收入歸因。

目的地可讓行銷人員將在Adobe Experience Platform中建立的區段推送至Marketo，這些區段會顯示為靜態清單。

## 支援的身分和屬性 {#supported-identities-attributes}

>[!NOTE]
>
>在 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 啟動目標工作流程， *強制* 來對應身分和 *可選* 映射屬性。 從「身分命名空間」標籤對應電子郵件和/或ECID是確保人員在Marketo中符合的最重要動作。 對應電子郵件可確保最高的匹配率。

### 支援的身分 {#supported-identities}

| Target身分 | 說明 |
|---|---|
| ECID | 代表ECID的命名空間。 此命名空間也可由下列別名引用：&quot;Adobe Marketing Cloud ID&quot;、&quot;Adobe Experience Cloud ID&quot;、&quot;Adobe Experience Platform ID&quot;。 請參閱下列檔案，內容如下 [ECID](/help/identity-service/ecid.md) 以取得更多資訊。 |
| 電子郵件 | 代表電子郵件地址的命名空間。 此類型的命名空間通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 |

{style=&quot;table-layout:auto&quot;}

### 支援的屬性 {#supported-attributes}

您可以將屬性從Experience Platform對應至貴組織在Marketo中可存取的任何屬性。 在Marketo中，您可以使用 [說明API請求](https://developers.marketo.com/rest-api/lead-database/leads/#describe) 以擷取您的組織可存取的屬性欄位。

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您會使用 [!DNL Marketo Engage] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 設定目的地和啟用區段 {#set-up}

>[!IMPORTANT]
> 
>* 若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions).
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。


如需如何設定目的地和啟用區段的詳細指示，請參閱 [推送Adobe Experience Platform區段至Marketo靜態清單](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) 在Marketo檔案中。

以下影片也示範設定Marketo目的地和啟用區段的步驟。

>[!IMPORTANT]
>
>視訊未完全反映目前的功能。 如需最新資訊，請參閱上述連結的指南。 視訊的下列部分已過時：
> 
>* 您應在Experience PlatformUI中使用的目的地卡片是 **[!UICONTROL Marketo V2]**.
>* 影片未顯示新 **[!UICONTROL 人員建立]** 「連線至目標」工作流程中的「選取器」欄位。
>* 影片中傳出的兩個限制不再適用。 除了錄制影片時支援的區段成員資格資訊之外，您現在還可以映射許多其他設定檔屬性欄位。 您也可以將區段成員匯出至尚未存在於Marketo靜態清單中的Marketo，這些區段成員會新增至清單中。
>* 在 **[!UICONTROL 排程區段步驟]** 在Marketo V1中，您需要手動新增 **[!UICONTROL 對應ID]** 成功將資料匯出至Marketo。 Marketo V2不再需要此手動步驟。


>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
