---
title: edgeConfigId
description: 決定您要傳送資料的目的地資料串流ID。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

此 `edgeConfigId` 屬性是一個字串，可決定 [資料流](../../../datastreams/overview.md) 在Adobe Experience Platform中，您要將資料傳送至。 將資料傳送至Adobe時需要此屬性。

若要尋找資料串流ID：

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 資料串流]**.
1. 使用搜尋欄位來找出所需的資料流，然後選取 **[!UICONTROL 複製]** ![複製](../../assets/copy.png) 資料串流ID旁。

您也可以選取想要的資料流名稱，資料流ID會顯示在右欄以供您複製。

## 使用Web SDK標籤擴充功能選取資料串流ID

從可用資料串流清單中選擇，或直接輸入資料串流ID，當 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 找到 [!UICONTROL 資料串流] 區段，然後選取所需的判斷資料流的方法。
   * 如果從清單中選擇，請從每個相應的下拉式清單中選取沙箱和資料流。
   * 如果輸入值，請輸入所需的資料流ID。
1. 按一下 **[!UICONTROL 儲存]**，然後發佈您的變更。

您可以針對生產、測試和開發標籤環境，將資料傳送至不同的資料串流。

## 使用Web SDK JavaScript程式庫選取資料串流ID

設定 `edgeConfigId` 字串屬性 `configure` 命令。 所有Web SDK實作都需要此屬性。 如果忽略此屬性，Web SDK就不會知道要將資料傳送至哪個資料流，導致該資料永久遺失。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

如果您在單一頁面上設定多個Web SDK執行個體，則必須設定不同的 `edgeConfigId` 適用於每個執行個體。
