---
keywords: 目錄服務；問題；常見問題；faq；資料集常見問題
title: 常見問題
description: 關於Adobe Experience Platform目錄服務和資料集的最常見問題解答。
exl-id: 70d2a352-75bd-4bbc-98e6-aeea16306f63
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 常見問題 {#faq}

本檔案提供有關Adobe Experience Platform目錄服務和資料集的常見問題解答。 有關其他Experience Platform服務的問題和疑難排解，包括所有Experience Platform API遇到的問題，請參閱[Experience Platform疑難排解指南](../landing/troubleshooting.md)。

## 保留原則和規則 {#retention-policies-and-rules}

### 我可以套用保留原則規則到哪些型別的資料集？

+++回答

您可以在使用ExperienceEvent XDM類別建立的資料集上設定保留原則。 對於設定檔服務，保留原則只能在設定檔啟用ExperienceEvent資料集後套用至資料集。

+++

### 我可以為Data Lake和Profile Service設定不同的保留原則嗎？

+++回答

可以，您可以對Data Lake和Profile Service套用不同的保留政策。

+++

## 保留工作執行與時間 {#retention-job-execution-and-timing}

### 資料集保留工作多久會從Data Lake服務中刪除資料？

+++回答

系統會每週評估及處理資料集過期時間，刪除過期的所有記錄。 如果事件已擷取至Experience Platform超過30天（擷取日期> 30天），且其事件日期超過定義的保留期，則會視為已過期。

+++

### 資料集保留工作多久會從設定檔服務中刪除資料？

+++回答

設定保留原則後，如果現有事件的事件時間戳記超過保留期間，則會立即從Experience Platform中刪除現有事件。 一旦新事件的時間戳記超過保留期間，就會刪除這些事件。

例如，如果您在5月15日套用30天到期原則，便會發生下列情況：

- 新事件在擷取時會收到30天的有效期。
- 時間戳記早於4月15日的現有事件會立即刪除。
- 時間戳記在4月15日之後的現有事件，其時間戳記將在30天後到期。 例如，4月18日的事件將會在5月18日刪除。

+++

## 資料集使用情況和監視

### 如何檢查我目前的資料集使用情形？

+++回答

您可以在[!UICONTROL 資料集]詳細目錄頁面上，以個別量度的形式檢視資料湖和設定檔中最新的資料集層級儲存大小。 您也可以排序欄以識別最大的資料集，並確保套用保留原則。 「授權使用情況」儀表板中提供了沙箱層級的使用情況。 如需詳細資訊，請參閱[授權使用檔案](../dashboards/guides/license-usage.md)。

+++

### 如何驗證資料保留工作是否成功？

+++回答

您可以在[資料集保留組態UI](./datasets/user-guide.md#data-retention-policy)和[!UICONTROL 資料集]詳細目錄頁面中，檢查最後一個資料保留工作的時間戳記。 歷史資料集使用量報表目前無法使用，但已規劃於未來發行。

+++

## 資料復原 {#data-recovery}

### 我可以復原已刪除的資料嗎？

+++回答

否，一旦套用保留原則，任何超過保留期的資料都會永久刪除且無法復原。

+++
