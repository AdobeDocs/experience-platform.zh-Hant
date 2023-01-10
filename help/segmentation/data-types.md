---
keywords: Experience Platform；首頁；熱門主題；資料類型；資料類型；資料類型；分段資料類型；分段；分段；分段服務；分段服務資料類型；
solution: Experience Platform
title: 分段服務中支援的資料類型
description: Adobe分段服務支援所有Experience Data Model(XDM)資料類型。 構成區段定義的規則會透過下列資料類型來情境化。
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# 分段服務中支援的資料類型

Adobe Experience Platform區段服務支援所有Experience Data Model(XDM)資料類型。 構成區段定義的規則會透過下列資料類型來情境化。

## 字串資料

區段定義使用字串資料來定義區段對象的非數值限制，例如「國家/地區名稱」或「忠誠計畫層級」。

字串資料會使用邏輯、包含/排除和比較陳述式包含在區段定義中。 將字串屬性新增至區段定義後，您就可以使用字串相關陳述式，以對其他字串欄位評估它。

| 語句類型 | 範例 |
| -------------- | -------- |
| 邏輯 | `and`、`or`、`not` |
| 包容/排他 | `include`, `must` `exist`, `exclude`, `must not exist` |
| 比較 | `equals`, `does not equal`, `contains`, `starts with` |

## 日期資料

日期資料可讓您透過使用特定開始/結束日期，或使用下表所示的日期相關陳述式，將以時間為基礎的內容指派給區段定義。 一個實作可能是隨時建立與您品牌互動的客戶對象 *今年* 而且也很活躍 *with* 最近幾天。

| 範例欄位 | 與日期相關的報表 | 時間表 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | 與區段建置日期相關。 |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | 在任何指定周/月內相關。 |

## 體驗事件

作為Adobe Experience Platform架構， [!DNL XDM ExperienceEvents] 記錄明確和隱含的客戶互動 [!DNL Platform] — 整合應用程式，包括進行交互時系統的快照。 [!DNL ExperienceEvents] 是事實記錄。 因此，在區段定義期間，您可以使用這些資料來源。

如下表所示，事件資料是使用有助於精簡事件行為並指定事件屬性的關鍵字呈現。

| 關鍵字 | 使用 |
| ------- | --- |
| 包含/排除 | 透過包含或遺漏資料來說明事件的行為。 |
| 任何/全部 | 有助於判斷合格區段的數量。 |
| 「應用時間規則」切換按鈕 | 納入日期資料。 |
| 等於、不等於、開頭為、開頭為、結尾為、結尾為、不結尾為、包含、不包含、存在、不存在 | 納入字串資料。 |

### 對象分享

外部受眾也可作為新區段定義的元件，將其屬性規則新增至新區段。

目前僅支援Adobe Audience Manager作為外部受眾，未來將啟用其他來源。 如需如何將Adobe Audience Manager對象與Platform搭配使用的詳細資訊，請參閱 [Adobe Audience Manager檔案中的對象共用指南](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### 區段共用

在Platform中建立的區段，可用於其他 [Adobe Experience Cloud Core Services](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=zh-Hant). 若要啟用此功能，您需要聯絡您的解決方案架構師或顧問。

## 其他資料類型

除了上述資料類型外，支援的資料類型清單還包括：

- 統一資源標識符(URI)
- 列舉
- 數字
- 長
- 整數
- 簡短
- 位元組
- 布林值
- 陣列
- 物件
- 地圖
