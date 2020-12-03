---
keywords: airship attributes;airship destination
title: 飛艇屬性目標
seo-title: 飛艇屬性目標
description: 順暢地將Adobe觀眾資料傳遞至Ansphiry，做為觀眾屬性，以便在Ansphiry中定位。
seo-description: 順暢地將Adobe觀眾資料傳遞至Ansphiry，做為觀眾屬性，以便在Ansphiry中定位。
translation-type: tm+mt
source-git-commit: 24c8dd0f01d7ea14b2fa5827722e797bd209f50c
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 1%

---


# （測試版）目 [!DNL Airship Attributes] 標 {#airship-attributes-destination}

>[!IMPORTANT]
>
>Adobe [!DNL Airship Attributes] Experience Platform中的目的地目前為beta版。 文件和功能可能會有所變更。

## 概述 {#overview}

[!DNL Airship] 是領先的客戶互動平台，可協助您在客戶生命週期的每個階段，為您的使用者提供有意義的個人化全通道訊息。

此整合會將Adobe描述檔資料傳 [!DNL Airship] 入為 [屬性](https://docs.airship.com/guides/audience/attributes/) ，以進行定位或觸發。

若要進一步了 [!DNL Airship]解，請參 [閱Axphire Docs](https://docs.airship.com)。


>[!TIP]
>
>此檔案頁面由團隊建 [!DNL Airship] 立。 如需任何查詢或更新要求，請直接在 [support.axish.com與他們聯絡](https://support.airship.com/)。

## 先決條件 {#prerequisites}

您必須先： [!DNL Airship]

* 在專案中啟用 [!DNL Airship] 屬性。
* 產生用於驗證的承載Token。

>[!TIP]
>
>如果您 [!DNL Airship] 尚未透過 [此註冊連結](https://go.airship.eu/accounts/register/plan/starter/) ，請建立帳戶。

### 啟用屬性 {#enable-attributes}

Adobe Experience Platform描述檔屬性類似於屬性， [!DNL Airship] 使用本頁下面進一步說明的對應工具，可在Platform中輕鬆地彼此對應。

[!DNL Airship] 專案有數個預先定義和預設屬性。 如果您有自訂屬性，則必須先定義 [!DNL Airship] 它。 如需詳 [細資訊，請參閱設定和管理屬性](https://docs.airship.com/tutorials/audience/attributes/) 。

### 持牌代號 {#bearer-token}

前往 **[!UICONTROL Airship儀表板]** 中的「設 **[!UICONTROL 定]** 」「API與整合」，並 [](https://go.airship.com)**** 在左側功能表中選取Token。

按一 **[!UICONTROL 下「建立Token]**」。

為您的Token提供好記的名稱，例如「Adobe屬性目的地」，並選取「完整存取權」做為角色。

按一 **[!UICONTROL 下「建立Token]** 」，並將詳細資訊儲存為機密。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用目標，以下是Adobe Experience Platform客戶可使用此目標解決的 [!DNL Airship Attributes] 範例使用案例。

### 使用案例#1

運用在Adobe Experience Platform中收集的個人檔案資料，在任何通道中個人化訊息和豐 [!DNL Airship]富內容。 例如，利用描述 [!DNL Experience Platform] 檔資料在中設定位置屬性 [!DNL Airship]。 這可讓酒店品牌針對每位使用者顯示最近的酒店位置影像。

### 使用案例#2

運用Adobe Experience Platform的屬性進一步豐富個人檔案， [!DNL Airship] 並將其與SDK或預測性資料 [!DNL Airship] 結合。 例如，零售商可以建立包含忠誠度狀態和位置資料（來自平台的屬性）的區段，並預計會流失資料，以傳送高針對性訊息給居住在內華達州拉斯維加斯的黃金忠誠度狀態使用者，而且攪動的可能性很高。 [!DNL Airship]

## 連線至 [!DNL Airship Attributes] {#connect-airship-attributes}

在「 **[!UICONTROL 目標]** >目錄 **[!UICONTROL 」中，捲動至「]**&#x200B;行動參與 **** 」類別。 選擇 **[!DNL Airship Attributes]**，然後選擇 **[!UICONTROL 配置]**。

>[!NOTE]
>
>如果此目標已存在連接，您可以在目標卡上看到 **[!UICONTROL 「激活]** 」按鈕。 有關「激活」( **[!UICONTROL Activate]** )和「配置」( **[!UICONTROL Configure]**)之間差異的詳細資訊，請參 [閱目標工作區文檔的「目錄](../../ui/destinations-workspace.md#catalog) 」(Catalog)部分。

![連接至飛艇屬性](../../assets/catalog/mobile-engagement/airship/catalog.png)

在「 **Account** 」（帳戶）步驟中 [!DNL Airship Attributes] ，如果您先前已設定連線至您的目的地，請選取「 **** Existing Account」（現有帳戶）並選取您現有的連線。 或者，您可以選 **[!UICONTROL 擇「新帳戶]** 」來設定新連線 [!DNL Airship Attributes]。 選 **[!UICONTROL 取「連線至目的地]** 」，使用您從控制面板產生的 [!DNL Airship] 不記名Token，將Adobe Experience Platform連線至您的專 [!DNL Airship] 案。

>[!NOTE]
>
>Adobe Experience Platform支援驗證程式中的認證驗證，如果您在帳戶中輸入錯誤的認證，則會顯示錯誤 [!DNL Airship] 訊息。 這可確保您不會以不正確的憑證完成工作流程。

![連接至飛艇屬性](../../assets/catalog/mobile-engagement/airship/connect.png)

在確認您的認證並將Adobe Experience Platform連線至您的專案後，您就可以選取「下 [!DNL Airship] 一 **[!UICONTROL 步」以繼續]** 設定 **** 。

在「驗 **[!UICONTROL 證]** 」步驟中，輸入啟 **[!UICONTROL 動流程的「名稱]** 」 **[!UICONTROL 和「說明]** 」。

此外，在此步驟中，您可以選擇美國或歐盟的資料中心，具體取決於哪 [!DNL Airship] 個資料中心適用於此目標。 最後，選取一或多個將資料匯出至目的地的行銷使用案例。 您可以從Adobe定義的行銷使用案例中選擇，也可以自行建立。 有關行銷使用案例的詳細資訊，請參 [閱即時CDP中的資料治理頁](../../../rtcdp/privacy/data-governance-overview.md#destinations) 。 如需個別Adobe定義之行銷使用案例的詳細資訊，請參閱「資 [料使用政策」概觀](../../../data-governance/policies/overview.md#core-actions)。

在填 **[!UICONTROL 入上述欄位後]** ，選取「建立目標」。

![連接至飛艇屬性](../../assets/catalog/mobile-engagement/airship/select-domain.png)

您的目標現在已建立。 如果您想 **[!UICONTROL 稍後啟動區段]** ，可以選取「儲存並退出」，或選取「下一步 **** 」以繼續工作流程，並選取要啟動的區段。 在這兩種情況下，請參閱下一 [節「啟動區段](#activate-segments)」，以瞭解其餘的工作流程。

## 啟用區段 {#activate-segments}

若要啟用區段 [!DNL Airship Attributes]至，請遵循下列步驟：

在「 **[!UICONTROL 目標>瀏覽]**」中，選 [!DNL Airship Attributes] 取您要啟用區段的目標。

![activate-flow](../../assets/catalog/mobile-engagement/airship/browse.png)

按一下目標的名稱。 這會帶您進入「啟動」流程。

請注意，如果目的地已有啟動流程，您可以看到目前傳送至目的地的區段。 選取 **[!UICONTROL 右側邊欄]** 「編輯啟動」，然後依照下列步驟修改啟動詳細資訊。

![activate-flow](../../assets/catalog/mobile-engagement/airship/activate.png)

選擇「 **[!UICONTROL 啟動]**」。 在「啟 **[!UICONTROL 動目標]** 」工作流程的「選 **[!UICONTROL 取區段」頁面上，選取要傳送的區段]**[!DNL Airship Attributes]。

![區段到目的地](../../assets/catalog/mobile-engagement/airship/select-segments.png)

在映 **[!UICONTROL 射步驟]** ，從 [](../../../xdm/home.md) XDM架構中選擇要映射到目標架構的屬性和標識。 選擇 **[!UICONTROL 添加新映射]** ，以瀏覽方案並將其映射到相應的目標標識。

![身份映射初始螢幕](../../assets/catalog/mobile-engagement/airship/identity-mapping.png)

[!DNL Airship] 屬性可以在代表裝置例項（例如iPhone）的頻道上設定，或指名用戶（其將使用者的所有裝置對應至通用識別碼，例如客戶ID）上。 如果您的架構中有純文字（未雜湊）電子郵件地址作為主要身分識別，請在「來源屬性」中選取電子郵件欄位，並在「 ****[!DNL Airship]**** Target身分識別」下方的右欄中對應至指名的使用者，如下所示。

![指名用戶映射](../../assets/catalog/mobile-engagement/airship/mapping.png)

對於應映射到頻道（即設備）的標識符，請根據源映射到相應的頻道。 下圖顯示如何建立兩個映射：

* iOS頻道的IDFA iOS廣 [!DNL Airship] 告ID
* Adobe屬 `fullName` 性為「 [!DNL Airship] 完整名稱」屬性

>[!NOTE]
>
>為屬性映射選擇目標欄位時，請使用 [!DNL Airship] 顯示在儀表板中的用戶友好名稱。

**地圖識別**

選擇源欄位：

![連接至飛艇屬性](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

選擇目標欄位：

![連接至飛艇屬性](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**地圖屬性**

選擇源屬性：

![選擇源欄位](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

選擇目標屬性：

![選取目標欄位](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

驗證映射：

![頻道對應](../../assets/catalog/mobile-engagement/airship/mapping.png)

在「區 **[!UICONTROL 段排程]** 」頁面上，目前停用排程。 按一 **[!UICONTROL 下「下]** 一步」(Next)以繼續檢閱步驟。

![目前已停用排程](../../assets/catalog/mobile-engagement/airship/scheduling.png)

在「審 **[!UICONTROL 閱]** 」頁面上，您可以看到您所選項目的摘要。 選擇 **[!UICONTROL 取消]** ，以劃分流程，選擇 **[!UICONTROL 返回]** ，修改設定，或選擇完 **[!UICONTROL 成]** ，確認選擇並開始向目標發送資料。

>[!IMPORTANT]
>
>在此步驟中，Adobe Experience Platform會檢查資料使用政策違規。 以下是違反原則的範例。 除非您解決違規問題，否則無法完成區段啟動工作流程。 有關如何解決違反策略的資訊，請參 [閱資料治理文檔部分](../../../rtcdp/privacy/data-governance-overview.md#enforcement) 中的策略實施。

![確認選擇](../../assets/common/data-policy-violation.png)

如果未檢測到任何違反策略的情況，請選擇「完 **[!UICONTROL 成]** 」以確認您的選擇並開始向目標發送資料。

![審查](../../assets/catalog/mobile-engagement/airship/review.png)

## 資料使用與治理 {#data-usage-governance}

處理 [!DNL Adobe Experience Platform] 資料時，所有目標都符合資料使用原則。 有關如何實施資料 [!DNL Adobe Experience Platform] 治理的詳細資訊，請 [參閱即時CDP中的資料治理](../../../rtcdp/privacy/data-governance-overview.md)。
