---
keywords: Experience Platform; home；熱門主題；攝取；攝取批處理資料；教學課程；批處理；教學課程；用戶介面指南；
solution: Experience Platform
title: 將資料內嵌至Experience Platform
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform可讓您輕鬆將資料匯入為符合已知體驗資料模型(XDM)架構的Parce檔案或資料格式的批次檔案。
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# 將資料收錄到Adobe Experience Platform

Adobe Experience Platform可讓您輕鬆將資料匯入至[!DNL Platform]為批次檔案。 要提取的資料示例可以包括來自CRM系統中的平面檔案（如Parce檔案）或符合模式註冊表中已知[!DNL Experience Data Model](XDM)模式的資料的配置檔案資料。

## 快速入門

要完成本教學課程，您必須具有[!DNL Experience Platform]的存取權。 如果您沒有[!DNL Experience Platform]中IMS組織的存取權，請在繼續之前先與系統管理員聯絡。

如果您想要使用資料擷取API來擷取資料，請先閱讀[批次擷取開發人員指南](../batch-ingestion/api-overview.md)。

## 資料集工作區

[!DNL Experience Platform]中的「資料集」工作區可讓您檢視和管理IMS組織建立的所有資料集，並建立新的資料集。

按一下左側導覽中的&#x200B;**[!UICONTROL Datasets]**，檢視資料集工作區。 「資料集」工作區包含資料集清單，包括顯示名稱、建立（日期和時間）、源、模式和上次批處理狀態的列，以及上次更新資料集的日期和時間。

>[!NOTE]
>
>按一下搜尋列旁的篩選圖示，使用篩選功能僅檢視為[!DNL Profile]啟用的資料集。

![查看所有資料集](../images/tutorials/ingest-batch-data/datasets-overview.png)

## 建立資料集

若要建立資料集，請按一下「資料集」工作區右上角的&#x200B;**[!UICONTROL Create Dataset]**。

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

在&#x200B;**[!UICONTROL Create Dataset]**&#x200B;畫面上，選擇您要「[!UICONTROL Create Dataset from Schema]」還是「[!UICONTROL Create Dataset from CSV File]」。

在本教學課程中，將使用模式來建立資料集。 按一下&#x200B;**[!UICONTROL Create Dataset from Schema]**&#x200B;繼續。

![選擇資料來源](../images/tutorials/ingest-batch-data/create-dataset.png)

## 選擇資料集模式

在&#x200B;**[!UICONTROL Select Schema]**&#x200B;螢幕上，按一下要使用的方案旁邊的單選按鈕選擇方案。 在本教學課程中，資料集將使用「忠誠度成員」架構建立。 使用搜尋列來篩選結構描述是找到您所尋找的精確結構描述的有用方式。

選擇了要使用的方案旁邊的單選按鈕後，按一下&#x200B;**[!UICONTROL Next]**。

![選擇方案](../images/tutorials/ingest-batch-data/select-schema.png)

## 設定資料集

在&#x200B;**[!UICONTROL Configure Dataset]**&#x200B;畫面上，您必須為資料集指定名稱，而且可能也會提供資料集的說明。

**資料集名稱的附註：**

- 資料集名稱應簡短且具說明性，以便稍後在資料庫中輕鬆找到資料集。
- 資料集名稱必須是唯一的，這表示資料集名稱也應足夠具體，以免日後重複使用。
- 最好使用說明欄位來提供資料集的其他相關資訊，因為這可協助其他使用者在未來區隔資料集。

資料集有名稱和說明後，按一下&#x200B;**[!UICONTROL Finish]**。

![設定資料集](../images/tutorials/ingest-batch-data/configure-dataset.png)

## 資料集活動

現在已建立空的資料集，您已返回「資料集」工作區的&#x200B;**[!UICONTROL Dataset Activity]**&#x200B;標籤。 您應該會在工作區的左上角看到資料集名稱，以及「未新增任何批次」通知。 由於您尚未將任何批次新增至此資料集，因此預期會出現此情況。

在「資料集」工作區的右側，您會看到&#x200B;**[!UICONTROL Info]**&#x200B;標籤，其中包含與新資料集相關的資訊，例如資料集ID、名稱、說明、表格名稱、架構、串流和來源。 「資訊」標籤也包含資料集建立時間及其上次修改日期的相關資訊。

在「資訊」標籤中也有&#x200B;**[!UICONTROL Profile]**&#x200B;切換，用於啟用資料集以搭配[!DNL Real-time Customer Profile]使用。 此切換的使用，以及[!DNL Real-time Customer Profile]，將在下一節中詳細說明。

![資料集活動](../images/tutorials/ingest-batch-data/sample-dataset.png)

## 為[!DNL Real-time Customer Profile]啟用資料集

資料集用於將資料擷取到[!DNL Experience Platform]中，而資料最終用於識別個人並將來自多個來源的資訊結合在一起。 銜接資訊稱為[!DNL Real-Time Customer Profile]。 為了讓[!DNL Platform]知道哪些資訊應包含在[!DNL Real-Time Profile]中，可使用&#x200B;**[!UICONTROL Profile]**&#x200B;切換來標籤資料集以包含。

