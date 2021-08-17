---
keywords: 飛艇標籤；飛艇目的地
title: Airship標籤連接
description: 流暢地將Adobe對象資料傳遞至Airship，作為對象標籤，以在Airship內鎖定目標。
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 1%

---

# (Beta)[!DNL Airship Tags]連接 {#airship-tags-destination}

>[!IMPORTANT]
>
>Adobe Experience Platform中的[!DNL Airship Tags]目的地目前為測試版。 文件和功能可能會有所變更。

## 概覽

[!DNL Airship] 是領先的客戶參與平台，可協助您在客戶生命週期的每個階段，為使用者提供有意義的個人化全通路訊息。

此整合會將Adobe Experience Platform區段資料以[Tags](https://docs.airship.com/guides/audience/tags/)傳遞至[!DNL Airship]，以鎖定目標或觸發。

若要深入了解[!DNL Airship]，請參閱[Airship檔案](https://docs.airship.com)。


>[!TIP]
>
>此檔案頁面由[!DNL Airship]團隊建立。 有關任何查詢或更新請求，請直接聯繫[support.airship.com](https://support.airship.com/)。

## 先決條件

您必須先以下列方式將Adobe Experience Platform區段傳送至[!DNL Airship]:

* 在[!DNL Airship]專案中建立標籤群組。
* 生成用於驗證的承載令牌。

>[!TIP]
> 
>若尚未透過[此註冊連結](https://go.airship.eu/accounts/register/plan/starter/)建立[!DNL Airship]帳戶。

## 標籤群組

Adobe Experience Platform中的區段概念類似於Airship中的[Tags](https://docs.airship.com/guides/audience/tags/)，在實作上稍有差異。 此整合會將Experience Platform區段](../../../xdm/field-groups/profile/segmentation.md)中使用者[成員資格的狀態對應至[!DNL Airship]標籤是否存在。 例如，在`xdm:status`變更為`realized`的平台區段中，標籤會新增至[!DNL Airship]頻道，或此設定檔對應至的指名使用者。 如果`xdm:status`變更為`exited`，則會移除標籤。

若要啟用此整合，請在[!DNL Airship]中建立&#x200B;*標籤群組*，名為`adobe-segments`。

>[!IMPORTANT]
>
>建立新標籤組&#x200B;**時，請勿勾選顯示「[!DNL Allow these tags to be set only from your server]」的選項按鈕**。 這麼做會導致Adobe標籤整合失敗。

如需建立標籤群組的相關指示，請參閱[管理標籤群組](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups)。

## 生成承載令牌

前往[Airship控制面板](https://go.airship.com)中的&#x200B;**[!UICONTROL 設定]**&quot; **[!UICONTROL API與整合]**，然後在左側功能表中選取&#x200B;**[!UICONTROL Token]**。

按一下「**[!UICONTROL 建立代號]**」。

提供您代號的好記名稱，例如「Adobe標籤目的地」，並為角色選取「完全存取」。

按一下「**[!UICONTROL 建立代號]**」並將詳細資訊儲存為機密。

## 使用案例

為協助您更清楚了解您應如何及何時使用[!DNL Airship Tags]目的地，以下是Adobe Experience Platform客戶可借由使用此目的地解決的範例使用案例。

### 使用案例#1

零售商或娛樂平台可以建立其忠誠客戶的使用者設定檔，並將這些區段傳入[!DNL Airship]，以便在行動行銷活動上進行訊息定位。

### 使用案例#2

當使用者落入或離開Adobe Experience Platform內的特定區段時，即時觸發一對一訊息。

例如，零售商在Platform中設定牛仔褲品牌專屬區段。 當某人將牛仔褲偏好設定設為特定品牌時，該零售商現在可以觸發行動訊息。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!UICONTROL 承載權杖]**:您從控制面板產生的承載代 [!DNL Airship] 號。
* **[!UICONTROL 名稱]**:輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 網域]**:選擇美國或歐盟資料中心，具體取決於 [!DNL Airship] 哪個資料中心適用於此目的地。


## 啟用此目的地的區段 {#activate}

請參閱[將設定檔和區段啟用至目的地](../../ui/activate-destinations.md) ，以取得將對象區段啟用至目的地的指示。

## 對應考量事項 {#mapping-considerations}

[!DNL Airship] 標籤可在代表裝置例項（例如iPhone）的頻道上設定，或是指名使用者，此指名使用者會將使用者的所有裝置對應至通用識別碼，例如客戶ID。如果您的結構中有純文字（未雜湊）電子郵件地址作為主要身分，請在&#x200B;**[!UICONTROL 來源屬性]**&#x200B;中選取電子郵件欄位，並在&#x200B;**[!UICONTROL 目標身分]**&#x200B;下方右欄中對應至[!DNL Airship]指名的使用者，如下所示。

![命名用戶映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

對於應映射到通道（即設備）的標識符，根據源映射到相應的通道。 下列影像顯示如何將Google Advertising ID對應至[!DNL Airship] Android頻道。

![連接到Airship ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![TagsConnect到Airship ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![TagsChannel映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## 資料使用與控管 {#data-usage-governance}

處理資料時，所有[!DNL Adobe Experience Platform]目標都符合資料使用策略。 有關[!DNL Adobe Experience Platform]如何實施資料控管的詳細資訊，請參閱[資料控管概述](../../../data-governance/home.md)。
