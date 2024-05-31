---
title: 客戶時間戳記排序
description: 瞭解如何將客戶時間戳記訂購新增至資料集，以確保設定檔資料的一致性。
badgePrivateBeta: label="私人測試版" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: dffbdafc3f063906c8c8fb648ace59b2f1aedab8
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# 客戶時間戳記排序

在Adobe Experience Platform中，透過串流擷取來擷取資料至設定檔存放區時，預設不保證資料順序。 訂購客戶時間戳記時，您可以保證最新訊息（根據提供的客戶時間戳記）會保留在設定檔存放區中。 所有過時的訊息都會被捨棄，並且 **非** 可用於使用設定檔資料（例如細分和目的地）的下游服務。 因此，這樣可讓您的設定檔資料保持一致，並使您的設定檔資料與來源系統保持同步。

若要啟用客戶時間戳記排序，請使用 `extSourceSystemAudit.lastUpdatedDate` 欄位(在 [外部來源系統稽核屬性欄位群組](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) 和聯絡您的Adobe技術客戶經理或Adobe客戶服務，瞭解您的沙箱和資料集資訊。

## 限制

在此私人測試版中，使用客戶時間戳記訂購時會套用下列限制：

- 您只能將客戶時間戳記訂購用於 **設定檔屬性** 內嵌方式 **串流擷取** 設定檔存放區中。
   - 有 **否** 為資料湖或Identity Service中的資料提供訂購保證。
- 您只能在以下位置使用客戶時間戳記排序： **非生產** 沙箱。
- 您只能將客戶時間戳記訂單套用至 **5** 每個沙箱的資料集。
- 您 **無法** 使用串流更新插入，在已啟用客戶時間戳記排序的資料集中傳送部分列更新。
- 此 `extSourceSystemAudit.lastUpdatedDate` 欄位 **必須** 位於 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 格式。 使用ISO 8601格式時， **必須** 採用格式的完整日期時間 `yyyy-MM-ddTHH:mm:ss.sssZ` (例如， `2028-11-13T15:06:49.001Z`)。
- 所有擷取的資料列 **必須** 包含 `extSourceSystemAudit.lastUpdatedDate` 欄位做為最上層欄位群組。 這表示此欄位 **必須** 並未巢狀內嵌於XDM結構描述中。 如果此欄位遺失或格式不正確，格式錯誤的記錄將 **非** 內嵌，並傳送相對應的錯誤訊息。
- 任何已啟用客戶時間戳記排序的資料集 **必須** 是不含任何先前已擷取資料的新資料集。
- 對於任何給定的設定檔片段，僅限包含較新的列 `extSourceSystemAudit.lastUpdatedDate` 將會內嵌。 包含 `extSourceSystemAudit.lastUpdatedDate` 將會捨棄已過期或年齡相同的專案。

## 推薦

在實作客戶時間戳記訂購時，請記得下列考量事項：

- 您負責同步所有將資料傳送至設定檔存放區的內部系統時鐘。
- 您的ISO 8061格式時間戳記應該有毫秒等級的精確度。
