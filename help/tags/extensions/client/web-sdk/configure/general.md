---
title: SDK執行個體組態設定
description: 設定Web SDK執行個體的一般設定。
exl-id: cc22b8b3-88c6-4030-91b4-60e14a3b0f42
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---

# SDK執行個體組態設定 {#sdk-instance}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_sdkinstance"
>title="SDK執行個體"
>abstract="設定SDK執行個體名稱、其所屬的IMS組織和邊緣網域。"

此設定區段會控管Web SDK執行個體名稱、其適用的IMS組織，以及您要將資料傳送到的位置。 依預設，執行個體名為`alloy`。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 找出位於展開[!UICONTROL SDK instances]摺疊式功能表正下方的執行個體名稱。

![此影像顯示標籤UI中Web SDK標籤擴充功能的一般設定](../assets/web-sdk-ext-general.png)

提供下列選項：

## [!UICONTROL Name]

Adobe Experience Platform Web SDK標籤擴充功能支援頁面上的多個例項。 此名稱可用來傳送資料給多個組織，而不需要重複的網頁SDK標籤資料庫。 您可以將執行個體名稱變更為任何有效的JavaScript物件名稱。

## [!UICONTROL IMS organization ID]

您要在Adobe傳送資料的組織ID。 大部分時間都會使用自動填入的預設值。 頁面上有多個例項時，請找到您要傳送資料的第二個組織，以該組織的值填入此欄位。

## [!UICONTROL Edge domain]

擴充功能傳送及接收資料的網域。 依預設，欄位包含`<COMPANYID>.data.adobedc.net`。 舊版實作可能包含預設值`edge.adobedc.net`，該值也是有效的。

Adobe建議在大部分情況下使用第一方網域。 如需如何設定適合資料收集的第一方網域的指示，請參閱[Adobe管理的憑證方案](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert)。 另請參閱JavaScript資料庫檔案中的[`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md)，以取得設定此值的指引。
