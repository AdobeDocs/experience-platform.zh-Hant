---
title: orgId
description: orgId屬性是字串，用於告知Adobe要將資料傳送至哪個組織。
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# `orgId`

`orgId`屬性是字串，用於告知Adobe要將資料傳送至哪個組織。 **使用Web SDK傳送的所有資料都需要此屬性。**

若要尋找您的`orgID`：

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 在Adobe Experience Cloud中的任何地方，按&#x200B;**`[Ctrl]`** + **`[I]`**。 [!UICONTROL User Data Debugger]視窗隨即開啟。
1. 按一下&#x200B;**[!UICONTROL Copy]**&#x200B;旁的![ ](../../assets/copy.png)複製[!UICONTROL Current Org ID]，或按一下「**[!UICONTROL Assigned Orgs]**」索引標籤以檢視您可以存取的其他組織ID。
1. 完成尋找所需資訊後，請按一下&#x200B;**[!UICONTROL Close]**。

組織ID一律為24個字元的英數字串，且結尾一律為`@AdobeOrg`。

執行`orgId`命令時設定`configure`字串。 如果您在設定Web SDK時省略此屬性，Web SDK會擲回主控台錯誤，且資料不會傳送至Adobe。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

## 使用網頁SDK標籤擴充功能設定組織ID

您可以使用[SDK執行個體組態設定](/help/tags/extensions/client/web-sdk/configure/general.md)，在Web SDK標籤擴充功能中設定此設定。 欄位會根據建立標籤屬性的組織自動填入。
