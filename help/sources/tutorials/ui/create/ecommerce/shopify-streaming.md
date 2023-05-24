---
title: 在UI中建立SHOPIFY流連接和資料流
description: 瞭解如何使用平台用戶介面建立Shopify流源連接和資料流
badge: β
exl-id: 3368ecf6-0c61-49ce-bc9c-29ee50b3f037
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# 建立源連接和資料流 [!DNL Shopify Streaming] 使用UI的資料

本教程提供建立 [!DNL Shopify Streaming] 源連接和資料流。

## 快速入門 {#getting-started}

本教程需要對以下Experience Platform組成部分進行有效理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

>[!IMPORTANT]
>
>本教程要求您完成了 [!DNL Shopify Streaming] 帳戶。 有關設定帳戶的步驟，請閱讀 [[!DNL Shopify Streaming] 概述](../../../../connectors/ecommerce/shopify-streaming.md)。

## 連接 [!DNL Shopify Streaming] 帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左導航欄訪問 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 **電子商務** 類別，選擇 [!DNL Shopify Streaming]，然後選擇 **[!UICONTROL 添加資料]**。

![Experience Platform源目錄](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## 選擇資料

的 **[!UICONTROL 選擇資料]** 步驟，為您提供介面以選擇您帶到平台的資料。

* 介面的左側部分是一個瀏覽器，允許您查看帳戶中的可用資料流；
* 該介面的右部分允許您從JSON檔案預覽多達100行的資料。

選擇 **[!UICONTROL 上載檔案]** 從本地系統上載JSON檔案。 或者，可以將要上載的JSON檔案拖放到 [!UICONTROL 拖放檔案] 的子菜單。

![源工作流的添加資料步驟。](../../../../images/tutorials/create/shopify-streaming/select-data.png)

上載檔案後，預覽介面將更新以顯示上載的架構的預覽。 預覽介面允許您檢查檔案的內容和結構。 您還可以使用 [!UICONTROL 搜索欄位] 用於從架構中訪問特定項的實用程式。

完成後，選擇 **[!UICONTROL 下一個]**。

![源工作流的預覽步驟。](../../../../images/tutorials/create/shopify-streaming/preview.png)

## 資料流詳細資訊

的 **資料流詳細資訊** 步驟，為您提供了使用現有資料集或為資料流建立新資料集的選項，以及為資料流提供名稱和說明的機會。 在此步驟中，您還可以配置配置檔案接收、錯誤診斷、部分接收和警報的設定。

完成後，選擇 **[!UICONTROL 下一個]**。

![源工作流的資料流詳細資訊步驟。](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## 映射

的 [!UICONTROL 映射] 步驟，提供一個介面，用於將源欄位從源架構映射到目標架構中相應的目標XDM欄位。

平台根據您選擇的目標架構或資料集為自動映射欄位提供智慧建議。 您可以手動調整映射規則以適合您的使用情形。 根據您的需要，您可以選擇直接映射欄位，或使用資料準備函式轉換源資料以導出計算值或計算值。 有關使用映射器介面和計算欄位的全面步驟，請參見 [資料準備UI指南](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html)。

成功映射源資料後，選擇 **[!UICONTROL 下一個]**。

![源工作流的映射步驟。](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## 請檢閱

的 **[!UICONTROL 審閱]** 步驟，允許您在建立新資料流之前查看它。 詳細資訊按以下類別分組：

* **[!UICONTROL 連接]**:顯示源類型、所選源檔案的相關路徑以及該源檔案中的列數。
* **[!UICONTROL 分配資料集和映射欄位]**:顯示源資料正被攝取到的資料集，包括該資料集所遵循的架構。

查看資料流後，選擇 **[!UICONTROL 完成]** 並為建立資料流留出一些時間。

![源工作流的審閱步驟。](../../../../images/tutorials/create/shopify-streaming/review.png)

## 獲取流終結點URL

建立流資料流後，現在可以檢索流終結點URL。 此終結點將用於訂閱Webhook，允許流源與Experience Platform通信。

要檢索流終結點，請轉到 [!UICONTROL 資料流活動] 剛建立的資料流的頁，並從 [!UICONTROL 屬性] 的子菜單。

![資料流活動中的流終結點。](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## 後續步驟

按照本教程，您已建立了與 [!DNL Shopify Streaming] 帳戶。 有關如何連接的說明 [!DNL Shopify Streaming] 帳戶，請閱讀有關 [建立源連接和資料流以流 [!DNL Shopify] 使用流服務API的資料](../../../api/create/ecommerce/shopify-streaming.md)。
