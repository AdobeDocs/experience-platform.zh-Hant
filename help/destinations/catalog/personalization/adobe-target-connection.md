---
keywords: 目標個性化；目的地；體驗平台目標；adobe目標目標；
title: Adobe Target
description: Adobe Target是一個應用程式，在跨網站、移動應用等的所有入站客戶交互中提供基於人工智慧的即時個性化和實驗功能。
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 05217dead7e1365d6dcc0cc7ae4078628514d1d5
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 1%

---

# Adobe Target {#adobe-target-connection}

## 總覽 {#overview}

Adobe Target是一個應用程式，在跨網站、移動應用等的所有入站客戶交互中提供基於人工智慧的即時個性化和實驗功能。

Adobe Target是Adobe Experience Platform的個性化連接。

## 先決條件 {#prerequisites}

此整合由 [Adobe Experience PlatformWeb SDK](../../../edge/home.md)。 您必須使用此SDK才能使用此目標。

>[!IMPORTANT]
>
>在建立 [!DNL Adobe Target] 連接，閱讀有關如何 [為同一頁和下一頁個性化設定配置個性化目標](../../ui/configure-personalization-destinations.md)。 本指南將引導您跨多個Experience Platform元件完成同一頁和下一頁個性化使用案例所需的配置步驟。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!DNL Profile request]** | 您正在請求在Adobe Target目標中映射的所有段以獲得單個配置檔案。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style=&quot;table-layout:auto&quot;}

## 使用案例 {#use-cases}

**個性化首頁標題**

一家房屋租賃和銷售公司希望根據Adobe Experience Platform的客戶細分資格，在自己的首頁上打出一個標語，個性化自己的首頁。 公司可以選擇哪些受眾應該獲得個性化體驗，並將這些體驗作為目標服務的目標標準發送給Adobe Target。

## 連接到目標 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="關於資料流ID"
>abstract="此選項確定在響應頁面時將包括段的資料收集資料流的位置。 下拉菜單僅顯示啟用了目標配置的資料流。 必須先配置資料流，然後才能配置目標。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="瞭解如何配置資料流"

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

Adobe Experience Platform自動連接到您公司的Adobe Target實例。 不需要身份驗證。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **名稱**:填寫此目標的首選名稱。
* **說明**:輸入目標的說明。 例如，您可以提及您為此目標使用的市場活動。 此欄位為可選欄位。
* **資料流ID**:這確定在響應頁面時將包括段的資料收集資料流的位置。 下拉菜單僅顯示啟用了目標配置的資料流。 請參閱 [配置資料流](../../../edge/fundamentals/datastreams.md) 的子菜單。

## 將段激活到此目標 {#activate}

閱讀 [激活配置檔案和段以配置請求目標](../../ui/activate-profile-request-destinations.md) 有關激活此目標受眾段的說明。

## 導出的資料 {#exported-data}

Adobe Target從Adobe Experience Platform邊緣網路讀取配置檔案資料，因此不會導出任何資料。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。
