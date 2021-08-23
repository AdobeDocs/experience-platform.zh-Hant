---
keywords: Experience Platform；首頁；熱門主題；本機系統；檔案上傳；對應csv；對應csv檔案；將csv檔案對應至xdm；將csv對應至xdm;ui指南；
solution: Experience Platform
title: 在UI中建立本機檔案上傳來源連接器
topic-legacy: overview
type: Tutorial
description: 了解如何為本機系統建立來源連線，將本機檔案帶入Platform
source-git-commit: 1bf112db27b534e2ec977be7b47e3becf75ee066
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 1%

---

# 在UI中建立本機檔案上傳來源連接器

本教學課程提供建立本機檔案上傳來源連接器，以使用使用者介面將本機檔案內嵌至Platform的步驟。

## 快速入門

本教學課程需要妥善了解Platform的下列元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Platform用來組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

## 將本機檔案上傳至Platform

在平台UI中，從左側導覽列選取&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL 目錄]螢幕顯示您可以為其建立帳戶的各種源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在[!UICONTROL 本地系統]類別下，選擇&#x200B;**[!UICONTROL 本地檔案上載]**，然後選擇&#x200B;**[!UICONTROL 配置]**。

![目錄](../../../../images/tutorials/create/local/catalog.png)

### 使用現有資料集

「[!UICONTROL 資料流詳細資訊]」頁可讓您選擇要將CSV資料內嵌到現有資料集還是新資料集。

若要將CSV資料內嵌至現有資料集，請選取「**[!UICONTROL 現有資料集]**」。 您可以使用[!UICONTROL 進階搜尋]選項，或捲動下拉式功能表中的現有資料集清單，以擷取現有資料集。

![select-existing-dataset](../../../../images/tutorials/create/local/select-existing-dataset.png)

選取資料集後，請提供資料流的名稱和可選說明。

在此過程中，您還可以啟用[!UICONTROL 錯誤診斷]和[!UICONTROL 部分獲取]。 [!UICONTROL 錯誤] 診斷可針對資料流中發生的任何錯誤記錄生成詳細的錯誤消息，而部 [!UICONTROL 分] 內嵌則允許您內嵌包含錯誤的資料，最多可以手動定義某個閾值。如需詳細資訊，請參閱[部分批次內嵌概述](../../../../../ingestion/batch-ingestion/partial.md) 。

![dataflow-detail-existing](../../../../images/tutorials/create/local/dataflow-detail-existing.png)

### 使用新資料集

若要將CSV資料內嵌至新資料集，請選取「**[!UICONTROL 新資料集]**」 ，然後提供輸出資料集名稱和選用說明。 接下來，選擇要使用[!UICONTROL 高級搜索]選項或滾動下拉菜單中現有架構清單來映射的架構。

![select-new-dataset](../../../../images/tutorials/create/local/select-new-dataset.png)

選擇架構後，請為資料流提供名稱和可選說明，然後為資料流應用[!UICONTROL 錯誤診斷]和[!UICONTROL 部分獲取]設定。 完成後，選擇&#x200B;**[!UICONTROL Next]**。

### 選擇資料

此時會出現「選取資料」步驟，提供您上傳本機檔案並預覽其結構和內容的介面。 選擇&#x200B;**[!UICONTROL 選擇檔案]**&#x200B;以從本地系統上載CSV檔案。 或者，您也可以將要上傳的CSV檔案拖放至[!UICONTROL 拖放檔案]面板。

>[!TIP]
>
>本機檔案上傳目前僅支援CSV檔案。 每個檔案的最大檔案大小為1 GB。

![選擇檔案](../../../../images/tutorials/create/local/choose-files.png)

上傳檔案後，預覽介面會更新，以顯示檔案的內容和結構。

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

您可以根據您的檔案選擇列分隔符，如制表符、逗號、垂直號或自定義列分隔符。 選取&#x200B;**[!UICONTROL 分隔字元]**&#x200B;下拉式箭頭，然後從功能表中選取適當的分隔字元。

完成後，選擇&#x200B;**[!UICONTROL Next]**。

![分隔字元](../../../../images/tutorials/create/local/delimiter.png)

### 映射

此時將顯示[!UICONTROL 映射]步驟，提供一個介面，用於將源架構中的源欄位映射到目標架構中相應的目標XDM欄位。

![映射介面](../../../../images/tutorials/create/local/mapping-interface.png)

#### 預覽資料

選取「**[!UICONTROL 預覽資料]**」 ，即可查看所選資料集中最多100列範例資料的對應結果。

![預覽對應](../../../../images/tutorials/create/local/preview-mapping.png)

在預覽期間，身分欄會優先順序排列為第一個欄位，因為這是驗證對應結果時所需的關鍵資訊。 完成後，選擇&#x200B;**[!UICONTROL Close]**。

