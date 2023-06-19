---
title: 使用UI將您的RainFocus帳戶連結至Experience Platform
description: 瞭解如何使用UI將您的RainFocus帳戶連結至Experience Platform。
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: e90f05c44943f55630bd02d3b8bf04b01d07f320
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---

# 連線您的 [!DNL RainFocus] 要使用UIExperience Platform的帳戶

>[!NOTE]
>
>此 [!DNL RainFocus] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

本教學課程提供如何連線至 [!DNL RainFocus] 帳戶並將事件管理及分析資料串流至Adobe Experience Platform。

>[!IMPORTANT]
>
>此檔案頁面是由 [!DNL RainFocus] 團隊。 如有任何查詢或更新要求，請直接聯絡客戶服務<span>@rainfocus.com或造訪 [[!DNL RainFocus] 說明中心](https://help.rainfocus.com/hc/en-us)

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

### 先決條件

連線之前 [!DNL RainFocus] 要Experience Platform的帳號，您必須先完成下列先決條件工作：

* [收集必要的認證](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [建立XDM結構描述並定義身分欄位](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [在RainFocus中建立整合設定檔](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

完成先決條件設定後，您就可以繼續進行下列步驟。

## 將您的RainFocus帳戶連結至Experience Platform

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽列存取「來源」工作區。 此 *[!UICONTROL 目錄]* 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 *[!UICONTROL 分析]* 類別，選取 **[!UICONTROL RainFocus體驗]**，然後選取 **[!UICONTROL 新增資料]**.

![已選取RainFocus來源的Experience PlatformUI上的來源目錄。](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## 選擇資料

「選取資料」步驟隨即顯示，提供介面供您選取要帶入Experience Platform的資料。

* 介面的左側是瀏覽器，可讓您檢視帳戶內的可用資料流；
* 介面的右側部分可讓您預覽來自JSON檔案的最多100列資料。

選取 **[!UICONTROL 上傳檔案]** 以從您的本機系統上傳JSON檔案。 或者，您也可以將要上傳的JSON檔案拖放至「拖放檔案」面板。

上傳從下載的JSON裝載範例 **Rainfocus**.

![來源工作流程中的選取資料步驟。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

上傳檔案後，預覽介面會更新，以顯示您上傳的結構描述預覽。 預覽介面可讓您檢查檔案的內容和結構。 您也可以使用「搜尋」欄位公用程式來存取結構描述中的特定專案。

完成後，選取 **[!UICONTROL 下一個]**.

![來源工作流程的資料預覽步驟。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## 資料流詳細資訊

此 **資料流詳細資料** 步驟隨即顯示，為您提供使用現有資料集或為資料流建立新資料集的選項，以及提供資料流名稱和說明的機會。 在此步驟中，您還可以配置設定檔擷取、錯誤診斷、部分擷取和警示的設定。

完成後，選取 **[!UICONTROL 下一個]**.

![來源工作流程的資料流詳細資料步驟。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## 映射 {#mapping}

「對應」步驟隨即顯示，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

Experience Platform會根據您選取的目標結構描述或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以視需要選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算值或計算值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱 [資料準備UI指南](../../../../../data-prep/ui/mapping.md).

成功對應來源資料後，請選取 **[!UICONTROL 下一個]**.

![來源工作流程的對應步驟。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## 請檢閱

此 **檢閱** 步驟隨即顯示，可讓您在建立新資料流之前對其進行檢閱。 詳細資料會分組到以下類別中：

* **連線**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **指派資料集和對應欄位**：顯示要將來源資料擷取到哪個資料集中，包括資料集所堅持的結構描述。

檢閱資料流後，選取 **完成** 並留出一些時間來建立資料流。

![來源工作流程的稽核步驟。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## 取得您的串流端點URL {#get-your-streaming-endpoint-url}

建立串流資料流後，您現在可以擷取串流端點URL。 此端點將用於訂閱您的webhook，允許您的串流來源與Experience Platform通訊。

若要擷取您的串流端點，請前往 *[!UICONTROL 資料流活動]* 您剛建立之資料流的頁面，並從底部複製端點 *[!UICONTROL 屬性]* 面板。

![來源工作區中的資料流活動頁面，其中反白了串流端點URL。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## 在RainFocus中啟用整合設定檔

當您的資料流完成並擷取到串流端點URL後，您現在可以啟用 [!DNL Integration Profile] 在 [!DNL RainFocus].

* 登入 [[!DNL RainFocus] 平台](https://app.rainfocus.com). 在主要導覽區中選取 **[!DNL Libraries]** 和 **[!DNL Integration Profiles]**
* 開啟 [!DNL Integration Profile] 您先前建立且屬於 [必備條件](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus).
* 貼上 **資料流ID** 和 **串流端點** 從Experience Platform中的資料流複製並選取 **儲存**

## 後續步驟

依照本教學課程所述，您已為建立連線， [!DNL RainFocus] 來源，可讓您將事件管理和Analytics資料串流至Experience Platform。

## 其他資源

下列檔案針對下列專案的細微差別提供額外指引： [!DNL RainFocus] 來源。

* [RainFocus支援中心](https://help.rainfocus.com/hc/en-us)
* [在Adobe Developer入口網站中建立Adobe服務帳戶(JWT)](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [在API中建立結構描述](../../../../../xdm/tutorials/create-schema-api.md)
* [在UI中建立結構](../../../../../xdm/tutorials/create-schema-ui.md)
* [在UI中定義身分欄位](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)