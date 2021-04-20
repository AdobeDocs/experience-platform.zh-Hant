---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Microsoft Dynamics Source Connector概觀
topic: overview
description: 瞭解如何使用API或使用者介面將Microsoft Dynamics連線至Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---


# Microsoft Dynamics 連接器

Adobe Experience Platform允許從外部來源接收資料，同時提供使用[!DNL Platform]服務構建、標籤和增強傳入資料的能力。 您可以從多種來源收錄資料，例如Adobe應用程式、雲端儲存空間、資料庫等。

[!DNL Experience Platform] 支援從協力廠商CRM系統擷取資料。支援CRM提供者包括[!DNL Microsoft Dynamics]。

## IP位址允許清單

在使用來源連接器之前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

>[!IMPORTANT]
>
>[!DNL Microsoft Dynamics]源連接器當前不支援與平台的相同區域連接。 這表示如果您的Azure例項使用與平台相同的網路區域，則無法建立與平台來源的連線。 目前僅支援跨地區連線。 如需詳細資訊，請洽詢您的Adobe客戶經理。

下面的文檔提供了如何使用API或用戶介面將[!DNL Microsoft Dynamics]連接到[!DNL Platform]的資訊：

## 使用API將[!DNL Microsoft Dynamics]連接至[!DNL Platform]

- [使用Flow Service API建立Microsoft Dynamics來源連線](../../tutorials/api/create/crm/ms-dynamics.md)
- [使用Flow Service API探索CRM系統](../../tutorials/api/explore/crm.md)
- [使用Flow Service API收集CRM資料](../../tutorials/api/collect/crm.md)

## 使用UI將[!DNL Microsoft Dynamics]連接至[!DNL Platform]

- [在UI中建立Microsoft Dynamics來源連線](../../tutorials/ui/create/crm/dynamics.md)
- [在UI中為CRM連接配置資料流](../../tutorials/ui/dataflow/crm.md)