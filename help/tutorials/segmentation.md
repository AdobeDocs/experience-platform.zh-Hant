---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 區段教學課程
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform劃分服務提供使用者介面和RESTful API，可讓您建立區段，並從即時客戶個人檔案資料產生受眾。 這些區段可在Platform上集中設定和維護，且可供任何Adobe解決方案存取。
exl-id: e45de6b5-ff71-4908-ad79-898084763704
source-git-commit: 36f64b3a1e75c9badaee29e28408504eabac64fe
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# 區段教學課程

Adobe Experience Platform [!DNL Segmentation Service]提供使用者介面和RESTful API，可讓您建立區段，並從[!DNL Real-time Customer Profile]資料產生對象。 這些區段在[!DNL Platform]上集中配置和維護，任何Adobe解決方案都可輕鬆訪問。 若要深入了解分段，請先閱讀[分段服務概述](../segmentation/home.md)。

## 建立區段定義

區段定義是用來描述目標對象之關鍵特性或行為的規則集。 概念化後，區段定義中概述的規則將用於決定區段的合格受眾成員。 可使用[!DNL Platform]使用者介面或API來開發、測試、預覽和儲存區段定義。 若要建立區段定義，請依照[建立區段API教學課程](../segmentation/tutorials/create-a-segment.md)或[區段產生器UI使用手冊](../segmentation/ui/overview.md)操作。

## 評估區段和存取結果

開發、測試並儲存區段定義後，您就可以透過排程評估或隨需評估來評估區段。 排程評估（也稱為「排程分段」）可讓您針對在特定時間執行匯出工作建立週期性排程，而隨需評估則涉及建立區段工作以立即建立受眾。 若要深入了解，請造訪[評估及存取區段結果](../segmentation/tutorials/evaluate-a-segment.md)的教學課程。

## 匯出區段資料

匯出包含[!DNL Profile]資料的區段需要先建立要匯出資料的資料集](../segmentation/tutorials/create-dataset-export-segment.md)，然後起始新的匯出工作。 [有關生成導出作業的步驟，請參見[評估段](../segmentation/tutorials/evaluate-a-segment.md)的教程。

## 配置合併策略

Adobe Experience Platform可讓您從多個來源匯整資料並加以結合，以便查看每個客戶的完整檢視。 將此資料集合在一起時，[!DNL Platform]會使用合併原則來判斷資料的優先順序，以及將結合哪些資料來建立該統一檢視。 使用RESTful API或用戶介面，您可以建立新的合併策略、管理現有策略，以及為組織設定預設的合併策略。 要了解有關合併策略及其在Experience Platform中的作用的詳細資訊，請從閱讀[合併策略概述](../profile/merge-policies/overview.md)開始。

## 強制區段符合資料使用情形

在[!DNL Real-time Customer Profile]中啟用的段在其段定義中包含合併策略ID。 此合併原則包含要納入區段之資料集的相關資訊，而這些資料集又包含任何適用的資料使用標籤。 如需針對對象區段強制遵循資料使用量的具體步驟，請參閱區段[資料使用量遵循實施教學課程](../segmentation/tutorials/governance.md)。

## 串流細分

串流區段是指當事件進入特定區段群組時，立即評估客戶的能力。 透過此功能，大部分的區段規則現在都可在資料傳入Adobe Experience Platform時評估，這表示區段成員資格會保持最新，而不會執行排程的區段工作。 若要深入了解，請造訪[串流區段概述](../segmentation/api/streaming-segmentation.md)。

## 多實體細分

多實體分段是根據產品、商店或其他非設定檔類別，以其他資料擴充[!DNL Profile]資料的功能。 連接後，其他類的資料就可用，就像它們是[!DNL Profile]架構的本機資料。 若要了解移動，請參閱[多實體分段檔案](../segmentation/multi-entity-segmentation.md)。
