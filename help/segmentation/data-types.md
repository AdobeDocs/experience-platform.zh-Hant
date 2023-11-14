---
solution: Experience Platform
title: 分段服務支援的資料型別
description: Adobe細分服務支援所有Experience Data Model (XDM)資料型別。 構成區段定義的規則會根據下列資料型別進行內容化。
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 3%

---

# 分段服務中支援的資料型別

Adobe Experience Platform Segmentation Service支援所有Experience Data Model (XDM)資料型別。 構成區段定義的規則會根據下列資料型別進行內容化。

## 字串資料

區段定義會使用字串資料來定義對象的非數值限制，例如「國家/地區名稱」或「忠誠計畫等級」。

字串資料會使用邏輯、包含/排除及比較陳述式包含在區段定義中。 將字串屬性新增至區段定義後，您就可以使用字串相關陳述式，以根據其他字串欄位進行評估。

| 陳述式型別 | 範例 |
| -------------- | -------- |
| 邏輯 | `and`、`or`、`not` |
| 包含/排除 | `include`, `must` `exist`, `exclude`, `must not exist` |
| 比較 | `equals`, `does not equal`, `contains`, `starts with` |

## 日期資料

日期資料可讓您使用特定的開始/結束日期，或使用與日期相關的陳述式，將基於時間的內容指派給區段定義，如下表所示。 其中一個實作可能是建立隨時與您的品牌互動的客戶受眾 *今年* 並且也一直處於作用中 *範圍* 過去幾天。

| 範例欄位 | 日期相關陳述式 | 時間表 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | 與建立區段定義的日期相關。 |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | 在任何指定周/月內相關。 |

## 體驗事件

作為Adobe Experience Platform結構描述， [!DNL XDM ExperienceEvents] 記錄與以下專案的明確和隱含客戶互動： [!DNL Platform] — 整合的應用程式，包括發生互動時的系統快照。 [!DNL ExperienceEvents] 是事實記錄。 因此，區段定義期間可供您使用的資料來源。

如下表所示，事件資料會使用關鍵字轉譯，有助於改善事件行為並指定事件屬性。

| 關鍵字 | 使用 |
| ------- | --- |
| 包含/排除 | 透過包含或遺漏資料來說明事件的行為。 |
| 任何/全部 | 協助判斷合格區段定義的數量。 |
| 「套用時間規則」切換按鈕 | 納入日期資料。 |
| 等於、不等於、開頭為、開頭為、結尾為、結尾為、包含、不包含、存在、不存在 | 納入字串資料。 |

### 對象分享

外部受眾也可作為新區段定義的元件，將其屬性規則新增至新區段定義。

目前僅Adobe Audience Manager支援作為外部對象，未來會啟用其他來源。 有關搭配Platform使用Adobe Audience Manager對象的詳細資訊，請參閱 [Adobe Audience Manager檔案中的對象共用指南](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### 區段定義共用

在Platform中建立的區段定義可用於其他內 [Adobe Experience Cloud核心服務](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html). 若要啟用此功能，您必須連絡解決方案架構師或顧問。

## 其他資料型別

除了上述的資料型別以外，支援的資料型別清單也包含：

- 統一資源識別碼(URI)
- 列舉
- 數字
- 長
- 整數
- 短
- 位元組
- 布林值
- 陣列
- 物件
- 地圖
