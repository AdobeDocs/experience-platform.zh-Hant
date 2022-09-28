---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；行銷活動；行銷活動管理服務
title: 使用Platform UI建立Adobe Campaign Managed Cloud Services來源連線
description: 了解如何使用Platform UI將Adobe Experience Platform連線至Adobe Campaign Managed Cloud Services。
exl-id: 067ed558-b239-4845-8c85-3bf9b1d4caed
source-git-commit: b9f032c903da2bdb9f37179b1693119bf7b0029d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 使用Platform UI建立Adobe Campaign Managed Cloud Services來源連線

本教學課程提供建立來源連線的步驟，以將Adobe Campaign Managed Cloud Services資料帶入Adobe Experience Platform。

## 快速入門

本指南需要妥善了解下列Experience Platform元件：

* [來源](../../../../home.md):Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加上標籤，以及增強傳入資料。
* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [沙箱](../../../../../sandboxes/home.md):Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以協助開發及改進數位體驗應用程式。

## 將Adobe Campaign Managed Cloud Services連線至Platform

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 您也可以使用搜尋列來縮小顯示的來源。

在 **[!UICONTROL Adobe應用程式]** 類別，選擇 **[!UICONTROL Adobe Campaign Managed Cloud Services]** 然後選取 **[!UICONTROL 新增資料]**.

![顯示Adobe Campaign Managed Cloud Services卡的來源目錄。](../../../../images/tutorials/create/campaign/catalog.png)

### 選擇資料 {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Adobe Campaign環境例項"
>abstract="您要使用的Adobe Campaign環境名稱。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="目標對應"
>abstract="目標對應是Campaign用來傳送訊息的技術物件，並包含傳送傳送所需的所有技術設定（地址、電話號碼、選擇加入指標、其他識別碼……）。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="架構名稱"
>abstract="Adobe Campaign資料庫中定義的實體名稱。"
>text="Learn more in documentation"

此 [!UICONTROL 選擇資料] 步驟，提供介面來設定 [!UICONTROL Adobe Campaign例項], [!UICONTROL 目標對應]，和 [!UICONTROL 架構名稱].

| 屬性 | 說明 |
| --- | --- |
| Adobe Campaign例項 | 您使用的Adobe Campaign環境例項名稱。 |
| 目標對應 | Campaign用於傳送訊息的技術物件，並包含傳送傳送所需的所有技術設定。 |
| 架構名稱 | 您要帶入Platform的架構實體名稱。 選項包括傳送記錄和追蹤記錄。 |

![可在其中設定Adobe Campaign例項、目標對應和結構名稱的介面。](../../../../images/tutorials/create/campaign/select-data.png)

提供Campaign執行個體、目標對應和架構名稱的值後，畫面會更新，以顯示架構的預覽以及範例資料集。 完成後，請選取 **[!UICONTROL 下一個]**.

![結構階層的預覽以及資料集的範例](../../../../images/tutorials/create/campaign/preview.png)

### 使用現有資料集

此 [!UICONTROL 資料流詳細資訊] 頁面可讓您選擇要使用現有資料集，還是為資料流配置新資料集。

若要使用現有資料集，請選取 **[!UICONTROL 現有資料集]**. 您可以使用 [!UICONTROL 進階搜尋] 選項，或透過捲動下拉式選單中的現有資料集清單來執行。

選取資料集後，請提供資料流的名稱和可選說明。

![顯示現有資料集選項的介面。](../../../../images/tutorials/create/campaign/existing-dataset.png)

### 使用新資料集

若要使用新資料集，請選取 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和選用說明。 接下來，使用 [!UICONTROL 進階搜尋] 選項，或透過捲動下拉式選單中的現有結構清單來執行。 完成後，請選取 **[!UICONTROL 下一個]**.

![顯示新資料集選項的介面。](../../../../images/tutorials/create/campaign/new-dataset.png)

### 啟用警報

您可以啟用警報，以接收有關資料流狀態的通知。 從清單中選擇警報，以訂閱並接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱來源警報](../../alerts.md).

完成向資料流提供詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

![可為資料流啟用的不同警報類型的選擇。](../../../../images/tutorials/create/campaign/alerts.png)

### 將資料欄位對應至XDM結構

此 [!UICONTROL 對應] 步驟，提供您一個介面，將來源架構的來源欄位對應至目標架構中適當的目標XDM欄位。

Platform會根據您選取的目標結構或資料集，為自動對應欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以視需要選擇直接映射欄位，或使用資料準備函式來轉換源資料，以導出計算值或計算值。 有關使用映射器介面和計算欄位的完整步驟，請參閱 [資料準備UI指南](../../../../../data-prep/ui/mapping.md).

>[!IMPORTANT]
>
>將來源欄位對應至目標XDM欄位時，您必須確定將指定的主要身分欄位對應至其適當的目標XDM欄位。

成功映射源資料後，請選擇 **[!UICONTROL 下一個]**.

![一個映射樹，其中四個源資料欄位被映射到其對應的XDM架構欄位。](../../../../images/tutorials/create/campaign/mapping.png)

### 查看資料流

此 **[!UICONTROL 檢閱]** 步驟顯示，允許您在建立新資料流之前對其進行查看。 詳細資料會分組為下列類別：

* **[!UICONTROL 連線]**:顯示源類型、所選源檔案的相關路徑以及該源檔案中的列數。
* **[!UICONTROL 指派資料集和對應欄位]**:顯示要擷取來源資料的資料集，包括資料集所遵守的結構。

審核資料流後，請選擇 **[!UICONTROL 完成]** 並允許建立資料流的時間。

![顯示連線和資料集資訊的審核頁面。](../../../../images/tutorials/create/campaign/review.png)

### 監視您的資料集活動

建立資料流後，您可以監視正在通過資料流進行內嵌的資料，以查看有關內嵌速率以及成功和失敗批處理的資訊。

若要開始檢視資料集活動，請選取 **[!UICONTROL 資料流]** 來源目錄中。

![已選擇資料流標題頁簽的源目錄頁。](../../../../images/tutorials/create/campaign/dataflows.png)

接下來，從顯示的資料流清單中選擇目標資料集。

![已選取Adobe Campaign傳送記錄目標資料集的現有資料流清單。](../../../../images/tutorials/create/campaign/target-dataset.png)

資料集活動頁面隨即顯示。 從這裡，您可以看到資料流效能的資訊，包括內嵌率、成功批次和失敗批次。

此頁還提供一個介面，用於更新資料流的元資料描述、啟用部分獲取和錯誤診斷，以及向資料集添加新資料。

![介面，其圖形代表所選資料集的擷取率。](../../../../images/tutorials/create/campaign/dataset-activity.png)

## 後續步驟

依照本教學課程，您已成功建立資料流，將您的Campaign v8傳送記錄檔和追蹤記錄檔資料帶入Platform。 下游Platform服務(例如 [!DNL Real-time Customer Profile] 和 [!DNL Data Science Workspace]. 如需詳細資訊，請參閱下列檔案：

* [[!DNL Real-time Customer Profile]概述](../../../../../profile/home.md)
* [[!DNL Data Science Workspace]概述](../../../../../data-science-workspace/home.md)
