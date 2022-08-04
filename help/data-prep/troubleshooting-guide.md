---
keywords: Experience Platform；首頁；熱門主題；
title: 資料準備故障排除指南
topic-legacy: troubleshooting
description: 本文檔提供有關Adobe Experience Platform資料準備的常見問題解答。
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: 4bb21ce5861419964b80a827269e40ef3e6483f8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# [!DNL Data Prep] 故障排除指南

本文檔提供有關Adobe Experience Platform的常見問題解答 [!DNL Data Prep]以及常見錯誤的故障排除指南。 有關一般平台API的問題和故障排除資訊，請參見 [Adobe Experience PlatformAPI故障排除指南](../landing/troubleshooting.md)。

## 常見問題集

以下是有關 [!DNL Data Prep] 和答案。

### 如何解決轉換錯誤？

[!DNL Data Prep] 將所有轉換錯誤鎖定到其發生的列。 因此，該列無效，行的其餘部分將繼續處理。 這些轉換問題記錄為 **警告**。 建議您定期檢查警告並調整轉換邏輯以解決轉換問題。 這將提高接收到的資料的質量。

如果標籤為 **必需** 將因轉換問題而失效，則不會攝取行。 啟用部分資料接收後，您可以在整個流失敗之前設定此類拒絕的閾值。 如果無效屬性未影響任何架構級別驗證，將繼續接收該行。

即使沒有任何轉換錯誤，也將拒絕任何無效行。 例如，資料接收流可能具有到必需欄位的傳遞映射（無轉換邏輯），並且該屬性沒有傳入值。 此行將被拒絕。

### 如何逃避場上的特殊人物？

可以使用 `${...}`。 但是，包含帶句點的欄位(`.`)不受此機制支援。 在與層次結構交互時，如果子屬性具有句點(`.`)，必須使用反斜線(`\`)以轉義特殊字元。 比如說， `address` 是包含屬性的對象 `street.name`，這可以稱為 `address.street\.name` 而不是 `address.street.name`。
