---
keywords: Experience Platform；首頁；熱門主題；本機系統；檔案上傳；對應csv；對應csv檔案；將csv檔案對應至xdm；將csv對應至xdm；ui指南；
solution: Experience Platform
title: 在UI中建立本機檔案上傳Source聯結器
type: Tutorial
description: 瞭解如何建立本機系統的來源連線，以將本機檔案帶到Platform
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# 在UI中建立本機檔案上傳來源聯結器

本教學課程提供建立本機檔案上傳來源聯結器的步驟，以便使用使用者介面將本機檔案擷取到Platform。

## 快速入門

本教學課程需要您實際瞭解下列Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

## 將本機檔案上傳到Platform

在Platform UI中，從左側導覽列選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在[!UICONTROL 本機系統]類別下，選取&#x200B;**[!UICONTROL 本機檔案上傳]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![目錄](../../../../images/tutorials/create/local/catalog.png)

### 使用現有的資料集

[!UICONTROL 資料流詳細資料]頁面可讓您選取是否要將CSV資料擷取至現有資料集或新資料集。

若要將CSV資料內嵌到現有的資料集中，請選取&#x200B;**[!UICONTROL 現有的資料集]**。 您可以使用[!UICONTROL 進階搜尋]選項或捲動下拉式選單中的現有資料集清單，來擷取現有資料集。

選取資料集後，為資料流命名並選填說明。

在此程式期間，您也可以啟用[!UICONTROL 錯誤診斷]和[!UICONTROL 部分擷取]。 [!UICONTROL 錯誤診斷]可針對資料流中發生的任何錯誤記錄產生詳細的錯誤訊息，而[!UICONTROL 部分擷取]可讓您擷取包含錯誤的資料，最多可擷取到您手動定義的特定臨界值。 如需詳細資訊，請參閱[部分批次擷取總覽](../../../../../ingestion/batch-ingestion/partial.md)。

![現有的資料集](../../../../images/tutorials/create/local/existing-dataset.png)

### 使用新資料集

若要將CSV資料擷取至新資料集，請選取&#x200B;**[!UICONTROL 新資料集]**，然後提供輸出資料集名稱和選用的說明。 接下來，使用[!UICONTROL 進階搜尋]選項，或捲動下拉式選單中的現有結構描述清單，選取要對應的結構描述。

選取結構描述後，提供資料流的名稱和選擇性說明，然後套用您要用於資料流的[!UICONTROL 錯誤診斷]和[!UICONTROL 部分擷取]設定。 完成後，選取&#x200B;**[!UICONTROL 下一步]**。

![新資料集](../../../../images/tutorials/create/local/new-dataset.png)

### 選取資料

[!UICONTROL 選取資料]步驟隨即顯示，為您提供可上傳本機檔案並預覽其結構和內容的介面。 選取&#x200B;**[!UICONTROL 選擇檔案]**&#x200B;以從您的本機系統上傳CSV檔案。 或者，您也可以將要上傳的CSV檔案拖放到[!UICONTROL 拖放檔案]面板。

>[!TIP]
>
>本機檔案上傳目前僅支援CSV檔案。 每個檔案的大小上限為1 GB。

![choose-files](../../../../images/tutorials/create/local/choose-files.png)

上傳檔案後，預覽介面會更新以顯示檔案的內容和結構。

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

根據您的檔案，您可以選取欄分隔符號，例如定位字元、逗號、直立線符號，或來源資料的自訂欄分隔符號。 選取&#x200B;**[!UICONTROL 分隔符號]**&#x200B;下拉式箭號，然後從功能表中選取適當的分隔符號。

完成後，選取&#x200B;**[!UICONTROL 下一步]**。

![分隔符號](../../../../images/tutorials/create/local/delimiter.png)

## 對應

[!UICONTROL 對應]步驟出現，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

您可以根據自己的需求，選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算或計算的值。 如需使用對應介面的完整步驟，請參閱[資料準備UI指南](../../../../../data-prep/ui/mapping.md)。

您的對應集準備就緒後，請選取&#x200B;**[!UICONTROL 完成]**，並等待一段時間以建立新的資料流。

![對應](../../../../images/tutorials/create/local/mapping.png)

## 監視資料擷取

對應和建立CSV檔案後，您就可以使用監視儀表板監視透過該檔案擷取的資料。 如需詳細資訊，請參閱有關UI](../../../../../dataflows/ui/monitor-sources.md)中[監視來源資料流程的教學課程。

## 後續步驟

依照本教學課程，您已成功將一般CSV檔案對應至XDM結構描述，並將其內嵌至Platform。 此資料現在可供下游[!DNL Platform]服務（例如[!DNL Real-Time Customer Profile]）使用。 如需詳細資訊，請參閱[[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)的概觀。
