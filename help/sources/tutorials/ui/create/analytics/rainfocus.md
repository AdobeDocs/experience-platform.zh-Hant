---
title: 使用UI將您的RainFocus帳戶連結至Experience Platform
description: 瞭解如何使用UI將您的RainFocus帳戶連結至Experience Platform。
badge: Beta
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 1%

---

# 使用使用者介面將您的[!DNL RainFocus]帳戶連線至Experience Platform

>[!NOTE]
>
>[!DNL RainFocus]來源是測試版。 如需使用Beta版標示來源的相關資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

本教學課程提供如何連線您的[!DNL RainFocus]帳戶以及串流事件管理和分析資料至Adobe Experience Platform的步驟。

>[!IMPORTANT]
>
>此來源聯結器和檔案頁面是由[!DNL RainFocus]團隊建立和維護的。 若有任何查詢或更新要求，請直接透過clientcare<span>@rainfocus.com聯絡他們，或造訪[[!DNL RainFocus] 說明中心](https://help.rainfocus.com/hc/en-us)

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

### 先決條件

您必須先完成下列先決條件作業，才能將[!DNL RainFocus]帳戶連線至Experience Platform：

* [收集必要的認證](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [建立XDM結構描述並定義身分欄位](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [在RainFocus中建立整合設定檔](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

完成先決條件設定後，您就可以繼續進行下列步驟。

## 將您的RainFocus帳戶連結至Experience Platform

在Experience Platform UI中，從左側導覽列中選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取來源工作區。 *[!UICONTROL 目錄]*&#x200B;畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;*[!UICONTROL Analytics]*&#x200B;類別下，選取&#x200B;**[!UICONTROL RainFocus體驗]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![已選取RainFocus來源的Experience Platform UI上的來源目錄。](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## 選取資料

「選取資料」步驟隨即顯示，提供介面讓您選取要帶入Experience Platform的資料。

* 介面的左側是瀏覽器，可讓您檢視帳戶內的可用資料流；
* 介面的右側部分可讓您預覽JSON檔案中最多100列的資料。

選取&#x200B;**[!UICONTROL 上傳檔案]**&#x200B;以從您的本機系統上傳JSON檔案。 或者，您也可以將要上傳的JSON檔案拖放至「拖放檔案」面板。

上傳從&#x200B;**RainFocus**&#x200B;下載的範例JSON裝載。

![來源工作流程中的選取資料步驟。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

上傳檔案後，預覽介面會更新，以顯示您上傳的結構描述預覽。 預覽介面可讓您檢查檔案的內容和結構。 您也可以使用「搜尋」欄位公用程式，從架構中存取特定專案。

完成後，選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的資料預覽步驟。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## 資料流詳細資料

**資料流詳細資料**&#x200B;步驟隨即顯示，為您提供使用現有資料集或建立資料流新資料集的選項，以及提供資料流名稱和說明的機會。 在此步驟中，您還可以配置設定檔擷取、錯誤診斷、部分擷取和警報的設定。

完成後，選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的資料流詳細資料步驟。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## 對應 {#mapping}

「對應」步驟隨即顯示，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

Experience Platform會根據您選取的目標結構或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以根據自己的需求，選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算或計算的值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱[資料準備UI指南](../../../../../data-prep/ui/mapping.md)。

成功對應來源資料後，請選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的對應步驟。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## 審核

**檢閱**&#x200B;步驟隨即顯示，可讓您在建立新資料流之前先檢閱該資料流。 詳細資料會分組到以下類別中：

* **連線**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **指派資料集與對應欄位**：顯示要將來源資料擷取到哪個資料集，包括資料集所堅持的結構描述。

檢閱您的資料流後，請選取&#x200B;**完成**，並等待一些時間來建立資料流。

![來源工作流程的稽核步驟。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## 取得您的串流端點URL {#get-your-streaming-endpoint-url}

建立串流資料流後，您現在可以擷取串流端點URL。 此端點將用於訂閱您的webhook，讓您的串流來源能夠與Experience Platform通訊。

若要擷取您的串流端點，請移至您剛建立之資料流的&#x200B;*[!UICONTROL 資料流活動]*&#x200B;頁面，並從&#x200B;*[!UICONTROL 屬性]*&#x200B;面板底部複製端點。

![來源工作區中的資料流活動頁面，串流端點URL已反白顯示。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## 在RainFocus中啟用整合設定檔

資料流完成且擷取到串流端點URL後，您現在可以在[!DNL RainFocus]中啟用[!DNL Integration Profile]。

* 登入[[!DNL RainFocus] 平台](https://app.rainfocus.com)。 在主要導覽區中選取&#x200B;**[!DNL Libraries]**&#x200B;和&#x200B;**[!DNL Integration Profiles]**
* 開啟您先前建立的[!DNL Integration Profile]，作為[必要條件](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)的一部分。
* 貼上從Experience Platform中的資料流複製的&#x200B;**資料流識別碼**&#x200B;和&#x200B;**串流端點**，並選取&#x200B;**儲存**

## 後續步驟

依照此教學課程中的指示，您已建立您[!DNL RainFocus]來源的連線，可讓您將事件管理及分析資料串流至Experience Platform。

## 其他資源

下列檔案針對[!DNL RainFocus]來源周圍的細微差別提供額外指引。

* [RainFocus說明中心](https://help.rainfocus.com/hc/en-us)
* [在Adobe Developer入口網站中建立Adobe服務帳戶(JWT)](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [在API中建立結構描述](../../../../../xdm/tutorials/create-schema-api.md)
* [在UI中建立結構](../../../../../xdm/tutorials/create-schema-ui.md)
* [在UI中定義身分欄位](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html?lang=zh-Hant)
