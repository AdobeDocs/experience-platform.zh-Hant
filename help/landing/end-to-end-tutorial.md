---
keywords: Experience Platform；首頁；熱門主題；CJA；歷程分析；客戶歷程分析；行銷活動協調；協調；客戶歷程；歷程；歷程協調；功能；地區
title: Adobe Experience Platform端對端範例工作流程
description: 以高層級方式瞭解Adobe Experience Platform的基本端對端工作流程。
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 1%

---

# Adobe Experience Platform端對端範例工作流程

Adobe Experience Platform是市面上功能最強大、最靈活、最開放的系統，可建置和管理可提升客戶體驗的完整解決方案。 Platform可讓組織集中和標準化來自任何系統的客戶資料與內容，並運用資料科學和機器學習技術大幅改善豐富個人化體驗的設計和傳遞。

Platform以RESTful API為基礎，向開發人員公開系統的完整功能，以支援使用熟悉工具輕鬆整合企業解決方案。 Platform可讓您內嵌客戶資料、將資料分段至您要鎖定的對象，並將這些對象啟用至外部目的地，進而取得客戶的整體檢視。 下列教學課程顯示端對端工作流程，顯示從透過來源擷取到透過目的地啟用對象的所有步驟。

![Experience Platform端對端工作流程](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## 快速入門

此端對端工作流程使用多個Adobe Experience Platform服務。 以下是此工作流程中使用的服務清單，以及其概觀連結：

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md)： [!DNL Platform]用來組織客戶體驗資料的標準化架構。 若要充分利用「細分」，請確定您的資料已根據[資料模型最佳實務](../xdm/schema/best-practices.md)被擷取為設定檔和事件。
- [[!DNL Identity Service]](../identity-service/home.md)：透過跨裝置和系統橋接身分，讓您全面瞭解客戶及其行為。
- [來源](../sources/home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
- [[!DNL Segmentation Service]](../segmentation/home.md)： [!DNL Segmentation Service]可讓您將儲存在[!DNL Experience Platform]中與個人（例如客戶、潛在客戶、使用者或組織）相關的資料分割成較小的群組。
- [[!DNL Real-Time Customer Profile]](../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
- [資料集](../catalog/datasets/overview.md)： [!DNL Experience Platform]中資料持續性的儲存和管理建構。
- [目的地](../destinations/home.md)：目的地是預先建置的與常用應用程式的整合，可讓您順暢地從Platform啟用資料，以用於跨管道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例。

## 建立 XDM 結構描述

在將資料內嵌至Platform之前，您必須先建立XDM結構描述以說明該資料的結構。 當您在下一步內嵌資料時，會將您的傳入資料對應至此結構描述。 若要瞭解如何建立範例XDM結構描述，請閱讀有關[使用結構描述編輯器](../xdm/tutorials/create-schema-ui.md)建立結構描述的教學課程。

上述教學課程說明如何設定結構描述的身分欄位。 身分欄位代表可用來識別與記錄或時間序列事件相關的個人欄位。 身分欄位是在Platform中建構客戶身分圖表的重要元件，這最終會影響Real-time Customer Profile如何將不同的資料片段合併在一起，以獲得客戶的完整檢視。 如需有關如何在Platform中檢視身分圖表的詳細資訊，請參閱[如何使用身分圖表檢視器](../identity-service/features/identity-graph-viewer.md)的教學課程。

您需要啟用結構描述以用於Real-time Customer Profile，以便可以根據您的結構描述從資料建構客戶設定檔。 如需詳細資訊，請參閱結構描述UI指南中[為設定檔](../xdm/ui/resources/schemas.md#profile)啟用結構描述的相關章節。

## 將您的資料內嵌至Platform

建立XDM結構描述後，您就可以開始將資料引進系統中。

所有帶入Platform的資料都會在擷取時儲存至個別資料集。 資料集是對應至特定XDM結構描述的資料記錄集合。 您必須先明確設定相關資料集，[!DNL Real-Time Customer Profile]才能使用您的資料。 如需有關如何為設定檔啟用資料集的完整指示，請參閱[資料集UI指南](../catalog/datasets/user-guide.md#enable-profile)和[資料集組態API教學課程](../profile/tutorials/dataset-configuration.md)。 設定資料集後，您就可以開始將資料擷取至其中。

Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源 (如 Adobe 應用程式、雲端型的儲存空間、資料庫和其他許多來源) 內嵌資料。 例如，您可以使用[Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md)來內嵌資料。 您可以在[來源聯結器概觀](../sources/home.md)中找到可用來源的完整清單。

如果您使用Amazon S3做為來源聯結器，您可以依照有關[建立Amazon S3聯結器](../sources/tutorials/api/create/cloud-storage/s3.md)的API教學課程，或有關[建立Amazon S3聯結器](../sources/tutorials/ui/create/cloud-storage/s3.md)的UI教學課程中的指示，瞭解如何在聯結器內建立、連線及擷取資料。

如需來源聯結器的詳細指示，請閱讀[來源聯結器概觀](../sources/home.md)。 若要深入瞭解流量服務、來源所依據的API，請閱讀[流量服務API參考](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

透過來源聯結器將您的資料匯入Platform並儲存在已啟用設定檔的資料集後，就會根據您在XDM結構描述中設定的身分資料自動建立客戶設定檔。

首次將資料上傳到新資料集時，或設定新的ETL流程或資料來源時，建議仔細檢查資料，確保資料已正確上傳，且產生的設定檔包含您期望的資料。 如需如何在Platform UI中存取客戶設定檔的詳細資訊，請參閱[即時客戶設定檔UI指南](../profile/ui/user-guide.md)。 如需有關如何使用即時客戶設定檔API存取設定檔的詳細資訊，請參閱[使用實體端點](../profile/api/entities.md)的指南。

## 評估您的資料

一旦您從內嵌的資料成功產生設定檔後，您就可以使用細分來評估資料。 區段是定義個人資料存放區中之個人子集所共用的特定屬性或行為的程式，以便區分可行銷人群組與您的客戶群。 若要深入瞭解細分，請閱讀[細分服務總覽](../segmentation/home.md)。

### 建立區段定義

若要開始使用，您必須建立區段定義，以叢集客戶來建立目標對象。 區段定義是規則的集合，可用來定義您要鎖定的對象。 若要建立區段定義，您可以依照使用[區段產生器](../segmentation/ui/segment-builder.md)的UI指南中的指示，或依照[建立區段](../segmentation/tutorials/create-a-segment.md)的API教學課程中的指示進行。

建立區段定義後，請務必保留區段定義ID的備註。

### 評估您的區段定義

建立區段定義後，您可以建立區段作業，以一次性例項評估區段，或建立排程以持續評估區段。

若要依需求評估節段定義，您可以建立節段工單。 區段作業為非同步程式，可根據參照的區段定義和合併原則建立新的受眾區段。 合併原則是一組規則，Platform可使用此規則來決定要使用哪些資料來建立客戶設定檔，以及當來源之間有差異時，會優先處理哪些資料。 若要瞭解如何使用合併原則，請參閱[合併原則使用者介面指南](../profile/merge-policies/ui-guide.md)。

建立並評估區段作業後，您就可以取得關於區段的資訊，例如對象規模或處理期間可能發生的錯誤。 若要瞭解如何建立區段作業，包括您需要提供的所有詳細資訊，請閱讀[區段作業開發人員指南](../segmentation/api/segment-jobs.md)。

若要持續評估區段定義，您可以建立並啟用排程。 排程是一種工具，可用於在指定時間每天自動執行區段作業一次。 若要瞭解如何建立及啟用排程，您可以依照[排程端點](../segmentation/api/schedules.md)的API指南中的指示操作。

## 匯出您的評估資料

建立一次性區段作業或進行中的排程後，您可以建立區段匯出作業以將結果匯出至資料集，或將結果匯出至目的地。 以下章節提供這兩個選項的指引。

### 將評估過的資料匯出至資料集

建立一次性區段作業或進行中的排程後，您可以建立區段匯出作業來匯出結果。 區段匯出作業是一種非同步工作，會將評估對象的相關資訊傳送至資料集。

在建立匯出作業之前，您必須先建立資料集以匯出資料。 若要瞭解如何建立資料集，請閱讀教學課程中有關評估區段的[建立目標資料集](../segmentation/tutorials/evaluate-a-segment.md#create-dataset)的章節，以確保您在建立資料集後記下資料集ID。 建立資料集後，您可以建立匯出作業。 若要瞭解如何建立匯出作業，您可以依照[匯出作業端點](../segmentation/api/export-jobs.md)的API指南中的指示操作。

### 將評估後的資料匯出至目的地

或者，在建立一次性區段作業或進行中的排程後，您可以將結果匯出至目的地。 目的地是端點，例如外部服務上的Adobe應用程式，可在此啟用和傳送對象。 您可以在[目的地目錄](../destinations/catalog/overview.md)中找到可用目的地的完整清單。

如需如何啟用批次或電子郵件行銷目的地的資料說明，請參閱[如何使用Platform UI](../destinations/ui/activate-batch-profile-destinations.md)啟用批次設定檔匯出目的地的受眾資料的教學課程，以及如何使用Flow Service API連線到批次目的地並啟用資料的[指南](../destinations/api/connect-activate-batch-destinations.md)。

## 監視您的Platform資料活動

Platform可讓您透過資料流追蹤資料的處理方式，資料流代表在平台各種元件之間行動資料的工作。 這些資料流是跨不同服務設定的，有助於將資料從來源聯結器移至目標資料集，然後由[!DNL Identity Service]和[!DNL Real-Time Customer Profile]使用，最後啟用至目的地。 監視儀表板可讓您以視覺化方式呈現資料流的歷程。 若要瞭解如何監視Platform UI中的資料流，請參閱[監視來源資料流](../dataflows/ui/monitor-sources.md)和[監視目的地資料流](../dataflows/ui/monitor-destinations.md)的教學課程。

您也可以使用[!DNL Observability Insights]，透過使用統計量度和事件通知來監視Platform活動。 您可以透過Platform UI訂閱警報通知，或將其傳送至已設定的webhook。 如需有關如何從Experience PlatformUI檢視、啟用、停用及訂閱可用警示的詳細資訊，請參閱[[!UICONTROL 警示] UI指南](../observability/alerts/ui.md)。 如需有關如何透過Webhook接收警示的詳細資訊，請參閱[訂閱Adobe I/O事件通知](../observability/alerts/subscribe.md)的指南。

## 後續步驟

閱讀本教學課程後，您已大致瞭解Platform的簡易端對端流程。 若要進一步瞭解Adobe Experience Platform，請閱讀[平台概觀](./home.md)。 若要進一步瞭解如何使用Platform UI和Platform API，請分別閱讀[Platform UI指南](./ui-guide.md)和[Platform API指南](./api-guide.md)。
