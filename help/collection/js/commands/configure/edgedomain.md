---
title: edgeDomain
description: 決定您要傳送資料的目的地網域。
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 2d3c31e399989652a0472bbe2174ca8d8554ba30
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 3%

---

# `edgeDomain`

`edgeDomain`屬性可讓您變更Web SDK傳送資料的網域。 使用自訂網域有助於減少廣告封鎖程式的影響。

>[!NOTE]
>
>此屬性不會變更Cookie的設定位置。 Web SDK一律會設定[第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hant)，無論其最終傳送資料的位置為何。

您對`edgeDomain`使用的值取決於您參與[Adobe管理的憑證方案](https://experienceleague.adobe.com/zh-hant/docs/core-services/interface/data-collection/adobe-managed-cert)：

**如果您的組織參與Adobe管理的憑證方案**，請將值設定為設定憑證時選取的第一方網域。 通常此值是您的組織所擁有的子網域。 例如 `data.example.com`。您組織中的CNAME記錄會將該資料轉送至Adobe。

**如果您的組織未參與憑證方案**，請將值設定為`data.adobedc.net`的子網域。 Adobe建議您使用貴組織的Adobe指派IMS公司ID以維持一致性。 例如 `example.data.adobedc.net`。使用下列步驟來判斷您的IMS公司ID：

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 在Experience Cloud介面中的任何位置，按下`[Cmd]` + `[I]` (macOS)或`[Ctrl]` + `[I]` (Windows)。
1. 出現&#x200B;**[!UICONTROL User data debugger]**。 選取 **[!UICONTROL Assigned orgs]** 索引標籤。
1. 展開所需的IMS組織。
1. 找到&#x200B;**[!UICONTROL Tenant]**&#x200B;欄位。 建議使用此值的`data.adobedc.net`子網域。

執行`edgeDomain`命令時設定`configure`字串。 如果您在設定SDK時省略此屬性，其預設值為`edge.adobedc.net`。 雖然預設值是可接受的，但Adobe認為，設定組織專屬值是最佳做法。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```

## 使用Web SDK標籤擴充功能的Edge網域

設定擴充功能時，**[!UICONTROL Edge domain]** SDK執行個體組態設定[底下的](/help/tags/extensions/client/web-sdk/configure/general.md)欄位是這個屬性等同的標籤擴充功能。
