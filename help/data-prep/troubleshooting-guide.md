---
keywords: Experience Platform；首頁；熱門主題；
title: 資料準備疑難排解指南
description: 本檔案提供Adobe Experience Platform資料準備常見問題的解答。
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# [!DNL Data Prep] 疑難排解指南

本檔案提供關於Adobe Experience Platform常見問題的解答 [!DNL Data Prep]，以及常見錯誤的疑難排解指南。 如需Platform API的一般問題和疑難排解資訊，請參閱 [Adobe Experience Platform API疑難排解指南](../landing/troubleshooting.md).

## 常見問題集

以下是關於 [!DNL Data Prep] 以及他們的答案。

### 如何解決轉換錯誤？

[!DNL Data Prep] 將所有轉換錯誤本地化到發生這些錯誤的列。 因此，該欄會無效，而行的其餘部分將會繼續處理。 這些轉換問題記錄為 **警告**. 建議您定期檢閱警告，並調整轉換邏輯以考慮轉換問題。 這會提高擷取至Experience Platform的資料品質。

如果欄標示為 **必填** 因轉換問題而無效，則不會擷取列。 啟用部分資料擷取時，您可以在整個流程失敗前設定此類拒絕的臨界值。 如果無效屬性未影響任何架構層級驗證，則會繼續擷取該列。

即使沒有任何轉換錯誤，任何無效的列也將被拒絕。 例如，資料擷取流程可能具有到必要欄位的傳遞對應（無轉換邏輯），且該屬性沒有傳入值。 此行將被拒絕。

### 如何在欄位中逸出特殊字元？

您可以使用 `${...}`. 不過，包含帶句號(`.`)不受此機制支援。 與階層互動時，如果子屬性具有句點(`.`)，您必須使用反斜線(`\`)以逸出特殊字元。 例如， `address` 是包含屬性的物件 `street.name`，接著這可稱為 `address.street\.name` 而非 `address.street.name`.

### 計算欄位的最大長度是多少？

計算欄位的長度上限為4096個字元。