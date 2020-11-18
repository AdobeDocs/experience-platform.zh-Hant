---
keywords: airship tags;airship destination
title: 飛艇標籤目的地
seo-title: 飛艇標籤目的地
description: 順暢地將Adobe觀眾資料傳遞至Axphiry做為觀眾標籤，以便在Axphiry中定位。
seo-description: 順暢地將Adobe觀眾資料傳遞至Axphiry做為觀眾標籤，以便在Axphiry中定位。
translation-type: tm+mt
source-git-commit: 4b1bf5bbce57a22529c5d025c5bae10557400d54
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 1%

---


# （測試版）目 [!DNL Airship Tags] 標 {#airship-tags-destination}

>[!IMPORTANT]
>
>Adobe [!DNL Airship Tags] Experience Platform中的目的地目前為beta版。 文件和功能可能會有所變更。

## 概述

[!DNL Airship] 是領先的客戶互動平台，可協助您在客戶生命週期的每個階段，為您的使用者提供有意義的個人化全通道訊息。

此整合會將Adobe Experience Platform區段資料作為標籤傳遞 [!DNL Airship] 至 [Tags](https://docs.airship.com/guides/audience/tags/) ，以進行定位或觸發。

若要進一步了 [!DNL Airship]解，請參 [閱Axphire Docs](https://docs.airship.com)。


>[!TIP]
>
>此檔案頁面由團隊建 [!DNL Airship] 立。 如需任何查詢或更新要求，請直接在 [support.axish.com與他們聯絡](https://support.airship.com/)。

## 必要條件

您必須先下列步驟，才能將Adobe Experience Platform區 [!DNL Airship]段傳送至：

* 在專案中建立標籤 [!DNL Airship] 群組。
* 產生用於驗證的承載Token。

>[!TIP]
> 
>如果您 [!DNL Airship] 尚未透過 [此註冊連結](https://go.airship.eu/accounts/register/plan/starter/) ，請建立帳戶。

### 標籤群組

Adobe Experience Platform中的區段概念類似於 [Tags](https://docs.airship.com/guides/audience/tags/) in Airship，在實作上略有不同。 此整合會將使用者在Experience Platform區 [段中的會籍狀態對應至標籤的存在與否](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins)[!DNL Airship] 狀態。 例如，在變更為的「平台」區 `xdm:status` 段中 `realized`，標籤會新增至此 [!DNL Airship] 描述檔對應至的頻道或指名用戶。 如果變 `xdm:status` 更為 `exited`，則標籤會移除。

若要啟用此整合，請建立 *名稱中的標* 記群組 [!DNL Airship]`adobe-segments`。

>[!IMPORTANT]
>
>建立新標籤群組時 **請勿勾選** 「[!DNL Allow these tags to be set only from your server]」的選項按鈕。 這麼做會導致Adobe標籤整合失敗。

如需 [建立標籤群組的指示](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) ，請參閱管理標籤群組。

### 持牌代號

1. 前往 **[!UICONTROL Airship儀表板]** 中的「設 **[!UICONTROL 定]** 」「API與整合」，並 [](https://go.airship.com)**** 在左側功能表中選取Token。
1. 按一 **[!UICONTROL 下「建立Token]**」。
1. 為您的Token提供好記的名稱，例如「Adobe Tags Destination」，並選取「All Access」（完整存取）做為角色。
1. 按一 **[!UICONTROL 下「建立Token]** 」，並將詳細資訊儲存為機密。


## 使用個案

為協助您更清楚瞭解您應如何及何時使用目標，以下是Adobe Experience Platform客戶可使用此目標解決的 [!DNL Airship Tags] 範例使用案例。

### 使用案例#1

零售商或娛樂平台可建立忠誠客戶的使用者個人檔案，並將這些細分傳遞至行動宣傳 [!DNL Airship] 的訊息鎖定目標。

### 使用案例#2

當使用者進入或離開Adobe Experience Platform中的特定細分時，即時觸發一對一訊息。

例如，零售商在Platform中設定牛仔品牌專屬區隔。 當某人將牛仔褲偏好設定設為特定品牌時，該零售商現在可以觸發行動訊息。

## 連線至 [!DNL Airship Tags] {#connect-airship-tags}

1. 在「 **[!UICONTROL 目標]** >目錄 **[!UICONTROL 」中，捲動至「]**&#x200B;行動參與 **** 」類別。 選擇 **[!DNL Airship Tags]**，然後選擇 **[!UICONTROL 配置]**。

   >[!NOTE]
   >
   >如果此目標已存在連接，您可以在目標卡上看到 **[!UICONTROL 「激活]** 」按鈕。 有關「激活」( **[!UICONTROL Activate]** )和「配置」( **[!UICONTROL Configure]**)之間差異的詳細資訊，請參 [閱目標工作區文檔的「目錄](/help/rtcdp/destinations/destinations-workspace.md#catalog) 」(Catalog)部分。

   ![連接至飛艇標籤](/help/rtcdp/destinations/assets/airship-tags-in-catalog.png)

2. 在「 **Account** 」（帳戶）步驟中 [!DNL Airship Tags] ，如果您先前已設定連線至您的目的地，請選取「 **** Existing Account」（現有帳戶）並選取您現有的連線。 或者，您可以選 **[!UICONTROL 擇「新帳戶]** 」來設定新連線 [!DNL Airship Tags]。 選 **[!UICONTROL 取「連線至目的地]** 」，使用您從控制面板產生的 [!DNL Airship] 不記名Token，將Adobe Experience Platform連線至您的專 [!DNL Airship] 案。

   >[!NOTE]
   >
   >Adobe Experience Platform支援驗證程式中的認證驗證，如果您在帳戶中輸入錯誤的認證，則會顯示錯誤 [!DNL Airship] 訊息。 這可確保您不會以不正確的憑證完成工作流程。

   ![連接至飛艇標籤](/help/rtcdp/destinations/assets/airshiptags1-connect-account.png)

3. 在確認您的認證並將Adobe Experience Platform連線至您的專案後，您就可以選取「下 [!DNL Airship] 一 **[!UICONTROL 步」以繼續]** 設定 **** 。

4. 在「驗 **[!UICONTROL 證]** 」步驟中，輸入啟 **[!UICONTROL 動流程的「名稱]** 」 **[!UICONTROL 和「說明]** 」。 <br> 此外，在此步驟中，您可以選擇美國或歐盟的資料中心，具體取決於哪 [!DNL Airship] 個資料中心適用於此目標。 最後，選取一或多個將資料匯出至目的地的行銷使用案例。 您可以從Adobe定義的行銷使用案例中選擇，也可以自行建立。 有關行銷使用案例的詳細資訊，請參 [閱即時CDP中的資料治理頁](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 如需個別Adobe定義之行銷使用案例的詳細資訊，請參閱「資 [料使用政策」概觀](/help/data-governance/policies/overview.md#core-actions)。 <br> 在填 **[!UICONTROL 入上述欄位後]** ，選取「建立目標」。

   ![連接至飛艇標籤](/help/rtcdp/destinations/assets/airshiptags2-select-domain.png)

5. 您的目標現在已建立。 如果您想 **[!UICONTROL 稍後啟動區段]** ，可以選取「儲存並退出」，或選取「下一步 **** 」以繼續工作流程，並選取要啟動的區段。 在這兩種情況下，請參閱下一 [節「啟動區段](#activate-segments)」，以瞭解其餘的工作流程。

## 啟用區段 {#activate-segments}

若要啟用區段 [!DNL Airship Tags]至，請遵循下列步驟：

1. 在「 **[!UICONTROL 目標>瀏覽]**」中，選 [!DNL Airship Tags] 取您要啟用區段的目標。 ![activate-flow](/help/rtcdp/destinations/assets/airship-tags-activate1.png)
2. 按一下目標的名稱。 這會帶您進入「啟動」流程。
請注意，如果目的地已有啟動流程，您可以看到目前傳送至目的地的區段。 選取 **[!UICONTROL 右側邊欄]** 「編輯啟動」，然後依照下列步驟修改啟動詳細資訊。  ![activate-flow](/help/rtcdp/destinations/assets/airship-tags-activate2.png)
3. 選擇 **[!UICONTROL 激活]**;
4. 在「啟 **[!UICONTROL 動目標]** 」工作流程的「選 **[!UICONTROL 取區段」頁面上，選取要傳送的區段]**[!DNL Airship Tags]。
   ![區段到目的地](/help/rtcdp/destinations/assets/airshiptags3-select-segments.png)
5. 在映 **[!UICONTROL 射步驟]** ，從 [](https://docs.adobe.com/content/help/zh-Hant/experience-platform/xdm/home.html) XDM架構中選擇要映射到目標架構的屬性和標識。 選擇 **[!UICONTROL 添加新映射]** ，以瀏覽方案並將其映射到相應的目標標識。
   ![身份映射初始螢幕](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] 可以在代表裝置例項（例如iPhone）的頻道上設定標籤，或指名用戶，其將使用者的所有裝置對應至通用識別碼（例如客戶ID）。 如果您的架構中有純文字（未雜湊）電子郵件地址作為主要身分識別，請在「來源屬性」中選取電子郵件欄位，並在「 ****[!DNL Airship]****Target身分識別」下方的右欄中對應至指名的使用者，如下所示。
   ![指名用戶映](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)射：對於應映射到渠道（即設備）的標識符，請根據源映射到相應的渠道。 下列影像顯示如何將Google廣告ID對應至 [!DNL Airship] Android頻道。
   ![連接至飛艇標籤](/help/rtcdp/destinations/assets/airshiptags4-select-source-identity.png)
   ![連接至飛艇標籤](/help/rtcdp/destinations/assets/airshiptags5-select-target-identity.png)
   ![頻道對應](/help/rtcdp/destinations/assets/airshiptags6-mappingoption1.png)

6. 在「區 **[!UICONTROL 段排程]** 」頁面上，目前停用排程。 按一 **[!UICONTROL 下「下]** 一步」(Next)以繼續檢閱步驟。
7. 在「審 **[!UICONTROL 閱]** 」頁面上，您可以看到您所選項目的摘要。 選擇 **[!UICONTROL 取消]** ，以劃分流程，選擇 **[!UICONTROL 返回]** ，修改設定，或選擇完 **[!UICONTROL 成]** ，確認選擇並開始向目標發送資料。

>[!IMPORTANT]
>
>在此步驟中，Adobe Experience Platform會檢查資料使用政策違規。 以下是違反原則的範例。 除非您解決違規問題，否則無法完成區段啟動工作流程。 有關如何解決違反策略的資訊，請參 [閱資料治理文檔部分](/help/rtcdp/privacy/data-governance-overview.md#enforcement) 中的策略實施。

![確認選擇](/help/rtcdp/destinations/assets/data-policy-violation.png)

如果未檢測到任何違反策略的情況，請選擇「完 **[!UICONTROL 成]** 」以確認您的選擇並開始向目標發送資料。

![確認選擇](/help/rtcdp/destinations/assets/Airship-tags-review.png)


## 資料使用與治理 {#data-usage-governance}

處理 [!DNL Adobe Experience Platform] 資料時，所有目標都符合資料使用原則。 有關如何實施資料 [!DNL Adobe Experience Platform] 治理的詳細資訊，請 [參閱即時CDP中的資料治理](/help/rtcdp/privacy/data-governance-overview.md)。

