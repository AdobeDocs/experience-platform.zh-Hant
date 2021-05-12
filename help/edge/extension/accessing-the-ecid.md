---
title: '存取ECID '
description: Adobe Experience Platform網頁SDK擴充功能運用Adobe Experience Platform Launch的ECID
source-git-commit: 3002036d7366e2f7310aa62e53c7c391d9ff7a07
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 5%

---


# 存取ECID

[!DNL Experience Cloud Identity (ECID)]是網站訪客的永久識別碼。 在某些情況下，您可能會偏好存取ECID（例如傳送給第三方）。

若要在Adobe Experience Platform Launch境記憶體取ECID,Adobe建議：

1. 請確定您的屬性已設定[規則元件sequencing](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing)。
1. 建立新規則。
1. 新增[!UICONTROL Library Loaded]事件至規則。
1. 將[!UICONTROL Custom Condition]動作新增至規則並包含下列程式碼（假設您為SDK例項設定的名稱為`alloy`）:

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 儲存規則。

然後，您應該可以像使用任何其他資料元素一樣，使用`%ECID%`或`_satellite.getVar("ECID")`在後續規則中存取ECID。