![預覽面板](../../../../images/tutorials/create/local/preview-panel.png)

#### 新增計算欄位

計算欄位允許根據輸入架構中的屬性建立值。 然後，可將這些值指派給目標架構中的屬性，並提供名稱和說明，以便更輕鬆參考。

選擇&#x200B;**[!UICONTROL 添加計算欄位]**&#x200B;按鈕以繼續。

![add-calculated-field](../../../../images/tutorials/create/local/add-calculated-field.png)

此時將顯示[!UICONTROL 建立計算欄位]面板。 左側對話方塊包含計算欄位中支援的欄位、函式和運算子。 選取其中一個索引標籤，以開始將函式、欄位或運算子新增至運算式編輯器。

![create-calculated-field](../../../../images/tutorials/create/local/create-calculated-field.png)

| 標記 | 說明 |
| --------- | ----------- |
| 函數 | 函式索引標籤列出可用於轉換資料的函式。 若要進一步了解您可在計算欄位中使用的函式，請閱讀有關[使用資料準備（映射器）函式](../../../../../data-prep/functions.md)的指南。 |
| 欄位 | 「欄位」頁簽列出源架構中可用的欄位和屬性。 |
| 運算元 | 運算子索引標籤會列出可用於轉換資料的運算子。 |

選取運算式編輯器，以手動新增欄位、函式和運算子。 建立計算欄位後，請選擇&#x200B;**[!UICONTROL Save]**&#x200B;以繼續。

![運算式編輯器](../../../../images/tutorials/create/local/expression-editor.png)

#### 篩選源架構映射樹

要篩選源架構，請選擇&#x200B;**[!UICONTROL 所有源欄位]**，然後從下拉菜單中選擇要映射的特定欄位。

下表顯示源架構樹的排序選項：

| 來源欄位 | 說明 |
| --- | --- |
| [!UICONTROL 所有源欄位] | 此選項顯示源架構的所有源欄位。 預設會顯示此選項。 |
| [!UICONTROL 必填欄位] | 此選項篩選源架構，僅顯示完成映射所需的欄位。 |
| [!UICONTROL 身分欄位] | 此選項篩選源架構，以僅顯示為「標識」標籤的欄位。 |
| [!UICONTROL 已映射欄位] | 此選項將篩選源架構，以僅顯示已映射的欄位。 |
| [!UICONTROL 未映射的欄位] | 此選項會篩選源架構，以僅顯示尚未映射的欄位。 |
| [!UICONTROL 含建議的欄位] | 此選項會篩選來源結構，僅顯示包含對應建議的欄位。 |

![all-source-fields](../../../../images/tutorials/create/local/all-source-fields.png)

#### 智慧型建議

Platform會根據您選取的目標結構或資料集，自動為自動對應欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。

![source-schema-tree](../../../../images/tutorials/create/local/source-schema-tree.png)

要接受所有自動生成映射值，請選擇&#x200B;**[!UICONTROL 接受所有目標欄位]**。

![全目標欄位](../../../../images/tutorials/create/local/all-target-fields.png)

有時，來源結構有多個建議可供使用。 發生此情況時，對應卡片會顯示最顯著的建議，後面接著一個藍色圓圈，裡面包含可用的其他建議數量。 選取燈泡圖示會顯示其他建議的清單。 您可以選取您要對應至之建議旁的核取方塊，以選擇其中一個替代建議。

![手動映射](../../../../images/tutorials/create/local/manual-mapping.png)

或者，您可以選擇手動將源架構映射到目標架構。 要執行此操作，請暫留在要映射的源架構上，然後選擇加號(`+`)表徵圖。

![select-plus-icon](../../../../images/tutorials/create/local/select-plus-icon.png)

此時會出現&#x200B;**[!UICONTROL 將來源對應至目標欄位]**&#x200B;彈出視窗。 從此處，您可以選取要映射的欄位，然後按一下&#x200B;**[!UICONTROL Save]**&#x200B;以添加新映射。

![map-source-to-target-field](../../../../images/tutorials/create/local/map-source-to-target-field.png)

完成後，選擇&#x200B;**[!UICONTROL Finished]**。

![完成](../../../../images/tutorials/create/local/finish.png)

## 監控資料擷取

CSV檔案對應並建立後，您就可以使用監控控制面板來監控透過它擷取的資料。 如需詳細資訊，請參閱UI](../../../../../dataflows/ui/monitor-sources.md)中關於[監控來源資料流的教學課程。

## 後續步驟

依照本教學課程，您已成功將一般CSV檔案對應至XDM架構，並將其擷取至Platform。 下游[!DNL Platform]服務（例如[!DNL Real-time Customer Profile]）現在可以使用此資料。 如需詳細資訊，請參閱[[!DNL Real-time Customer Profile]](../../../../../profile/home.md)的概觀。
