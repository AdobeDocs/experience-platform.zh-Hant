---
title: 存取ECID
description: Adobe Experience Platform Web SDK擴充功能運用標籤中的ECID
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 5%

---

# 存取ECID

此 [!DNL Experience Cloud Identity (ECID)] 是您網站訪客的永久識別碼。 在某些情況下，您可能會偏好存取ECID（例如傳送給第三方）。

若要在標籤中存取ECID,Adobe建議：

1. 確認屬性已設定 [規則元件排序](../../tags/ui/managing-resources/rules.md#sequencing) 已啟用。
1. 建立新規則。
1. 新增 [!UICONTROL 程式庫已載入] 事件。
1. 新增 [!UICONTROL 自訂條件] 動作至具有下列程式碼的規則(假設您為SDK例項設定的名稱為 `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 儲存規則。

之後，您應該就能使用 `%ECID%` 或 `_satellite.getVar("ECID")` 就像您要其他資料元素一樣。
