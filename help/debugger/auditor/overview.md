---
title: 審計員頁籤
description: 瞭解如何使用Adobe Experience Platform調試器中的「審計者」頁籤testAdobe Experience Cloud實施。
keywords: Debugger；Experience Platform Debugger 擴充功能；Chrome；擴充功能；Auditor；DTM；Target
exl-id: 409094f8-a7d9-45f7-ba12-b5e6250abc0f
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 34%

---

# 「審計者」頁籤

在Adobe Experience Platform調試器中，可以使用 **[!UICONTROL 審計員]** 頁籤以在頁面上運行一系列審計test。

要使用此功能：

1. 選擇 **[!UICONTROL 審計員]** 的子菜單。
1. 選擇 **[!UICONTROL 運行審計員Test]**。 test完成後，其結果將顯示在下面。

![「審計器」頁籤上test結果的螢幕快照](../images/auditor-results.png)

結果清單會顯示測試項目及其結果，並提供解決問題的相關建議。

## 解釋test結果

每個test都被加權，而您的test分數等於分配的權重。 如果你通過一個重量為5的test，你會得到5分。

| 分數 | 說明 |
| --- | --- |
| 0 | 提醒您應注意的問題，但不影響分數。 |
| 1 | 建議優化。 不影響資料正確性。 |
| 2 | 如果此test失敗，則表示您將無法訪問Adobe Experience Cloud的最新功能和修復程式。 |
| 3 | Test效率以及實施是否遵循最佳做法。 |
| 4 | 失敗表示您可能正在收集不可靠的資料。 |
| 5 | 失敗意味著您可能看到資料丟失。 |

所有test要麼通過要麼失敗。 測試目的在於確認是否符合測試條件，因此並不會因為部分符合而獲得部分分數。例如，如果測試檢查您是否有最新版的 Adobe 解決方案，而您只比最新版本舊一個版本，您得到的分數仍會與舊五個版本相同。最新版本包括效能改進和錯誤修復，因此建議使用最新版本。

**強烈建議**&#x200B;您修正層級 4 或層級 5 的結果。

**建議**&#x200B;您修正層級 1 到層級 3 的結果。

## 支援的Adobe技術

審計者功能可以對以下Adobe技術進行分級：

* Adobe Advertising Cloud DSP
* Adobe Advertising Cloud Search
* Adobe Analytics
* Adobe Experience Cloud Identity Service
* Adobe Target
* 標籤(以前稱為Adobe Experience Platform Launch)

## Test

有關此功能提供的test規則的詳細資訊，請參閱以下檔案：

* [標記一致性](./tag-consistency.md)
* [標記是否存在](./tag-presence.md)
* [設定](./configuration.md)
* [警報](./alerts.md)
