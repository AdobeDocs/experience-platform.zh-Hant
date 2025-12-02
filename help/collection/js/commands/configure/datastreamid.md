---
title: datastreamId
description: 決定您要傳送資料的目的地資料串流ID。
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: b9fea4833c4fe869b27c1270aafd3f7ed62d59db
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# `datastreamId`

`datastreamId`屬性是字串，可決定您要將資料傳送到Adobe Experience Platform中的[資料串流](/help/datastreams/overview.md)。 將資料傳送至Adobe時需要此屬性。 Web SDK 2.20.0版或更舊版本改用`edgeConfigId`。

若要尋找資料串流ID：

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**。
1. 使用搜尋欄位來尋找所需的資料流，然後選取資料流識別碼旁的&#x200B;**[!UICONTROL Copy]** ![複製](../../assets/copy.png)。

或者，您可以選取想要的資料流名稱，資料流ID會顯示在右欄以供您複製。

## 程式碼範例

執行`datastreamID`命令時設定`configure`字串屬性。 所有Web SDK實作都需要此屬性。 如果忽略此屬性，Web SDK就不會知道要將資料傳送至哪個資料流，導致該資料永久遺失。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

>[!NOTE]
>
>如果您在單一頁面上設定多個Web SDK執行個體，則必須為每個執行個體設定不同的`datastreamId`。

## 使用網頁SDK標籤擴充功能選取資料串流ID

請參閱Web SDK標籤擴充功能檔案中的[資料流組態設定](/help/tags/extensions/client/web-sdk/configure/datastreams.md)，瞭解如何使用標籤為每個環境設定所要的資料流。 您可以針對生產、測試和開發標籤環境，將資料傳送至不同的資料串流。
