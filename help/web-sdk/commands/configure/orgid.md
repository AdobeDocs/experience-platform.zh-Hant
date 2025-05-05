---
title: orgId
description: orgId屬性是字串，用於告知Adobe資料將傳送至哪個組織。
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

`orgId`屬性是字串，用於告知Adobe要將資料傳送至哪個組織。 **使用Web SDK傳送的所有資料都需要此屬性。**

若要尋找您的`orgID`：

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 在Adobe Experience Cloud中的任何地方，按&#x200B;**`[Ctrl]`** + **`[I]`**。 [!UICONTROL 使用者資料偵錯工具]視窗開啟。
1. 按一下[!UICONTROL 目前組織ID]旁的&#x200B;**[!UICONTROL 複製]** ![複製](../../assets/copy.png)，或按一下&#x200B;**[!UICONTROL 指派的組織]**&#x200B;索引標籤以檢視您可以存取的其他組織ID。
1. 完成尋找所需資訊後，請按一下[關閉]。**&#x200B;**

組織ID一律為24個字元的英數字串，且結尾一律為`@AdobeOrg`。

## 使用Web SDK標籤延伸設定`orgID`

在[設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)時，請在&#x200B;**[!UICONTROL IMS組織ID]**&#x200B;文字欄位中輸入組織ID。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 將所需的組織ID輸入頂端附近的[!UICONTROL IMS組織ID]文字欄位中。
1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript資料庫設定`orgID`

執行`configure`命令時設定`orgId`字串。 如果您在設定Web SDK時省略此屬性，Web SDK會擲回主控台錯誤，且資料不會傳送給Adobe。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
