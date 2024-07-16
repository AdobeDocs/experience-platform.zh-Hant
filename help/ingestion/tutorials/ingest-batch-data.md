---
keywords: Experience Platform；首頁；熱門主題；擷取；擷取批次資料；教學課程；批次擷取；教學課程；ui指南；
solution: Experience Platform
title: 將資料擷取至Experience Platform
type: Tutorial
description: Adobe Experience Platform可讓您以Parquet檔案的形式，輕鬆將資料匯入為批次檔案，或是符合已知Experience Data Model (XDM)架構的資料。
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: 8351f6907a0dc4a4bba01c7f6e9dec7c376c8575
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---

# 將資料內嵌至Adobe Experience Platform

Adobe Experience Platform可讓您輕鬆將資料匯入[!DNL Platform]作為批次檔案。 要擷取的資料範例可能包括CRM系統中平面檔案（例如Parquet檔案）的設定檔資料，或是符合結構描述登入中已知[!DNL Experience Data Model] (XDM)結構描述的資料。

## 快速入門

若要完成本教學課程，您必須有[!DNL Experience Platform]的存取權。 如果您沒有[!DNL Experience Platform]中組織的存取權，請在繼續之前與您的系統管理員交談。

如果您偏好使用資料擷取API來擷取資料，請先閱讀[批次擷取開發人員指南](../batch-ingestion/api-overview.md)。

## 資料集工作區

[!DNL Experience Platform]中的資料集工作區可讓您檢視和管理貴組織建立的所有資料集，並建立新的資料集。

按一下左側導覽中的&#x200B;**[!UICONTROL 資料集]**&#x200B;以檢視「資料集」工作區。 資料集工作區包含資料集清單，其中包括顯示名稱、建立時間（日期和時間）、來源、結構描述和上次批次狀態，以及上次更新資料集的日期和時間的欄。

>[!NOTE]
>
>按一下搜尋列旁的篩選圖示，即可使用篩選功能，僅檢視為[!DNL Profile]啟用的資料集。

![檢視所有資料集](../images/tutorials/ingest-batch-data/datasets-overview.png)

## 建立資料集

若要建立資料集，請按一下資料集工作區右上角的&#x200B;**[!UICONTROL 建立資料集]**。

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

在&#x200B;**[!UICONTROL 建立資料集]**&#x200B;畫面上，選取您要「[!UICONTROL 從結構描述建立資料集]」還是「[!UICONTROL 從CSV檔案建立資料集]」。

在本教學課程中，將會使用結構描述來建立資料集。 按一下&#x200B;**[!UICONTROL 從結構描述建立資料集]**&#x200B;以繼續。

![選取資料來源](../images/tutorials/ingest-batch-data/create-dataset.png)

## 選取資料集結構描述

在&#x200B;**[!UICONTROL 選取結構描述]**&#x200B;畫面上，按一下要使用的結構描述旁的單選按鈕來選擇結構描述。 在本教學課程中，將使用忠誠會員結構描述製作資料集。 使用搜尋列來篩選結構描述是找出您要尋找的確切結構描述的實用方式。

選取要使用的結構描述旁邊的單選按鈕後，按一下&#x200B;**[!UICONTROL 下一步]**。

![選取結構描述](../images/tutorials/ingest-batch-data/select-schema.png)

## 設定資料集

在&#x200B;**[!UICONTROL 設定資料集]**&#x200B;畫面上，您必須為資料集命名，也可以提供資料集的說明。

**資料集名稱的附註：**

- 資料集名稱應簡短且具有描述性，以便日後在程式庫中輕鬆找到資料集。
- 資料集名稱必須是唯一的，這表示它也應該是足夠具體的，以使其在將來不會重複使用。
- 最佳實務是使用說明欄位來提供資料集的額外資訊，因為這樣可協助其他使用者日後區分資料集。

資料集有了名稱和描述後，請按一下&#x200B;**[!UICONTROL 完成]**。

![設定資料集](../images/tutorials/ingest-batch-data/configure-dataset.png)

## 資料集活動

現在已建立空的資料集，而且您已返回「資料集」工作區中的&#x200B;**[!UICONTROL 資料集活動]**&#x200B;索引標籤。 您應該會在工作區的左上角看到資料集的名稱，並附上「未新增任何批次」的通知。 這是正常情況，因為您尚未新增任何批次至此資料集。

在資料集工作區的右側，您會看到&#x200B;**[!UICONTROL 資訊]**&#x200B;索引標籤，其中包含與新資料集相關的資訊，例如資料集ID、名稱、說明、資料表名稱、結構描述、串流和來源。 資訊索引標籤也包含資料集的建立時間及其上次修改日期的相關資訊。

此外，在「資訊」標籤中還有&#x200B;**[!UICONTROL 設定檔]**&#x200B;切換，用於啟用您的資料集以搭配[!DNL Real-Time Customer Profile]使用。 此切換及[!DNL Real-Time Customer Profile]的使用將在下一節中詳細說明。

![資料集活動](../images/tutorials/ingest-batch-data/sample-dataset.png)

## 為[!DNL Real-Time Customer Profile]啟用資料集

