---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: 即時客戶個人檔案教學課程
topic: tutorial
type: Tutorial
description: 本檔案概述了相關步驟，並提供教學課程連結，以完成個別工作流程。
translation-type: tm+mt
source-git-commit: 844ef4a0131e41d3a7a3da319ccf7f8d5cf1f40d
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---


# 設定 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service]

為了為您的組 [!DNL Real-time Customer Profile] 織進行設定，您必須完成多個不同的工作流程。 本檔案概述了相關步驟，並提供教學課程連結，以完成個別工作流程。

若要進一步了 [!DNL Real-time Customer Profile]解，請先閱讀描述 [檔概觀](../profile/home.md)。

## 即時客戶個人檔案UI總覽

即時客戶個人檔案可讓您對個別客戶建立全方位的檢視，並結合來自多個通道的資料，包括線上、離線、CRM和協力廠商資料。

**本指南將幫助您：**
- 瞭解Profiles  UI和可用功能。
- 檢視並管理您的個人檔案資料。

若要進一步瞭解，請造訪 [即時客戶個人檔案使用指南](../profile/ui/user-guide.md)

## 即時客戶個人檔案API

即時客戶個人檔案API包含多個端點。 個人檔案可讓您將來自多個通道（例如線上、離線、CRM和第三方資料）的分散客戶資料整合為一個統一的檢視，提供每個客戶互動的可操作的時間戳記帳戶。 請閱讀即 [時客戶個人檔案API概觀](../profile/api/overview.md) ，以取得每個可用端點及其使用案例的詳細資訊。

**目前提供下列API開發人員指南：**
- [計算屬性(alpha) ](../profile/api/computed-attributes.md) -瞭解計算屬性的使用案例，以及如何設定、存取、更新和刪除計算屬性。
- [邊緣投影](../profile/api/edge-projections.md) -瞭解如何建立、檢視、更新、刪除和列出投影目標。 此外，本檔案還包含有關列出和建立投影組態的資訊，並提供使用選擇器的範例。
- [實體（描述檔存取）](../profile/api/entities.md) -瞭解如何透過身分或身分清單存取描述檔資料。 此外，瞭解如何使用身分識別、依身分區分單一個人檔案，以及存取多個架構實體，來存取多個描述檔的時間系列事件。
- [匯出工作（描述檔匯出）](../profile/api/export-jobs.md) -瞭解如何建立、檢視、監視和取消匯出工作。
- [合併策略](../profile/api/merge-policies.md) -瞭解合併策略的元件以及如何訪問、建立、更新和刪除合併策略。
- [預覽範例狀態（描述檔預覽）](../profile/api/preview-sample-status.md) -瞭解如何檢視最後範例狀態、依資料集列出描述檔分發，以及依命名空間列出描述檔分發。
- [描述檔系統工作（刪除請求）](../profile/api/profile-system-jobs.md) -瞭解如何在描述檔商店中檢視、建立和移除資料集或批次的刪除請求。

若要進一步瞭解並取得使用即時客戶描述檔API執行CRUD作業所需的值，請造訪快速入 [門指南](../profile/api/getting-started.md)。

## 為和服務啟用 [!DNL Profile] 架 [!DNL Identity] 構

在可將資料收錄至Adobe Experience Platform並用於建立之前 [!DNL Real-time Customer Profiles]，必須先建立一個架構，以提供將要收錄之資料的結構，且該架構必須啟用，才能用於 [!DNL Profile] 和Adobe Experience Platform [!DNL Identity Service]。

**本指南將幫助您：**
- 瀏覽現有結構。
- 建立架構並命名。
- 新增並定義XDM混音。
- 將您的架構欄位設為身分欄位。
- 為您的架構啟用描述檔。

有關建立同時啟用和的架構的逐步說明 [!DNL Profile][!DNL Identity Service]，請參閱使用「架構註冊表API」建立架構或使用「架構生成器UI [」](../xdm/tutorials/create-schema-api.md) 建立架構的教程 [](../xdm/tutorials/create-schema-ui.md)。

## 為和配置數 [!DNL Profile] 據集 [!DNL Identity]

若要開始將資料 [!DNL Profile]擷取至，您必須已正確設定資料集以便與和 [!DNL Real-time Customer Profile] 搭配使 [!DNL Identity Service]用。

**本指南將幫助您：**
- 建立已啟用描述檔的資料集。
- 配置現有資料集。
- 將資料內嵌至資料集。
- 確認您的資料集已啟用設定檔，並使用Identity Service。

若要開始，請依照API教學課程，針對 [描述檔和身分設定資料集](../profile/tutorials/dataset-configuration.md)。

## 配置合併策略

Adobe Experience Platform可讓您從多個來源匯整資料並加以匯整，以全面瞭解每個客戶。 將這些資料整合在一起時，合併原則是用來決定 [!DNL Platform] 資料的優先順序以及將哪些資料合併以建立該統一檢視的規則。

**本指南將幫助您：**
- 建立新的合併原則。
- 管理現有的合併原則。
- 為組織設定預設的合併原則。
- 瞭解合併策略違規。

若要在UI中使用合併原則，請 [!DNL Platform] 造訪合併原 [則使用指南](../profile/ui/merge-policies.md)。 若要使用即時客戶設定檔API來處理合併原則，請參閱合 [並原則開發人員指南](../profile/api/merge-policies.md)。

## 設定邊緣投影

為即時跨多個通道為客戶提供協調、一致且個人化的體驗，需要隨時提供適當的資料，並在變更時持續更新。 Adobe [!DNL Experience Platform] 可透過使用所謂的邊緣來即時存取資料。 邊緣是地理位置優越的伺服器，可儲存資料，讓應用程式可輕鬆存取。 資料通過投影被路由到邊，投影目的地定義資料要發送到的邊，投影配置定義將在邊上提供的特定資訊。

**本指南將幫助您：**
- 列出、建立、查看、更新和刪除邊投影目標。
- 列出並建立邊投影配置。
- 瞭解選擇器。

如需詳細資訊以及開始使用邊緣，請參閱 [!DNL Real-time Customer Profile] API [邊緣投影子指南](../profile/api/edge-projections.md)。

## 自訂描述檔資料在UI中的顯示方式

在Experience Platform使用者介面中，您可以以客戶個人檔案的形式檢視即時客戶個人檔案資料並與之互動。 UI中顯示的描述檔資訊已從多個描述檔片段合併在一起，以形成每個客戶的單一檢視。 這包括基本屬性、連結身分和頻道偏好設定等詳細資訊。 配置檔案中顯示的預設欄位也可以在組織級別更改，以顯示首選的配置檔案屬性。

**本指南將幫助您：**
- 重新排序、調整大小、編輯和移除卡片。
- 新增屬性。
- 新增資訊卡。
- 恢復預設值。

若要進一步瞭解自訂描述檔資料，請造訪描述檔自 [訂檔案](../profile/ui/profile-customization.md)

## 後續步驟

在您為組織設 [!DNL Real-time Customer Profile] 定後，您就可以開始將資料新增至個別客戶個人檔案，並根據特定客戶屬性建立受眾細分。 若要開始使用，請參閱下列教學課程：

- [新增資料至即時客戶個人檔案](../profile/tutorials/add-profile-data.md)
- [建立區段](../segmentation/tutorials/create-a-segment.md)