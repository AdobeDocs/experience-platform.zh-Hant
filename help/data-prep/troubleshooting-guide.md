---
keywords: Experience Platform；首頁；熱門主題；
title: 資料準備疑難排解指南
description: 本檔案提供有關Adobe Experience Platform資料準備常見問題的解答。
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# [!DNL Data Prep]疑難排解指南

本檔案提供有關Adobe Experience Platform [!DNL Data Prep]常見問題的解答，以及常見錯誤的疑難排解指南。 如需Platform API的一般問題和疑難排解資訊，請參閱[Adobe Experience Platform API疑難排解指南](../landing/troubleshooting.md)。

## 常見問題集

以下為關於[!DNL Data Prep]常見問題集及其答案的清單。

### 如何解決轉換錯誤？

[!DNL Data Prep]將所有轉換錯誤當地語系化至其發生的資料行。 因此，該欄會失效，而列的其餘部分會繼續處理。 這些轉換問題記錄為&#x200B;**警告**。 建議您定期檢閱警告，並調整轉換邏輯，以解決轉換問題。 這會提高擷取至Experience Platform的資料品質。

如果標示為&#x200B;**必要**&#x200B;的欄因轉換問題而無效，則不會擷取該列。 啟用部分資料擷取時，您可以設定在整個流程失敗之前此類拒絕的臨界值。 如果取消的屬性並未影響任何結構描述層級的驗證，則會繼續內嵌列。

即使沒有任何轉換錯誤，任何無效列也會被拒絕。 例如，資料擷取流程可能會將傳遞對應（無轉換邏輯）對應到必填欄位，且該屬性沒有傳入值。 將拒絕此列。

### 如何在欄位中逸出特殊字元？

您可以使用`${...}`來逸出欄位中的特殊字元。 但是，此機制不支援包含具有句點(`.`)之欄位的JSON檔案。 與階層互動時，如果子屬性有句點(`.`)，您必須使用反斜線(`\`)來逸出特殊字元。 例如，`address`是包含屬性`street.name`的物件，然後可以將其稱為`address.street\.name`而非`address.street.name`。

### 計算欄位的最大長度是多少？

計算欄位的長度上限為4096個字元。