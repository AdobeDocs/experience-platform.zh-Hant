---
keywords: Experience Platform；首頁；熱門主題；攝取；攝取批處理資料；教程；批處理攝取；教程；用戶介面；
solution: Experience Platform
title: 將資料接收到Experience Platform
type: Tutorial
description: Adobe Experience Platform允許您以符合已知體驗資料模型(XDM)架構的Parke檔案或資料的形式輕鬆地將資料作為批處理檔案導入。
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 1%

---

# 將資料擷取至 Adobe Experience Platform

Adobe Experience Platform允許您輕鬆將資料導入 [!DNL Platform] 作為批處理檔案。 要攝取的資料的示例可以包括來自CRM系統中的平面檔案（例如Parke檔案）的簡檔資料或符合已知資料的資料 [!DNL Experience Data Model] (XDM)架構。

## 快速入門

要完成本教程，您必須具有訪問 [!DNL Experience Platform]。 如果您沒有訪問 [!DNL Experience Platform]，請在繼續之前與系統管理員聯繫。

如果您希望使用資料接收API來接收資料，請從讀取 [批量攝取顯影劑指南](../batch-ingestion/api-overview.md)。

## 資料集工作區

資料集工作區 [!DNL Experience Platform] 允許您查看和管理您的組織建立的所有資料集，以及建立新資料集。

通過按一下 **[!UICONTROL 資料集]** 的上界。 資料集工作區包含資料集清單，包括顯示名稱、建立（日期和時間）、源、模式和上次批處理狀態以及上次更新資料集的日期和時間的列。

>[!NOTE]
>
>按一下「搜索」欄旁邊的篩選器表徵圖，使用篩選功能僅查看為 [!DNL Profile]。

![查看所有資料集](../images/tutorials/ingest-batch-data/datasets-overview.png)

## 建立資料集

要建立資料集，請按一下 **[!UICONTROL 建立資料集]** 在資料集工作區的右上角。

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

在 **[!UICONTROL 建立資料集]** 螢幕，選擇是否要「[!UICONTROL 從架構建立資料集]&quot;或&quot;[!UICONTROL 從CSV檔案建立資料集]。

在本教程中，將使用一個模式來建立資料集。 按一下 **[!UICONTROL 從架構建立資料集]** 繼續。

![選擇資料源](../images/tutorials/ingest-batch-data/create-dataset.png)

## 選擇資料集架構

在 **[!UICONTROL 選擇方案]** 螢幕中，按一下要使用的架構旁邊的單選按鈕來選擇架構。 在本教程中，資料集將使用會員架構建立。 使用搜索欄篩選方案是查找要查找的確切方案的有用方法。

選擇了要使用的架構旁邊的單選按鈕後，按一下 **[!UICONTROL 下一個]**。

![選擇架構](../images/tutorials/ingest-batch-data/select-schema.png)

## 設定資料集

在 **[!UICONTROL 配置資料集]** 螢幕中，您需要為資料集指定名稱，並且可能還會提供資料集的說明。

**資料集名稱注釋：**

- 資料集名稱應簡短且描述性強，以便以後可以在庫中輕鬆找到資料集。
- 資料集名稱必須唯一，這意味著它也應足夠具體，以便以後不會重用。
- 最好使用說明欄位提供有關資料集的其他資訊，因為它可能有助於其他用戶將來區分資料集。

資料集有名稱和描述後，按一下 **[!UICONTROL 完成]**。

![設定資料集](../images/tutorials/ingest-batch-data/configure-dataset.png)

## 資料集活動

現在已建立空資料集，並且您已返回到 **[!UICONTROL 資料集活動]** 頁籤。 您應在工作區的左上角看到資料集的名稱，並看到通知「未添加批」。 由於您尚未向此資料集添加任何批處理，因此需要執行此操作。

在資料集工作區的右側，您將看到 **[!UICONTROL 資訊]** 頁籤，包含與新資料集相關的資訊，如資料集ID、名稱、說明、表名、架構、流和源。 「資訊」頁籤還包含有關建立資料集的時間及其上次修改日期的資訊。

「資訊」(Info)頁籤中還包含  **[!UICONTROL 配置檔案]** 切換用於啟用資料集以用於 [!DNL Real-Time Customer Profile]。 使用此切換， [!DNL Real-Time Customer Profile]，將在下面的章節中詳細說明。

![資料集活動](../images/tutorials/ingest-batch-data/sample-dataset.png)

## 為 [!DNL Real-Time Customer Profile]

資料集用於將資料插入 [!DNL Experience Platform]資料最終被用來識別個體並將來自多個來源的資訊拼接起來。 把資訊拼湊起來的 [!DNL Real-Time Customer Profile]。 為了 [!DNL Platform] 瞭解哪些資訊應包括在 [!DNL Real-Time Profile]，可以使用 **[!UICONTROL 配置檔案]** 切換。

