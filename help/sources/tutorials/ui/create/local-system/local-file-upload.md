---
keywords: Experience Platform；首頁；熱門主題；本地系統；檔案上載；映射csv；映射csv檔案；將csv檔案映射到xdm；將csv映射到xdm;ui指南；
solution: Experience Platform
title: 在UI中建立本地檔案上載源連接器
type: Tutorial
description: 瞭解如何為本地系統建立源連接以將本地檔案帶到平台
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# 在UI中建立本地檔案上載源連接器

本教程提供了建立本地檔案上載源連接器的步驟，以使用用戶介面將本地檔案接收到平台。

## 快速入門

本教程需要瞭解平台的以下元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):平台組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

## 將本地檔案上載到平台

在平台UI中，選擇 **[!UICONTROL 源]** 從左導航欄訪問 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可為其建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 [!UICONTROL 本地系統] 類別，選擇 **[!UICONTROL 本地檔案上載]**，然後選擇 **[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/local/catalog.png)

### 使用現有資料集

的 [!UICONTROL 資料流詳細資訊] 頁面，您可以選擇是將CSV資料插入現有資料集還是新資料集。

要將CSV資料插入現有資料集，請選擇 **[!UICONTROL 現有資料集]**。 可以使用 [!UICONTROL 高級搜索] 選項，或通過在下拉菜單中滾動現有資料集清單來執行此操作。

選擇資料集後，請為資料流提供名稱和可選說明。

在此過程中，您還可以 [!UICONTROL 錯誤診斷] 和 [!UICONTROL 部分攝取]。 [!UICONTROL 錯誤診斷] 為資料流中出現的任何錯誤記錄啟用詳細的錯誤消息生成，同時 [!UICONTROL 部分攝取] 允許您接收包含錯誤的資料，最高可達您手動定義的特定閾值。 查看 [部分批處理接收概述](../../../../../ingestion/batch-ingestion/partial.md) 的子菜單。

![現有資料集](../../../../images/tutorials/create/local/existing-dataset.png)

### 使用新資料集

要將CSV資料插入新資料集，請選擇 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和可選說明。 接下來，選擇要映射到的方案 [!UICONTROL 高級搜索] 選項，或通過在下拉菜單中滾動現有架構清單來執行。

選擇方案後，為資料流提供名稱和可選說明，然後應用 [!UICONTROL 錯誤診斷] 和 [!UICONTROL 部分攝取] 的子目錄。 完成後，選擇 **[!UICONTROL 下一個]**。

![新資料集](../../../../images/tutorials/create/local/new-dataset.png)

### 選擇資料

的 [!UICONTROL 選擇資料] 步驟，提供一個介面以上載本地檔案並預覽其結構和內容。 選擇 **[!UICONTROL 選擇檔案]** 從本地系統上載CSV檔案。 或者，可以將要上載的CSV檔案拖放到 [!UICONTROL 拖放檔案] 的子菜單。

>[!TIP]
>
>本地檔案上載當前僅支援CSV檔案。 每個檔案的最大檔案大小為1 GB。

![選擇檔案](../../../../images/tutorials/create/local/choose-files.png)

上載檔案後，預覽介面將更新以顯示檔案的內容和結構。

![預覽樣本資料](../../../../images/tutorials/create/local/preview-sample-data.png)

根據檔案的不同，可以為源資料選擇列分隔符，如制表符、逗號、管道或自定義列分隔符。 選擇 **[!UICONTROL 分隔符]** 下拉箭頭，然後從菜單中選擇相應的分隔符。

完成後，選擇 **[!UICONTROL 下一個]**。

![分隔符](../../../../images/tutorials/create/local/delimiter.png)

## 映射

的 [!UICONTROL 映射] 步驟，提供一個介面，用於將源欄位從源架構映射到目標架構中相應的目標XDM欄位。

根據您的需要，您可以選擇直接映射欄位，或使用資料準備函式轉換源資料以導出計算值或計算值。 有關使用映射介面的全面步驟，請參見 [資料準備UI指南](../../../../../data-prep/ui/mapping.md)。

映射集準備好後，選擇 **[!UICONTROL 完成]** 並允許建立新資料流時間。

![映射](../../../../images/tutorials/create/local/mapping.png)

## 監視資料內嵌

映射和建立CSV檔案後，您可以使用監視面板監視通過其接收的資料。 有關詳細資訊，請參見上的教程 [監視UI中的源資料流](../../../../../dataflows/ui/monitor-sources.md)。

## 後續步驟

按照本教程，您已成功將平面CSV檔案映射到XDM架構，並將其插入平台。 此資料現在可供下游使用 [!DNL Platform] 服務，如 [!DNL Real-Time Customer Profile]。 請參閱的概述 [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) 的子菜單。
