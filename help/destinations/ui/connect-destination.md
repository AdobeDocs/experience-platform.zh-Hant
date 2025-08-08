---
title: 建立新的目的地連線
type: Tutorial
description: 瞭解如何在Adobe Experience Platform中連線至目的地、啟用警示，以及為已連線的目的地設定行銷動作。
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: ec6f055de02610e23f30051c4fed4f362e9fbc53
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 4%

---

# 建立新的目的地連線

>[!IMPORTANT]
> 
>* 若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要連線到支援資料集匯出的目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理和啟用資料集目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

## 概觀 {#overview}

您必須先設定與目的地平台的連線，才能將對象資料傳送至目的地。 本文會說明如何設定新的目的地連線，然後您可以使用Adobe Experience Platform使用者介面啟用對象或匯出資料集。

## 在目錄中尋找所需的目的地 {#setup}

1. 移至&#x200B;**[!UICONTROL 連線]** > **[!UICONTROL 目的地]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤。

   ![Experience Platform UI熒幕擷圖，顯示目的地目錄頁面。](../assets/ui/connect-destinations/catalog.png)

2. 目錄中的目的地卡片可能會有不同的動作控制項，實際情形取決於您是否有現有的目的地連線，以及目的地是否支援啟用受眾、匯出資料集或兩者。 您可能會看見目的地卡片的下列任一控制項：

   * **[!UICONTROL 設定]**。 您必須先設定與此目的地的連線，才能啟用對象或匯出資料集。
   * **[!UICONTROL 啟動]**。 已經設定連線到此目的地。 此目的地支援對象啟用和資料集匯出。
   * **[!UICONTROL 啟用對象]**。 已經設定連線到此目的地。 此目的地僅支援對象啟用。

   如需這些控制項之間差異的詳細資訊，您也可以參閱目的地工作區檔案的[目錄](../ui/destinations-workspace.md#catalog)區段。

   根據您可用的控制項，選取&#x200B;**[!UICONTROL 設定]**、**[!UICONTROL 啟用]**&#x200B;或&#x200B;**[!UICONTROL 啟用對象]**。

   ![Experience Platform UI熒幕擷圖，顯示醒目提示「設定」控制項的目的地目錄頁面。](../assets/ui/connect-destinations/set-up.png)

   ![Experience Platform UI熒幕擷圖，顯示反白顯示「啟用對象」控制項的目的地目錄頁面。](../assets/ui/connect-destinations/activate-segments.png)

3. 如果您已選取&#x200B;**[!UICONTROL 設定]**，請跳至下一個步驟，以[驗證](#authenticate)至目的地。

   若您選取&#x200B;**[!UICONTROL 啟用]**、**[!UICONTROL 啟用對象]**&#x200B;或&#x200B;**[!UICONTROL 匯出資料集]**，您現在可以看到現有目的地連線的清單。

   選取&#x200B;**[!UICONTROL 設定新目的地]**&#x200B;以建立與目的地的新連線。

   ![Experience Platform UI熒幕擷圖，顯示可用目的地的清單，並反白顯示「設定新目的地」控制項。](../assets/ui/connect-destinations/configure-new-destination.png)

## 驗證目標 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_account_name"
>title="帳戶名稱"
>abstract="輸入名稱以便日後協助您輕鬆識別此目標帳戶。如果您有多個連線連至同一目標，這個做法尤其實用。"

連線到目的地的第一個步驟是驗證到目的地平台。

根據您連線到的目的地，您可能會被帶往目的地合作夥伴的頁面進行驗證，或者系統可能會要求您直接在Experience Platform工作流程中輸入驗證認證。

設定新的目的地連線時，您必須提供&#x200B;**[!UICONTROL 帳戶名稱]**，以及選擇性的&#x200B;**[!UICONTROL 描述]**。 這些欄位適用於所有目的地。

* **[!UICONTROL 帳戶名稱]**：輸入可協助您日後輕鬆識別此目的地帳戶的名稱。 如果您有多個連線連至同一目標，這個做法尤其實用。
* **[!UICONTROL 描述]** （選擇性）：新增任何可協助您或您的團隊區分帳戶的其他詳細資料，例如連線的目的或相關的業務內容。

在這些欄位中提供清楚的描述性資訊，可讓您在啟用對象時，更輕鬆地管理和選取正確的目的地帳戶。

以下是驗證[!DNL Amazon S3]目的地所需的輸入範例。 每個目的地檔案頁面都會提供必要輸入的詳細指示（例如，請參閱[[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate)和[[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate)的驗證區段）。

**[!DNL Amazon S3]必要和選用的驗證引數**

![此影像顯示驗證Amazon S3目的地時的必要和選用輸入引數。](../assets/ui/connect-destinations/s3-new-acc.png)

## 設定連線引數 {#set-up-connection-parameters}

如果您已經設定目的地驗證，您可以繼續使用現有帳戶，也可以設定新帳戶。

視您連線的目的地而定，可能會要求您輸入不同型別的連線引數。 例如，當連線到[!DNL Amazon S3]目的地時，會要求您提供有關[!DNL Amazon S3]儲存貯體名稱和將儲存檔案的資料夾路徑的詳細資料。 以下是兩個[!DNL Amazon S3]目的地和[!DNL Trade Desk]目的地所需輸入的範例。 每個目的地檔案頁面都會提供必要輸入的詳細指示。

>[!IMPORTANT]
>
>下列影像僅供說明之用。 目的地連線的詳細資料因目的地而異。 如需您目的地的連線詳細資訊，請閱讀每個&#x200B;**目的地目錄**&#x200B;頁面中的[連線到目的地](../catalog/overview.md)區段（例如，[[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect)、[[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect)或[[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)）。

**[!DNL Amazon S3]必要和選用的輸入引數**

![此影像顯示連線至Amazon S3目的地時的必要和選用輸入引數。](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]必要和選用的輸入引數**

![此影像顯示連線至交易台目的地時所需的和選用的輸入引數。](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### 設定轉存檔案的檔案格式選項 {#file-formatting-and-compression-options}

對於以檔案為基礎的目的地，您可以設定與匯出檔案的格式化和壓縮方式相關的各種設定。 如需所有可用格式設定和壓縮選項的詳細資訊，請閱讀[設定檔案型目的地的檔案格式設定選項](/help/destinations/ui/batch-destinations-file-formatting-options.md)。

![顯示CSV檔案的檔案型別選取範圍與各種選項的影像。](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### 設定目的地連線，用於對象啟用、帳戶啟用、潛在客戶啟用或資料集匯出 {#segment-activation-or-dataset-exports}

有些檔案型目的地支援對已知客戶、帳戶客戶或潛在客戶進行受眾啟用，也支援資料集匯出。 對於這些目的地，您可以選擇是否要建立連線，讓您[啟用對象](/help/destinations/ui/activate-batch-profile-destinations.md)、[帳戶](/help/destinations/ui/activate-account-audiences.md)、[潛在客戶](/help/destinations/ui/activate-prospect-audiences.md)或[匯出資料集](/help/destinations/ui/export-datasets.md)。

>[!WARNING]
>
>匯出資料集時，請注意，僅支援在壓縮模式下匯出至JSON檔案。 在壓縮與未壓縮模式中支援匯出至[!DNL Parquet]個檔案。

![顯示資料型別選擇控制項的影像，使用者可在對象啟用與資料集匯出之間選擇。](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### 啟用目的地警示 {#enable-alerts}

1. （選用）選取您要訂閱的目的地資料流警示。 建立資料流時，您可以訂閱警示以接收有關資料流執行狀態、成功或失敗的警示訊息。 根據您連線的目的地型別（檔案型或串流），可用的警報會有所不同。 閱讀[訂閱內文中目的地警示](alerts.md)，以取得目的地資料流警示的詳細資訊。

   ![[設定新目的地]對話方塊中反白了內容中目的地警示訂閱選項。](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. 選取&#x200B;**[!UICONTROL 下一步]**。

   ![反白顯示[設定新目的地]對話方塊的[下一步]控制項，讓使用者繼續進行工作流程的下一步。](../assets/ui/connect-destinations/next.png)

## 選取行銷動作 {#select-marketing-actions}

1. 選取適用於您要匯出至目的地之資料的行銷動作。 行銷動作會指出資料匯出至目的地的目的。 您可以從Adobe定義的行銷動作中選取，或建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用原則概觀](../../data-governance/policies/overview.md)頁面。

   ![此設定新目的地對話方塊中會反白顯示可用的行銷動作。 用來完成「連線至目的地」工作流程的可用控制項也會反白顯示。](../assets/ui/connect-destinations/governance.png)

2. 選取&#x200B;**[!UICONTROL 儲存並退出]**&#x200B;以儲存目的地組態，或選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續前往對象資料[啟動流程](activation-overview.md)。

## 後續步驟 {#next-steps}

閱讀本檔案後，您已瞭解如何使用Experience Platform UI建立與目的地的連線。 提醒一下，可用和必要的連線引數會因目的地而異。 您也應該參閱[目的地目錄](/help/destinations/catalog/overview.md)中的目的地檔案頁面，以取得關於每個目的地型別的必要輸入和可用選項的特定資訊。

接著，您可以繼續[啟用對象](/help/destinations/ui/activation-overview.md)或[將資料集](/help/destinations/ui/export-datasets.md)匯出至您的目的地。