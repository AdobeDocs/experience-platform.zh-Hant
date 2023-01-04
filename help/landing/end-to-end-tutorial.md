---
keywords: Experience Platform；首頁；熱門主題；CJA；歷程分析；客戶歷程分析；行銷活動協調；協調；客戶歷程；歷程；歷程協調；功能；地區
title: Adobe Experience Platform端對端範例工作流程
topic-legacy: getting started
description: 全面了解Adobe Experience Platform的基本端對端工作流程。
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 3%

---

# Adobe Experience Platform端對端範例工作流程

Adobe Experience Platform是市面上功能最強大、最靈活、最開放的系統，可用來建立和管理可提升客戶體驗的完整解決方案。  Platform 可讓組織集中和標準化來自任何系統的客戶資料與內容，並運用資料科學和機器學習技術大幅改善豐富個人化體驗的設計和傳遞。

Platform以RESTful API為基礎，向開發人員開放系統的完整功能，支援使用熟悉的工具輕鬆整合企業解決方案。 Platform可讓您擷取客戶資料、將資料分段至您要鎖定的對象，以及將這些對象啟用至外部目的地，從而衍生出客戶的整體檢視。 下列教學課程會顯示端對端工作流程，其中顯示從透過來源擷取到透過目的地啟用受眾的所有步驟。

