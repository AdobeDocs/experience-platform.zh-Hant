---
title: 重複資料型別
description: 瞭解重複體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 9d40bc1d-33d1-4c33-a143-13fdcf8dc255
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 6%

---

# [!UICONTROL 重複]資料型別

[!UICONTROL Repeat]是標準的Experience Data Model (XDM)資料型別，提供一組描述事件排程時間的規則。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![重複資料型別結構](../../../images/healthcare/data-types/reference.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 繫結期間] | `boundsPeriod` | [[!UICONTROL 週期]](../data-types/period.md) | 開始和結束時間。 |
| [!UICONTROL 繫結範圍] | `boundsRange` | [[!UICONTROL Range]](../data-types/range.md) | 範圍限制。 |
| [!UICONTROL 繫結期間] | `boundsDuration` | [[!UICONTROL 持續時間]](../data-types/duration.md) | 持續時間限制。 |
| [!UICONTROL 計數] | `count` | 整數 | 重複次數，最小值為`0`。 |
| [!UICONTROL 最大計數] | `countMax` | 整數 | 重複次數上限，最小值為`0`。 |
| [!UICONTROL 星期] | `dayOfWeek` | 字串陣列 | 字串陣列，詳細說明可用天數。 此屬性的值必須等於下列一或多個已知列舉值。 <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |
| [!UICONTROL 持續時間] | `duration` | 雙精度 | 時間長度。 |
| [!UICONTROL 最大持續時間] | `durationMax` | 雙精度 | 時間長度上限。 |
| [!UICONTROL 期間單位] | `durationUnit` | 字串 | 期間單位。 此屬性的值必須等於下列一或多個已知列舉值。 <li> `s` （秒） </li> <li> `min` （分鐘） </li> <li> `h` （每小時） </li> <li> `d` （每日） </li>  <li> `wk` （每週） </li> <li> `mo` （每月） </li> <li> `a` （每年）</li> |
| [!UICONTROL 頻率] | `frequency` | 雙精度 | 一段期間內應發生的重複次數，最小值為`0`。 |
| [!UICONTROL 最大頻率] | `frequencyMax` | 雙精度 | 以句點發生的重複次數上限，最小值為`0`。 |
| [!UICONTROL 位移] | `offset` | 整數 | 到事件之前或之後的分鐘數。 |
| [!UICONTROL 週期] | `period` | 雙精度 | 套用頻率的持續時間。 |
| [!UICONTROL 最大期間] | `periodMax` | 雙精度 | 期間的上限。 |
| [!UICONTROL 週期單位] | `periodUnit` | 字串 | 時間單位。 此屬性的值必須等於下列一或多個已知列舉值。 <li> `s` （秒） </li> <li> `min` （分鐘） </li> <li> `h` （每小時） </li> <li> `d` （每日） </li>  <li> `wk` （每週） </li> <li> `mo` （每月） </li> <li> `a` （每年）</li> |
| [!UICONTROL 每日時間] | `timeOfDay` | 字串陣列 | 動作在一天中發生的時間。 |
| [!UICONTROL When] | `when` | 字串陣列 | 動作時段的程式碼。 |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.schema.json)
