---
keywords: Experience Platform；首頁；熱門主題；本機系統；檔案上傳；對應csv；對應csv檔案；將csv檔案對應至xdm；將csv對應至xdm;ui指南；
solution: Experience Platform
title: 在UI中建立本機檔案上傳來源連接器
type: Tutorial
description: 了解如何為本機系統建立來源連線，將本機檔案帶入Platform
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# 在UI中建立本機檔案上傳來源連接器

本教學課程提供建立本機檔案上傳來源連接器，以使用使用者介面將本機檔案內嵌至Platform的步驟。

## 快速入門

本教學課程需要妥善了解Platform的下列元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Platform用來組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

## 將本機檔案上傳至Platform

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 [!UICONTROL 本地系統] 類別，選擇 **[!UICONTROL 本機檔案上傳]**，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/local/catalog.png)

### 使用現有資料集

此 [!UICONTROL 資料流詳細資訊] 頁面可讓您選取要將CSV資料內嵌至現有資料集或新資料集。

若要將CSV資料內嵌至現有資料集，請選取 **[!UICONTROL 現有資料集]**. 您可以使用 [!UICONTROL 進階搜尋] 選項，或透過捲動下拉式選單中的現有資料集清單來執行。

選取資料集後，請提供資料流的名稱和可選說明。

在此程式中，您也可以啟用 [!UICONTROL 錯誤診斷] 和 [!UICONTROL 部分擷取]. [!UICONTROL 錯誤診斷] 為資料流中發生的任何錯誤記錄啟用詳細的錯誤消息生成，同時 [!UICONTROL 部分擷取] 可讓您內嵌包含錯誤的資料，最高可以是您手動定義的特定臨界值。 請參閱 [部分批次內嵌概觀](../../../../../ingestion/batch-ingestion/partial.md) 以取得更多資訊。

![現有資料集](../../../../images/tutorials/create/local/existing-dataset.png)

### 使用新資料集

若要將CSV資料內嵌至新資料集，請選取 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和選用說明。 接下來，使用 [!UICONTROL 進階搜尋] 選項，或透過捲動下拉式選單中的現有結構清單來執行。

在選定架構後，為資料流提供名稱和可選說明，然後應用 [!UICONTROL 錯誤診斷] 和 [!UICONTROL 部分擷取] 資料流所需的設定。 完成後，請選取 **[!UICONTROL 下一個]**.

![新資料集](../../../../images/tutorials/create/local/new-dataset.png)

### 選擇資料

此 [!UICONTROL 選擇資料] 步驟，提供您上傳本機檔案及預覽其結構和內容的介面。 選擇 **[!UICONTROL 選擇檔案]** 從本機系統上傳CSV檔案。 或者，您也可以將您要上傳的CSV檔案拖放至 [!UICONTROL 拖放檔案] 中。

>[!TIP]
>
>本機檔案上傳目前僅支援CSV檔案。 每個檔案的最大檔案大小為1 GB。

![選擇檔案](../../../../images/tutorials/create/local/choose-files.png)

上傳檔案後，預覽介面會更新，以顯示檔案的內容和結構。

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

您可以根據您的檔案選擇列分隔符，如制表符、逗號、垂直號或自定義列分隔符。 選取 **[!UICONTROL 分隔字元]** 下拉式箭頭，然後從功能表中選取適當的分隔字元。

完成後，請選取 **[!UICONTROL 下一個]**.

![分隔字元](../../../../images/tutorials/create/local/delimiter.png)

## 映射

此 [!UICONTROL 對應] 步驟，提供您一個介面，將來源架構的來源欄位對應至目標架構中適當的目標XDM欄位。

您可以視需要選擇直接映射欄位，或使用資料準備函式來轉換源資料，以導出計算值或計算值。 如需使用對應介面的完整步驟，請參閱 [資料準備UI指南](../../../../../data-prep/ui/mapping.md).

在對應集準備就緒後，選取 **[!UICONTROL 完成]** 並為建立新資料流留出一些時間。

![映射](../../../../images/tutorials/create/local/mapping.png)

## 監視資料內嵌

CSV檔案對應並建立後，您就可以使用監控控制面板來監控透過它擷取的資料。 如需詳細資訊，請參閱 [監視UI中的源資料流](../../../../../dataflows/ui/monitor-sources.md).

## 後續步驟

依照本教學課程，您已成功將一般CSV檔案對應至XDM架構，並將其擷取至Platform。 此資料現在可供下游使用 [!DNL Platform] 服務，例如 [!DNL Real-Time Customer Profile]. 請參閱以下概觀： [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) 以取得更多資訊。
