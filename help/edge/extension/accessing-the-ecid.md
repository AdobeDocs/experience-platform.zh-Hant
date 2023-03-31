---
title: 存取ECID
description: 了解如何存取Adobe Experience Platform標籤中的Experience CloudID(ECID)
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 5%

---


# 存取ECID

此 [!DNL Experience Cloud ID (ECID)] 是永久性Experience Cloud識別碼，可協助您識別網站的訪客。 在特定情況下（例如傳送識別碼至協力廠商平台），您可能需要 [!DNL ECID].

若要存取 [!DNL ECID] 在標籤中，遵循下列步驟：

1. 確認屬性已設定 [規則元件排序](../../tags/ui/managing-resources/rules.md#sequencing) 已啟用。
2. 建立新規則。
3. 新增 [!UICONTROL 程式庫已載入] 事件。
4. 新增 [!UICONTROL 自訂條件] 動作，並搭配下列程式碼(假設您為SDK例項設定的名稱為 `alloy`):

   ```javascript
   return alloy("getIdentity")
       .then(function(result) {
           _satellite.setVar("ECID", result.identity.ECID);
       });
   ```

5. 儲存規則。

您現在應該可以存取 [!DNL ECID] 在後續規則中，使用 `%ECID%` 或 `_satellite.getVar("ECID")`，類似於您存取任何其他資料元素的方式。
