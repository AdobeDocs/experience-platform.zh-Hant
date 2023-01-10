---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；環境；資料類型；資料類型；
solution: Experience Platform
title: 環境資料類型
description: 本檔案概述環境XDM資料類型。
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 5%

---

# [!UICONTROL 環境] 資料類型

[!UICONTROL 環境] 是標準的XDM資料類型，可描述觀察到的事件的周圍環境，具體詳細說明網路和軟體版本等暫存資訊。

>[!IMPORTANT]
>
>所有值都應與 [DeviceAtlas](https://deviceatlas.com) 資料庫，由Adobe授權。

<img src="../images/data-types/environment.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_dc` | 物件 | 包含單一欄位的物件， `language`，指出環境的語言，以代表使用者的語言、地理或文化偏好，以呈現資料。 語言是在語言代碼中指定，如 [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [瀏覽器詳細資訊](./browser-details.md) | 說明環境的瀏覽器專屬詳細資訊，例如瀏覽器名稱、版本、JavaScript版本、使用者代理字串，以及接受語言。 |
| `ISP` | 字串 | 用戶的Internet服務提供商的名稱。 |
| `carrier` | 字串 | 向用戶銷售和提供通信服務的移動網路運營商或MNO（也稱為無線服務提供商、無線運營商、蜂窩公司或移動網路運營商）的名稱。 |
| `colorDepth` | 整數 | 用於單個像素的每個顏色分量的位數。 |
| `connectionType` | 字串 | Internet連接類型。 接受的值包括： <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | 字串 | 使用者ISP的網域。 |
| `ipV4` | 字串 | 分配給參與使用網際網路協定進行通信（32位）的電腦網路的設備的數字標籤。 |
| `ipV6` | 字串 | 分配給參與使用網際網路協定進行通信（128位）的電腦網路的設備的數字標籤。 |
| `operatingSystem` | 字串 | 進行觀察時使用的作業系統名稱。 屬性不應包含任何版本資訊，例如 `10.5.3`，但改為包含「版本」指定，例如 `Ultimate` 或 `Professional`. |
| `operatingSystemVendor` | 字串 | 進行觀察時使用的作業系統供應商的名稱。 |
| `operatingSystemVersion` | 字串 | 進行觀察時使用的作業系統的完整版本標識符。 版本通常以數值組成，但可能採用供應商定義的格式。 |
| `type` | 字串 | 應用程式環境的類型。 請參閱 [附錄](#type) ，以了解接受的值。 |
| `viewportHeight` | 整數 | 體驗內顯示的視窗的垂直大小（像素）。 對於Web檢視事件，這是瀏覽器檢視區高度。 |
| `viewPortWidth` | 整數 | 體驗內顯示的視窗水準大小（像素）。 對於Web檢視事件，這是瀏覽器檢視區寬度。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## 附錄

下節包含 [!UICONTROL 裝置] 資料類型。

## 類型的接受值 {#type}

下表概述 `type` 及其相關含義：

| 值 | 說明 |
| --- | --- |
| `browser` | 瀏覽器 |
| `application` | 應用程式 |
| `iot` | 物聯網 |
| `external` | 外部系統 |
| `widget` | 應用程式擴充功能 |
