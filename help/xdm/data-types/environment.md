---
keywords: Experience Platform;home；常用主題；模式；模式；XDM;fields；模式；環境；資料類型；資料類型；
solution: Experience Platform
title: 環境資料類型
topic-legacy: overview
description: 本文檔概述了環境XDM資料類型。
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 4%

---

# [!UICONTROL Environment] 資料類型

[!UICONTROL Environment] 是標準的XDM資料類型，它描述了所觀察事件的周圍環境，具體詳述了諸如網路和軟體版本的過渡資訊。

>[!IMPORTANT]
>
>所有值都應與[DeviceAtlas](https://deviceatlas.com)資料庫對齊，並由Adobe授權。

<img src="../images/data-types/environment.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_dc` | 物件 | 包含單一欄位`language`的對象，該欄位指示環境的語言，以表示用戶對資料表示的語言、地理或文化偏好。 語言在[IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt)中定義的語言代碼中指定。 |
| `browserDetails` | [瀏覽器詳細資訊](./browser-details.md) | 說明環境的瀏覽器特定詳細資訊，例如瀏覽器名稱、版本、JavaScript版本、使用者代理字串和接受語言。 |
| `ISP` | 字串 | 用戶的Internet服務提供商的名稱。 |
| `carrier` | 字串 | 向用戶銷售和提供通信服務的移動網路運營商或MNO（也稱為無線服務提供商、無線運營商、蜂窩公司或移動網路運營商）的名稱。 |
| `colorDepth` | 整數 | 用於單個像素的每個顏色元件的位數。 |
| `connectionType` | 字串 | 網際網路連線類型。 接受的值包括： <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | 字串 | 用戶ISP的域。 |
| `ipV4` | 字串 | 分配給參與使用網際網路協定進行通信的電腦網路（32位）的設備的數值標籤。 |
| `ipV6` | 字串 | 分配給參與使用網際網路協定進行通信的電腦網路（128位）的設備的數字標籤。 |
| `operatingSystem` | 字串 | 進行觀察時使用的作業系統的名稱。 屬性不應包含任何版本資訊（例如`10.5.3`），但應包含「edition」（版本）名稱，例如`Ultimate`或`Professional`。 |
| `operatingSystemVendor` | 字串 | 進行觀察時使用的作業系統供應商的名稱。 |
| `operatingSystemVersion` | 字串 | 進行觀察時所用作業系統的完整版本識別碼。 版本通常以數字形式組成，但可能採用供應商定義的格式。 |
| `type` | 字串 | 應用程式環境的類型。 有關接受的值，請參見[附錄](#type)。 |
| `viewportHeight` | 整數 | 體驗顯示於其中之視窗的垂直大小（像素）。 對於Web檢視事件，此為瀏覽器檢視區高度。 |
| `viewPortWidth` | 整數 | 體驗顯示於其中之視窗的水準大小（像素）。 對於Web檢視事件，此為瀏覽器檢視埠寬度。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## 附錄

以下部分包含有關[!UICONTROL Device]資料類型的其他資訊。

## 類型{#type}的接受值

下表概述`type`的接受值及其相關含義：

| 值 | 說明 |
| --- | --- |
| `browser` | 瀏覽器 |
| `application` | 應用程式 |
| `iot` | 物聯網 |
| `external` | 外部系統 |
| `widget` | 應用程式擴充功能 |
