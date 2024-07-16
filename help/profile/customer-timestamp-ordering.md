---
title: 客戶時間戳記排序
description: 瞭解如何將客戶時間戳記訂購新增至資料集，以確保設定檔資料的一致性。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 客戶時間戳記排序

在Adobe Experience Platform中，透過串流擷取來擷取資料至設定檔存放區時，預設不保證資料順序。 訂購客戶時間戳記時，您可以保證最新訊息（根據提供的客戶時間戳記）會保留在設定檔存放區中。 所有過時的訊息都會被捨棄，且&#x200B;**無法**&#x200B;用於使用設定檔資料（例如細分和目的地）的下游服務。 因此，這樣可讓您的設定檔資料保持一致，並使您的設定檔資料與來源系統保持同步。

若要啟用客戶時間戳記排序，請使用[外部Source系統稽核屬性欄位群組](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md)中的`extSourceSystemAudit.lastUpdatedDate`欄位，並連絡您的Adobe技術客戶經理，或向Adobe客戶服務人員提供您的沙箱和資料集資訊。

## 限制

在此私人測試版中，使用客戶時間戳記訂購時會套用下列限制：

- 您只能在設定檔存放區上透過&#x200B;**串流擷取**&#x200B;擷取的&#x200B;**設定檔屬性**&#x200B;使用客戶時間戳記排序。
   - 資料湖或身分服務中的資料有&#x200B;**no**&#x200B;個訂購保證。
- 您只能在&#x200B;**非生產**&#x200B;沙箱上使用客戶時間戳記排序。
- 您只能對每個沙箱的&#x200B;**5**&#x200B;資料集套用客戶時間戳記排序。
- 您&#x200B;**無法**&#x200B;在已啟用客戶時間戳記排序的資料集中，使用串流更新插入來傳送部分資料列更新。
- `extSourceSystemAudit.lastUpdatedDate`欄位&#x200B;**必須**&#x200B;為[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)格式。 使用ISO 8601格式時，它&#x200B;**必須**&#x200B;為格式`yyyy-MM-ddTHH:mm:ss.sssZ`的完整日期時間（例如`2028-11-13T15:06:49.001Z`）。
- 所有擷取的資料列&#x200B;**必須**&#x200B;包含`extSourceSystemAudit.lastUpdatedDate`欄位做為最上層欄位群組。 這表示此欄位&#x200B;**不得**&#x200B;巢狀內嵌於XDM結構描述中。 如果此欄位遺失或格式不正確，將不會擷取格式錯誤的記錄&#x200B;****，而且將會傳送對應的錯誤訊息。
- 任何啟用客戶時間戳記排序&#x200B;**的資料集都必須**&#x200B;是沒有任何先前擷取資料的新資料集。
- 對於任何給定的設定檔片段，只會擷取包含較新`extSourceSystemAudit.lastUpdatedDate`的列。 包含較舊或相同年齡之`extSourceSystemAudit.lastUpdatedDate`的資料列將被捨棄。

## 建議

在實作客戶時間戳記訂購時，請記得下列考量事項：

- 您負責同步所有將資料傳送至設定檔存放區的內部系統時鐘。
- 您的ISO 8061格式時間戳記應該有毫秒等級的精確度。
