---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；位址；xdm:address；資料類型；資料類型；
solution: Experience Platform
title: 郵遞區號資料類型
description: 本檔案概述「郵遞區號」XDM資料類型。
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# [!UICONTROL 郵遞區號] 資料類型

[!UICONTROL 郵遞區號] 是標準的XDM資料類型，可說明郵寄地址的詳細資訊。

<img src="../images/data-types/postal-address.png" width="450" /><br />

| 屬性 | 說明 |
| --- | --- |
| `city` | 城市的名字。 |
| `country` | 政府管理領土的名稱。 這是自由格式欄位，可以使用任何語言提供國家/地區名稱。 |
| `countryCode` | 兩個字元 <a href="https://datahub.io/core/country-list">ISO 3166-1alpha-2</a> 國家/地區的代碼。 |
| `createdByBatchID` | 建立地址記錄的所擷取批次檔案的ID。 |
| `dmaID` | Nielsen媒體研究指定的市場區域。 |
| `label` | 地址的自由格式名稱。 |
| `lastVerifiedDate` | 上次驗證地址仍與人員關聯的日期。 |
| `modifiedByBatchID` | 上次修改記錄的所擷取批次檔案的ID。 |
| `msaID` | 觀察發生地的美國大都市統計區。 |
| `postOfficeBox` | 地址的郵寄箱。 |
| `postalCode` | 位置的郵遞區號。 郵遞區號不適用於所有國家/地區。 在某些國家/地區，這只會包含部分郵遞區號。 |
| `primary` | 指示是否為個人主要地址的布林值。 設定檔只能有一個 `primary` 在指定時間點處理。 |
| `region` | 地址的地區、縣或地區。 |
| `repositoryCreatedBy` | 建立記錄的用戶ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶ID。 |
| `stateProvince` | 觀察的州或省部分。 格式會遵循 [ISO 3166-2（國家/地區和細分）](https://www.unece.org/cefact/locode/subdivisions.html) 標準。 |
| `status` | 指示當前是否可以使用該地址。 |
| `statusReason` | 目前的說明 `status`. |
| `street1` - `street4` | 這四個欄位的用途是包含主要街道級別資訊、公寓編號、街號和街道名稱。 `street2` to `street4` 為選填。 |

{style="table-layout:auto"}

如需郵遞區號資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
