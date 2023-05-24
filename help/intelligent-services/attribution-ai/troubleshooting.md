---
keywords: Experience Platform；入門；屬性；流行主題；屬性ai輸入；屬性ai輸出；屬性ai疑難解答；屬性ai錯誤
solution: Experience Platform, Real-time Customer Data Platform
feature: Attribution AI
title: Attribution AI錯誤疑難解答
description: 查找Attribution AI中常見錯誤的答案。
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Attribution AI錯誤疑難解答

本文檔提供有關Attribution AI的常見問題解答。

## 無法訪問Chrome Incognito中的Attribution AI

由於GoogleChrome的隱藏模式安全設定中的更新，出現了在GoogleChrome的隱藏模式中載入錯誤。 該問題正在與Chrome一起積極研究，以使experience.adobe.com成為可信域。

<img src="./images/faq/error.PNG" width="500" /><br />

### 建議的修復

要解決此問題，您需要將experience.adobe.com添加為始終可以使用cookie的站點。 從導航開始 **chrome://settings/cookies**。 下一步，向下滾動到 **自定義行為** 部分，然後選擇 **添加** 按鈕「始終可以使用cookie的站點」。 在出現的跨距中，複製和貼上 `[*.]experience.adobe.com` 選擇 **包括第三方Cookie** 複選框。 完成後，選擇 **添加** 然後在隱藏中重新載入Attribution AI。

![建議修復](./images/faq/cookies2.gif)