預設情況下，此切換處於關閉狀態。 如果選擇開啟 [!DNL Profile]，所有資料都將被攝取到資料集中，用於幫助識別個體並將其拼接在一起 [!DNL Real-Time Profile]。

瞭解有關 [!DNL Real-Time Customer Profile] 使用身份，請查看 [身份服務](../../identity-service/home.md) 文檔。

為 [!DNL Real-Time Customer Profile]，按一下 **[!UICONTROL 配置檔案]** 切換 **[!UICONTROL 資訊]** 頁籤。

![配置檔案切換](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

將出現一個對話框，要求您確認要為 [!DNL Real-Time Customer Profile]。

![啟用配置檔案對話框](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

按一下 **[!UICONTROL 啟用]** 切換器會變藍，表示它已開啟。

![為配置檔案啟用](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## 將資料添加到資料集

資料可以以多種不同方式添加到資料集中。 您可以選擇使用 [!DNL Data Ingestion] API或ETL夥伴，如 [!DNL Unifi] 或 [!DNL Informatica]。 在本教程中，將使用 **[!UICONTROL 添加資料]** 頁籤。

要開始向資料集添加資料，請按一下 **[!UICONTROL 添加資料]** 頁籤。 現在，您可以拖放檔案或瀏覽電腦以查找要添加的檔案。

>[!NOTE]
>
>平台支援兩種檔案類型進行資料接收，即Parfect或JSON。 一次最多可以添加五個檔案，每個檔案的最大檔案大小為1 GB。

![「添加資料」頁籤](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## 上載檔案

拖放（或瀏覽並選擇）要上載的Parke或JSON檔案後， [!DNL Platform] 將立即開始處理檔案和 **[!UICONTROL 正在上載]** 對話框將出現在 **[!UICONTROL 添加資料]** 的子菜單。

![上載對話框](../images/tutorials/ingest-batch-data/uploading-file.png)

## 資料集度量

檔案上載完後， **[!UICONTROL 資料集活動]** 頁籤不再顯示「未添加批」。 相反， **[!UICONTROL 資料集活動]** 頁籤現在顯示資料集度量。 在此階段，所有度量都將顯示「0」，因為尚未載入批。

該頁籤的底部有一個清單，顯示 **[!UICONTROL 批ID]** 通過這些資料 [&quot;向資料集添加資料&quot;](#add-data-to-dataset) 處理。 還包括與批相關的資訊，包括接收日期、接收的記錄數和當前批狀態。

![資料集度量](../images/tutorials/ingest-batch-data/batch-id.png)

## 批詳細資訊

按一下 **[!UICONTROL 批ID]** 查看 **[!UICONTROL 批概覽]**，顯示有關批的其他詳細資訊。 一旦批完成載入，有關該批的資訊將更新，以顯示所接收的記錄數和檔案大小。 狀態也將更改為「成功」或「失敗」。 如果批失敗 **[!UICONTROL 錯誤代碼]** 部分將包含有關接收過程中的任何錯誤的詳細資訊。

有關批量攝取的詳細資訊和常見問題，請參閱 [批量攝取故障排除指南](../batch-ingestion/troubleshooting.md)。

返回到 **[!UICONTROL 資料集活動]** 螢幕中，按一下資料集的名稱(**[!UICONTROL 會員詳細資訊]**)。

![批概覽](../images/tutorials/ingest-batch-data/batch-details.png)

## 預覽資料集

資料集準備好後， **[!UICONTROL 預覽資料集]** 顯示在 **[!UICONTROL 資料集活動]** 頁籤。

按一下 **[!UICONTROL 預覽資料集]** 開啟一個對話框，其中顯示資料集中的示例資料。 如果使用架構建立資料集，則資料集架構的詳細資訊將顯示在預覽的左側。 可以使用箭頭展開架構，以查看架構結構。 預覽資料中的每個列標題都表示資料集中的欄位。

![資料集詳細資訊](../images/tutorials/ingest-batch-data/dataset-preview.png)

## 後續步驟和其他資源

現在，您已建立了資料集並成功將測試的資料 [!DNL Experience Platform]，您可以重複這些步驟以建立新資料集或將更多資料接收到現有資料集。

要瞭解有關批量攝取的詳細資訊，請閱讀 [批處理接收概述](../batch-ingestion/overview.md) 通過觀看下面的視頻來補充學習。

>[!WARNING]
>
>的 [!DNL Platform] 以下視頻中顯示的UI已過期。 有關最新的UI螢幕截圖和功能，請參閱上面的文檔。

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
