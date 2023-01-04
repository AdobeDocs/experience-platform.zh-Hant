---
keywords: Experience Platform；機器學習模型；Data Science Workspace；即時客戶設定檔；熱門主題；機器學習深入分析
solution: Experience Platform
title: 透過機器學習深入分析，豐富即時客戶設定檔
topic-legacy: tutorial
type: Tutorial
description: 本檔案提供如何透過機器學習深入分析，讓即時客戶設定檔更加豐富的指南。
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 豐富 [!DNL Real-Time Customer Profile] 使用機器學習分析

Adobe Experience Platform [!DNL Data Science Workspace] 提供工具和資源，用於建立、評估及運用機器學習模型，以產生資料預測和深入分析。 將機器學習深入分析擷取至 [!DNL Profile]啟用資料集，相同資料也會擷取為 [!DNL Profile] 然後可以使用 [!DNL Adobe Experience Platform Segmentation Service].

本檔案提供教學課程的連結，讓您能夠豐富內容 [!DNL Real-Time Customer Profile] 以及機器學習見解。

## 快速入門

若要完成下列教學課程，您必須充分了解擷取功能 [!DNL Profile] 資料和建立區段。 開始本教學課程之前，請先檢閱下列服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供每個客戶的完整、統一的呈現。
- [[!DNL Identity Service]](../../identity-service/home.md):啟用 [!DNL Real-Time Customer Profile] 將不同資料來源的身分擷取至Platform中。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform用來組織客戶體驗資料的標準化架構。

除了上述檔案外，強烈建議您也檢閱下列結構描述指南和結構編輯器：

- [結構構成基本概念](../../xdm/schema/composition.md):說明合成要用於的結構描述的XDM結構描述、構建組塊、原則和最佳實務 [!DNL Experience Platform].
- [結構編輯器教學課程](../../xdm/tutorials/create-schema-ui.md):提供使用中的結構描述編輯器建立結構描述的詳細指示 [!DNL Experience Platform].

## 建立和設定輸出結構和資料集 {#create-an-output-schema-and-dataset}

向富裕邁出的第一步 [!DNL Real-Time Customer Profile] 有了分數深入分析，您就能了解資料定義的真實物件（例如人員）。 了解您的資料可讓您描述和設計可增加意義的結構，就像設計關係資料庫一樣。

從指定類開始合成架構。 類別會定義結構將包含的資料的行為方面（記錄或時間序列）。 若要開始建立自己的結構，請依照 [使用架構編輯器建立架構](../../xdm/tutorials/create-schema-ui.md). 請注意，在您為 [!DNL Profile]，您必須將資料集的結構設定為具有主要身分欄位，然後啟用 [!DNL Profile]. 資料擷取至 [!DNL Profile]啟用資料集，相同資料也會擷取為 [!DNL Profile] 記錄。

如果您偏好使用 [!DNL Schema Registry] 請改為從閱讀 [[!DNL Schema Registry] 開發人員指南](../../xdm/api/getting-started.md) 在嘗試上的教學課程之前 [使用API建立結構](../../xdm/tutorials/create-schema-api.md).

準備好結構和資料集後，您就可以使用適當的模型執行計分執行，借此產生計分資料並內嵌至資料集。

## 使用 [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

在您產生並擷取計分資料深入分析至 [!DNL Profile]啟用資料集，您可以使用 [!DNL Segment Builder].

此 [!DNL Segment Builder] 提供豐富的工作區，可讓您與 [!DNL Profile] 資料元素。 工作區提供建立和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖磚。 關注 [[!DNL Segment Builder] 使用手冊](../../segmentation/ui/segment-builder.md) 若要了解：

- 使用屬性、事件和現有對象的組合作為建置區塊，來建立區段定義。
- 使用規則產生器畫布和容器來控制執行區段規則的順序。
- 檢視潛在對象的預估值，讓您可視需要調整區段定義。
- 啟用排程分段的所有區段定義。
- 啟用串流細分的指定區段定義。

## 後續步驟 {#next-steps}

若要深入了解區段和 [!DNL Segment Builder]，請閱讀 [區段服務概觀](../../segmentation/home.md).

若要深入了解 [!DNL Real-Time Customer Profile]，請閱讀 [即時客戶個人檔案概觀](../../profile/home.md)
