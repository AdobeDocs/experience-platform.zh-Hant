---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 區段教學課程
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform區段服務提供使用者介面和REST風格的API，可讓您建立區段並從即時客戶個人檔案資料產生受眾。 這些區段是在平台上集中設定和維護的，任何Adobe解決方案都可輕鬆存取。
exl-id: e45de6b5-ff71-4908-ad79-898084763704
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# 區段教學課程

Adobe Experience Platform[!DNL Segmentation Service]提供使用者介面和RESTful API，可讓您建立區段並從您的[!DNL Real-time Customer Profile]資料產生觀眾。 這些區段是集中設定並維護在[!DNL Platform]上，任何Adobe解決方案都可輕鬆存取。 若要進一步瞭解分段，請先閱讀[分段服務概觀](../segmentation/home.md)。

## 建立區段定義

區段定義是用於描述目標對象之關鍵特性或行為的規則集。 概念化後，區段定義中概述的規則會用來決定區段的合格讀者成員。 使用[!DNL Platform]使用者介面或API，即可開發、測試、預覽和儲存區段定義。 若要建立區段定義，請依照[建立區段API教學課程](../segmentation/tutorials/create-a-segment.md)或[區段產生器UI使用指南](../segmentation/ui/overview.md)進行。

## 評估區段並存取結果

開發、測試和儲存區段定義後，您就可以透過排程評估或隨選評估來評估區段。 排程評估（也稱為「排程區段」）可讓您建立在特定時間執行匯出工作的循環排程，而隨選評估則包括建立區段工作以立即建立觀眾。 若要進一步瞭解，請造訪[評估和存取區段結果的教學課程。](../segmentation/tutorials/evaluate-a-segment.md)

## 匯出區段資料

匯出包含[!DNL Profile]資料的區段需要先建立資料集[，然後開始新的匯出工作。 ](../segmentation/tutorials/create-dataset-export-segment.md)有關生成導出作業的步驟，請參見[評估段](../segmentation/tutorials/evaluate-a-segment.md)的教程。

## 配置合併策略

Adobe Experience Platform可讓您從多個來源匯整資料，並加以結合，以全面瞭解每個客戶。 合併策略是[!DNL Platform]用於確定資料的優先順序以及將哪些資料合併以建立該統一視圖的規則，將這些資料合併在一起。 使用REST風格的API或用戶介面，您可以建立新的合併策略、管理現有策略，並為組織設定預設的合併策略。 要在[!DNL Platform] UI中使用合併策略，請訪問[合併策略使用手冊](../profile/ui/merge-policies.md)。 要使用[!DNL Real-time Customer Profile] API使用合併策略，請參閱[合併策略開發人員指南](../profile/api/merge-policies.md)。

## 強制區段的資料使用符合性

在[!DNL Real-time Customer Profile]中啟用的區段在其區段定義中包含合併原則ID。 此合併策略包含有關哪些資料集要包含在段中的資訊，這些資料集又包含任何適用的資料使用標籤。 如需針對對象區段強制執行資料使用合規性的特定步驟，請依照[區段資料使用合規性實施教學課程](../segmentation/tutorials/governance.md)進行。

## 串流區段

串流區段是指當事件進入特定區段群組時，可立即評估客戶的能力。 有了這項功能，大部份的區段規則現在都可以在資料傳入Adobe Experience Platform時進行評估，這表示區段成員資格將會保持最新，而不會執行排程的區段工作。 若要進一步瞭解，請造訪[串流區段概觀](../segmentation/api/streaming-segmentation.md)。

## 多實體分段

多實體分段是指能夠根據產品、商店或其他非描述檔類別，以額外資料擴充[!DNL Profile]資料。 連接後，其他類的資料將變為可用，就像它們是[!DNL Profile]模式的本地資料。 若要瞭解移動，請參閱[多實體分段檔案](../segmentation/multi-entity-segmentation.md)。
