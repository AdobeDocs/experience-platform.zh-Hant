---
keywords: 行動；佈雷茲；報文傳送；
title: Braze連接
description: Braze是一個全面的客戶參與平台，可為客戶與其喜愛的品牌之間提供相關且難忘的體驗。
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 3d7151645bc90a2dcbd6b31251ed459029ab77c9
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# [!DNL Braze] 連接

## 概覽 {#overview}

[!DNL Braze]目的地可協助您將設定檔資料傳送至[!DNL Braze]。

[!DNL Braze] 是全方位的客戶互動平台，可為客戶與其喜愛的品牌之間提供相關且難忘的體驗。

若要將設定檔資料傳送至[!DNL Braze]，您必須先連線至目的地。

## 目的地細節 {#specifics}

請注意下列特定於[!DNL Braze]目的地的詳細資訊：

* [!DNL Adobe Experience Platform] 區段會匯出 [!DNL Braze] 至屬 `AdobeExperiencePlatformSegments` 性下。

>[!NOTE]
>
>請記住，將其他自訂屬性傳送至[!DNL Braze]可能會導致[!DNL Braze]資料點耗用量增加。 傳送其他自訂屬性之前，請洽詢您的[!DNL Braze]客戶經理。

## 使用案例 {#use-cases}

身為行銷人員，我想要將目標鎖定在行動參與目的地的使用者，並在[!DNL Adobe Experience Platform]中內建區段。 此外，我也想在[!DNL Adobe Experience Platform]中更新區段和設定檔時，根據其[!DNL Adobe Experience Platform]設定檔的屬性，為他們提供個人化體驗。

## 支援的身分 {#supported-identities}

[!DNL Braze] 支援啟用下表所述的身分。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| external_id | 支援任何身分對應的自訂[!DNL Braze]識別碼。 | 只要將任何[identity](../../../identity-service/namespaces.md)對應至[!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation)目的地，即可將其傳送至[!DNL Braze]目的地。 |

## 匯出類型 {#export-type}

**[!DNL Profile-based]**  — 您要匯出區段的所有成員，以及所需的架構欄位(例如：根據您的欄位對應，以電子郵件地址、電話號碼、姓氏)和/或身分識別。[!DNL Adobe Experience Platform] 區段會匯出 [!DNL Braze] 至屬 `AdobeExperiencePlatformSegments` 性下。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!UICONTROL Braze帳戶代號]**:這是你的 [!DNL Braze] [!DNL API] 鑰匙。您可以在此處找到有關如何獲取[!DNL API]鍵的詳細說明：[REST API密鑰概述](https://www.braze.com/docs/api/api_key/)。
* **[!UICONTROL 名稱]**:輸入一個名稱，以便您將來識別此目標。
* **[!UICONTROL 說明]**:輸入說明，以便您在未來識別此目的地。
* **[!UICONTROL 端點實例]**:請洽詢您 [!DNL Braze] 的代表您應使用哪個端點執行個體。

## 啟用此目的地的區段 {#activate}

請參閱[對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) ，以取得對此目的地啟用受眾區段的指示。

## 對應考量事項 {#mapping-considerations}

若要將您的對象資料從[!DNL Adobe Experience Platform]正確傳送至[!DNL Braze]目的地，您必須執行欄位對應步驟。

對應包含在[!DNL Platform]帳戶的[!DNL Experience Data Model](XDM)架構欄位與目標目的地對應的欄位之間建立連結。

若要將XDM欄位正確對應至[!DNL Braze]目的地欄位，請執行下列步驟：

在[!UICONTROL 映射]步驟中，按一下&#x200B;**[!UICONTROL 添加新映射]**。

![Braze目標添加映射](../../assets/catalog/mobile-engagement/braze/mapping.png)

在[!UICONTROL 源欄位]部分，按一下空欄位旁的箭頭按鈕。

![佈雷茲目標源映射](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

在[!UICONTROL 選擇源欄位]窗口中，可以在兩個XDM欄位類別之間進行選擇：
* [!UICONTROL 選擇屬性]:使用此選項將特定欄位從XDM結構對應至屬 [!DNL Braze] 性。

![佈雷茲目標映射源屬性](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL 選取身分命名空間]:使用此選項可將身分 [!DNL Platform] 命名空間對應至命 [!DNL Braze] 名空間。

![佈雷茲目標映射源命名空間](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

選擇源欄位，然後按一下&#x200B;**[!UICONTROL 選擇]**。

在[!UICONTROL 目標欄位]區段中，按一下欄位右側的對應圖示。

![佈雷茲目標對應](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

在[!UICONTROL 選擇目標欄位]窗口中，您可以在兩個目標欄位類別之間進行選擇：
* [!UICONTROL 選取身分命名空間]:使用此選項可將身分識別命 [!DNL Platform] 名空間對應至身 [!DNL Braze] 分識別命名空間。
* [!UICONTROL 選取自訂屬性]:使用此選項可將XDM屬性對應至您在 [!DNL Braze] 帳戶中定義的自訂 [!DNL Braze] 屬性。<br> 您也可以使用此選項，將現有的XDM屬性重新命名為 [!DNL Braze]。例如，將`lastName` XDM屬性對應至[!DNL Braze]中的自訂`Last_Name`屬性，將在[!DNL Braze]中建立`Last_Name`屬性（如果尚未存在），並將`lastName` XDM屬性對應至該屬性。

![佈雷茲目標對應欄位](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

選擇目標欄位，然後按一下&#x200B;**[!UICONTROL 選擇]**。

您現在應該會在清單中看到欄位對應。

![Braze目標映射完成](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

若要新增更多對應，請重複先前的步驟。

## 對應範例 {#mapping-example}

假設您的XDM設定檔結構和[!DNL Braze]例項包含下列屬性和身分：

|  | XDM設定檔結構 | [!DNL Braze] 例項 |
|---|---|---|
| 屬性 | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| 身分 | <ul><li>電子郵件</code></li><li>Google廣告ID(GAID)</code></li><li>廣告商適用的Apple ID(IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

正確的對應如下所示：

![佈雷茲目標對應範例](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## 匯出的資料 {#exported-data}

要驗證資料是否已成功導出到[!DNL Braze]目標，請檢查[!DNL Braze]帳戶。 [!DNL Adobe Experience Platform] 區段會匯出 [!DNL Braze] 至屬 `AdobeExperiencePlatformSegments` 性下。

## 資料使用與控管 {#data-usage-governance}

處理資料時，所有[!DNL Adobe Experience Platform]目標都符合資料使用策略。 有關[!DNL Adobe Experience Platform]如何實施資料控管的詳細資訊，請參閱[資料控管概述](../../../data-governance/home.md)。
