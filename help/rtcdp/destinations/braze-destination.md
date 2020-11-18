---
keywords: mobile; braze; messaging;
title: Braze Destination
seo-title: Braze Destination
description: Braze是一個全面的客戶互動平台，為客戶和他們喜愛的品牌提供相關且值得回味的體驗。
seo-description: Braze是一個全面的客戶互動平台，為客戶和他們喜愛的品牌提供相關且值得回味的體驗。
translation-type: tm+mt
source-git-commit: 9126a9b3a27aa0a0ecefb5d490475423d7840791
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 1%

---


# （測試版）目 [!DNL Braze] 標

>[!IMPORTANT]
>
>Adobe Experience Platform中的Braze目標目前正在測試中。 文件和功能可能會有所變更。

## 概述 {#overview}

目標 [!DNL Braze] 可協助您傳送描述檔資料 [!DNL Braze]。

[!DNL Braze] 是全方位的客戶互動平台，可為客戶與他們喜愛的品牌提供相關且值得回味的體驗。

若要傳送描述檔資 [!DNL Braze]料至，您必須先連線至目的地。

## 目標規格 {#destination-specs}

請注意下列目標專屬的詳細 [!DNL Braze] 資訊：

* 只要您將任 [何身分](../../identity-service/namespaces.md) ，就可 [!DNL Braze] 以將其映射至目的地 [!DNL Braze][`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation)。
* [!DNL Adobe Experience Platform] 區段會匯出至 [!DNL Braze] 屬性下 `AdobeExperiencePlatformSegments` 方。

## 使用案例 {#use-cases}

身為行銷人員，我想鎖定行動參與目標的使用者，並內建區段 [!DNL Adobe Experience Platform]。 此外，我希望在中更新細分和個人檔案時，根據個人檔案的屬 [!DNL Adobe Experience Platform] 性，為他們提供個人化體驗 [!DNL Adobe Experience Platform]。

## 匯出類型 {#export-type}

**[!DNL Profile-based]** -您要匯出區段的所有成員，以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)和／或身分，視您的欄位對應而定。
[!DNL Adobe Experience Platform] 區段會匯出至 [!DNL Braze] 屬性下 `AdobeExperiencePlatformSegments` 方。


## 連接到目標 {#connect-destination}

1. 在「連 **[!UICONTROL 接]** >目 **[!UICONTROL 標]**」中，選 [!DNL Braze]擇並選 **[!UICONTROL 擇配置]**。

   ![配置Braze目標](assets/braze-destination-configure.png)

   >[!NOTE]
   >
   >如果此目標已存在連接，您可以在目標卡上看到 **[!UICONTROL 「激活]** 」按鈕。 有關「激活」( **[!UICONTROL Activate]** )和「配置」( **[!UICONTROL Configure]**)之間差異的詳細資訊，請參 [閱目標工作區文檔的「目錄](../destinations/destinations-workspace.md#catalog) 」(Catalog)部分。
   >
   >![啟動Braze Destination](assets/braze-destination-activate.png)

1. 在「帳 [!UICONTROL 戶] 」步驟中 [!DNL Braze] ，您需要提供您的帳戶Token。 這是你的 [!DNL Braze][!DNL API] 鑰匙。 您可以在這裡找到有關如何獲得密鑰的詳 [!DNL API] 細說明： [REST API金鑰概觀](https://www.braze.com/docs/api/api_key/)。 輸入標籤，然後按一 **[!UICONTROL 下「連線至目的地」]**。
   ![Braze目標帳戶步驟](assets/braze-destination-account.png)

1. 按&#x200B;**[!UICONTROL 「下一步」]**。

1. 在「驗 [!UICONTROL 證] 」步驟中，您需要輸入連接詳 [!DNL Braze] 細資訊：
   * **[!UICONTROL 名稱]**:輸入您將來識別此目的地的名稱。
   * **[!UICONTROL 說明]**:輸入說明，以幫助您識別未來的目標。
   * **[!UICONTROL 端點實例]**:詢問您的 [!DNL Braze] 代表您應使用哪個端點實例。
   * **[!UICONTROL 行銷使用案例]**:行銷使用案例會指出資料將匯出至目的地的方式。 您可以從Adobe定義的行銷使用案例中選擇，也可以建立自己的行銷使用案例。 如需行銷使用案例的詳細資訊，請參閱Adobe [Experience Platform中的資料治理](../privacy/data-governance-overview.md#destinations) 頁面。 如需個別Adobe定義之行銷使用案例的詳細資訊，請參閱「資 [料使用政策」概觀](../../data-governance/policies/overview.md#core-actions)。

   ![Braze驗證步驟](assets/braze-destination-authentication.png)

1. 按一 **[!UICONTROL 下建立目標]**。 您的目標現在已建立。 如果您想稍 **[!UICONTROL 後啟動區段，可以按一下「儲存並退出]** 」，或選取「下一步 **** 」以繼續工作流程並選取要啟動的區段。 在這兩種情況下，請參閱下一 [節「啟用區段](#activate-segments)」，以瞭解其餘的工作流程。

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](activate-destinations.md#select-attributes) ，請參閱啟用設定檔和區段至目的地。

## 欄位對應 {#field-mapping}

若要正確地將受眾資料 [!DNL Adobe Experience Platform] 從目的地 [!DNL Braze] 傳送，您必須執行欄位對應步驟。

映射包括在帳戶中的(XDM) [!DNL Experience Data Model] 架構欄位與目標目標目標 [!DNL Platform] 中對應的欄位之間建立連結。

要正確將XDM欄位映射到目標 [!DNL Braze] 欄位，請執行以下步驟：

1. 在「映 [!UICONTROL 射] 」步驟中，單 **[!UICONTROL 擊「添加新映射」]**。

   ![Braze目標添加映射](assets/braze-destination-mapping.png)

2. 在「來 [!UICONTROL 源欄位] 」區段中，按一下空欄位旁的箭頭按鈕。

   ![Braze目標源映射](assets/braze-destination-mapping-source.png)

3. 在「選 [!UICONTROL 擇源欄位] 」窗口中，可以選擇兩種XDM欄位：
   * [!UICONTROL 選擇屬性]:使用此選項可將XDM架構中的特定欄位映射到屬 [!DNL Braze] 性。

      ![Braze目標映射源屬性](assets/braze-destination-mapping-attributes.png)

   * [!UICONTROL 選擇身份名稱空間]:使用此選項可將身分命名空 [!DNL Platform] 間對應至命名空 [!DNL Braze] 間。

      ![Braze目標映射源命名空間](assets/braze-destination-mapping-namespaces.png)
   選擇您的來源欄位，然後按一下「選 **[!UICONTROL 擇」]**。

4. 在「目 [!UICONTROL 標欄位] 」區段中，按一下欄位右側的對應圖示。

   ![Braze目標映射](assets/braze-destination-mapping-target.png)

5. 在「選 [!UICONTROL 擇目標欄位] 」窗口中，您可以在三個目標欄位類別中進行選擇：
   * [!UICONTROL 選擇屬性]:使用此選項可將XDM屬性映射至標準 [!DNL Braze] 屬性。
   * [!UICONTROL 選擇身份名稱空間]:使用此選項可將身份名 [!DNL Platform] 稱空間映射到身份 [!DNL Braze] 名稱空間。
   * [!UICONTROL 選擇自訂屬性]:使用此選項可將XDM屬性映射至您在帳 [!DNL Braze] 戶中定義的自訂 [!DNL Braze] 屬性。
      * 也可以使用此選項將現有XDM屬性更名為 [!DNL Braze]。 例如，將 `lastName` XDM屬性映射到中的自定義 `Last_Name` 屬性 [!DNL Braze]，將在中建立屬性（如果不存在），並將 `Last_Name`[!DNL Braze]`lastName` XDM屬性映射到該屬性。

   ![標籤目標映射欄位](assets/braze-destination-mapping-target-fields.png)

   選擇您的目標欄位，然後按一 **[!UICONTROL 下選擇]**。

6. 您現在應該會在清單中看到欄位對應。

   ![Braze目標映射完成](assets/braze-destination-mapping-complete.png)

7. 要添加更多映射，請重複步驟1到6。

### 範例 {#mapping-example}

假設您的XDM描述檔架構和實例 [!DNL Braze] 包含下列屬性和身份：

|  | XDM配置檔案模式 | [!DNL Braze] 例項 |
|---|---|---|
| 屬性 | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>名字</code></li><li>姓氏</code></li><li>電話號碼</code></li></ul> |
| 身份 | <ul><li>電子郵件</code></li><li>Google廣告ID(GAID)</code></li><li>廣告商專用的Apple ID(IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

正確的對應如下所示：

![Braze目標映射示例](assets/braze-destination-mapping-example.png)

## 匯出的資料 {#exported-data}

若要確認資料是否已成功匯出至目 [!DNL Braze] 標，請檢查您的 [!DNL Braze] 帳戶。 [!DNL Adobe Experience Platform] 區段會匯出至 [!DNL Braze] 屬性下 `AdobeExperiencePlatformSegments` 方。

## 資料使用與治理 {#data-usage-governance}

處理 [!DNL Adobe Experience Platform] 資料時，所有目標都符合資料使用原則。 有關如何實施資料 [!DNL Adobe Experience Platform] 治理的詳細資訊，請 [參閱即時CDP中的資料治理](/help/rtcdp/privacy/data-governance-overview.md)。