依預設，此切換為關閉。 如果您選擇在[!DNL Profile]上切換，所有收錄到資料集的資料都將用來協助識別個人，並將其[!DNL Real-Time Profile]接合在一起。

若要進一步瞭解[!DNL Real-time Customer Profile]和使用身分識別，請參閱[Identity Service](../../identity-service/home.md)檔案。

若要啟用[!DNL Real-time Customer Profile]的資料集，請按一下&#x200B;**[!UICONTROL Info]**&#x200B;標籤中的&#x200B;**[!UICONTROL Profile]**&#x200B;切換。

![描述檔切換](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

將出現一個對話框，要求您確認您要為[!DNL Real-time Customer Profile]啟用資料集。

![「啟用配置檔案」對話框](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

按一下&#x200B;**[!UICONTROL Enable]**，切換將會變成藍色，表示已開啟。

![啟用設定檔](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## 新增資料至資料集

資料可以多種不同的方式新增至資料集。 您可以選擇使用[!DNL Data Ingestion] API或ETL合作夥伴，例如[!DNL Unifi]或[!DNL Informatica]。 在本教學課程中，資料會使用UI中的&#x200B;**[!UICONTROL Add Data]**&#x200B;標籤新增至資料集。

若要開始將資料新增至資料集，請按一下&#x200B;**[!UICONTROL Add Data]**&#x200B;標籤。 您現在可以拖放檔案，或瀏覽您的電腦以尋找您要新增的檔案。

>[!NOTE]
>
>平台支援兩種檔案類型以擷取資料，Parce或JSON。 一次最多可以添加五個檔案，每個檔案的最大檔案大小為10 GB。

![「添加資料」頁籤](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## 上傳檔案

在您拖放（或瀏覽並選取）您要上傳的Parce或JSON檔案後，[!DNL Platform]將立即開始處理檔案，而&#x200B;**[!UICONTROL Uploading]**&#x200B;對話方塊將會出現在&#x200B;**[!UICONTROL Add Data]**&#x200B;標籤上，顯示檔案上傳的進度。

![上傳對話方塊](../images/tutorials/ingest-batch-data/uploading-file.png)

## 資料集度量

檔案上傳完成後，**[!UICONTROL Dataset Activity]**&#x200B;標籤不會再顯示「未新增任何批次」。 現在，**[!UICONTROL Dataset Activity]**&#x200B;標籤會顯示資料集度量。 由於批次尚未載入，所有量度在此階段會顯示「0」。

在標籤的底部有一個清單，顯示剛透過[&quot;新增資料至資料集&quot;](#add-data-to-dataset)程式所擷取之資料的&#x200B;**[!UICONTROL Batch ID]**。 另外還包括與批相關的資訊，包括提取日期、提取的記錄數和當前批狀態。

![資料集度量](../images/tutorials/ingest-batch-data/batch-id.png)

## 批次詳細資訊

按一下&#x200B;**[!UICONTROL Batch ID]**&#x200B;以檢視&#x200B;**[!UICONTROL Batch Overview]**，顯示有關批次的其他詳細資訊。 在批次完成載入後，有關批次的資訊將會更新，以顯示所擷取的記錄數和檔案大小。 狀態也會變更為「成功」或「失敗」。 如果批處理失敗， **[!UICONTROL Error Code]**&#x200B;部分將包含有關提取過程中任何錯誤的詳細資訊。

有關批處理提取的詳細資訊和常見問題，請參閱[批處理提取疑難解答指南](../batch-ingestion/troubleshooting.md)。

若要返回&#x200B;**[!UICONTROL Dataset Activity]**&#x200B;畫面，請按一下階層連結中資料集的名稱(**[!UICONTROL Loyalty Details]**)。

![批次概述](../images/tutorials/ingest-batch-data/batch-details.png)

## 預覽資料集

資料集準備就緒後，**[!UICONTROL Dataset Activity]**&#x200B;標籤頂端會顯示&#x200B;**[!UICONTROL Preview Dataset]**&#x200B;選項。

按一下&#x200B;**[!UICONTROL Preview Dataset]**&#x200B;以開啟對話方塊，顯示資料集內的範例資料。 如果使用模式建立資料集，則資料集模式的詳細資料會顯示在預覽的左側。 可以使用箭頭展開模式以查看模式結構。 預覽資料中的每個欄標題代表資料集中的欄位。

![資料集詳細資訊](../images/tutorials/ingest-batch-data/dataset-preview.png)

## 後續步驟和其他資源

現在您已建立資料集並成功將資料擷取至[!DNL Experience Platform]，您可以重複這些步驟以建立新資料集或將更多資料擷取至現有資料集。

若要進一步瞭解批次擷取，請閱讀[批次擷取概觀](../batch-ingestion/overview.md)，並觀賞以下影片以補充您的學習經驗。

>[!WARNING]
>
>下列視訊中顯示的[!DNL Platform] UI已過期。 請參閱上述檔案以取得最新的UI螢幕擷取和功能。

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
