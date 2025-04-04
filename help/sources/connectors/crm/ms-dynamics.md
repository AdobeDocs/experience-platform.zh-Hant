---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics；microsoft dynamics；dynamics；Dynamics
solution: Experience Platform
title: Microsoft Dynamics Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Microsoft Dynamics連線至Adobe Experience Platform。
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 3%

---

# Microsoft Dynamics 連接器

Adobe Experience Platform允許從外部來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

[!DNL Experience Platform]支援從協力廠商CRM系統擷取資料。 CRM提供者的支援包括[!DNL Microsoft Dynamics]。

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 從[!DNL Microsoft Dynamics]到XDM的欄位對應

若要在[!DNL Microsoft Dynamics]與Experience Platform之間建立來源連線，[!DNL Microsoft Dynamics]來源資料欄位必須先對應到適當的目標XDM欄位，才能內嵌到Experience Platform中。

請參閱下列內容，以取得有關[!DNL Microsoft Dynamics]資料集與Experience Platform之間的欄位對應規則的詳細資訊：

- [連絡人](../adobe-applications/mapping/dynamics.md#contacts)
- [銷售機會](../adobe-applications/mapping/dynamics.md#leads)
- [帳戶](../adobe-applications/mapping/dynamics.md#accounts)
- [機會](../adobe-applications/mapping/dynamics.md#opportunities)
- [機會聯絡人角色](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [行銷活動](../adobe-applications/mapping/dynamics.md#campaigns)
- [行銷清單](../adobe-applications/mapping/dynamics.md#marketing-list)
- [行銷清單成員](../adobe-applications/mapping/dynamics.md#marketing-list-members)

以下檔案提供如何使用API或使用者介面將[!DNL Microsoft Dynamics]連線到[!DNL Experience Platform]的資訊：

## 使用API連線[!DNL Microsoft Dynamics]至[!DNL Experience Platform]

- [使用Flow Service API建立Microsoft Dynamics基本連線](../../tutorials/api/create/crm/ms-dynamics.md)
- [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為CRM來源建立資料流](../../tutorials/api/collect/crm.md)

## 使用UI連線[!DNL Microsoft Dynamics]至[!DNL Experience Platform]

- [在UI中建立Microsoft Dynamics來源連線](../../tutorials/ui/create/crm/dynamics.md)
- [在UI中為CRM連線建立資料流](../../tutorials/ui/dataflow/crm.md)
