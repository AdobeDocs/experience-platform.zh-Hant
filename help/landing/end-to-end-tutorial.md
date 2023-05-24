---
keywords: Experience Platform；首頁；熱門主題；CJA；行程分析；客戶行程分析；活動業務流程；業務流程；客戶行程；行程；行程協調；區域
title: Adobe Experience Platform端到端示例工作流
description: 瞭解Adobe Experience Platform的基本端到端高級工作流。
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 3%

---

# Adobe Experience Platform端到端示例工作流

Adobe Experience Platform是市場上功能最強大、最靈活、最開放的系統，用於構建和管理能夠推動客戶體驗的完整解決方案。  Platform 可讓組織集中和標準化來自任何系統的客戶資料與內容，並運用資料科學和機器學習技術大幅改善豐富個人化體驗的設計和傳遞。

該平台基於REST風格的API而構建，它向開發人員公開了系統的全部功能，支援使用熟悉的工具輕鬆整合企業解決方案。 平台允許您通過接收客戶資料、將資料分段到您要瞄準的受眾，以及將這些受眾激活到外部目標來獲取客戶的整體視圖。 以下教程將顯示端到端工作流，其中顯示了從通過源接收到通過目標激活受眾的所有步驟。

![Experience Platform端到端工作流](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## 快速入門

此端到端工作流使用多個Adobe Experience Platform服務。 以下是此工作流中使用的服務清單，其中包含指向其概述的連結：

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。 為最好地利用分段，請確保根據 [資料建模的最佳做法](../xdm/schema/best-practices.md)。
- [[!DNL Identity Service]](../identity-service/home.md):通過跨設備和系統橋接身份，讓您全面瞭解客戶及其行為。
- [源](../sources/home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] 允許您劃分儲存在 [!DNL Experience Platform] 將個人（如客戶、潛在客戶、用戶或組織）關聯到較小的組。
- [[!DNL Real-Time Customer Profile]](../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
- [資料集](../catalog/datasets/overview.md):資料永續的儲存與管理結構 [!DNL Experience Platform]。
- [目標](../destinations/home.md):目標是預構建的與常用應用程式的整合，這些整合允許從平台無縫激活資料，用於跨渠道營銷活動、電子郵件活動、目標廣告和許多其他使用案例。

## 建立 XDM 結構描述

在將資料導入平台之前，必須先建立XDM架構來描述該資料的結構。 在下一步中接收資料時，將將傳入資料映射到此架構。 要瞭解如何建立示例XDM架構，請閱讀上的教程 [使用架構編輯器建立架構](../xdm/tutorials/create-schema-ui.md)。

上面的教程介紹如何為架構設定標識欄位。 標識欄位表示一個欄位，該欄位可用於標識與記錄或時間系列事件相關的個人。 身份欄位是如何在平台中構建客戶身份圖的關鍵元件，它最終影響即時客戶配置檔案如何將不同的資料片段合併到一起以獲得客戶的完整視圖。 有關如何在平台中查看標識圖形的詳細資訊，請參見上的教程 [如何使用標識圖形查看器](../identity-service/ui/identity-graph-viewer.md)。

您需要啟用您的架構以在即時客戶配置檔案中使用，以便可以根據您的架構從資料構建客戶配置檔案。 請參閱 [為配置檔案啟用架構](../xdm/ui/resources/schemas.md#profile) 中。

## 將資料插入平台

建立XDM架構後，可開始將資料帶入系統。

引入平台的所有資料在接收時都儲存到各個資料集。 資料集是映射到特定XDM模式的資料記錄的集合。 在您的資料可用之前 [!DNL Real-Time Customer Profile]，必須具體配置有關的資料集。 有關如何為配置檔案啟用資料集的完整說明，請參見 [資料集UI指南](../catalog/datasets/user-guide.md#enable-profile) 和 [資料集配置API教程](../profile/tutorials/dataset-configuration.md)。 資料集配置完畢後，可以開始將資料插入資料集。

平台允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種來源 (如 Adobe 應用程式、雲端型的儲存空間、資料庫和其他許多來源) 內嵌資料。 例如，您可以使用 [AmazonS3](../sources/tutorials/api/create/cloud-storage/s3.md)。 可在 [源連接器概述](../sources/home.md)。

如果您使用AmazonS3作為源連接器，則可以按照API教程中的任何一個說明 [建立AmazonS3連接器](../sources/tutorials/api/create/cloud-storage/s3.md) 或UI教程 [建立AmazonS3連接器](../sources/tutorials/ui/create/cloud-storage/s3.md) 瞭解如何在連接器中建立、連接和接收資料。

有關源連接器的詳細說明，請閱讀 [源連接器概述](../sources/home.md)。 要瞭解有關流服務（源所基於的API）的詳細資訊，請閱讀 [流服務API參考](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

一旦您的資料通過源連接器進入平台並儲存在啟用了配置檔案的資料集中，客戶配置檔案將根據您在XDM架構中配置的身份資料自動建立。

首次將資料上載到新資料集或設定新ETL進程或資料源時，建議仔細檢查資料以確保資料已正確上載且生成的配置檔案包含您期望的資料。 有關如何在平台UI中訪問客戶配置檔案的詳細資訊，請參閱 [即時客戶概要檔案UI指南](../profile/ui/user-guide.md)。 有關如何使用Real-Time Customer Profile API訪問配置檔案的詳細資訊，請參閱上的指南 [使用實體端點](../profile/api/entities.md)。

## 評估資料

從所攝取的資料成功生成配置檔案後，可以使用分段來評估資料。 細分是定義個人子集與您的配置檔案儲存共用的特定屬性或行為的過程，以便將可銷售的一組人員與您的客戶群區分開來。 要瞭解有關分段的詳細資訊，請閱讀 [分段服務概述](../segmentation/home.md)。

### 建立段定義

要開始，必須建立段定義以集群客戶以建立目標受眾。 段定義是規則的集合，您可以使用這些規則定義要瞄準的受眾。 要建立段定義，請按照UI指南中的任何一個說明使用 [段生成器](../segmentation/ui/segment-builder.md) 或API教程 [建立段](../segmentation/tutorials/create-a-segment.md)。

建立段定義後，請確保記錄段定義ID。

### 評估段定義

在建立段定義後，您可以建立段任務以將段作為一次性實例進行評估，也可以建立計畫以持續評估段。

要按需求評估段定義，您可以建立段任務。 段作業是一個非同步過程，它基於引用的段定義和合併策略建立新的受眾段。 合併策略是一組規則，平台使用這些規則來確定將使用哪些資料來建立客戶配置檔案，以及當源之間存在差異時將優先排列哪些資料。 要瞭解如何使用合併策略，請參閱 [合併策略UI指南](../profile/merge-policies/ui-guide.md)。

一旦建立和評估了段作業，您就可以獲取有關段的資訊，如受眾的大小或處理過程中可能發生的錯誤。 要瞭解如何建立段作業，包括您需要提供的所有詳細資訊，請閱讀 [段作業開發人員指南](../segmentation/api/segment-jobs.md)。

要持續評估段定義，可以建立並啟用計畫。 調度是一種工具，可用於在指定時間每天自動運行段作業一次。 要瞭解如何建立和啟用計畫，可以按照API指南中的說明 [計畫終結點](../segmentation/api/schedules.md)。

## 導出評估的資料

建立一次性段作業或日常計畫後，您可以建立段導出作業以將結果導出到資料集或將結果導出到目標。 以下各節提供了這兩個選項的指導。

### 將評估的資料導出到資料集

在建立一次性段作業或持續計畫後，您可以通過建立段導出作業來導出結果。 段導出作業是將關於所評估的受眾的資訊發送到資料集的非同步任務。

在建立導出作業之前，必須首先建立資料集以將資料導出到。 要瞭解如何建立資料集，請閱讀上的 [建立目標資料集](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) 在有關評估段的教程中，確保在建立資料集ID後記錄資料集ID。 建立資料集後，可以建立導出作業。 要瞭解如何建立導出作業，請按照 [導出作業終結點](../segmentation/api/export-jobs.md)。

### 將評估的資料導出到目標

或者，在建立一次性段作業或日常計畫後，可以將結果導出到目標。 目標是終結點，例如外部服務上的Adobe應用程式，其中可激活和傳遞受眾。 可用目標的完整清單位於 [目標目錄](../destinations/catalog/overview.md)。

有關如何將資料激活到批處理或電子郵件營銷目標的說明，請參見上的教程 [如何使用平台UI激活受眾資料以批處理配置檔案導出目標](../destinations/ui/activate-batch-profile-destinations.md) 和 [有關如何使用流服務API連接到批處理目標和激活資料的指南](../destinations/api/connect-activate-batch-destinations.md)。

## 監視您的平台資料活動

平台允許您通過使用資料流來跟蹤資料的處理方式，資料流是跨平台各個元件移動資料的作業的表示形式。 這些資料流是跨不同的服務配置的，可幫助將資料從源連接器移動到目標資料集，然後由 [!DNL Identity Service] 和 [!DNL Real-Time Customer Profile] 最終被激活到目的地。 監視面板可以直觀顯示資料流的運行過程。 要瞭解如何在平台UI中監視資料流，請參見上的教程 [監視源的資料流](../dataflows/ui/monitor-sources.md) 和 [監視目標的資料流](../dataflows/ui/monitor-destinations.md)。

您還可以通過使用統計度量和事件通知來監視平台活動 [!DNL Observability Insights]。 您可以通過平台UI訂閱警報通知或將其發送到已配置的Webhook。 有關如何查看、啟用、禁用和訂閱Experience PlatformUI中可用警報的詳細資訊，請參閱 [[!UICONTROL 警報] UI指南](../observability/alerts/ui.md)。 有關如何通過Webhooks接收警報的詳細資訊，請參閱上的指南 [訂閱Adobe I/O事件通知](../observability/alerts/subscribe.md)。

## 後續步驟

閱讀本教程後，您將獲得一個針對平台的簡單端到端流的基本簡介。 要瞭解有關Adobe Experience Platform的更多資訊，請閱讀 [平台概述](./home.md)。 要瞭解有關使用平台UI和平台API的更多資訊，請閱讀 [平台UI指南](./ui-guide.md) 和 [平台API指南](./api-guide.md) 分別進行。
