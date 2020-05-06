---
title: 擷取Experience Cloud ID
seo-title: Adobe Experience Platform Web SDK擷取Experience Cloud ID
description: 瞭解如何取得Adobe Experience Cloud Id。
seo-description: 瞭解如何取得Adobe Experience Cloud Id。
translation-type: tm+mt
source-git-commit: fc48c11cb1f8a88f9fec8a36646f59f39ac3819f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---


# （測試版）擷取Experience Cloud ID

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Cloud為每個消費者使用唯一ID。 如果要使用此唯一ID，請使用命 `getIdentity` 令。 `getIdentity` 傳回目前訪客的現有ECID。 對於尚未擁有ECID的首次訪客，此命令會產生新的ECID。

>[!NOTE]
>
>此方法通常用於需要讀取Experience Cloud ID的自訂解決方案。 標準實作不會使用它。

```javascript
alloy("getIdentity")
  .then(function(ecid) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```
