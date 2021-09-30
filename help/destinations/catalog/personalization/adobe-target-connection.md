---
keywords: 目標個人化；目的地；experience platform target目的地；adobe target目的地；
title: Adobe Target連線（測試版）
description: Adobe Target是一款應用程式，可在網站、行動應用程式等所有傳入客戶互動中，提供即時、1:1和AI支援的個人化和實驗。
source-git-commit: 0635828cf3f637e67d2cabda860ca452e61892d4
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---


# Adobe Target連線（測試版） {#adobe-target-connection}

## 總覽 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform中的Adobe Target連線目前為測試版。 檔案和功能可能會有所變更。

Adobe Target是一款應用程式，可在網站、行動應用程式等所有傳入客戶互動中，提供即時、1:1 、 AI支援的個人化和實驗。

Adobe Target是Adobe Experience Platform中的個人化連線。

## 先決條件 {#prerequisites}

此整合由[Adobe Experience Platform Web SDK](../../../edge/home.md)提供支援。 您必須使用此SDK才能使用此目的地。

## 匯出類型 {#export-type}

**設定檔請求**  — 您要求在Adobe Target目的地中對應的所有區段，以取得單一設定檔。

## 使用案例 {#use-cases}

**個人化首頁橫幅**

一家房屋租賃與銷售公司想要根據Adobe Experience Platform中的客戶區段資格，使用橫幅來個人化其首頁。 公司可以選取哪些對象應該獲得個人化體驗，並將這些對象傳送至Adobe Target，作為其Target選件的鎖定目標條件。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

Adobe Experience Platform會自動連線至您公司的Adobe Target執行個體。 不需要驗證。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **名稱**:填寫此目的地的首選名稱。
* **說明**:輸入目的地的說明。例如，您可以提及您使用此目的地的促銷活動。 此欄位為選填欄位。
* **資料流ID**:這會決定要將區段納入頁面回應中的資料收集資料流。下拉式功能表只會顯示已啟用目的地設定的資料流。 如需詳細資訊，請參閱[設定資料流](../../../edge/fundamentals/datastreams.md) 。

## 啟用此目的地的區段 {#activate}

請參閱[將設定檔和區段啟用至設定檔請求目的地](../../ui/activate-profile-request-destinations.md) ，以取得關於將對象區段啟用至此目的地的指示。

## 匯出的資料 {#exported-data}

Adobe Target會從Adobe Experience Platform邊緣網路讀取設定檔資料，因此不會匯出任何資料。

## 資料使用與控管 {#data-usage-governance}

處理資料時，所有[!DNL Adobe Experience Platform]目標都符合資料使用策略。 有關[!DNL Adobe Experience Platform]如何實施資料控管的詳細資訊，請參閱[資料控管概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。
