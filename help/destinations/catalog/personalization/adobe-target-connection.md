---
keywords: 目標個人化；目的地；experience platform target目的地；adobe target目的地；
title: Adobe Target連線（測試版）
description: Adobe Target是一款應用程式，可在網站、行動應用程式等所有傳入客戶互動中，提供即時、1:1和AI支援的個人化和實驗。
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: fae3d9a5aff3e84354831026e9724e1c85d32b5c
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Adobe Target連線（測試版） {#adobe-target-connection}

## 總覽 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform中的Adobe Target連線目前為測試版。 檔案和功能可能會有所變更。

Adobe Target是一款應用程式，可在網站、行動應用程式等所有傳入客戶互動中，提供即時、1:1 、 AI支援的個人化和實驗。

Adobe Target是Adobe Experience Platform中的個人化連線。

## 先決條件 {#prerequisites}

此整合由 [Adobe Experience Platform Web SDK](../../../edge/home.md). 您必須使用此SDK才能使用此目的地。

## 匯出類型 {#export-type}

**設定檔要求**  — 您要求在Adobe Target目的地中對應的所有區段，以取得單一設定檔。

## 使用案例 {#use-cases}

**個人化首頁橫幅**

一家房屋租賃與銷售公司想要根據Adobe Experience Platform中的客戶區段資格，使用橫幅來個人化其首頁。 公司可以選取哪些對象應該獲得個人化體驗，並將這些對象傳送至Adobe Target，作為其Target選件的鎖定目標條件。

## 連接到目標 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="關於資料流ID"
>abstract="此選項會決定要將區段納入頁面回應中的資料收集資料流。 下拉式功能表只會顯示已啟用目的地設定的資料流。 您必須先設定資料流，才能設定目的地。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="了解如何設定資料流。"

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

Adobe Experience Platform會自動連線至您公司的Adobe Target執行個體。 不需要驗證。

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **名稱**:填寫此目的地的首選名稱。
* **說明**:輸入目的地的說明。 例如，您可以提及您使用此目的地的促銷活動。 此欄位為選填欄位。
* **資料流ID**:這會決定要將區段納入頁面回應中的資料收集資料流。 下拉式功能表只會顯示已啟用目的地設定的資料流。 請參閱 [設定資料流](../../../edge/fundamentals/datastreams.md) 以取得更多詳細資訊。

## 啟用此目的地的區段 {#activate}

閱讀 [啟動設定檔和區段至設定檔請求目的地](../../ui/activate-profile-request-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 匯出的資料 {#exported-data}

Adobe Target會從Adobe Experience Platform邊緣網路讀取設定檔資料，因此不會匯出任何資料。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
