---
title: Marketo Engage目的地
description: Marketo Engage是唯一適用於行銷、廣告、分析和商業的端對端客戶體驗管理(CXM)解決方案。 它可讓您自動化並管理從CRM銷售機會管理和客戶參與到帳戶式行銷和收入歸因的活動。
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: c57a519b5a230dc62699808cf5c020d48cc79083
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 1%

---

# Marketo Engage目的地 {#beta-marketo-engage-destination}

## 目的地變更記錄檔 {#changelog}

>[!IMPORTANT]
>
>隨著[增強型Marketo V2目的地聯結器](/help/release-notes/2022/july-2022.md#destinations)的發行，您現在會在目的地目錄中看到兩個Marketo卡片。
>* 如果您已經啟用資料至&#x200B;**[!UICONTROL Marketo V1]**&#x200B;目的地：請在2023年2月前建立新的資料流至&#x200B;**[!UICONTROL Marketo V2]**&#x200B;目的地，並刪除現有資料流至&#x200B;**[!UICONTROL Marketo V1]**&#x200B;目的地。 自該日期起，**[!UICONTROL Marketo V1]**&#x200B;目的地卡片將會移除。
>* 如果您尚未建立任何資料流至&#x200B;**[!UICONTROL Marketo V1]**&#x200B;目的地，請使用新的&#x200B;**[!UICONTROL Marketo V2]**&#x200B;卡片來連線並匯出資料至Marketo。

![並排檢視中兩個Marketo目的地卡片的影像。](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Marketo V2目的地的改良專案包括：

* 在啟動工作流程的&#x200B;**[!UICONTROL 排程區段]**&#x200B;步驟中，在Marketo V1中，您需要手動新增&#x200B;**對應ID**，才能成功將資料匯出至Marketo。 Marketo V2不再需要此手動步驟。
* 在啟動工作流程的&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，在Marketo V1中，您只能將XDM欄位對應到Marketo中的三個目標欄位： `firstName`、`lastName`和`companyName`。 透過Marketo V2版本，您現在可以將XDM欄位對應至Marketo中的更多欄位。 如需詳細資訊，請閱讀下面的[支援的屬性](#supported-attributes)區段。

## 概觀 {#overview}

[!DNL Marketo Engage]是行銷、廣告、分析和商務的唯一端對端客戶體驗管理(CXM)解決方案。 它可讓您自動化並管理從CRM銷售機會管理和客戶參與到帳戶式行銷和收入歸因的活動。

目的地可讓行銷人員將在Adobe Experience Platform中建立的對象推送至Marketo，以便顯示為靜態清單。

## 支援的身分和屬性 {#supported-identities-attributes}

>[!NOTE]
>
>在啟用目的地工作流程的[對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中，必須有&#x200B;*個對應身分識別專案*，而且必須有&#x200B;*個選擇性*&#x200B;個對應屬性。 從「身分名稱空間」標籤對應電子郵件和/或ECID是確保人員在Marketo中相符的最重要事項。 對應電子郵件可確保最高的符合率。

### 支援的身分 {#supported-identities}

| 目標身分 | 說明 |
|---|---|
| ECID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 如需詳細資訊，請參閱[ECID](/help/identity-service/features/ecid.md)上的下列檔案。 |
| 電子郵件 | 代表電子郵件地址的名稱空間。 這種型別的名稱空間通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 |

{style="table-layout:auto"}

### 支援的屬性 {#supported-attributes}

您可以將屬性從Experience Platform對應至貴組織在Marketo中可存取的任何屬性。 在Marketo中，您可以使用[Describe API要求](https://developers.marketo.com/rest-api/lead-database/leads/#describe)來擷取貴組織有權存取的屬性欄位。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出具有[!DNL Marketo Engage]目的地中所使用識別碼（電子郵件、ECID）之對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 設定目的地並啟用對象 {#set-up}

>[!IMPORTANT]
> 
>* 若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

如需如何設定目的地及啟用對象的詳細指示，請參閱Marketo檔案中的[將Adobe Experience Platform對象推送至Marketo靜態清單](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=zh-Hant)。

以下影片也會示範設定Marketo目的地和啟用對象的步驟。

>[!IMPORTANT]
>
>此影片並未完整反映目前的功能。 如需最新資訊，請參閱以上連結的指南。 視訊的下列部分已過時：
> 
>* 您應在Experience Platform UI中使用的目的地卡片是&#x200B;**[!UICONTROL Marketo V2]**。
>* 影片未顯示連線至目的地工作流程中的新&#x200B;**[!UICONTROL 人員建立]**&#x200B;選擇器欄位。 若要使用該欄位，您必須在屬性對應步驟期間同時對應名字和姓氏。
>* 影片中叫用的兩個限制不再適用。 除了錄製影片時支援的對象成員資格資訊之外，您現在可以對應許多其他設定檔屬性欄位。 您也可以將尚未存在於Marketo靜態清單中的受眾成員匯出至Marketo，這些受眾成員將會新增至清單中。
>* 在Marketo V1的啟動工作流程的&#x200B;**[!UICONTROL 排程對象步驟]**&#x200B;中，您需要手動新增&#x200B;**[!UICONTROL 對應ID]**，才能成功將資料匯出至Marketo。 Marketo V2不再需要此手動步驟。

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

## 監視目的地 {#monitor-destination}

連線到目的地並建立目的地資料流後，您可以使用Real-Time CDP中的[監視功能](/help/dataflows/ui/monitor-destinations.md)來取得每次資料流執行中在您的目的地啟用的設定檔記錄的廣泛資訊。

[!DNL Marketo Engage]連線的監視資訊包括與每個資料流和資料流執行中的啟用、排除和失敗身分相關的對象層級資訊。 [閱讀更多](/help/dataflows/ui/monitor-destinations.md#segment-level-view)有關此功能的資訊。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)。

