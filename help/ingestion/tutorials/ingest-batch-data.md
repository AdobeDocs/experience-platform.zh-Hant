---
keywords: Experience Platform；首頁；熱門主題；擷取；擷取批次資料；教學課程；批次擷取；教學課程；ui指南；
solution: Experience Platform
title: 將資料內嵌至Experience Platform
type: Tutorial
description: Adobe Experience Platform可讓您輕鬆以Parquet檔案或符合已知Experience Data Model(XDM)結構的資料形式，將資料匯入為批次檔案。
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 0%

---

# 將資料內嵌至Adobe Experience Platform

Adobe Experience Platform可讓您輕鬆將資料匯入 [!DNL Platform] 作為批處理檔案。 要擷取的資料範例可包括來自CRM系統中平面檔案（例如Parquet檔案）的設定檔資料，或符合已知的資料 [!DNL Experience Data Model] (XDM)架構（位於結構註冊表中）。

## 快速入門

若要完成本教學課程，您必須擁有 [!DNL Experience Platform]. 如果您無權存取 [!DNL Experience Platform]，請在繼續操作之前與系統管理員聯繫。

如果您偏好使用資料擷取API來內嵌資料，請先閱讀 [批次內嵌開發人員指南](../batch-ingestion/api-overview.md).

## 資料集工作區

內的資料集工作區 [!DNL Experience Platform] 可讓您檢視及管理IMS組織建立的所有資料集，並建立新的資料集。

按一下「 」以檢視資料集工作區 **[!UICONTROL 資料集]** 的下一頁。 「資料集」工作區包含資料集清單，包括顯示名稱、已建立（日期和時間）、來源、結構、上次批次狀態的欄，以及上次更新資料集的日期和時間。

>[!NOTE]
>
>按一下搜尋列旁的篩選圖示，即可使用篩選功能，只檢視已啟用的資料集 [!DNL Profile].

![檢視所有資料集](../images/tutorials/ingest-batch-data/datasets-overview.png)

## 建立資料集

若要建立資料集，請按一下 **[!UICONTROL 建立資料集]** 位於「資料集」工作區的右上角。

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

在 **[!UICONTROL 建立資料集]** 螢幕上，選擇是否「[!UICONTROL 從結構建立資料集]&quot;或&quot;[!UICONTROL 從CSV檔案建立資料集]」。

在本教學課程中，會使用結構來建立資料集。 按一下 **[!UICONTROL 從結構建立資料集]** 繼續。

![選擇資料源](../images/tutorials/ingest-batch-data/create-dataset.png)

## 選取資料集結構

在 **[!UICONTROL 選擇架構]** 畫面中，按一下您要使用之架構旁的選項按鈕來選擇架構。 在本教學課程中，資料集將使用忠誠會員結構來建立。 使用搜尋列來篩選結構是找到您要尋找確切結構的實用方法。

選取您要使用之架構旁的選項按鈕後，按一下 **[!UICONTROL 下一個]**.

![選擇架構](../images/tutorials/ingest-batch-data/select-schema.png)

## 設定資料集

在 **[!UICONTROL 設定資料集]** 畫面中，您必須為資料集命名，也可能提供資料集的說明。

**資料集名稱附註：**

- 資料集名稱應簡短且具描述性，以便稍後在資料庫中輕鬆找到資料集。
- 資料集名稱必須是唯一的，亦即資料集名稱也應足夠明確，以免日後重複使用。
- 最佳實務是使用說明欄位提供資料集的其他相關資訊，這可能有助於其他使用者日後區分資料集。

資料集有名稱和說明後，按一下 **[!UICONTROL 完成]**.

![設定資料集](../images/tutorials/ingest-batch-data/configure-dataset.png)

## 資料集活動

現在已建立空白資料集，且您已傳回至 **[!UICONTROL 資料集活動]** 標籤。 您應該會在工作區的左上角看到資料集名稱，並看到「尚未新增任何批次」通知。 這是預期的情況，因為您尚未將任何批次新增至此資料集。

在資料集工作區的右側，您會看到 **[!UICONTROL 資訊]** 索引標籤，內含與新資料集相關的資訊，例如資料集ID、名稱、說明、表格名稱、結構、串流和來源。 「資訊」索引標籤也包含資料集建立時間和上次修改日期的相關資訊。

在「資訊」標籤中，  **[!UICONTROL 設定檔]** 切換該選項，以啟用資料集，以便與 [!DNL Real-Time Customer Profile]. 使用此切換開關，以及 [!DNL Real-Time Customer Profile]，將在以下章節中詳細說明。

![資料集活動](../images/tutorials/ingest-batch-data/sample-dataset.png)

## 為啟用資料集 [!DNL Real-Time Customer Profile]

