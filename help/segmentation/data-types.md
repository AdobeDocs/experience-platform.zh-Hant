---
keywords: Experience Platform；主題；熱門主題；資料類型；資料類型；資料類型；資料類型；分段資料類型；分段資料類型；分段；分段服務；分段服務；分段服務；分段服務資料類型；
solution: Experience Platform
title: 分段服務中支援的資料類型
description: Adobe分段服務支援所有體驗資料模型(XDM)資料類型。 構成段定義的規則按以下資料類型上下文化。
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# 分段服務中支援的資料類型

Adobe Experience Platform分段服務支援所有體驗資料模型(XDM)資料類型。 構成段定義的規則按以下資料類型上下文化。

## 字串資料

段定義使用字串資料為段受眾定義非數字約束，如&quot;國家/地區名稱&quot;或&quot;忠誠計畫級別&quot;。

字串資料使用邏輯、包含/排除和比較語句包括在段定義中。 在將字串屬性添加到段定義後，您可以使用與字串相關的語句根據其他字串欄位計算它。

| 語句類型 | 範例 |
| -------------- | -------- |
| 邏輯 | `and`、`or`、`not` |
| 包容/排斥 | `include`, `must` `exist`, `exclude`, `must not exist` |
| 比較 | `equals`, `does not equal`, `contains`, `starts with` |

## 日期資料

日期資料允許您通過使用特定起始日期/終止日期或使用下表所示的與日期相關的語句將基於時間的上下文分配給段定義。 一個實施方案可能是建立隨時與您的品牌互動的客戶群 *今年* 而且一直很活躍 *內* 最近幾天。

| 示例欄位 | 與日期相關的聲明 | 時間表 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | 與分部建立之日相關。 |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | 在任何給定周/月內相關。 |

## 體驗事件

作為Adobe Experience Platform的圖式， [!DNL XDM ExperienceEvents] 記錄顯性和隱性客戶交互 [!DNL Platform] — 整合應用程式，包括交互時的系統快照。 [!DNL ExperienceEvents] 是事實記錄。 因此，它們是段定義期間可供您使用的資料源。

如下表所示，使用關鍵字來呈現事件資料，這些關鍵字有助於細化事件行為並指定事件屬性。

| 關鍵字 | 使用 |
| ------- | --- |
| 包含/排除 | 描述通過包含或遺漏資料而發生的事件的行為。 |
| 任意/全部 | 幫助確定合格段的數量。 |
| 「應用時間規則」切換按鈕 | 合併日期資料。 |
| 等於、不等於、開頭為、不開頭為、結尾為、不結尾為、包含、不包含、存在、不存在 | 合併字串資料。 |

### 對象分享

外部受眾也可以用作新段定義的元件，將其屬性規則添加到新段。

目前，只有Adobe Audience Manager作為外部受眾受支援，今後還將啟用其他來源。 有關使用Adobe Audience Manager受眾和平台的更多資訊，請參見 [Adobe Audience Manager檔案中的受眾分享指南](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)。

### 段共用

在平台中建立的段可用於其他 [Adobe Experience Cloud核心服務](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=zh-Hant)。 要啟用此功能，您需要聯繫您的解決方案設計師或顧問。

## 其他資料類型

除上述資料類型外，支援的資料類型清單還包括：

- 統一資源標識符(URI)
- 枚舉
- 數字
- 龍
- 整數
- 短
- 位元組
- 布林值
- 陣列
- 物件
- 地圖
