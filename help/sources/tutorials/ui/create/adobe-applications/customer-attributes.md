---
keywords: Experience Platform；首頁；熱門主題；客戶屬性
solution: Experience Platform
title: 在UI中建立客戶屬性源連接
type: Tutorial
description: 瞭解如何在UI中建立源連接，以將客戶屬性配置檔案資料帶入Adobe Experience Platform。
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 4%

---

# 在UI中建立客戶屬性源連接

本教程提供了在UI中建立源連接以將客戶屬性配置檔案資料導入Adobe Experience Platform的步驟。 有關客戶屬性的詳細資訊，請參閱 [客戶屬性概述](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=zh-Hant??lang=zh-Hant)。

>[!IMPORTANT]
>
>客戶屬性源當前不支援啟用或禁用資料流。

## 建立源連接

>[!NOTE]
>
>如果已為客戶屬性配置檔案資料建立源連接，則禁用與源連接的選項。

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立連接的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索欄找到要使用的特定源。

在 [!UICONTROL Adobe應用程式] 類別，選擇 **[!UICONTROL 客戶屬性]** ，然後選擇 **[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/customer-attributes/catalog.png)

### 選擇客戶屬性資料源

的 [!UICONTROL 添加資料] 螢幕列出了「客戶屬性」的所有可用資料源。 每個客戶屬性源連接只能選擇一個資料集。

>[!NOTE]
>
>欄位組、方案和資料集作為流設定的一部分在現成情況下建立。 它們將保持原樣，並且您必須手動刪除它們（如果需要）。

客戶屬性源不支援架構演化。 如果客戶屬性資料源的模式輸入發生更改，則它將與平台不相容。 作為解決方法，您可以刪除現有客戶屬性資料流及其關聯的資料集、模式和欄位組，然後使用更新的模式和資料源建立新的資料流。

>[!IMPORTANT]
>
>雖然您可以刪除客戶屬性資料流，但即使刪除資料流後，其相應的資料集仍將保留。 請參閱上的指南 [刪除資料集](../../../../../catalog/datasets/user-guide.md) 有關如何手動刪除資料集的步驟。

要建立新連接，請從清單中選擇資料源，然後選擇 **[!UICONTROL 下一個]**。

![添加資料](../../../../images/tutorials/create/customer-attributes/add-data.png)

### 提供資料流詳細資訊

的 [!UICONTROL 資料流詳細資訊] 步驟，允許您提供資料流的名稱和簡短說明。 在此過程中，您還可以配置 [!UICONTROL 錯誤診斷]。 [!UICONTROL 部分攝取], [!UICONTROL 警報]。

[!UICONTROL 錯誤診斷] 為資料流中出現的任何錯誤記錄啟用詳細的錯誤消息生成，同時 [!UICONTROL 部分攝取] 允許您接收包含錯誤的資料，最高可達您手動定義的特定閾值。 查看 [部分批處理接收概述](../../../../../ingestion/batch-ingestion/partial.md) 的子菜單。

您可以啟用警報來接收有關資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱源警報](../../alerts.md)。

完成向資料流提供詳細資訊後，選擇 **[!UICONTROL 下一個]**。

![資料流詳細資訊](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### 查看資料流

的 [!UICONTROL 審閱] 步驟，允許您在建立新資料流之前查看它。 詳細資訊按以下類別分組：

* **[!UICONTROL 連接]**:顯示源類型、所選源檔案的相關路徑以及該源檔案中的列數。
* **[!UICONTROL 分配資料集和映射欄位]**:顯示源資料正被攝取到的資料集，包括該資料集所遵循的架構。

![審查](../../../../images/tutorials/create/customer-attributes/review.png)

## 後續步驟

建立連線後，系統會自動建立目標結構和資料集以包含傳入的資料。初始接收完成後，下游平台服務(如 [!DNL Real-Time Customer Profile] 和 [!DNL Segmentation Service]。 有關詳細資訊，請參閱以下文檔：

* [[!DNL Real-Time Customer Profile] 概覽](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概覽](../../../../../segmentation/home.md)
