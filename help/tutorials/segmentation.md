---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 區段教學課程
topic: tutorial
description: Adobe Experience Platform Segmentation Service提供使用者介面和REST風格的API，可讓您建立細分並從即時客戶個人檔案資料產生受眾。 這些區段是在Platform上集中設定和維護的，任何Adobe解決方案都可輕鬆存取。
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# 區段教學課程

Adobe Experience Platform提 [!DNL Segmentation Service] 供使用者介面和REST風格的API，讓您從資料中建立細分並產生受 [!DNL Real-time Customer Profile] 眾。 這些區段是集中設定和維護的， [!DNL Platform]任何Adobe解決方案都可輕鬆存取。 若要進一步瞭解區段，請先閱讀區段服務 [概觀](../segmentation/home.md)。

## 建立區段定義

區段定義是用於描述目標對象之關鍵特性或行為的規則集。 概念化後，區段定義中概述的規則會用來決定區段的合格讀者成員。 您可使用使用者介面或API來開發、測試、預覽和儲存區 [!DNL Platform] 段定義。 若要建立區段定義，請遵循 [建立區段API教學課程](../segmentation/tutorials/create-a-segment.md) ，或 [「區段產生器UI」使用指南](../segmentation/ui/overview.md)。

## 評估區段並存取結果

開發、測試和儲存區段定義後，您就可以透過排程評估或隨選評估來評估區段。 排程評估（也稱為「排程區段」）可讓您建立在特定時間執行匯出工作的循環排程，而隨選評估則包括建立區段工作以立即建立觀眾。 若要進一步瞭解，請造訪評估和存 [取區段結果的教學課程](../segmentation/tutorials/evaluate-a-segment.md)。

## 匯出區段資料

匯出包含資 [!DNL Profile] 料的區段 [時，必須先建立資料匯出至的資料集](../segmentation/tutorials/create-dataset-export-segment.md)，然後開始新的匯出工作。 有關產生匯出工作的步驟，請參閱評估區段 [的教學課程](../segmentation/tutorials/evaluate-a-segment.md)。

## 配置合併策略

Adobe Experience Platform可讓您從多個來源匯整資料並加以匯整，以全面瞭解每個客戶。 將這些資料整合在一起時，合併原則是用來決定 [!DNL Platform] 資料的優先順序以及將哪些資料合併以建立該統一檢視的規則。 使用REST風格的API或用戶介面，您可以建立新的合併策略、管理現有策略，並為組織設定預設的合併策略。 若要在UI中使用合併原則，請 [!DNL Platform] 造訪合併原 [則使用指南](../profile/ui/merge-policies.md)。 若要使用 [!DNL Real-time Customer Profile] API使用合併原則，請參 [閱合併原](../profile/api/merge-policies.md)則開發人員指南。

## 強制區段的資料使用符合性

在中啟用的區段在其區 [!DNL Real-time Customer Profile] 段定義中包含合併原則ID。 此合併策略包含有關哪些資料集要包含在段中的資訊，這些資料集又包含任何適用的資料使用標籤。 如需針對對象區段強制實施資料使用合規性的特定步驟，請遵循區 [段的資料使用合規性教學課程](../segmentation/tutorials/governance.md)。

## 串流區段

串流區段是指當事件進入特定區段群組時，可立即評估客戶的能力。 有了這項功能，大部份的區段規則現在都可以在資料傳入Adobe Experience Platform時進行評估，這表示區段會籍會保持最新狀態，而不會執行排程的區段工作。 若要進一步瞭解，請造訪串 [流區段總覽](../segmentation/api/streaming-segmentation.md)。

## 多實體分段

多實體分段是指能夠根據產 [!DNL Profile] 品、商店或其他非描述檔類別，以額外資料擴充資料。 連線後，其他類別的資料就會變成架構的原生 [!DNL Profile] 資料。 若要瞭解移動，請參 [閱多實體分段檔案](../segmentation/multi-entity-segmentation.md)。