資料集用於將資料擷取到[!DNL Experience Platform]，而該資料最終用於識別個人並將來自多個來源的資訊拼接在一起。 該拼接資訊稱為[!DNL Real-Time Customer Profile]。 為了讓[!DNL Platform]知道哪些資訊應包含在[!DNL Real-Time Profile]中，可以使用&#x200B;**[!UICONTROL 設定檔]**&#x200B;切換將資料集標示為包含。

依預設，此切換為關閉。 如果您選擇開啟[!DNL Profile]，所有擷取到資料集中的資料都將用於協助識別個人並將其[!DNL Real-Time Profile]拼接在一起。

若要進一步瞭解[!DNL Real-Time Customer Profile]和使用身分，請檢閱[身分識別服務](../../identity-service/home.md)檔案。

若要啟用[!DNL Real-Time Customer Profile]的資料集，請在&#x200B;**[!UICONTROL 資訊]**&#x200B;索引標籤中按一下&#x200B;**[!UICONTROL 設定檔]**&#x200B;切換按鈕。

![設定檔切換](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

會出現對話方塊，要求您確認要啟用[!DNL Real-Time Customer Profile]的資料集。

![啟用設定檔對話方塊](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

按一下[啟用]****，切換將變成藍色，表示已開啟。

已為設定檔](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)啟用![

## 新增資料到資料集

資料可以透過多種不同方式新增到資料集中。 您可以選擇使用[!DNL Data Ingestion] API或ETL夥伴，例如[!DNL Unifi]或[!DNL Informatica]。 在本教學課程中，將會使用UI內的&#x200B;**[!UICONTROL 新增資料]**&#x200B;索引標籤，將資料新增到資料集中。

若要開始新增資料到資料集，請按一下&#x200B;**[!UICONTROL 新增資料]**&#x200B;索引標籤。 您現在可以拖放檔案，或瀏覽電腦尋找您要新增的檔案。

>[!NOTE]
>
>Platform支援兩種檔案型別以進行資料擷取：Parquet或JSON。 您一次最多可以新增5個檔案，每個檔案的大小上限為1 GB。

![新增資料索引標籤](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## 上傳檔案 {#upload-file}

拖放（或瀏覽並選取）您要上傳的Parquet或JSON檔案後，[!DNL Platform]將立即開始處理該檔案，且&#x200B;**[!UICONTROL 新增資料]**&#x200B;索引標籤上將會顯示&#x200B;**[!UICONTROL 上傳]**&#x200B;對話方塊，顯示檔案上傳的進度。

![正在上傳對話方塊](../images/tutorials/ingest-batch-data/uploading-file.png)

## 資料集量度

檔案上傳完成後，**[!UICONTROL 資料集活動]**&#x200B;索引標籤不再顯示「未新增任何批次」。 **[!UICONTROL 資料集活動]**&#x200B;索引標籤現在改為顯示資料集量度。 此階段所有量度都會顯示「0」，因為批次尚未載入。

索引標籤底部是清單，顯示剛透過[「將資料新增至資料集」](#add-data-to-dataset)程式擷取的資料的&#x200B;**[!UICONTROL 批次ID]**。 也包括與批次相關的資訊，包括擷取日期、擷取的記錄數以及目前的批次狀態。

![資料集量度](../images/tutorials/ingest-batch-data/batch-id.png)

## 批次詳細資料

按一下&#x200B;**[!UICONTROL 批次ID]**&#x200B;以檢視&#x200B;**[!UICONTROL 批次總覽]**，顯示批次的其他詳細資料。 批次載入完成後，批次的相關資訊將會更新，以顯示擷取的記錄數量和檔案大小。 狀態也會變更為「成功」或「失敗」。 如果批次失敗，**[!UICONTROL 錯誤碼]**&#x200B;區段將包含有關擷取期間任何錯誤的詳細資料。

如需有關批次擷取的詳細資訊和常見問題，請參閱[批次擷取疑難排解指南](../batch-ingestion/troubleshooting.md)。

若要返回&#x200B;**[!UICONTROL 資料集活動]**&#x200B;畫面，請按一下階層連結中的資料集名稱（**[!UICONTROL 熟客方案詳細資料]**）。

![批次總覽](../images/tutorials/ingest-batch-data/batch-details.png)

## 預覽資料集

資料集準備就緒後，**[!UICONTROL 預覽資料集]**&#x200B;的選項會顯示在&#x200B;**[!UICONTROL 資料集活動]**&#x200B;索引標籤的頂端。

按一下&#x200B;**[!UICONTROL 預覽資料集]**&#x200B;以開啟對話方塊，顯示資料集中的範例資料。 如果資料集是使用結構描述建立的，則資料集結構描述的詳細資料將顯示在預覽的左側。 您可以使用箭頭展開結構描述以檢視結構描述結構。 預覽資料中的每個欄標題代表資料集中的欄位。

![資料集詳細資料](../images/tutorials/ingest-batch-data/dataset-preview.png)

## 後續步驟和其他資源

現在您已建立資料集並成功將資料內嵌至[!DNL Experience Platform]，您可以重複這些步驟來建立新資料集，或將更多資料內嵌至現有資料集。

若要深入瞭解批次擷取，請閱讀[批次擷取概觀](../batch-ingestion/overview.md)，並觀看以下影片以補充您的學習。

>[!WARNING]
>
>下列影片中顯示的[!DNL Platform] UI已過期。 請參閱上述檔案，瞭解最新的UI熒幕擷取畫面及功能。

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
