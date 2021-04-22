---
keywords: Experience Platform;home；熱門主題；enable dataset;Dataset;dataset
solution: Experience Platform
title: 資料集UI指南
topic-legacy: datasets
description: 瞭解如何在Adobe Experience Platform用戶介面中使用資料集時執行常見操作。
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
translation-type: tm+mt
source-git-commit: d2f19cc97082f75e66cf38e54b5bdb89482930ed
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---

# 資料集UI指南

本使用手冊提供在Adobe Experience Platform用戶介面中使用資料集時執行常見操作的說明。

## 快速入門

本使用手冊需要對Adobe Experience Platform的下列元件有正確的理解：

* [資料集](overview.md):中用於資料持久性的儲存和管理結構 [!DNL Experience Platform]。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [架構構成基礎](../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器](../../xdm/tutorials/create-schema-ui.md):瞭解如何使用使用者介面建立您自己 [!DNL Schema Editor] 的自 [!DNL Platform] 訂XDM架構。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md):確保遵守有關客戶資料使用的法規、限制和政策。

## 檢視資料集

在[!DNL Experience Platform] UI中，按一下左側導覽中的&#x200B;**[!UICONTROL Datasets]**&#x200B;以開啟&#x200B;**[!UICONTROL Datasets]**&#x200B;控制面板。 控制面板會列出您組織的所有可用資料集。 會針對每個列出的資料集顯示詳細資訊，包括其名稱、資料集所遵守的架構，以及最近擷取執行的狀態。

![](../images/datasets/user-guide/browse-datasets.png)

按一下資料集的名稱以存取其&#x200B;**[!UICONTROL Dataset activity]**&#x200B;畫面，並查看您選取之資料集的詳細資訊。 該活動頁籤包括圖形，該圖形可視化正在消耗的消息速率以及成功和失敗批的清單。

![](../images/datasets/user-guide/dataset-activity-1.png)
![](../images/datasets/user-guide/dataset-activity-2.png)

## 預覽資料集

在&#x200B;**[!UICONTROL Dataset activity]**&#x200B;畫面中，按一下畫面右上角的&#x200B;**[!UICONTROL Preview dataset]**&#x200B;以預覽最多100列資料。 如果資料集為空，預覽連結將會停用，而會指出預覽不可用。

![](../images/datasets/user-guide/click-to-preview.png)

在預覽視窗中，資料集的架構階層檢視會顯示在右側。

![](../images/datasets/user-guide/preview-dataset.png)

要獲得更強穩的資料存取方法，[!DNL Experience Platform]提供下游服務，如[!DNL Query Service]和[!DNL JupyterLab]以探索和分析資料。 如需詳細資訊，請參閱下列檔案：

* [查詢服務概述](../../query-service/home.md)
* [JupyterLab使用指南](../../data-science-workspace/jupyterlab/overview.md)

## 建立資料集{#create}

若要建立新資料集，請先按一下&#x200B;**[!UICONTROL Datasets]**&#x200B;控制面板中的&#x200B;**[!UICONTROL Create dataset]**。

![](../images/datasets/user-guide/click-to-create.png)

在下一個畫面中，您會看到下列兩個建立新資料集的選項：

