---
title: 處理命令回應
description: 使用JavaScript承諾處理命令的回應。
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 處理命令回應

有些Web SDK命令可能會傳回包含對貴組織可能有用的資料的物件。 如有需要，您可以選擇如何處理該資料。 命令回應對於主張和目的地來說非常重要，因為它們需要Edge Network資料才能有效運作。

命令回應使用JavaScript [promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise)，做為建立promise時未知之值的Proxy。 知道值後，就會使用值「解析」Promise。

## 使用Web SDK標籤擴充功能處理命令回應

建立訂閱&#x200B;**[!UICONTROL 傳送事件完成]**&#x200B;事件的規則作為規則的一部分。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 規則]**，然後選取所要的規則。
1. 在[!UICONTROL 事件]下，選取現有事件或建立事件。
1. 將[!UICONTROL 擴充功能]下拉式清單欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將[!UICONTROL 事件型別]設為&#x200B;**[!UICONTROL 傳送事件完成]**。
1. 按一下&#x200B;**[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

然後您可以包含動作&#x200B;**[!UICONTROL 套用主張]**&#x200B;或&#x200B;**[!UICONTROL 套用回應]**&#x200B;至此規則。

1. 檢視上述建立或編輯的規則時，請選取現有動作或建立動作。
1. 將[!UICONTROL 擴充功能]下拉式欄位設定為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將[!UICONTROL 動作型別]設定為&#x200B;**[!UICONTROL 套用主張]**&#x200B;或&#x200B;**[!UICONTROL 套用回應]**，視所要的行為而定。
1. 設定動作的所需欄位，然後按一下[保留變更]。**&#x200B;**

## 使用Web SDK JavaScript程式庫處理命令回應

使用`then`和`catch`方法判斷命令成功或失敗的時間。 如果`then`或`catch`的用途對您的實作並不重要，您可以省略。

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    console.log("The sendEvent command succeeded.");
  })
  .catch(function(error) {
    console.log("The sendEvent command failed.");
  });
```

命令傳回的所有promise都使用`result`物件。 例如，您可以使用[`getLibraryInfo`](getlibraryinfo.md)命令從`result`物件取得程式庫資訊：

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

此`result`物件的內容取決於您使用的命令與使用者同意的組合。 如果使用者未針對特定目的提供其同意，則回應物件僅包含可在使用者同意的內容中提供的資訊。
