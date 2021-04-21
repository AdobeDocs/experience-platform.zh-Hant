---
keywords: Experience Platform；主題；熱門話題；資料類型；資料類型；資料類型；資料類型；分段資料類型；分段；分段服務；分段服務資料類型；
solution: Experience Platform
title: 分段服務中支援的資料類型
topic-legacy: overview
description: Adobe分段服務支援所有體驗資料模型(XDM)資料類型。 構成區段定義的規則會依下列資料類型來情境化。
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# 區段服務中支援的資料類型

Adobe Experience Platform區段服務支援所有Experience Data Model(XDM)資料類型。 構成區段定義的規則會依下列資料類型來情境化。

## 字串資料

區段定義使用字串資料來定義區段對象的非數值限制，例如「國家／地區名稱」或「忠誠度方案層級」。

字串資料會使用邏輯、包含／排除和比較陳述式包含在區段定義中。 在將字串屬性新增至區段定義後，您就可以使用字串相關陳述式，針對其他字串欄位來評估。

| 語句類型 | 範例 |
| -------------- | -------- |
| 邏輯 | `and`, `or`, `not` |
| 包含／排除 | `include`, `must` `exist`, `exclude`, `must not exist` |
| 比較 | `equals`,  `does not equal`,  `contains`,  `starts with` |

## 日期資料

日期資料可讓您使用特定的開始／結束日期或使用與日期相關的陳述式，將時間相關的內容指派給區段定義。 其中一個實作可能是建立在&#x200B;*今年*&#x200B;任何時候與您的品牌互動，且在&#x200B;*最近幾天內也*&#x200B;活躍的客戶群。

| 範例欄位 | 與日期相關的聲明 | 時間表 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`,  `yesterday`,  `this month`,  `this year` | 與區段建立當日相關。 |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | 在任何指定的周／月內相關。 |

## 體驗事件

作為Adobe Experience Platform模式，[!DNL XDM ExperienceEvents]記錄了與[!DNL Platform]整合應用程式的顯式和隱式客戶交互，包括交互發生時系統的快照。 [!DNL ExperienceEvents] 是事實記錄。因此，它們是區段定義期間可供您使用的資料來源。

如下表所示，事件資料會使用有助於調整事件行為並指定事件屬性的關鍵字來呈現。

| 關鍵字 | 使用 |
| ------- | --- |
| 包含／排除 | 說明事件透過包含或遺漏資料的行為。 |
| 任何／所有 | 協助判斷符合資格的區段數。 |
| 「套用時間規則」切換按鈕 | 整合日期資料。 |
| 等於、不等於、開頭為、不開頭為、結尾為、不結尾為、包含、不包含、存在、不存在 | 整合字串資料。 |

### 受眾分享

外部對象也可以用作新區段定義的元件，將其屬性規則新增至新區段。

目前，只有Adobe Audience Manager作為外部受眾受到支援，未來將啟用其他來源。 有關搭配平台使用Adobe Audience Manager觀眾的更多資訊，請參閱Adobe Audience Manager檔案](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)中的[觀眾分享指南。

### 區段共用

在平台中建立的區段可用於其他[Adobe Experience Cloud核心服務](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/experience-cloud.html)。 若要啟用此功能，您必須聯絡解決方案架構師或顧問。

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
