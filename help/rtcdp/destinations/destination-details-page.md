---
keywords: destinations;destination;destinations detail page;destinations details page
title: 「目標詳細資料」頁
seo-title: 「目標詳細資料」頁
description: '個別目的地的詳細資訊頁面提供目的地詳細資訊的概述，例如目的地名稱、ID、對應至目的地的區段，以及編輯啟動和啟用和停用資料流的控制項。 '
seo-description: '個別目的地的詳細資訊頁面提供目的地詳細資訊的概述，例如目的地名稱、ID、對應至目的地的區段，以及編輯啟動和啟用和停用資料流的控制項。 '
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 1%

---


# 目標詳細資訊頁 {#destinations-details-page}

個別目的地的詳細資訊頁面提供目的地詳細資訊的概述，例如目的地名稱、ID、對應至目的地的區段，以及編輯啟動和啟用和停用資料流的控制項。 若要檢視這些詳細資訊，請 **[!UICONTROL 前往「目標]** > **[!UICONTROL 瀏覽]** 」，然後按一下您要使用的目標名稱。

個別目的地的核心元件包括：

* 1 —— 目標名稱和ID
* 2 —— 啟用至目的地的區段
* 3 —— 右側導軌資訊
* 4 —— 控制項以編輯啟動和啟用／停用資料流

![目標頁面編號](/help/rtcdp/destinations/assets/destination-page-numbered.png)

導覽至個別目標頁面，以取得目標詳細資訊的概述，例如：

## 1.目標名稱和ID

您可以在頁面標題中看到目標名稱，在頁面URL中看到目標ID。

## 2.區段已啟動至目標

此區段顯示哪些區段目前已對應至目標，以及這些區段的詳細資訊。 如需詳細資訊，請參閱下表：

| 項目 | 說明 |
---------|----------|
| 區段名稱 | 區段的名稱。 |
| 區段說明 | 區段的說明。 |
| 開始日期 | 這些區段啟動至目的地的日期。 |
| 結束日期 | 這些區段將停止啟動至目的地的日期。 |
| 對應ID | *電子郵件行銷目的地不適用*。 指出目標平台中區段已知的ID。 |

## 3.右側欄位資訊

右邊欄包含您目的地的相關資訊。 如需詳細資訊，請參閱下表：

| 項目 | 說明 |
---------|----------|
| 平台 | 代表對象被傳送至的目標平台。 如需詳 [細資訊，請參閱目](/help/rtcdp/destinations/destinations-catalog.md) 標目錄。 |
| 說明 | 您可以編輯目標流的說明。 |
| 類別 | 指示目標類型。 如需詳 [細資訊，請參閱目](/help/rtcdp/destinations/destinations-catalog.md) 標目錄。 |
| 連線類型 | 指出您的觀眾是以何種形式傳送至目的地。 可以是 [!UICONTROL Cookie][!UICONTROL 或描述檔]。 |
| 頻率 | 指出觀眾被傳送至目的地的頻率。 可以是 [!UICONTROL 串流] 或 [!UICONTROL 批次]。 |
| 身份 | 代表目標所接受的身分名稱空間。 例如，「身分識別」欄位可以是GAID、IDFA、電子郵件。 如需所有接受的身分名稱空間，請參閱「身分名稱空間概 [觀」中的標準名稱空間](../../identity-service/namespaces.md)。 |
| 建立者 | 表示建立此目標流的用戶。 |
| 已建立 | 表示建立此目標流的UTC日期和時間。 |

## 4.控制項，以編輯啟動和啟用／停用資料流

「編輯啟動」控制項可讓您編輯對應至目的地的區段。 按「編輯啟動」以開啟區 [段啟動工作流程](/help/rtcdp/destinations/activate-destinations.md)。

使用「 **啟用／停用** 」切換以啟動和暫停資料匯出至目標。