![Experience Platform端對端工作流程](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## 快速入門

此端對端工作流程使用多個Adobe Experience Platform服務。 以下是此工作流程中使用的服務清單，其概覽連結如下：

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。 為了最能善用區段，請確定您的資料已根據 [資料模型最佳實務](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md):跨裝置和系統橋接身分，提供客戶及其行為的完整檢視。
- [來源](../sources/home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] 可讓您將儲存在 [!DNL Experience Platform] 與個人（例如客戶、潛在客戶、使用者或組織）相關而組成的較小群組。
- [[!DNL Real-Time Customer Profile]](../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
- [資料集](../catalog/datasets/overview.md):資料永續的儲存管理結構 [!DNL Experience Platform].
- [目的地](../destinations/home.md):目的地是與常用應用程式預先建立的整合，可順暢地啟動來自Platform的資料，以進行跨通路行銷活動、電子郵件行銷活動、目標廣告和許多其他使用案例。

## 建立 XDM 結構描述

將資料內嵌至Platform之前，您必須先建立XDM架構以說明該資料的結構。 在下一步中內嵌資料時，會將傳入的資料對應至此結構。 若要了解如何建立範例XDM結構，請閱讀以下的教學課程： [使用架構編輯器建立架構](../xdm/tutorials/create-schema-ui.md).

上述教學課程說明如何設定結構的身分欄位。 身分欄位代表一個欄位，可用來識別與記錄或時間序列事件相關的個別人員。 身分欄位是在Platform中建構客戶身分圖形的重要元件，這最終會影響即時客戶設定檔如何合併不同的資料片段，以完整了解客戶。 如需如何在Platform中檢視身分圖表的詳細資訊，請參閱 [如何使用身分圖表檢視器](../identity-service/ui/identity-graph-viewer.md).

您需要啟用您的結構以用於即時客戶設定檔，以便根據您的結構從資料中建構客戶設定檔。 請參閱 [啟用設定檔的結構](../xdm/ui/resources/schemas.md#profile) 如需詳細資訊，請參閱綱要UI指南。

## 將資料內嵌至Platform

建立XDM結構後，您就可以開始將資料匯入系統。

匯入Platform的所有資料都會在擷取時儲存至個別資料集。 資料集是對應至特定XDM結構的資料記錄集合。 資料可供使用之前 [!DNL Real-Time Customer Profile]，則必須明確設定相關資料集。 如需如何啟用設定檔資料集的完整指示，請參閱 [資料集UI指南](../catalog/datasets/user-guide.md#enable-profile) 和 [資料集設定API教學課程](../profile/tutorials/dataset-configuration.md). 設定資料集後，您就可以開始擷取資料。

Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加上標籤，以及增強傳入資料。 您可以從多種來源 (如 Adobe 應用程式、雲端型的儲存空間、資料庫和其他許多來源) 內嵌資料。 例如，您可以使用 [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). 可在 [來源連接器概觀](../sources/home.md).

如果您使用Amazon S3作為來源連接器，可以依照 [建立Amazon S3連接器](../sources/tutorials/api/create/cloud-storage/s3.md) 或上的UI教學課程 [建立Amazon S3連接器](../sources/tutorials/ui/create/cloud-storage/s3.md) 了解如何在連接器中建立、連線及內嵌資料。

有關源連接器的更多詳細說明，請閱讀 [來源連接器概觀](../sources/home.md). 若要進一步了解流量服務（來源所依據的API），請參閱 [流量服務API參考](https://www.adobe.io/experience-platform-apis/references/flow-service/).

透過來源連接器將資料匯入Platform，並儲存在啟用設定檔的資料集中後，系統就會根據您在XDM架構中設定的身分資料，自動建立客戶設定檔。

第一次將資料上傳至新資料集，或設定新的ETL程式或資料來源時，建議您仔細檢查資料，以確保資料已正確上傳，且產生的設定檔包含您預期的資料。 如需如何在Platform UI中存取客戶設定檔的詳細資訊，請參閱 [即時客戶個人檔案UI指南](../profile/ui/user-guide.md). 如需如何使用即時客戶設定檔API存取設定檔的詳細資訊，請參閱 [使用實體端點](../profile/api/entities.md).

## 評估您的資料

從擷取的資料成功產生設定檔後，您就可以使用細分來評估資料。 區段是定義個人子集合從您的設定檔存放區共用的特定屬性或行為的程式，以區分可行銷的一組人員和您的客戶群。 若要進一步了解分段，請閱讀 [細分服務概述](../segmentation/home.md).

### 建立區段定義

若要開始，您必須建立區段定義來將客戶叢集化，以建立目標受眾。 區段定義是規則的集合，可用來定義您要鎖定的對象。 若要建立區段定義，您可以依照UI指南中的指示，使用 [區段產生器](../segmentation/ui/segment-builder.md) 或API教學課程(於 [建立區段](../segmentation/tutorials/create-a-segment.md).

建立區段定義後，請務必記下區段定義ID。

### 評估區段定義

建立區段定義後，您可以建立區段工作以評估為一次性例項的區段，或建立排程以持續評估區段。

要按需評估段定義，您可以建立段任務。 區段工作是非同步程式，會根據參考的區段定義和合併原則建立新的對象區段。 合併原則是一組規則，Platform會使用這些規則來判斷要用來建立客戶設定檔的資料，以及當來源之間有差異時，系統會優先處理哪些資料。 若要了解如何使用合併原則，請參閱 [合併策略UI指南](../profile/merge-policies/ui-guide.md).

建立和評估區段工作後，您就能取得區段的相關資訊，例如對象大小或處理期間可能發生的錯誤。 若要了解如何建立區段工作，包括您需要提供的所有詳細資訊，請參閱 [區段作業開發人員指南](../segmentation/api/segment-jobs.md).

若要持續評估區段定義，您可以建立並啟用排程。 排程是一種工具，可用於在指定時間每天自動執行區段工作一次。 若要了解如何建立和啟用排程，您可以遵循 [排程端點](../segmentation/api/schedules.md).

## 匯出評估的資料

建立一次性區段工作或進行中的排程後，您可以建立區段匯出工作，將結果匯出至資料集，或將結果匯出至目的地。 以下各節就這兩個備選方案提供指導。

### 將評估的資料匯出至資料集

建立一次性區段工作或進行中的排程後，您可以建立區段匯出工作來匯出結果。 區段匯出工作是非同步任務，會將評估對象的相關資訊傳送至資料集。

建立匯出工作之前，您必須先建立資料集，將資料匯出至。 若要了解如何建立資料集，請閱讀 [建立target資料集](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) 在評估區段的教學課程中，請務必在建立資料集ID後加以注意。 建立資料集後，您可以建立匯出工作。 若要了解如何建立匯出工作，您可以遵循 [導出作業終結點](../segmentation/api/export-jobs.md).

### 將評估的資料導出到目標

或者，在建立一次性區段工作或進行中的排程後，您可以將結果匯出至目的地。 目的地是端點，例如外部服務上的Adobe應用程式，可在此啟動和傳送對象。 您可以在 [目的地目錄](../destinations/catalog/overview.md).

如需如何啟用資料以批次或透過電子郵件傳送行銷目的地的指示，請參閱 [如何使用Platform UI啟用受眾資料以批次描述檔匯出目的地](../destinations/ui/activate-batch-profile-destinations.md) 和 [如何使用流量服務API連線至批次目的地及啟用資料的指南](../destinations/api/connect-activate-batch-destinations.md).

## 監視您的Platform資料活動

Platform可讓您透過使用資料流來追蹤資料的處理方式，這些資料流是跨Platform不同元件移動資料之作業的表示。 這些資料流是在不同服務間配置的，有助於將資料從源連接器移動到目標資料集，然後由資料集使用 [!DNL Identity Service] 和 [!DNL Real-Time Customer Profile] 最終啟動至目的地之前。 監控控制面板可以以視覺化方式呈現資料流歷程。 若要了解如何監視Platform UI內的資料流，請參閱 [監視源的資料流](../dataflows/ui/monitor-sources.md) 和 [監視目標的資料流](../dataflows/ui/monitor-destinations.md).

您也可以使用統計量度和事件通知來監控Platform活動，方法是使用 [!DNL Observability Insights]. 您可以透過Platform UI訂閱警報通知，或將通知傳送至已設定的WebHook。 如需如何從Experience PlatformUI檢視、啟用、停用和訂閱可用警報的詳細資訊，請參閱 [[!UICONTROL 警報] UI指南](../observability/alerts/ui.md). 如需如何透過WebHook接收警報的詳細資訊，請參閱 [訂閱Adobe I/O事件通知](../observability/alerts/subscribe.md).

## 後續步驟

閱讀本教學課程後，您就可了解Platform的簡單端對端流程。 若要進一步了解Adobe Experience Platform，請閱讀 [平台概觀](./home.md). 若要進一步了解如何使用Platform UI和Platform API，請參閱 [Platform UI指南](./ui-guide.md) 和 [Platform API指南](./api-guide.md) 分別為5個。
