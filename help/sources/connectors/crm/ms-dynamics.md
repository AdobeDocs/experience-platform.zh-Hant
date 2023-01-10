---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics;microsoft dynamics;Dynamics;Dynamics
solution: Experience Platform
title: Microsoft Dynamics Source Connector概述
description: 了解如何使用API或使用者介面將Microsoft Dynamics連線至Adobe Experience Platform。
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Microsoft Dynamics 連接器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

[!DNL Experience Platform] 支援從協力廠商CRM系統擷取資料。 支援CRM提供者包括 [!DNL Microsoft Dynamics].

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 欄位對應來源 [!DNL Microsoft Dynamics] 到XDM

在 [!DNL Microsoft Dynamics] 平台， [!DNL Microsoft Dynamics] 將來源資料欄位擷取至Platform之前，必須先對應至其適當的目標XDM欄位。

請參閱下列內容，以取得關於 [!DNL Microsoft Dynamics] 資料集和Platform:

- [聯繫人](../adobe-applications/mapping/dynamics.md#contacts)
- [銷售機會](../adobe-applications/mapping/dynamics.md#leads)
- [帳戶](../adobe-applications/mapping/dynamics.md#accounts)
- [機會](../adobe-applications/mapping/dynamics.md#opportunities)
- [機會聯繫人角色](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campaigns](../adobe-applications/mapping/dynamics.md#campaigns)
- [行銷人員](../adobe-applications/mapping/dynamics.md#marketing-list)
- [行銷清單成員](../adobe-applications/mapping/dynamics.md#marketing-list-members)

以下檔案提供如何連線的資訊 [!DNL Microsoft Dynamics] to [!DNL Platform] 使用API或使用者介面：

## Connect [!DNL Microsoft Dynamics] to [!DNL Platform] 使用API

- [使用流量服務API建立Microsoft Dynamics基礎連線](../../tutorials/api/create/crm/ms-dynamics.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流服務API為CRM源建立資料流](../../tutorials/api/collect/crm.md)

## Connect [!DNL Microsoft Dynamics] to [!DNL Platform] 使用UI

- [在UI中建立Microsoft Dynamics來源連線](../../tutorials/ui/create/crm/dynamics.md)
- [在UI中為CRM連線建立資料流](../../tutorials/ui/dataflow/crm.md)
