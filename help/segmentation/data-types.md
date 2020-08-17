---
keywords: Experience Platform;home;popular topics;data type;data types;Data types;Data type
solution: Experience Platform
title: Adobe Experience Platform細分服務資料類型
topic: overview
description: 區段服務支援所有XDM資料類型。 構成區段定義的規則會依下列資料類型來情境化。
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 3%

---


# Adobe Experience Platform支援 [!DNL Segmentation Service] 的資料類型

支援內的所有XDM資料類型 [!DNL Segmentation Service]。 構成區段定義的規則會依下列資料類型來情境化。

## 字串資料

區段定義使用字串資料來定義區段對象的非數值限制，例如「國家／地區名稱」或「忠誠度方案層級」。

字串資料會使用邏輯、包含／排除和比較陳述式包含在區段定義中。 在將字串屬性新增至區段定義後，您就可以使用字串相關陳述式，針對其他字串欄位來評估。

| 語句類型 | 範例 |
| -------------- | -------- |
| 邏輯 | `and`, `or`, `not` |
| 包含／排除 | `include`, `must` `exist`, `exclude`, `must not exist` |
| 比較 | `equals`, `does not equal`, `contains`, `starts with` |

## 日期資料

日期資料可讓您使用特定的開始／結束日期或使用與日期相關的陳述式，將時間相關的內容指派給區段定義。 其中一項實作可能是為今年任何時間與您品牌互動且在過 *去幾天內也**活躍的客* 戶建立觀眾。

| 範例欄位 | 與日期相關的聲明 | 時間表 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | 與區段建立當日相關。 |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | 在任何指定的周／月內相關。 |

## 體驗事件

以Adobe Experience Platform架構 [!DNL XDM ExperienceEvents][!DNL Platform]記錄客戶與整合式應用程式的明確和隱含互動，包括互動發生時的系統快照。 [!DNL ExperienceEvents] 是事實記錄。 因此，它們是區段定義期間可供您使用的資料來源。

如下表所示，事件資料會使用有助於調整事件行為並指定事件屬性的關鍵字來呈現。

| 關鍵字 | 使用 |
| ------- | --- |
| 包含／排除 | 說明事件透過包含或遺漏資料的行為。 |
| 任何／所有 | 協助判斷符合資格的區段數。 |
| 「套用時間規則」切換按鈕 | 整合日期資料。 |
| 等於、不等於、開頭為、不開頭為、結尾為、不結尾為、包含、不包含、存在、不存在 | 整合字串資料。 |

### 受眾分享

外部對象也可以用作新區段定義的元件，將其屬性規則新增至新區段。

目前，只有Adobe Audience Manager才支援做為外部觀眾，未來會啟用其他來源。 有關搭配使用Adobe Audience Manager觀眾的更多資訊，請參閱Adobe Audience Manager [檔案中的觀眾分享指南](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)。

### 區段共用

在Platform中建立的區段可用於其他 [Adobe Experience Cloud核心服務](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/experience-cloud.html)。 若要啟用此功能，您必須聯絡解決方案架構師或顧問。

## 其他資料類型

除了上述資料類型外，支援的資料類型清單還包括：

- 統一資源標識符(URI)
- Enum
- 數字
- 長
- 整數
- 簡短
- 位元組
- 布林值
- 陣列
- 物件
- 地圖