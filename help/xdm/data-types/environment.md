---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；環境；資料類型；資料類型；
solution: Experience Platform
title: 環境資料類型
description: 本文檔概述了環境XDM資料類型。
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 4%

---

# [!UICONTROL 環境] 資料類型

[!UICONTROL 環境] 是一種標準的XDM資料類型，它描述觀察到的事件的周圍環境，特別是詳細描述臨時資訊，如網路和軟體版本。

>[!IMPORTANT]
>
>所有值都應與 [設備地圖集](https://deviceatlas.com) 資料庫，按Adobe許可。

<img src="../images/data-types/environment.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_dc` | 物件 | 包含單個欄位的對象， `language`，它表示環境的語言，以表示用戶對資料表示的語言、地理或文化偏好。 語言在語言代碼中指定，如中所定義 [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt)。 |
| `browserDetails` | [瀏覽器詳細資訊](./browser-details.md) | 描述特定於瀏覽器的環境詳細資訊，如瀏覽器名稱、版本、JavaScript版本、用戶代理字串和接受語言。 |
| `ISP` | 字串 | 用戶的Internet服務提供商的名稱。 |
| `carrier` | 字串 | 向用戶銷售和提供通信服務的移動網路運營商或MNO（也稱為無線服務提供商、無線運營商、蜂窩公司或移動網路運營商）的名稱。 |
| `colorDepth` | 整數 | 用於單個像素的每個顏色分量的位數。 |
| `connectionType` | 字串 | Internet連接類型。 接受的值包括： <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | 字串 | 用戶ISP的域。 |
| `ipV4` | 字串 | 分配給使用網際網路協定進行通信（32位）的電腦網路中的設備的數字標籤。 |
| `ipV6` | 字串 | 分配給使用網際網路協定進行通信（128位）的參與電腦網路的設備的數字標籤。 |
| `operatingSystem` | 字串 | 進行觀察時使用的作業系統的名稱。 屬性不應包含任何版本資訊，如 `10.5.3`，但包含「edition」（版本）指定 `Ultimate` 或 `Professional`。 |
| `operatingSystemVendor` | 字串 | 進行觀察時使用的作業系統供應商的名稱。 |
| `operatingSystemVersion` | 字串 | 進行觀察時使用的作業系統的完整版本標識符。 版本通常以數字形式組成，但可以採用供應商定義的格式。 |
| `type` | 字串 | 應用程式環境的類型。 查看 [附錄](#type) 為接受的值。 |
| `viewportHeight` | 整數 | 內部顯示體驗窗口的垂直大小（像素）。 對於Web視圖事件，這是瀏覽器視區高度。 |
| `viewPortWidth` | 整數 | 顯示內部體驗的窗口的水準大小（以像素為單位）。 對於Web視圖事件，這是瀏覽器視區寬度。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## 附錄

以下部分包含有關 [!UICONTROL 設備] 資料類型。

## 類型的接受值 {#type}

下表概述了 `type` 及其相關含義：

| 值 | 說明 |
| --- | --- |
| `browser` | 瀏覽器 |
| `application` | 應用程式 |
| `iot` | 物聯網 |
| `external` | 外部系統 |
| `widget` | 應用程式擴展 |