* [從架構建立資料集](#schema)
* [從CSV檔案建立資料集](#csv)

### 使用現有模式{#schema}建立資料集

在&#x200B;**[!UICONTROL Create dataset]**&#x200B;畫面中，按一下&#x200B;**[!UICONTROL Create dataset from schema]**&#x200B;以建立新的空資料集。

![](../images/datasets/user-guide/create-dataset-schema.png)

出現&#x200B;**[!UICONTROL Select schema]**&#x200B;步驟。 在按一下&#x200B;**[!UICONTROL Next]**&#x200B;之前，瀏覽模式清單並選擇資料集將遵循的模式。

![](../images/datasets/user-guide/select-schema.png)

出現&#x200B;**[!UICONTROL Configure dataset]**&#x200B;步驟。 為資料集提供名稱和選用說明，然後按一下&#x200B;**[!UICONTROL Finish]**&#x200B;以建立資料集。

![](../images/datasets/user-guide/configure-dataset-schema.png)

### 使用CSV檔案{#csv}建立資料集

當使用CSV檔案建立資料集時，會建立臨機模式，以提供資料集符合所提供CSV檔案的結構。 在&#x200B;**[!UICONTROL Create dataset]**&#x200B;畫面中，按一下說明&#x200B;**[!UICONTROL Create dataset from CSV file]**&#x200B;的方塊。

![](../images/datasets/user-guide/create-dataset-csv.png)

出現&#x200B;**[!UICONTROL Configure]**&#x200B;步驟。 為資料集提供名稱和選用說明，然後按一下&#x200B;**[!UICONTROL Next]**。

![](../images/datasets/user-guide/configure-dataset-csv.png)

出現&#x200B;**[!UICONTROL Add data]**&#x200B;步驟。 將CSV檔案拖放至畫面中央，或按一下&#x200B;**[!UICONTROL Browse]**&#x200B;來瀏覽檔案目錄，即可上傳該檔案。 該檔案最大可以有10GB的大小。 上傳CSV檔案後，按一下&#x200B;**[!UICONTROL Save]**&#x200B;以建立資料集。

>[!NOTE]
>
>CSV欄名稱必須以英數字元開頭，且只能包含字母、數字和底線。

![](../images/datasets/user-guide/add-csv-data.png)

## 啟用即時客戶個人資料資料集{#enable-profile}

每個資料集都能運用其收錄的資料豐富客戶個人檔案。 若要這麼做，資料集所遵循的架構必須相容，才能用於[!DNL Real-time Customer Profile]。 相容的架構符合下列需求：

* 架構至少有一個屬性指定為標識屬性。
* 架構具有定義為主標識的身份屬性。

有關為[!DNL Profile]啟用架構的詳細資訊，請參閱[架構編輯器使用手冊](../../xdm/tutorials/create-schema-ui.md)。

若要啟用描述檔的資料集，請存取其&#x200B;**[!UICONTROL Dataset activity]**&#x200B;畫面，然後按一下&#x200B;**[!UICONTROL Profile]**&#x200B;在&#x200B;**[!UICONTROL Properties]**&#x200B;欄內切換。 啟用後，資料集中的資料也會用來填入客戶個人檔案。

>[!NOTE]
>
>如果資料集已包含資料，且已啟用[!DNL Profile]，則[!DNL Profile]不會自動使用現有資料。 在[!DNL Profile]啟用資料集後，建議您重新收錄任何現有資料，讓其為客戶個人檔案提供資料。

![](../images/datasets/user-guide/enable-dataset-profiles.png)

## 在資料集上管理並強制執行資料控管

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 請參閱[資料治理概述](../../data-governance/home.md)以進一步瞭解標籤，或參閱[資料使用標籤使用指南](../../data-governance/labels/overview.md)以取得如何將標籤套用至資料集的指示。

## 刪除資料集

您可以先存取資料集的&#x200B;**[!UICONTROL Dataset activity]**&#x200B;畫面，以刪除資料集。 然後，按一下&#x200B;**[!UICONTROL Delete dataset]**&#x200B;將其刪除。

>[!NOTE]
>
>無法刪除由Adobe應用程式和服務(如Adobe Analytics、Adobe Audience Manager或[!DNL Offer Decisioning])建立和使用的資料集。

![](../images/datasets/user-guide/delete-dataset.png)

隨即出現確認框。 按一下&#x200B;**[!UICONTROL Delete]**&#x200B;以確認刪除資料集。

![](../images/datasets/user-guide/confirm-delete.png)

## 刪除啟用設定檔的資料集

如果[!DNL Profile]啟用資料集，透過UI刪除該資料集將會從「資料湖」和「平台」中的「設定檔」儲存區中將其刪除。

您只能使用即時客戶設定檔API從[!DNL Profile]商店刪除資料集（將資料保留在資料湖中）。 如需詳細資訊，請參閱[描述檔系統作業API端點指南](../../profile/api/profile-system-jobs.md)。

## 監控資料擷取

在[!DNL Experience Platform] UI中，按一下左側導覽中的&#x200B;**[!UICONTROL Monitoring]**。 **[!UICONTROL Monitoring]**&#x200B;控制面板可讓您檢視來自批次或串流擷取的傳入資料狀態。 要查看單個批的狀態，請按一下&#x200B;**[!UICONTROL Batch end-to-end]**&#x200B;或&#x200B;**[!UICONTROL Streaming end-to-end]**。 控制面板會列出所有批次或串流擷取執行，包括成功、失敗或仍在進行中的執行。 每個清單都會提供批次的詳細資訊，包括批次ID、目標資料集的名稱，以及所擷取的記錄數。 如果[!DNL Profile]啟用目標資料集，則也會顯示所擷取的身分和描述檔記錄數。

![](../images/datasets/user-guide/batch-listing.png)

您可以按一下個別的&#x200B;**[!UICONTROL Batch ID]**&#x200B;來存取&#x200B;**[!UICONTROL Batch overview]**&#x200B;控制面板，並查看批次的詳細資訊，包括批次無法收錄的錯誤記錄。

![](../images/datasets/user-guide/batch-overview.png)

如果要刪除批，可按一下儀表板右上角附近的&#x200B;**[!UICONTROL Delete batch]**&#x200B;進行刪除。 這麼做也會從批次原本擷取到的資料集中移除其記錄。

![](../images/datasets/user-guide/delete-batch.png)

## 後續步驟

本使用手冊提供了在[!DNL Experience Platform]用戶介面中使用資料集時執行常見操作的說明。 有關執行涉及資料集的常見[!DNL Platform]工作流的步驟，請參閱以下教程：

* [使用API建立資料集](create.md)
* [使用資料存取API查詢資料集資料](../../data-access/home.md)
* [使用API為即時客戶個人檔案和身分服務設定資料集](../../profile/tutorials/dataset-configuration.md)
