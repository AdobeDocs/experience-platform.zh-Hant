---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 即時客戶個人檔案教學課程
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# 設定即時客戶個人檔案和身分服務

為了為您的組織設定即時客戶描述檔，您必須完成多個不同的工作流程。 本檔案概述了相關步驟，並提供教學課程連結，以完成個別工作流程。 若要進一步瞭解即時客戶個人檔案，請先閱讀個人檔案總 [覽](../profile/home.md)。

## 啟用描述檔和身分識別的架構

資料必須先建立結構，以提供要擷取的資料結構，而且必須啟用該結構，才能在Profile和Adobe Experience Platform Identity Service中使用。 如需建立已啟用描述檔和身分服務之架構的逐步指示，請參閱使用架構註冊表API建立架構或 [使用架構產生器UI](../xdm/tutorials/create-schema-api.md) 建立架構的教學課程 [](../xdm/tutorials/create-schema-ui.md)。

## 設定描述檔和身分識別的資料集

若要開始將資料擷取至描述檔，您必須已正確設定資料集，以便與即時客戶描述檔和身分服務搭配使用。 若要開始，請依照設定 [資料集以進行描述檔和身分教學課程](../profile/tutorials/dataset-configuration.md)。

## 配置合併策略

Adobe Experience Platform可讓您從多個來源匯整資料並加以匯整，以全面瞭解每個客戶。 將這些資料整合在一起時，合併原則是平台用來決定資料的優先順序以及將哪些資料合併以建立統一檢視的規則。 使用REST風格的API或用戶介面，您可以建立新的合併策略、管理現有策略，並為組織設定預設的合併策略。 要在平台UI中使用合併策略，請訪問合 [並策略使用手冊](../profile/ui/merge-policies.md)。 若要使用即時客戶設定檔API來處理合併原則，請參閱合 [並原則開發人員指南](../profile/api/merge-policies.md)。

## 設定邊緣投影

為即時跨多個通道為客戶提供協調、一致且個人化的體驗，需要隨時提供適當的資料，並在變更時持續更新。 Adobe Experience Platform可讓您透過使用所謂的邊緣，即時存取資料。 邊緣是地理位置優越的伺服器，可儲存資料，讓應用程式可輕鬆存取。 資料通過投影被路由到邊，投影目的地定義資料要發送到的邊，投影配置定義將在邊上提供的特定資訊。 如需詳細資訊並開始使用邊緣，請參閱邊緣投影的即時客戶 [描述檔API子指南](../profile/api/edge-projections.md)。

## 後續步驟

在您為組織設定「即時客戶個人檔案」後，您可以開始將資料新增至個別客戶個人檔案，並根據特定客戶屬性建立受眾細分。 若要開始使用，請參閱下列教學課程：

* [新增資料至即時客戶個人檔案](../profile/tutorials/add-profile-data.md)
* [建立區段](../segmentation/tutorials/create-a-segment.md)