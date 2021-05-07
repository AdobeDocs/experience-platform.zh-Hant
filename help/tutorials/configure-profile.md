---
keywords: Experience Platform; home；熱門主題；即時客戶概要；身份服務；
solution: Experience Platform
title: 即時客戶個人檔案教學課程
topic-legacy: tutorial
type: Tutorial
description: 本檔案概述了相關步驟，並提供教學課程連結，以完成個別工作流程。
exl-id: cda6e7a7-9498-454c-94df-c6271a5a4fd4
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# 設定 [!DNL Real-time Customer Profile]

為了為您的組織配置[!DNL Real-time Customer Profile]，您需要完成多個單獨的工作流。 本檔案概述了相關步驟，並提供教學課程連結，以完成個別工作流程。

若要進一步瞭解[!DNL Real-time Customer Profile]，請先閱讀[描述檔概述](../profile/home.md)。

## 即時客戶個人檔案UI總覽

即時客戶個人檔案可讓您對個別客戶建立全方位的檢視，並結合來自多個通道的資料，包括線上、離線、CRM和協力廠商資料。

**本指南將幫助您：**
- 瞭解[!UICONTROL Profiles] UI和可用功能。
- 檢視並管理您的個人檔案資料。

若要進一步瞭解，請造訪[即時客戶基本資料使用指南](../profile/ui/user-guide.md)

## 即時客戶個人檔案API

即時客戶個人檔案API包含多個端點。 請閱讀[即時客戶個人資料API概觀](../profile/api/overview.md)，以取得每個可用端點及其使用案例的詳細資訊。

若要進一步瞭解並取得使用即時客戶設定檔API執行CRUD作業所需的值，請造訪[快速入門手冊](../profile/api/getting-started.md)。

## 為[!DNL Profile]和[!DNL Identity]服務啟用模式

在將資料收錄到Adobe Experience Platform並用於建立[!DNL Real-time Customer Profiles]之前，必須建立一個模式以提供要收錄的資料的結構，並且該模式必須啟用以用於[!DNL Profile]和Adobe Experience Platform[!DNL Identity Service]。

**本指南將幫助您：**
- 瀏覽現有結構。
- 建立架構並命名。
- 添加和定義XDM架構欄位組。
- 將您的架構欄位設為身分欄位。
- 為您的架構啟用描述檔。

有關建立同時啟用[!DNL Profile]和[!DNL Identity Service]架構的逐步說明，請參閱[使用架構註冊表API](../xdm/tutorials/create-schema-api.md)或[使用架構構建器UI](../xdm/tutorials/create-schema-ui.md)建立架構的教程。

## 為[!DNL Profile]和[!DNL Identity]配置資料集

要開始將資料裝入[!DNL Profile]中，必須已正確配置資料集以便與[!DNL Real-time Customer Profile]和[!DNL Identity Service]一起使用。

**本指南將幫助您：**
- 建立已啟用描述檔的資料集。
- 配置現有資料集。
- 將資料內嵌至資料集。
- 確認您的資料集已啟用設定檔，並使用Identity Service。

若要開始，請依照[的API教學課程，針對描述檔和身分設定資料集](../profile/tutorials/dataset-configuration.md)。

## 配置合併策略

Adobe Experience Platform可讓您從多個來源匯整資料，並加以結合，以全面瞭解每個客戶。 合併策略是[!DNL Platform]用於確定資料的優先順序以及將哪些資料合併以建立該統一視圖的規則，將這些資料合併在一起。

**本指南將幫助您：**
- 建立新的合併原則。
- 管理現有的合併原則。
- 為組織設定預設的合併原則。
- 瞭解合併策略違規。

要在[!DNL Platform] UI中使用合併策略，請訪問[合併策略使用手冊](../profile/ui/merge-policies.md)。 要使用即時客戶配置檔案API來處理合併策略，請參閱[合併策略開發人員指南](../profile/api/merge-policies.md)。

## 設定邊緣投影

為即時跨多個通道為客戶提供協調、一致且個人化的體驗，需要隨時提供適當的資料，並在變更時持續更新。 Adobe[!DNL Experience Platform]可讓您透過使用稱為邊緣的功能，即時存取資料。 邊緣是地理位置的伺服器，可儲存資料，讓應用程式可輕鬆存取。 資料通過投影被路由到邊，投影目的地定義資料要發送到的邊，投影配置定義將在邊上提供的特定資訊。

**本指南將幫助您：**
- 列出、建立、查看、更新和刪除邊投影目標。
- 列出並建立邊投影配置。
- 瞭解選擇器。

如需詳細資訊並開始使用邊緣，請參閱邊緣投影](../profile/api/edge-projections.md)上的[!DNL Real-time Customer Profile] API [子指南。

## 自訂描述檔資料在UI中的顯示方式

在Experience Platform使用者介面中，您可以以客戶個人檔案的形式檢視即時客戶個人檔案資料並與之互動。 UI中顯示的描述檔資訊已從多個描述檔片段合併在一起，以形成每個客戶的單一檢視。 這包括基本屬性、連結身分和頻道偏好設定等詳細資訊。 配置檔案中顯示的預設欄位也可以在組織級別更改，以顯示首選的配置檔案屬性。

**本指南將幫助您：**
- 重新排序、調整大小、編輯和移除卡片。
- 新增屬性。
- 新增資訊卡。
- 恢復預設值。

若要進一步瞭解自訂描述檔資料，請造訪[描述檔自訂檔案](../profile/ui/profile-customization.md)

## 後續步驟

為組織設定[!DNL Real-time Customer Profile]後，您就可以開始將資料新增至個別客戶個人檔案，並根據特定客戶屬性建立受眾區段。 若要開始使用，請參閱下列教學課程：

- [新增資料至即時客戶個人檔案](../profile/tutorials/add-profile-data.md)
- [建立區段](../segmentation/tutorials/create-a-segment.md)
