---
title: 終止支援Internet Explorer 10和11中的標籤
description: Adobe Experience Platform不再提供Internet Explorer 10和11標籤的更新支援。
exl-id: 35491c80-2a8a-4e07-baa7-a5db373b6852
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# 終止支援Internet Explorer 10和11中的標籤

隨著線上數位體驗環境的不斷演化，Adobe不再投入資源支援Adobe Experience Platform標籤適用的Internet Explorer 10 (IE10)和Internet Explorer 11 (IE11)。 雖然Adobe未主動移除對IE10和IE11的支援，但未來更新將不再考慮這些瀏覽器對新功能的影響。

## 為何不再支援IE10和IE11？

標籤不再支援IE10和IE11有四個原因：

* **Microsoft已停止支援IE10和IE11**：自2020年1月起，[Microsoft已停止支援IE10](https://docs.microsoft.com/en-us/lifecycle/announcements/internet-explorer-10-end-of-support)的安全性更新和非安全性更新。 自2022年6月起，[Microsoft已停止支援特定Windows版本的IE11](https://docs.microsoft.com/en-us/lifecycle/announcements/internet-explorer-11-end-of-support)。
* **更廣的產業正在停止支援IE10和IE11**：隨著更廣的產業停止支援IE10和IE11，標籤維持對這些技術回溯相容性的功能會越來越受阻礙。
* **現代技術不支援IE10和IE11**：若要讓標籤繼續支援最現代的技術，就必須終止支援IE10和IE11，因為這些現代技術與這些網頁瀏覽器不相容。
* **支援IE10和IE11會減慢整體功能的開發速度**：許多針對標籤發行的新功能都需要仔細考慮IE10和IE11。 考量這項考量需要花費數小時的額外工作，才能取得可搭配IE10和IE11使用的難以找到的測試工具、新增其他程式碼讓功能在沒有原生支援的IE10和IE11上運作，並研究確保功能如預期般運作。 透過停止支援IE10和IE11，Adobe可以更快地提供新功能。

## IE10和IE11淘汰的影響

停止支援後，將產生下列效果：

* 新功能可能不支援IE10和IE11。
* 將停止測試使用IE10和IE11支援目前和新功能。
* 原先支援IE10和IE11的功能可能不再支援這些瀏覽器。
