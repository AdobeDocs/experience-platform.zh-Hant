---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；地址；xdm:address;datatype；資料類型；
solution: Experience Platform
title: 郵政地址資料類型
description: 此文檔提供郵政地址XDM資料類型的概述。
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# [!UICONTROL 郵政地址] 資料類型

[!UICONTROL 郵政地址] 是描述郵件地址詳細資訊的標準XDM資料類型。

<img src="../images/data-types/postal-address.png" width="450" /><br />

| 屬性 | 說明 |
| --- | --- |
| `city` | 城市名稱。 |
| `country` | 政府管理領土的名稱。 這是一個自由格式欄位，可以使用任何語言命名國家/地區名稱。 |
| `countryCode` | 兩個字元 <a href="https://datahub.io/core/country-list">ISO 3166-1α-2</a> 國家代碼。 |
| `createdByBatchID` | 建立地址記錄的接收的批處理檔案的ID。 |
| `dmaID` | 尼爾森媒體研究指定了市場區域。 |
| `label` | 地址的自由格式名稱。 |
| `lastVerifiedDate` | 上次驗證地址為仍與人員關聯的日期。 |
| `modifiedByBatchID` | 上次修改記錄的所攝取的批處理檔案的ID。 |
| `msaID` | 觀察發生地的美國的都市統計區。 |
| `postOfficeBox` | 地址的郵局信箱。 |
| `postalCode` | 地點的郵遞區號。 並非所有國家都有郵遞區號。 在一些國家，這隻包含部分郵遞區號。 |
| `primary` | 一個布爾值，它指示這是否是個人的主地址。 配置檔案只能有一個 `primary` 地址。 |
| `region` | 地址的區、縣或區部分。 |
| `repositoryCreatedBy` | 建立記錄的用戶的ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶的ID。 |
| `stateProvince` | 觀察的省或州部分。 格式跟在 [ISO 3166-2（國家和地區）](https://www.unece.org/cefact/locode/subdivisions.html) 標準。 |
| `status` | 指示當前是否可以使用該地址。 |
| `statusReason` | 當前的說明 `status`。 |
| `street1` - `street4` | 這四個欄位應包含主要街道級別資訊、公寓編號、街道編號和街道名稱。 `street2` 至 `street4` 為可選項。 |

{style="table-layout:auto"}

有關郵政地址資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
