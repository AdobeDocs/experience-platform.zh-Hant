---
keywords: 飛艇標籤；飛艇目的地
title: 飛艇標籤連接
description: 順暢地將Adobe觀眾資料傳遞至Axphiry做為觀眾標籤，以便在Axphiry中定位。
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 1%

---


# （測試版）[!DNL Airship Tags]連接{#airship-tags-destination}

>[!IMPORTANT]
>
>Adobe Experience Platform中的[!DNL Airship Tags]目標目前正在測試中。 文件和功能可能會有所變更。

## 概述

[!DNL Airship] 是領先的客戶互動平台，可協助您在客戶生命週期的每個階段，為您的使用者提供有意義的個人化全通道訊息。

此整合會將Adobe Experience Platform區段資料以[Tags](https://docs.airship.com/guides/audience/tags/)的形式傳入[!DNL Airship]中，以用於定位或觸發。

若要進一步瞭解[!DNL Airship]，請參閱[飛艇檔案](https://docs.airship.com)。


>[!TIP]
>
>此文檔頁面由[!DNL Airship]團隊建立。 如需任何查詢或更新要求，請直接與[support.airship.com](https://support.airship.com/)聯絡。

## 先決條件

您必須先執行下列動作，才能將Adobe Experience Platform區段傳送至[!DNL Airship]:

* 在[!DNL Airship]專案中建立標籤群組。
* 產生用於驗證的承載Token。

>[!TIP]
> 
>如果您尚未透過[此註冊連結](https://go.airship.eu/accounts/register/plan/starter/)建立[!DNL Airship]帳戶。

### 標籤群組

Adobe Experience Platform中區段的概念與Airship中的[Tags](https://docs.airship.com/guides/audience/tags/)類似，在實作上略有不同。 此整合會將使用者在Experience Platform區段](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins)中的[會籍狀態對應至存在或不存在[!DNL Airship]標籤。 例如，在`xdm:status`變更為`realized`的「平台」區段中，標籤會新增至[!DNL Airship]頻道或此描述檔已映射至的指名用戶。 如果`xdm:status`變更為`exited`，則會移除標籤。

若要啟用此整合，請在[!DNL Airship]中建立名為`adobe-segments`的&#x200B;*標籤群組*。

>[!IMPORTANT]
>
>建立新標籤群組&#x200B;**請勿勾選**&#x200B;顯示&quot;[!DNL Allow these tags to be set only from your server]&quot;的選項按鈕。 這麼做會導致Adobe標籤整合失敗。

如需建立標籤群組的指示，請參閱[管理標籤群組](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups)。

### 持牌代號

前往[Airship儀表板](https://go.airship.com)中的&#x200B;**[!UICONTROL Settings]**&quot; **[!UICONTROL &quot; APIs &amp; Integrations]**，然後在左側功能表中選擇&#x200B;**[!UICONTROL Token]**。

按一下「建立Token **[!UICONTROL 」。]**

為您的Token提供好記的名稱，例如「Adobe Tags Destination」，並選取「All Access」（完整存取）做為角色。

按一下「建立Token ]**」，並將詳細資訊儲存為機密。**[!UICONTROL 

## 使用個案

為協助您進一步瞭解應如何及何時使用[!DNL Airship Tags]目標，以下是Adobe Experience Platform客戶可使用此目標解決的範例使用案例。

### 使用案例#1

零售商或娛樂平台可以建立忠誠客戶的使用者個人檔案，並將這些細分傳入[!DNL Airship]，以便在行動宣傳上鎖定訊息。

### 使用案例#2

當使用者進入或離開Adobe Experience Platform中的特定細分時，即時觸發一對一訊息。

例如，零售商在Platform中設定牛仔品牌專屬區隔。 當某人將牛仔褲偏好設定設為特定品牌時，該零售商現在可以觸發行動訊息。

## 連接到[!DNL Airship Tags] {#connect-airship-tags}

在&#x200B;**[!UICONTROL 目標]** > **[!UICONTROL 目錄]**&#x200B;中，滾動到&#x200B;**[!UICONTROL 移動參與]**&#x200B;類別。 選擇&#x200B;**[!DNL Airship Tags]**，然後選擇&#x200B;**[!UICONTROL 配置]**。

>[!NOTE]
>
>如果已存在與此目標的連接，您可以在目標卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按鈕。 有關&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之間差異的詳細資訊，請參閱目標工作區文檔的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

![連接至飛艇標籤](../../assets/catalog/mobile-engagement/airship-tags/catalog.png)

在&#x200B;**Account**&#x200B;步驟中，如果您先前已設定到[!DNL Airship Tags]目標的連接，請選擇&#x200B;**[!UICONTROL Existing Account]**&#x200B;並選擇您的現有連接。 或者，您可以選擇&#x200B;**[!UICONTROL 新帳戶]**&#x200B;來設定到[!DNL Airship Tags]的新連接。 選擇&#x200B;**[!UICONTROL 連線至目的地]**，以使用您從[!DNL Airship]控制面板產生的承載Token，將Adobe Experience Platform連線至您的[!DNL Airship]專案。

>[!NOTE]
>
>Adobe Experience Platform支援驗證程式中的認證驗證，如果您為[!DNL Airship]帳戶輸入錯誤的認證，則會顯示錯誤訊息。 這可確保您不會以不正確的憑證完成工作流程。

![連接至飛艇標籤](../../assets/catalog/mobile-engagement/airship-tags/connect-account.png)

在確認您的認證並將Adobe Experience Platform連線至您的[!DNL Airship]專案後，您可以選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續&#x200B;**[!UICONTROL Setup]**&#x200B;步驟。

在&#x200B;**[!UICONTROL 驗證]**&#x200B;步驟中，輸入激活流程的&#x200B;**[!UICONTROL 名稱]**&#x200B;和&#x200B;**[!UICONTROL 說明]**。

此外，在此步驟中，您可以選擇美國或歐盟的資料中心，具體取決於哪個[!DNL Airship]資料中心適用於此目標。 最後，選擇一個或多個將其資料導出到目標的&#x200B;**[!UICONTROL 行銷操作]**。 您可以從Adobe定義的行銷動作中選擇，也可以自行建立。 如需行銷動作的詳細資訊，請參閱[資料使用政策概述](../../../data-governance/policies/overview.md)。

在填寫上述欄位後，選擇「建立目標」。****

![連接至飛艇標籤](../../assets/catalog/mobile-engagement/airship-tags/select-domain.png)

您的目標現在已建立。 如果您想稍後啟動區段，可以選取&#x200B;**[!UICONTROL 儲存並退出]**，或選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續工作流程並選取要啟動的區段。 在這兩種情況下，請參閱工作流程的下一節[啟動區段](#activate-segments)。

## 啟用區段{#activate-segments}

若要將區段啟用至[!DNL Airship Tags]，請遵循下列步驟：

在&#x200B;**[!UICONTROL 目標>瀏覽]**&#x200B;中，選取您要啟用區段的[!DNL Airship Tags]目標。

![activate-flow](../../assets/catalog/mobile-engagement/airship-tags/browse.png)

按一下目標的名稱。 這會帶您進入「啟動」流程。

請注意，如果目的地已有啟動流程，您可以看到目前傳送至目的地的區段。 選擇右側導軌中的&#x200B;**[!UICONTROL 編輯激活]** ，然後按照以下步驟修改激活詳細資訊。

![activate-flow](../../assets/catalog/mobile-engagement/airship-tags/activate.png)

選擇&#x200B;**[!UICONTROL 激活]**。 在&#x200B;**[!UICONTROL 啟動目標]**&#x200B;工作流程的&#x200B;**[!UICONTROL 選擇區段]**&#x200B;頁面上，選取要傳送至[!DNL Airship Tags]的區段。

![區段到目的地](../../assets/catalog/mobile-engagement/airship-tags/select-segments.png)

在&#x200B;**[!UICONTROL 映射]**&#x200B;步驟中，從[XDM](../../../xdm/home.md)模式中選擇要映射到目標模式的屬性和標識。 選擇&#x200B;**[!UICONTROL 添加新映射]**&#x200B;以瀏覽方案並將其映射到相應的目標標識。

![身份映射初始螢幕](../../assets/catalog/mobile-engagement/airship-tags/identity-mapping.png)

[!DNL Airship] 可以在代表裝置例項（例如iPhone）的頻道上設定標籤，或指名用戶，其將使用者的所有裝置對應至通用識別碼（例如客戶ID）。如果您的架構中具有純文字檔案（未散列）電子郵件地址作為主要標識，請在&#x200B;**[!UICONTROL 源屬性]**&#x200B;中選擇電子郵件欄位，並映射到&#x200B;**[!UICONTROL 目標標識]**&#x200B;下右列中的[!DNL Airship]指名用戶，如下所示。

![指名用戶映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

對於應映射到頻道（即設備）的標識符，請根據源映射到相應的頻道。 下列影像顯示如何將Google廣告ID對應至[!DNL Airship] Android頻道。

![連接至飛艇標](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![簽連接至飛艇標](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![簽通道映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

在&#x200B;**[!UICONTROL 區段排程]**&#x200B;頁面上，排程目前停用。 按一下&#x200B;**[!UICONTROL Next]**&#x200B;繼續查看步驟。

在&#x200B;**[!UICONTROL Review]**&#x200B;頁面上，您可以看到您所選內容的摘要。 選擇&#x200B;**[!UICONTROL 取消]**&#x200B;以劃分流程，選擇&#x200B;**[!UICONTROL 返回]**&#x200B;以修改設定，或選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以確認選擇並開始向目標發送資料。

>[!IMPORTANT]
>
>在此步驟中，Adobe Experience Platform會檢查資料使用政策違規。 以下是違反原則的範例。 除非您解決違規問題，否則無法完成區段啟動工作流程。 有關如何解決策略違規的資訊，請參見資料治理文檔部分中的[策略實施](../../../data-governance/enforcement/auto-enforcement.md)。

![確認選擇](../../assets/common/data-policy-violation.png)

如果未檢測到任何違反策略的情況，請選擇&#x200B;**[!UICONTROL 完成]**&#x200B;以確認選擇並開始向目標發送資料。

![確認選擇](../../assets/catalog/mobile-engagement/airship-tags/review.png)


## 資料使用與治理{#data-usage-governance}

所有[!DNL Adobe Experience Platform]目標在處理資料時都符合資料使用原則。 有關[!DNL Adobe Experience Platform]如何實施資料治理的詳細資訊，請參閱[資料治理概述](../../../data-governance/home.md)。

