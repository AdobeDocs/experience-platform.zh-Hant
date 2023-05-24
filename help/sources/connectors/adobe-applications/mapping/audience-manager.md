---
keywords: Experience Platform；首頁；熱門主題；Audience Manager映射；受眾管理器映射
solution: Experience Platform
title: Adobe Audience Manager源連接器的映射欄位
description: 瞭解如何將Adobe Audience Manager資料（即時、掛接和配置檔案資料）映射到Audience Manager源連接器的相應體驗資料模型(XDM)欄位。
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Audience Manager欄位映射

下表包含Adobe Audience Manager資料（Realtime、Ontochd和Profile資料）中的欄位與其相應XDM欄位之間的映射。

請參閱 [XDM欄位字典](../../../../xdm/schema/field-dictionary.md) 的子菜單。

## 即時資料

類型：即時資料

| 即時資料欄位 | XDM欄位 |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *僅用於endUserId中存在的命名空間，並且僅用於第一個值。* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserId - *僅用於endUserId中存在的命名空間，並且僅用於第一個值。* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType →類型</li><li>製造商→製造商</li><li>marketingName →型號</li><li>modelNumber →模型</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country →國家/地區代碼</li><li>d_state →省</li><li>d_city →城市</li><li>d_postal →郵遞區號</li><li>d_lat →緯度</li><li>d_經度→經度</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → os名稱 </li><li>d_os_version → os_version</li></ul> |

{style="table-layout:auto"}

## 配置檔案資料

類型：配置檔案XDM

| 配置檔案欄位 | XDM欄位 |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style="table-layout:auto"}
