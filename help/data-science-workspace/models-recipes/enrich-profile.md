---
keywords: Experience Platform；機器學習模型；資料科學Workspace；即時客戶設定檔；熱門主題；機器學習深入分析
solution: Experience Platform
title: 透過機器學習深入分析豐富即時客戶設定檔
type: Tutorial
description: 本檔案提供如何透過機器學習深入解析豐富即時客戶設定檔的指南。
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# 以機器學習深入分析豐富[!DNL Real-Time Customer Profile]

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

Adobe Experience Platform [!DNL Data Science Workspace]提供各種工具和資源，用來建立、評估及運用機器學習模型，以產生資料預測和深入分析。 將機器學習深入分析擷取至啟用[!DNL Profile]的資料集時，該相同資料也會擷取為[!DNL Profile]記錄，然後可以使用[!DNL Adobe Experience Platform Segmentation Service]分段。

細分程式取決於對象的評估方法。 如果對象設定為&#x200B;**串流**，它將即時處理模型寫入設定檔的所有新更新。 但是，如果對象設定為&#x200B;**批次**&#x200B;評估，則會在下一個批次中評估新值。

本檔案提供教學課程的連結，可讓您透過機器學習深入分析擴充[!DNL Real-Time Customer Profile]。

## 快速入門

若要完成下列教學課程，您必須實際瞭解如何擷取[!DNL Profile]資料和建立對象。 在開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供每個個別客戶的完整、統一表示法。
- [[!DNL Identity Service]](../../identity-service/home.md)：透過從擷取到Platform的不同資料來源橋接身分來啟用[!DNL Real-Time Customer Profile]。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： Platform用來組織客戶體驗資料的標準化架構。

除了上述檔案之外，強烈建議您也檢閱下列有關結構描述和結構描述編輯器的指南：

- [結構描述構成的基本概念](../../xdm/schema/composition.md)：說明XDM結構描述、建置區塊、構成要用於[!DNL Experience Platform]的結構描述的原則和最佳實務。
- [結構描述編輯器教學課程](../../xdm/tutorials/create-schema-ui.md)：提供在[!DNL Experience Platform]中使用結構描述編輯器建立結構描述的詳細指示。

## 建立及設定輸出結構和資料集 {#create-an-output-schema-and-dataset}

若要使用評分見解來豐富[!DNL Real-Time Customer Profile]，第一步是瞭解您的資料所定義的真實世界物件（例如人員）。 瞭解您的資料後，您就可以描述和設計結構來增加意義，就像設計關聯式資料庫一樣。

構成結構描述從指派類別開始。 類別會定義結構描述將包含之資料（記錄或時間序列）的行為方面。 若要開始建立您自己的結構描述，請依照教學課程中有關[使用結構描述編輯器建立結構描述](../../xdm/tutorials/create-schema-ui.md)的步驟操作。 請注意，在啟用[!DNL Profile]的資料集之前，您需要先設定資料集的結構描述使其具有主要身分欄位，然後啟用[!DNL Profile]的結構描述。 將資料擷取至啟用[!DNL Profile]的資料集時，該資料也會擷取為[!DNL Profile]筆記錄。

如果您偏好改用[!DNL Schema Registry] API來撰寫結構描述，請先閱讀[[!DNL Schema Registry] 開發人員指南](../../xdm/api/getting-started.md)，再嘗試進行有關[使用API建立結構描述](../../xdm/tutorials/create-schema-api.md)的教學課程。

準備好您的結構描述和資料集後，您可以使用適當的模型執行評分回合，產生評分資料並內嵌到資料集中。

## 使用[!DNL Segment Builder]建立對象 {#create-audiences-using-the-segment-builder}

在您產生評分資料深入分析並內嵌至啟用[!DNL Profile]的資料集後，即可使用[!DNL Segment Builder]建立動態對象。

[!DNL Segment Builder]提供豐富的工作區，可讓您與[!DNL Profile]資料元素互動。 工作區提供用於建置和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖磚。 請依照[[!DNL Segment Builder] 使用手冊](../../segmentation/ui/segment-builder.md)瞭解以下資訊：

- 使用屬性、事件和現有對象的組合作為建置區塊來建立區段定義。
- 使用規則產生器畫布和容器來控制對象規則的執行順序。
- 檢視潛在對象的預估值，可讓您視需要調整區段定義。
- 啟用已排程區段的所有區段定義。
- 為串流細分啟用指定的區段定義。

## 後續步驟 {#next-steps}

若要深入瞭解對象和[!DNL Segment Builder]，請閱讀[細分服務總覽](../../segmentation/home.md)。

若要深入瞭解[!DNL Real-Time Customer Profile]，請閱讀[即時客戶個人檔案總覽](../../profile/home.md)
