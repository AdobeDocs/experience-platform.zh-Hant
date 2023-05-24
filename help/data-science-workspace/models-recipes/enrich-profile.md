---
keywords: Experience Platform；機器學習模型；資料科學工作區；即時客戶概要檔案；熱門主題；機器學習洞察力
solution: Experience Platform
title: 利用機器學習的洞察力豐富即時客戶資料
type: Tutorial
description: 本文檔提供了有關如何利用機器學習見解豐富即時客戶概要資訊的指南。
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 豐 [!DNL Real-Time Customer Profile] 通過機器學習

Adobe Experience Platform [!DNL Data Science Workspace] 提供工具和資源，以建立、評估和利用機器學習模型來生成資料預測和洞見。 當機器學習的洞察力被植入 [!DNL Profile]-enabled dataset，該資料也被作為 [!DNL Profile] 然後使用 [!DNL Adobe Experience Platform Segmentation Service]。

此文檔提供指向教程的連結，您可以豐富 [!DNL Real-Time Customer Profile] 你的機器學習洞察力。

## 快速入門

要完成以下教程，您需要對錄入有一定的瞭解 [!DNL Profile] 資料和建立段。 在開始本教程之前，請查看以下服務的文檔：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的聚合資料，為每個客戶提供完整、統一的表示。
- [[!DNL Identity Service]](../../identity-service/home.md):啟用 [!DNL Real-Time Customer Profile] 通過將來自不同資料源的身份橋接到平台。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):平台組織客戶體驗資料的標準化框架。

除了上述文檔外，強烈建議您還查看以下架構指南和架構編輯器：

- [架構組合的基礎](../../xdm/schema/composition.md):介紹用於合成架構的XDM架構、構建塊、原則和最佳做法 [!DNL Experience Platform]。
- [架構編輯器教程](../../xdm/tutorials/create-schema-ui.md):提供了有關使用中的架構編輯器建立架構的詳細說明 [!DNL Experience Platform]。

## 建立和配置輸出模式和資料集 {#create-an-output-schema-and-dataset}

邁向富裕的第一步 [!DNL Real-Time Customer Profile] 通過評分洞察力，可以瞭解資料定義的真實世界對象（如人）。 瞭解資料後，您就可以描述和設計添加含義的結構，就像設計關係資料庫一樣。

合成架構的開始是分配類。 類定義模式將包含的資料的行為方面（記錄或時間序列）。 要開始建立自己的架構，請按照本教程中的步驟操作 [使用架構編輯器建立架構](../../xdm/tutorials/create-schema-ui.md)。 請注意，在為 [!DNL Profile]，需要將資料集的架構配置為具有主標識欄位，然後為 [!DNL Profile]。 當資料被攝入 [!DNL Profile]-enabled dataset，該資料也被作為 [!DNL Profile] 記錄。

如果希望使用 [!DNL Schema Registry] API，從讀取 [[!DNL Schema Registry] 開發者指南](../../xdm/api/getting-started.md) 在嘗試教程之前 [使用API建立架構](../../xdm/tutorials/create-schema-api.md)。

一旦準備了模式和資料集，您就可以通過使用適當的模型執行計分運行來生成評分資料，並將評分資料攝取到資料集。

## 使用 [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

在生成並將評分資料洞察力接收到 [!DNL Profile]-enabled dataset ，您可以使用 [!DNL Segment Builder]。

的 [!DNL Segment Builder] 提供豐富的工作區，允許您與 [!DNL Profile] 資料元素。 工作區為生成和編輯規則提供了直觀的控制項，如用於表示資料屬性的拖放拼貼。 關注 [[!DNL Segment Builder] 使用手冊](../../segmentation/ui/segment-builder.md) 要瞭解：

- 使用屬性、事件和現有受眾的組合作為構建塊建立段定義。
- 使用規則生成器畫布和容器控制段規則的執行順序。
- 查看潛在受眾的估計值，以便根據需要調整段定義。
- 啟用所有段定義以進行計劃分段。
- 為流分段啟用指定的段定義。

## 後續步驟 {#next-steps}

瞭解有關段和 [!DNL Segment Builder]，閱讀 [分段服務概述](../../segmentation/home.md)。

瞭解有關 [!DNL Real-Time Customer Profile]，閱讀 [即時客戶概要資訊概述](../../profile/home.md)
