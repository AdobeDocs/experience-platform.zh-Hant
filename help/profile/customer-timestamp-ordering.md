---
title: 客戶時間戳記排序
description: 瞭解如何將客戶時間戳記訂購新增至資料集，以確保設定檔資料的一致性。
badgePrivateBeta: label="私人測試版" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c5789b872be49c3bd4a1ca61a2d44392ebd4a746
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# 客戶時間戳記排序

在Adobe Experience Platform中，透過串流擷取擷取來擷取資料至設定檔存放區時，不會自動保證資料順序。 訂購客戶時間戳記時，您可以保證最新訊息（根據提供的客戶時間戳記）會保留在設定檔存放區中。 因此，這樣可讓您的設定檔資料保持一致，並使您的設定檔資料與來源系統保持同步。

若要啟用客戶時間戳記訂購，您需要使用 `lastUpdatedDate` 欄位(在 [外部來源系統稽核屬性資料型別](../xdm/data-types/external-source-system-audit-attributes.md) 和聯絡您的Adobe技術客戶經理或Adobe客戶服務，瞭解您的沙箱和資料集資訊。

## 限制

在此私人測試版中，使用客戶時間戳記訂購時會套用下列限制：

- 您只能將客戶時間戳記訂購用於 **設定檔屬性** 內嵌方式 **串流擷取**.
- 您只能在以下位置使用客戶時間戳記排序： **非生產** 沙箱。
- 您只能將客戶時間戳記訂單套用至 **5** 每個沙箱的資料集。
- 此 `lastUpdatedDate` 欄位必須在 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 格式。
- 所有擷取的資料列 **必須** 包含 `lastUpdatedDate` 欄位。 如果此欄位遺失或格式不正確，擷取將會失敗。
- 任何已啟用客戶時間戳記排序的資料集 **必須** 是不含任何先前已擷取資料的新資料集。
- 對於任何給定的設定檔片段，僅限包含較新的列 `lastUpdatedDate` 將會內嵌。 如果列不包含較新的專案 `lastUpdatedDate`，則會捨棄該列。

## 推薦

在實作客戶時間戳記訂購時，請記得下列考量事項：

- 您負責同步所有將資料傳送到設定檔存放區之內部系統的時鐘。
- 您的ISO 8061格式時間戳記應該有毫秒等級的精確度。
- 「資料準備」搭配客戶時間戳記排序的使用方式為 **強烈建議**，接著會建立所有擷取列的副本及其時間戳記，以便在發生問題時進行更好的偵錯。
