---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics;Microsoft Dynamics;Dynamics;Dynamics
solution: Experience Platform
title: Microsoft Dynamics源連接器概述
topic-legacy: overview
description: 了解如何使用API或使用者介面將Microsoft Dynamics連線至Adobe Experience Platform。
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---

# Microsoft Dynamics 連接器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用[!DNL Platform]服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

[!DNL Experience Platform] 支援從協力廠商CRM系統擷取資料。支援CRM提供者包括[!DNL Microsoft Dynamics]。

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

>[!IMPORTANT]
>
>[!DNL Microsoft Dynamics]源連接器當前不支援與Platform的相同區域連接。 這表示，如果您的Azure執行個體使用與Platform相同的網路區域，則無法建立與Platform來源的連線。 目前僅支援跨地區連線。 如需詳細資訊，請連絡您的Adobe客戶經理。

以下檔案提供如何使用API或使用者介面將[!DNL Microsoft Dynamics]連線至[!DNL Platform]的資訊：

## 使用API將[!DNL Microsoft Dynamics]連線至[!DNL Platform]

- [使用流服務API建立Microsoft Dynamics基本連接](../../tutorials/api/create/crm/ms-dynamics.md)
- [使用流量服務API探索CRM來源的資料結構和內容](../../tutorials/api/explore/crm.md)
- [使用流服務API為CRM源建立資料流](../../tutorials/api/collect/crm.md)

## 使用UI將[!DNL Microsoft Dynamics]連線至[!DNL Platform]

- [在UI中建立Microsoft Dynamics源連接](../../tutorials/ui/create/crm/dynamics.md)
- [在UI中為CRM連線建立資料流](../../tutorials/ui/dataflow/crm.md)
