---
title: 傳送資料至Adobe Audience Manager
seo-title: 使用Adobe Experience Platform Web SDK將資料傳送至Adobe Audience Manager
description: 瞭解如何使用Experience Platform Web SDK將資料傳送至Adobe Audience Manager
seo-description: 瞭解如何使用Experience Platform Web SDK將資料傳送至Adobe Audience Manager
translation-type: tm+mt
source-git-commit: 4bea14d18ce119bdec0d428f885d240f92244cfc
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Experience Platform Edge網路上的Audience Manager

Adobe Experience Platform Web SDK已與Adobe Audience Manager整合，並支援從Audience Manager、Cookie和URL目的地傳送及接收資料，以及ID同步。

## 啟用Audience Manager

若要啟用Audience Manager，您必須執行下列動作：

- 在邊緣設定中啟 [用Audience Manager](../../fundamentals/edge-configuration.md)。
- 啟用或停用Cookie和URL目的地。
- 指定外部合作夥伴同步的ID同步容器（選用）

## 同步身分識別

Adobe Experience Platform Web SDK支援透過 [SyncIdentity命令宣告客戶ID及其驗證狀態](../../fundamentals/identity.md) 。

syncIdentity方法使用 [Identity Service Namespaces](../../../identity/../identity-service/namespaces.md) ，以指出身份相關的上下文。 身為Audience Manager客戶，您所有使用ID類型的現有資料來源： 跨裝置將自動擁有對應的身分名稱空間。 若要尋找Audience Manager資料來源的對應Identity Namespace，請登入Adobe Experience Platform並導覽至「身分識別」區段。

![名稱空間UI的視圖](../../../assets/edge_configuration_identity.png)

您可以在這裡依名稱搜尋您的Audience Manager資料來源。 syncIdentity方法使用Identity Symbol來指定Namespace。

任何使用ID類型的新Audience Manager資料來源： 跨裝置將產生對應的身分命名空間。 資料來源ID類型目前不支援Cookie和裝置廣告ID。 此外，在Adobe Experience Platform中建立的任何Identity Namespace都會產生對應的Audience Manager資料來源，但請注意syncIdentity方法僅支援Namespace Identity Symbols。