資料集可用來將資料擷取至 [!DNL Experience Platform]，而且這些資料最終可用來識別個人，並匯整來自多個來源的資訊。 連結在一起的資訊稱為 [!DNL Real-Time Customer Profile]. 為了 [!DNL Platform] 了解哪些資訊應包含在 [!DNL Real-Time Profile]，可使用 **[!UICONTROL 設定檔]** 切換。

依預設，此切換開關會關閉。 如果您選擇開啟 [!DNL Profile]，擷取至資料集的所有資料都將用來協助識別個人身分，並匯整個人資料 [!DNL Real-Time Profile].

若要深入了解 [!DNL Real-Time Customer Profile] 並處理身份，請檢閱 [Identity服務](../../identity-service/home.md) 檔案。

為啟用資料集 [!DNL Real-Time Customer Profile]，按一下 **[!UICONTROL 設定檔]** 在 **[!UICONTROL 資訊]** 標籤。

![設定檔切換](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

畫面會顯示對話方塊，詢問您是否要為 [!DNL Real-Time Customer Profile].

![啟用配置檔案對話框](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

按一下 **[!UICONTROL 啟用]** 切換開關會變成藍色，表示已開啟。

![為設定檔啟用](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## 新增資料至資料集

資料可透過多種不同方式新增至資料集。 您可以選擇使用 [!DNL Data Ingestion] API或ETL合作夥伴，例如 [!DNL Unifi] 或 [!DNL Informatica]. 在本教學課程中，資料將使用 **[!UICONTROL 新增資料]** 標籤。

若要開始將資料新增至資料集，請按一下 **[!UICONTROL 新增資料]** 標籤。 您現在可以拖放檔案，或瀏覽電腦以找到您要新增的檔案。

>[!NOTE]
>
>Platform支援兩種檔案類型，分別用於資料擷取：Parquet或JSON。 一次最多可以添加五個檔案，每個檔案的檔案大小上限為1 GB。

![「添加資料」頁簽](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## 上傳檔案

拖放（或瀏覽並選取）您要上傳的Parquet或JSON檔案後， [!DNL Platform] 會立即開始處理檔案， **[!UICONTROL 上傳]** 對話方塊中 **[!UICONTROL 新增資料]** 標籤，顯示檔案上傳的進度。

![上傳對話方塊](../images/tutorials/ingest-batch-data/uploading-file.png)

## 資料集量度

檔案上傳完成後， **[!UICONTROL 資料集活動]** 標籤不再顯示「尚未新增批次」。 反之， **[!UICONTROL 資料集活動]** 索引標籤現在會顯示資料集量度。 由於批次尚未載入，此階段所有量度都會顯示「0」。

在索引標籤底部，會顯示 **[!UICONTROL 批次ID]** 通過 [&quot;將資料添加到資料集&quot;](#add-data-to-dataset) 程式。 此外還包括與批相關的資訊，包括所擷取的日期、所擷取的記錄數，以及目前的批狀態。

![資料集量度](../images/tutorials/ingest-batch-data/batch-id.png)

## 批次詳細資料

按一下 **[!UICONTROL 批次ID]** 若要檢視 **[!UICONTROL 批次概觀]**，顯示有關批次的其他詳細資料。 批次載入完成後，會更新該批次的相關資訊，以顯示已擷取的記錄數和檔案大小。 狀態也會變更為「成功」或「失敗」。 如果批失敗 **[!UICONTROL 錯誤代碼]** 小節將包含擷取期間任何錯誤的詳細資訊。

如需批次內嵌的詳細資訊和常見問題，請參閱 [批次內嵌疑難排解指南](../batch-ingestion/troubleshooting.md).

若要返回 **[!UICONTROL 資料集活動]** 畫面上，按一下資料集的名稱(**[!UICONTROL 忠誠度詳細資料]**)。

![批次概觀](../images/tutorials/ingest-batch-data/batch-details.png)

## 預覽資料集

資料集準備就緒後，即可選擇 **[!UICONTROL 預覽資料集]** 顯示於 **[!UICONTROL 資料集活動]** 標籤。

按一下 **[!UICONTROL 預覽資料集]** 開啟對話方塊，顯示資料集內的範例資料。 如果資料集是使用結構建立，資料集結構的詳細資料會顯示在預覽的左側。 您可以使用箭頭來展開架構，以查看架構結構。 預覽資料中的每個欄標題代表資料集中的一個欄位。

![資料集詳細資訊](../images/tutorials/ingest-batch-data/dataset-preview.png)

## 後續步驟和其他資源

現在您已建立資料集，並成功將資料內嵌至 [!DNL Experience Platform]，您可以重複這些步驟來建立新資料集，或將更多資料內嵌至現有資料集。

若要進一步了解批次內嵌，請參閱 [批次內嵌概觀](../batch-ingestion/overview.md) 通過觀看下面的視頻來補充學習內容。

>[!WARNING]
>
>此 [!DNL Platform] 下列影片中顯示的UI已過期。 請參閱上述檔案，了解最新的UI螢幕擷取畫面和功能。

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
