---
keywords: Experience Platform；首頁；熱門主題；Audience Manager映射；觀眾管理器映射
solution: Experience Platform
title: Adobe Audience Manager源連接器的映射欄位
topic-legacy: overview
description: 瞭解如何將Adobe Audience Manager資料（即時、已登錄和配置檔案資料）映射到Audience Manager源連接器的相應體驗資料模型(XDM)欄位。
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
translation-type: tm+mt
source-git-commit: af5564a07577a0123e1a45043d5479f6ad45d73e
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# Audience Manager欄位映射

下表包含Adobe Audience Manager資料（即時、已登錄和配置檔案資料）中各欄位與其對應的XDM欄位之間的映射。

有關每個XDM欄位的詳細資訊，請參閱[XDM欄位字典](../../../../xdm/schema/field-dictionary.md)。

## 即時資料

類型：即時資料

| 即時資料欄位 | XDM欄位 |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` -僅 *限endUserIds中存在的名稱空間，且僅限第一個值。* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *僅適用於endUserIds中存在的名稱空間，且僅適用於第一個值。* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType → type</li><li>製造商→製造商</li><li>marketingName → model</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country→countryCode</li><li>d_state→stateProvince</li><li>d_city→城市</li><li>d_postal → postalCode</li><li>d_lat → latitude</li><li>d_lognitude →經度</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent→ userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → os名稱 </li><li>d_os_version → os_version</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 描述檔資料

類型：概要檔案XDM

| 描述檔欄位 | XDM欄位 |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style=&quot;table-layout:auto&quot;}
