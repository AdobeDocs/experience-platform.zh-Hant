---
title: Pinterest客戶清單連線
description: 從您的客戶清單、造訪過您網站的人員或已在Pinterest上與您的內容互動的人員建立對象。
source-git-commit: 9bd309ae9d9edf56de855422abd109af1a10cffc
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---


# Pinterest客戶清單連線

## 概覽 {#overview}

從您的客戶清單、造訪過您網站的人員或已在Pinterest上與您的內容互動的人員建立對象。

>[!IMPORTANT]
>
>這個目的地是Pinterest團隊建造的。 如有任何查詢或更新請求，請直接通過https://help.pinterest.com/en/contact聯繫。

## 先決條件 {#prerequisites}

* 使用者需要使用Pinterest帳戶進行驗證，該帳戶可存取他們要新增受眾的廣告商帳戶。 如需共用廣告商帳戶的詳細資訊，請前往：https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts。 具體而言，使用者需要「對象」存取層級。
* 有關客戶清單標識格式的詳細資訊，請參見：https://help.pinterest.com/en/business/article/audience-targeting。


## 支援的身分 {#supported-identities}

pinterest客戶清單目的地支援啟用下表所述的身分識別。 深入了解[identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)。

在目標啟動工作流程的[對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中，將所需身分對應至目標欄位&#x200B;*pinterest_audience*。 身分識別會在資料擷取至Pinterest時加以區分和解析。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 將&#x200B;*GAID*&#x200B;來源身分命名空間對應至目標身分欄位&#x200B;*pinterest_audience*。 身分識別會在資料擷取至Pinterest時加以區分和解析。 |
| IDFA | 廣告商專用的Apple ID | 將&#x200B;*IDFA*&#x200B;來源身分命名空間對應至目標身分欄位&#x200B;*pinterest_audience*。 身分識別會在資料擷取至Pinterest時加以區分和解析。 |
| 電子郵件 | 電子郵件地址（清除文字或使用SHA256演算法雜湊） | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 <br> 將Emailor  ** Email_ *LC_SHA256* 來源身分識別命名空間對應至目標身分欄 *位pinterest_audience*。 |

{style=&quot;table-layout:auto&quot;}

## 匯出類型 {#export-type}

**區段匯出**  — 您要匯出區段（對象）的所有成員，以及Pinterest客戶清單目的地所使用的識別碼（名稱、電話號碼或其他）。

## 使用案例 {#use-cases}

為協助您更清楚了解應如何及何時使用Pinterest客戶清單目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。


### 使用案例#1

從您的客戶清單、造訪過您網站的人員或已在Pinterest上與您的內容互動的人員建立對象。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。



### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:您的Pinterest廣告帳戶ID。

## 啟用此目的地的區段 {#activate}

請參閱[啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) ，以取得啟動受眾區段至此目的地的指示。

## 資料使用與控管 {#data-usage-governance}

處理資料時，所有[!DNL Adobe Experience Platform]目標都符合資料使用策略。 有關[!DNL Adobe Experience Platform]如何實施資料控管的詳細資訊，請參閱[資料控管概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。

## 其他資源 {#additional-resources}

如需詳細資訊，請參閱Pinterest說明中心頁面(https://help.pinterest.com/en/business/article/audience-targeting)。