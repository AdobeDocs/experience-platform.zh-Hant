---
title: '存取ECID '
description: Adobe Experience Platform Web SDK擴充功能運用標籤中的ECID
source-git-commit: befe1efa884706165b8d65803d06f6370a8a60f2
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 5%

---


# 存取ECID

[!DNL Experience Cloud Identity (ECID)]是您網站訪客的永久識別碼。 在某些情況下，您可能會偏好存取ECID（例如傳送給第三方）。

若要在標籤中存取ECID,Adobe建議：

1. 請確定屬性已設定為已啟用[規則元件排序](../../tags/ui/managing-resources/rules.md#sequencing)。
1. 建立新規則。
1. 將[!UICONTROL 程式庫已載入]事件新增至規則。
1. 使用下列程式碼將[!UICONTROL 自訂條件]動作新增至規則（假設您為SDK例項設定的名稱為`alloy`）:

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 儲存規則。

之後，您應該就能像使用任何其他資料元素一樣，使用`%ECID%`或`_satellite.getVar("ECID")`存取後續規則中的ECID。
