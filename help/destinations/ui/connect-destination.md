---
keywords: 連接目標；目標連接；如何連接目標
title: 建立新的目的地連線
type: Tutorial
description: 了解如何連線至Adobe Experience Platform中的目的地、啟用警報，以及為已連線的目的地設定行銷動作。
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 434b9ed4f64320b5fd73b752716cb34a8e48aec9
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---

# 建立新的目的地連線

>[!IMPORTANT]
> 
>* 若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。
>* 若要連線至支援資料集匯出的目的地，您需要 **[!UICONTROL 管理和啟用資料集目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。


## 總覽 {#overview}

您必須先設定與目的地平台的連線，才能將受眾資料傳送至目的地。 本文說明如何設定新的目的地連線，接著您就可以使用Adobe Experience Platform使用者介面啟用區段或匯出資料集。

## 在目錄中找到所需的目的地 {#setup}

1. 前往 **[!UICONTROL 連線]** > **[!UICONTROL 目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![Experience PlatformUI的螢幕擷圖，顯示目的地目錄頁面。](../assets/ui/connect-destinations/catalog.png)

2. 目錄中的目的地卡片可能有不同的動作控制，端視您是否有與目的地的現有連線，以及目的地是否支援啟用區段、匯出資料集或兩者皆然。 您可能會看到目標卡的下列任一控制項：

   * **[!UICONTROL 設定]**. 必須先將連線設定至此目的地，您才能啟用區段或匯出資料集。
   * **[!UICONTROL 啟動]**. 已設定到此目標的連接。 此目的地支援區段啟動和資料集匯出。
   * **[!UICONTROL 啟用區段]**. 已設定到此目標的連接。 此目的地僅支援區段啟用。

   如需這些控制項之間差異的詳細資訊，您也可以參閱 [目錄](../ui/destinations-workspace.md#catalog) 目標工作區檔案的區段。

   選取 **[!UICONTROL 設定]**, **[!UICONTROL 啟動]**，或 **[!UICONTROL 啟用區段]**，視您可使用的控制項而定。

   ![Experience PlatformUI的螢幕擷圖，顯示目的地目錄頁面，並反白顯示「設定」控制項。](../assets/ui/connect-destinations/set-up.png)

   ![Experience PlatformUI的螢幕擷圖，顯示目的地目錄頁面，並反白顯示「啟用區段」控制項。](../assets/ui/connect-destinations/activate-segments.png)

3. 如果您選取 **[!UICONTROL 設定]**，請跳到下一步， [驗證](#authenticate) 到目的地。

   如果您選取 **[!UICONTROL 啟動]**, **[!UICONTROL 啟用區段]**，或 **[!UICONTROL 匯出資料集]**，您現在可以看到現有目的地連線的清單。

   選擇 **[!UICONTROL 配置新目標]** 建立與目的地的新連線。

   ![Experience PlatformUI的螢幕擷圖，顯示可用目的地清單，並反白顯示設定新目的地控制項。](../assets/ui/connect-destinations/configure-new-destination.png)

## 驗證到目標 {#authenticate}

連接到目標的第一步是驗證到目標平台。

視您要連線的目標而定，系統可能會將您帶往目標合作夥伴的頁面進行驗證，或要求您直接在平台工作流程中輸入驗證憑證。 以下是驗證至 [!DNL Amazon S3] 目的地。 每個目的地檔案頁面都提供所需輸入的詳細指示(例如，請參閱 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) 和 [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate))。

**[!DNL Amazon S3]必要和選用驗證參數**

![在驗證Amazon S3目的地時顯示必要和選用輸入參數的影像。](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## 設定連接參數 {#set-up-connection-parameters}

如果您已設定目的地的驗證，則可以繼續使用現有帳戶，也可以設定新帳戶。

視您要連線的目的地而定，系統可能會要求您輸入不同類型的連線參數。 例如，當連線至 [!DNL Amazon S3] 目的地，系統會要求您提供 [!DNL Amazon S3] 儲存檔案的貯體名稱和資料夾路徑。 以下是 [!DNL Amazon S3] 目的地和 [!DNL Trade Desk] 目的地。 每個目的地檔案頁面都提供所需輸入的詳細指示。

>[!IMPORTANT]
>
>以下影像僅供圖例之用。 目的地的連線詳細資訊因目的地而異。 如需目的地連線詳細資訊的詳細資訊，請參閱 **連接到目標** 區段 [目的地目錄](../catalog/overview.md) 頁面(例如， [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect)，或 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details))。

**[!DNL Amazon S3]必要和選用的輸入參數**

![顯示連線至Amazon S3目的地時所需和選用輸入參數的影像。](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]必要和選用的輸入參數**

![顯示連接到交易台目標時所需和可選輸入參數的影像。](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### 設定導出檔案的檔案格式選項 {#file-formatting-and-compression-options}

對於基於檔案的目的地，您可以配置與導出檔案的格式化和壓縮方式相關的各種設定。 如需所有可用格式和壓縮選項的詳細資訊，請閱讀 [為檔案式目的地教學課程設定檔案格式選項](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![此影像顯示CSV檔案的檔案類型選取和各種選項。](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### 設定區段啟用或資料集匯出的目的地連線 {#segment-activation-or-dataset-exports}

有些以檔案為基礎的目的地支援區段啟動和資料集匯出。 對於這些目的地，您可以選擇要建立連線，以啟用區段或匯出資料集。

![影像顯示資料類型選取控制項，可讓使用者在區段啟動和資料集匯出之間進行選取。](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### 啟用目標警報 {#enable-alerts}

1. （可選）選擇要訂閱的目標資料流警報。 建立資料流時，您可以訂閱警報，以接收有關流運行狀態、成功或失敗的警報消息。 可用的警報會因您所連線的目標類型（以檔案為基礎或串流）而異。 閱讀 [訂閱內容內目的地警報](alerts.md) 有關目標資料流警報的詳細資訊。

   ![使用醒目提示的內容內目標警報訂閱選項，設定新目標對話方塊。](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. 選取&#x200B;**[!UICONTROL 「下一步」]**。

   ![「設定新目標」對話方塊會反白顯示「下一步」控制項，讓使用者繼續執行工作流程中的下一個步驟。](../assets/ui/connect-destinations/next.png)

## 選取行銷動作 {#select-marketing-actions}

1. 選取適用於您要匯出至目的地之資料的行銷動作。 行銷動作會指出要將資料匯出至目的地的目的。 您可以從Adobe定義的行銷動作中選取，或者您可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱 [資料使用原則概觀](../../data-governance/policies/overview.md) 頁面。

   ![以反白顯示可用行銷動作的「設定新目的地」對話方塊。 也會反白顯示完成連線至目標工作流程的可用控制項。](../assets/ui/connect-destinations/governance.png)

2. 選擇 **[!UICONTROL 儲存並退出]** 要保存目標配置，或選擇 **[!UICONTROL 下一個]** 繼續存取對象資料 [啟動流程](activation-overview.md).

## 後續步驟 {#next-steps}

閱讀本檔案後，您便學會了如何使用Experience PlatformUI來建立與目的地的連線。 提醒您，可用和必要的連線參數會因目的地而異。 您也應參閱 [目的地目錄](/help/destinations/catalog/overview.md) 以取得有關每個目的地類型所需輸入和可用選項的特定資訊。

接下來，您可以繼續 [啟用區段](/help/destinations/ui/activation-overview.md) 或 [匯出資料集](/help/destinations/ui/export-datasets.md) 到目的地。