---
keywords: Experience Platform;home；熱門主題；Audience Manager映射；Audience Manager映射
solution: Experience Platform
title: Adobe Audience Manager Source Connector的對應欄位
topic: overview
description: 瞭解如何將Adobe Audience Manager資料（即時、已登入和描述檔資料）對應至Audience Manager來源連接器的對應Experience Data Model(XDM)欄位。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Audience Manager欄位對應

下表包含Adobe Audience Manager資料（即時、已登錄和描述檔資料）中欄位與其對應XDM欄位之間的對應。

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

## 描述檔資料

類型：概要檔案XDM

| 描述檔欄位 | XDM欄位 |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
