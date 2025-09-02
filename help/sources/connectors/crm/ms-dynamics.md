---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics；microsoft dynamics；dynamics；Dynamics
solution: Experience Platform
title: Microsoft Dynamics Source聯結器總覽
description: 瞭解如何使用API或使用者介面將Microsoft Dynamics連線至Adobe Experience Platform。
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 16fe5340582dcea0ff40000fb516c1b72d5f150e
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# [!DNL Microsoft Dynamics]來源

[!DNL Microsoft Dynamics]是一套商務應用程式，可用來更有效地管理您的作業。 無論您是監督客戶關係、財務或供應鏈，[!DNL Microsoft Dynamics]都能提供您工具，讓您簡化工作流程，並做出更明智的決定。 此平台可支援企業資源規劃和客戶關係管理(CRM)，讓您在整合的系統中統一您的業務流程。

您可以使用[!DNL Microsoft Dynamics]來源將您[!DNL Microsoft Dynamics]帳戶的資料擷取至Adobe Experience Platform。

## IP位址允許清單

將來源連線至Experience Platform之前，您必須先將區域特定的IP位址新增至允許清單。 如需詳細資訊，請閱讀[允許列出IP位址以連線至Experience Platform](../../ip-address-allow-list.md)的指南。

## 從[!DNL Microsoft Dynamics]到XDM的欄位對應

若要在[!DNL Microsoft Dynamics]與Experience Platform之間建立來源連線，[!DNL Microsoft Dynamics]來源資料欄位必須先對應到適當的目標XDM欄位，才能內嵌到Experience Platform中。

請參閱下列內容，以取得有關[!DNL Microsoft Dynamics]資料集與Experience Platform之間的欄位對應規則的詳細資訊：

- [聯絡人](../adobe-applications/mapping/dynamics.md#contacts)
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
