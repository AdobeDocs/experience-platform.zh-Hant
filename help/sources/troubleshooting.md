---
keywords: Experience Platform；首頁；熱門主題；源；接收；故障排除；源；常見問題；源；源；連接器；源；源；連接器；faq；源；源；faq;source connectors;source connectors faqs;source connectors troubleshooting;
solution: Experience Platform
title: 源疑難解答
topic-legacy: troubleshooting
description: 本檔案回答了有關Adobe Experience Platform消息來源的常見問題。
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
source-git-commit: b55097b6e7cd49166f68d0c86b788cd36ebdebab
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# 源疑難解答指南

本檔案回答了有關Adobe Experience Platform消息來源的常見問題。 有關與其他相關的問題和故障排除 [!DNL Platform] 服務，包括在所有 [!DNL Platform] API，請參閱 [Experience Platform故障排除指南](../landing/troubleshooting.md)。

## 常見問答

以下是有關來源的常見問題解答的清單。

### 是否必須更改網路安全設定才能啟用源？

您可能需要允許列出某些IP地址才能啟用源。 有關詳細資訊，請閱讀特定源連接器上的文檔。

### 源支援哪些身份驗證類型？

可以使用連接字串、用戶名和密碼或訪問令牌和密鑰對源進行身份驗證。 有關支援的身份驗證類型的特定詳細資訊，可在指定源連接器的文檔中找到。

### 為什麼我最近的流量都會失敗？

如果您注意到您最近的所有流運行都失敗，則您的憑據可能已更改或過期。 要解決此問題，請嘗試使用最新憑據更新連接。

### 支援哪些檔案類型？

當前支援的檔案類型是分隔的檔案、JSON和Parmet。

### 對檔案名和大小的限制是什麼？

以下是源中檔案必須考慮的約束條件清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以正斜槓結尾(`/`)。 如果提供，將自動刪除。
- 必須正確轉義以下保留URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用以下字元： `" \ / : | < > * ?`。
- 不允許使用非法的URL路徑字元。 代碼點類似 `\uE000`，但在NTFS檔案名中有效，則不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，如控制字元（0x00到0x1F、\u0081等）。 有關HTTP/1.1中Unicode字串的規則，請參見 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許使用下列檔案名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM9、COM9prn、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。
- 每批檔案的最大數量為1500，最大批大小為100 GB。
- 每行的最大屬性或欄位數為10,000。
- 每個用戶每分鐘可發送的最大批次數為138。

### 支援哪些資料類型？

支援的資料類型包括整數、字串、布爾值、日期時間對象、陣列和對象。

### 支援哪些日期和時間格式？

源在接收資料時支援多種日期時間格式。 有關支援的日期時間格式的詳細資訊，請在 [資料格式處理指南](../data-prep/data-handling.md#dates) 在資料準備文檔中。

### 如何在CSV、JSON和Parket檔案中設定陣列格式？

JSON和Parket檔案本機支援陣列。 對於平面結構（如CSV），不支援陣列。 但是，可以使用資料準備函式（如分解和聯接）將具有多個值的字串分解為陣列。 有關這些資料準備功能的詳細資訊，請參閱 [資料準備功能指南](../data-prep/functions.md#string)

### 哪些來源支援部分攝取？

所有批量攝取源都支援部分攝取。 但是，流攝取源不支援部分攝取。

### 我何時應該使用部分攝取？

如果使用，應使用部分攝取 **不** 有約束，例如將整個檔案放入平台。 或者，如果您不介意接收可能包含錯誤的資料，則應使用部分攝取。

### 典型的部分攝取錯誤閾值是什麼？

部分攝取沒有「典型錯誤閾值」。 相反，此值可能因用例而異。 預設情況下，錯誤閾值設定為5%。

### 在建立新資料流後更新流運行狀態需要多長時間？

流程運行不會在瞬間產生，在指定後可能需要大約兩到三分鐘才能更新 `startTime`。 在建立新資料流後立即檢查流運行的狀態不會返回有關流運行的資訊 `lastRunDetails` 因為還沒發生。 建議在檢查流運行的狀態之前，允許在幾分鐘內生成資料流。