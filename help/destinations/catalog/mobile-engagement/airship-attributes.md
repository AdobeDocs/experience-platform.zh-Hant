---
keywords: 飛艇屬性；飛艇目的地
title: Airship屬性連接
description: 流暢地將Adobe對象資料傳遞至Airship，作為對象屬性，以在Airship內鎖定目標。
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: a765f6829f08f36010e0e12a7186bf5552dfe843
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# [!DNL Airship Attributes] 連接 {#airship-attributes-destination}

## 概覽 {#overview}

[!DNL Airship] 是領先的客戶參與平台，可協助您在客戶生命週期的每個階段，為使用者提供有意義的個人化全通路訊息。

此整合會將Adobe設定檔資料以[Attributes](https://docs.airship.com/guides/audience/attributes/)傳遞至[!DNL Airship]，以鎖定目標或觸發。

若要深入了解[!DNL Airship]，請參閱[Airship檔案](https://docs.airship.com)。

>[!TIP]
>
>此檔案頁面由[!DNL Airship]團隊建立。 有關任何查詢或更新請求，請直接聯繫[support.airship.com](https://support.airship.com/)。

## 先決條件 {#prerequisites}

您必須先：[!DNL Airship]

* 在[!DNL Airship]專案中啟用屬性。
* 生成用於驗證的承載令牌。

>[!TIP]
>
>若尚未透過[此註冊連結](https://go.airship.eu/accounts/register/plan/starter/)建立[!DNL Airship]帳戶。

## 啟用屬性 {#enable-attributes}

Adobe Experience Platform設定檔屬性類似於[!DNL Airship]屬性，而且使用本頁面下方所示的對應工具，即可在Platform中輕鬆相互對應。

[!DNL Airship] 專案有數個預先定義和預設屬性。如果您有自訂屬性，則必須先在[!DNL Airship]中定義它。 有關詳細資訊，請參閱[設定和管理屬性](https://docs.airship.com/tutorials/audience/attributes/)。

## 生成承載令牌 {#bearer-token}

前往[Airship控制面板](https://go.airship.com)中的&#x200B;**[!UICONTROL 設定]**&quot; **[!UICONTROL API與整合]**，然後在左側功能表中選取&#x200B;**[!UICONTROL Token]**。

按一下「**[!UICONTROL 建立代號]**」。

為代號提供好記的名稱，例如「Adobe屬性目的地」，並為角色選取「完全存取」。

按一下「**[!UICONTROL 建立代號]**」並將詳細資訊儲存為機密。

## 使用案例 {#use-cases}

為協助您更清楚了解您應如何及何時使用[!DNL Airship Attributes]目的地，以下是Adobe Experience Platform客戶可借由使用此目的地解決的範例使用案例。

### 使用案例#1

運用在Adobe Experience Platform中收集的設定檔資料，以個人化任何[!DNL Airship]管道中的訊息和豐富內容。 例如，利用[!DNL Experience Platform]配置檔案資料在[!DNL Airship]內設定位置屬性。 這可讓酒店品牌顯示每位使用者最近酒店位置的影像。

### 使用案例#2

運用Adobe Experience Platform的屬性，進一步擴充[!DNL Airship]設定檔，並將其與SDK或[!DNL Airship]預測資料結合。 例如，零售商可以建立一個區段，其中包含忠誠度狀態和位置資料（來自Platform的屬性）及[!DNL Airship]預計會流失資料，以傳送目標高度明確的訊息給居住在內華達州拉斯維加斯、且很可能轉譯的黃金忠誠度狀態使用者。

## 連接到目標 {#connect}

請參閱[對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) ，以取得對此目的地啟用受眾區段的指示。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!UICONTROL 承載權杖]**:您從控制面板產生的承載代 [!DNL Airship] 號。
* **[!UICONTROL 名稱]**:輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 網域]**:選擇美國或歐盟資料中心，具體取決於 [!DNL Airship] 哪個資料中心適用於此目的地。

## 啟用此目的地的區段 {#activate}

請參閱[對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) ，以取得對此目的地啟用受眾區段的指示。

## 對應考量事項 {#mapping-considerations}

[!DNL Airship] 屬性可在代表裝置例項（例如iPhone）的頻道上設定，或是指名使用者，可將使用者的所有裝置對應至通用識別碼（例如客戶ID）。如果您的結構中有純文字（未雜湊）電子郵件地址作為主要身分，請在&#x200B;**[!UICONTROL 來源屬性]**&#x200B;中選取電子郵件欄位，並在&#x200B;**[!UICONTROL 目標身分]**&#x200B;下方右欄中對應至[!DNL Airship]指名的使用者，如下所示。

![命名用戶映射](../../assets/catalog/mobile-engagement/airship/mapping.png)

對於應映射到通道（即設備）的標識符，根據源映射到相應的通道。 下圖顯示如何建立兩個對應：

* IDFA iOS廣告ID至[!DNL Airship] iOS通道
* Adobe`fullName`屬性至[!DNL Airship] &quot;Full Name&quot;屬性

>[!NOTE]
>
>為屬性對應選取目標欄位時，請使用[!DNL Airship]控制面板中顯示的好記名稱。

**對應身分**

選擇源欄位：

![連接到Airship屬性](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

選擇目標欄位：

![連接到Airship屬性](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**地圖屬性**

選擇源屬性：

![選擇源欄位](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

選擇目標屬性：

![選擇目標欄位](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

驗證映射：

![通道對應](../../assets/catalog/mobile-engagement/airship/mapping.png)


## 資料使用與控管 {#data-usage-governance}

處理資料時，所有[!DNL Adobe Experience Platform]目標都符合資料使用策略。 有關[!DNL Adobe Experience Platform]如何實施資料控管的詳細資訊，請參閱[資料控管概述](../../../data-governance/home.md)。
