---
keywords: Experience Platform；首頁；熱門主題；Audience Manager對應；audience manager對應
solution: Experience Platform
title: Adobe Audience Manager Source Connector的對應欄位
description: 了解如何將Adobe Audience Manager資料（即時、已上線和設定檔資料）對應至Audience Manager來源連接器的對應Experience Data Model(XDM)欄位。
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Audience Manager欄位對應

下表包含Adobe Audience Manager資料（即時、已上線和設定檔資料）中欄位與其對應XDM欄位之間的對應。

請參閱 [XDM欄位字典](../../../../xdm/schema/field-dictionary.md) 以取得每個XDM欄位的詳細資訊。

## 即時資料

類型：即時資料

| 即時資料欄位 | XDM欄位 |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *僅適用於endUserIds中存在的命名空間，且僅限第一個值。* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *僅適用於endUserIds中存在的命名空間，且僅限第一個值。* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType →類型</li><li>製造商→製造商</li><li>marketingName →模型</li><li>modelNumber →型號</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → state省</li><li>d_city →城市</li><li>d_postal →郵遞區號</li><li>d_lat →緯度</li><li>d_longitude →經度</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → os名稱 </li><li>d_os_version → os_version</li></ul> |

{style="table-layout:auto"}

## 設定檔資料

類型：設定檔XDM

| 設定檔欄位 | XDM欄位 |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style="table-layout:auto"}
