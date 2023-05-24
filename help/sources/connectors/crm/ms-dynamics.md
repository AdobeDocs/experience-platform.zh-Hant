---
keywords: Experience Platform；主題；熱門主題；Microsoft動態；microsoft動態；動態
solution: Experience Platform
title: MicrosoftDynamics源連接器概述
description: 瞭解如何使用API或用戶介面將MicrosoftDynamics連接到Adobe Experience Platform。
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Microsoft Dynamics 連接器

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

[!DNL Experience Platform] 支援從第三方CRM系統接收資料。 對CRM提供程式的支援包括 [!DNL Microsoft Dynamics]。

## IP地址允許清單

在使用源連接器之前，必須將IP地址清單添加到允許清單。 如果無法將特定於區域的IP地址添加到允許清單，則在使用源時可能會導致錯誤或效能不佳。 查看 [IP地址允許清單](../../ip-address-allow-list.md) 的子菜單。

## 欄位映射自 [!DNL Microsoft Dynamics] 到XDM

建立源連接 [!DNL Microsoft Dynamics] 平台， [!DNL Microsoft Dynamics] 在將源資料欄位納入平台之前，必須將其映射到相應的目標XDM欄位。

有關在以下位置之間的欄位映射規則的詳細資訊，請參閱以下 [!DNL Microsoft Dynamics] 資料集和平台：

- [聯繫人](../adobe-applications/mapping/dynamics.md#contacts)
- [銷售線索](../adobe-applications/mapping/dynamics.md#leads)
- [帳戶](../adobe-applications/mapping/dynamics.md#accounts)
- [機會](../adobe-applications/mapping/dynamics.md#opportunities)
- [機會聯繫人角色](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [行銷活動](../adobe-applications/mapping/dynamics.md#campaigns)
- [營銷員](../adobe-applications/mapping/dynamics.md#marketing-list)
- [市場營銷清單成員](../adobe-applications/mapping/dynamics.md#marketing-list-members)

以下文檔提供了有關如何連接的資訊 [!DNL Microsoft Dynamics] 至 [!DNL Platform] 使用API或用戶介面：

## 連接 [!DNL Microsoft Dynamics] 至 [!DNL Platform] 使用API

- [使用流服務API建立MicrosoftDynamics基連接](../../tutorials/api/create/crm/ms-dynamics.md)
- [使用流服務API瀏覽資料表](../../tutorials/api/explore/tabular.md)
- [使用流服務API為CRM源建立資料流](../../tutorials/api/collect/crm.md)

## 連接 [!DNL Microsoft Dynamics] 至 [!DNL Platform] 使用UI

- [在UI中建立MicrosoftDynamics源連接](../../tutorials/ui/create/crm/dynamics.md)
- [在UI中為CRM連接建立資料流](../../tutorials/ui/dataflow/crm.md)
