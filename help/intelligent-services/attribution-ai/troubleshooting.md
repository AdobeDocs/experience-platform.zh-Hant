---
keywords: Experience Platform；快速入門；attribution ai；熱門主題；attribution ai輸入；attribution ai輸出；attribution ai疑難排解；attribution ai錯誤
solution: Experience Platform, Real-time Customer Data Platform
feature: Attribution AI
title: Attribution AI錯誤疑難排解
description: 尋找常見錯誤的解答。Attribution AI
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Attribution AI錯誤疑難排解

本檔案提供關於Attribution AI常見問題的解答。

## 無法存取Chrome無痕中的Attribution AI

由於Google Chrome的無痕模式安全設定有更新，因此會出現Google Chrome無痕模式中的載入錯誤。 目前正與Chrome共同處理此問題，將experience.adobe.com設為值得信賴的網域。

<img src="./images/faq/error.PNG" width="500" /><br />

### 建議的修正

若要解決此問題，您需要將experience.adobe.com新增為一律可使用Cookie的網站。 首先，導覽至 **chrome://settings/cookies**. 下一步，向下捲動至 **自訂行為** 區段，接著選取 **新增** 按鈕（位於「一律可使用cookie的網站」旁）。 在顯示的彈出視窗中，複製並貼上 `[*.]experience.adobe.com` 然後選取 **包括第三方Cookie** 此網站上的複選框。 完成後，選取 **新增** 重新載入無痕Attribution AI。

![建議修正](./images/faq/cookies2.gif)
