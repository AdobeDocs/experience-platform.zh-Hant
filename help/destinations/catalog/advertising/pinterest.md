---
title: pinterest客戶清單連線
description: 從您的客戶清單、造訪過您網站的人，或已在Pinterest上與您的內容互動的人中建立對象。
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 8a48ce4185f8044b8563d0435dcec17030b90830
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 4%

---

# [!DNL Pinterest Customer List]個連線

## 概觀 {#overview}

從您的客戶清單、造訪過您網站的人，或已在Pinterest上與您的內容互動的人中建立對象。

>[!IMPORTANT]
>
>此目的地是由Pinterest團隊建置。 如有任何查詢或更新要求，請直接透過https://help.pinterest.com/en/contact聯絡。

## 先決條件 {#prerequisites}

* 使用者必須使用Pinterest帳戶進行驗證，該帳戶具有其要新增受眾的廣告商帳戶的存取權。 您可以在[這裡](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts)找到共用廣告商帳戶的詳細資料。 具體來說，使用者需要「對象」存取層級。
* 您可以在[這裡](https://help.pinterest.com/en/business/article/audience-targeting)找到客戶清單身分格式的詳細資料。

## 支援的身分 {#supported-identities}

[!DNL Pinterest Customer List]目的地支援下表所述的身分啟用。 深入瞭解[身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started)。

在目的地啟用工作流程的[對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中，將所需的身分對應到目標欄位&#x200B;*pinterest_audience*。 身分識別會在資料擷取至Pinterest時區分和解析。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 將&#x200B;*GAID*&#x200B;來源身分名稱空間對應到目標身分欄位&#x200B;*pinterest_audience*。 身分識別會在資料擷取至Pinterest時區分和解析。 |
| IDFA | [!DNL Apple ID for Advertisers] | 將&#x200B;*IDFA*&#x200B;來源識別名稱空間對應到目標識別欄位&#x200B;*pinterest_audience*。 身分識別會在資料擷取至Pinterest時區分和解析。 |
| EMAIL | 電子郵件地址（純文字或使用SHA256演演算法雜湊） | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 <br>將&#x200B;*Email*&#x200B;或&#x200B;*Email_LC_SHA256*&#x200B;來源身分名稱空間對應到目標身分欄位&#x200B;*pinterest_audience*。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出具有Pinterest客戶清單目的地所使用識別碼（名稱、電話號碼或其他）的對象所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL Pinterest Customer List]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 使用案例#1

從您的客戶清單、造訪過您網站的人，或已在Pinterest上與您的內容互動的人中建立對象。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 廣告帳戶ID]**：您的Pinterest廣告商ID。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)。

## 其他資源 {#additional-resources}

如需詳細資訊，請參閱[Pinterest說明中心頁面](https://help.pinterest.com/en/business/article/audience-targeting)。

+++ 檢視變更記錄檔


| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2023 年 11 月 | 功能和檔案更新 | Real-Time CDP中的Pinterest目的地現在使用v5廣告商API。 |

{style="table-layout:auto"}


+++
