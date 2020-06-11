---
title: 支援許可
seo-title: 支援Adobe Experience Platform Web SDK同意偏好設定
description: 瞭解如何使用Experience Platform Web SDK支援同意偏好設定
seo-description: 瞭解如何使用Experience Platform Web SDK支援同意偏好設定
translation-type: tm+mt
source-git-commit: c86ae6d887f52d8bb4b78dadc06060791c7a02c0
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# 支援許可

若要尊重使用者的隱私權，您可能會在允許SDK針對特定用途使用使用者特定資料之前，先要求使用者同意。 目前，SDK僅允許使用者選擇加入或退出所有用途，但Adobe希望未來能針對特定用途提供更精細的控制。

如果使用者選擇用於所有用途，則允許SDK執行下列工作：

* 傳送資料至Adobe伺服器或從Adobe伺服器傳送資料。
* 讀取和寫入Cookie或網頁儲存項目（除非使用者的選擇加入偏好設定持續存在）。

如果使用者退出所有用途，SDK不會執行任何這些工作。

## 設定同意

依預設，使用者會選擇加入所有用途。 若要防止SDK在使用者登入之前執行上述工作，請在SDK設定 `"defaultConsent": { "general": "pending" }` 期間傳遞如下：

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

當一般用途的預設同意設為待決時，嘗試執行任何依賴使用者選擇加入偏好設定的命令（例如，命令），會導致命令在SDK中排隊。 `event` 在您將使用者的選擇加入偏好設定傳達至SDK之前，不會處理這些命令。

此時，您可能會希望使用者在使用者介面中選擇加入。 收集使用者的偏好設定後，請將這些偏好設定傳達給SDK。

## 傳達同意偏好

如果用戶選擇，請執行 `setConsent` 將選項設定 `general` 為如 `in` 下的命令：

```javascript
alloy("setConsent", {
    consent: [{ 
      standard: "Adobe",
      version: "1.0",
      value: { 
        general: "in" 
      }
    }]
});
```

由於使用者現在已選擇加入，SDK會執行所有先前佇列的命令。 未來依賴使用者選擇加入的命令 _不會排_ 隊，而會立即執行。

如果用戶選擇退出，請執行該 `setConsent` 命令並將 `general` 選項設定為 `out` 如下：

```javascript
alloy("setConsent", {
    consent: [{ 
      standard: "Adobe",
      version: "1.0",
      value: { 
        general: "out" 
      }
    }]
});
```

>[!NOTE]
>
>使用者選擇退出後，SDK將不允許您將使用者同意設定為 `in`。

由於用戶選擇退出，因此拒絕從先前排隊的命令返回的承諾。 依賴使用者選擇的未來指令會傳回同樣遭拒的承諾。 有關處理或隱藏錯誤的詳細資訊，請參閱執 [行命令](executing-commands.md)。

>[!NOTE]
>
>目前，SDK僅支援其目 `general` 的。 雖然我們計畫建立一套更健全的目的或類別，以對應不同的Adobe功能和產品方案，但目前的實作方式是完全或完全不選擇加入。  這僅適用於Adobe Experience Platform Web SDK，而不適用於其他Adobe JavaScript程式庫。

## 持續遵守同意偏好

在您使用命令將使用者偏好設定傳達至SDK `setConsent` 後，SDK會將使用者偏好設定保留至Cookie。 下次使用者將您的網站載入瀏覽器時，SDK將會擷取並使用這些持續的偏好設定。 您不需要再次執行該 `setConsent` 命令，只需要通知用戶首選項的更改，您隨時都可以這樣做。