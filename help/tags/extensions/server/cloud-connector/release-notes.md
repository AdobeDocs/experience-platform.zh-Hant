---
title: Adobe Experience Platform Cloud Connector 擴充功能發行說明
description: Adobe Experience Platform 中 Cloud Connector 擴充功能的最新發行說明。
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '128'
ht-degree: 100%

---

# Adobe Experience Platform Cloud Connector 擴充功能發行說明

>[!NOTE]
>
>Adobe Experience Platform Launch 已進行品牌重塑，現在是 Adobe Experience Platform 中的一套資料彙集技術。 因此，這些產品文件都推出多項幾術語變更。如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

## 2023 年 1 月 17 日

v1.0.1

* 修正貼在 Body Raw textarea 中的有效 JSON 是儲存為字串而不是 JSON 的問題。
* 不允許在 GET 或 HEAD 請求上設定 Body。
* 修正儲存大於 5kb 的回應會導致規則執行失敗的錯誤。
