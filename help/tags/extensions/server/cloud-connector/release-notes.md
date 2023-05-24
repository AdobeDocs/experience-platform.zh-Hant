---
title: Adobe Experience Platform雲連接器擴展發行說明
description: Adobe Experience PlatformCloud Connector擴展的最新發行說明。
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 22%

---

# Adobe Experience Platform雲連接器擴展發行說明

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

## 2023 年 1 月 17 日

v1.0.1

* 修復貼上在Body Raw文本區域中的有效JSON被保存為字串而不是JSON的問題。
* 不允許對GET或HEAD請求設定正文。
* 修復錯誤，其中保存大於5kb的響應將導致規則執行失敗。
