---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；連線；連線至查詢服務；SSL;sslmode;
title: 查詢服務SSL選項
description: 了解SSL支援協力廠商連線至Adobe Experience Platform Query Service，以及如何使用驗證完整的SSL模式連線。
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 1%

---

# [!DNL Query Service] SSL選項

為提高安全性，Adobe Experience Platform [!DNL Query Service] 為加密用戶端/伺服器通訊的SSL連線提供原生支援。 本檔案涵蓋協力廠商用戶端連線可用的SSL選項 [!DNL Query Service] 以及如何使用 `verify-full` SSL參數值。

## 先決條件

本檔案假設您已下載第三方案頭用戶端應用程式，以便與您的平台資料搭配使用。 如需與協力廠商用戶端連線時如何整合SSL安全性的具體指示，請參閱其個別連線指南檔案。 要獲取所有 [!DNL Query Service] 支援的用戶端，請參閱 [客戶端連接概述](./overview.md).

## 可用SSL選項 {#available-ssl-options}

Platform支援各種SSL選項，以符合您的資料安全需求，並平衡加密和金鑰交換的處理開銷。

不同 `sslmode` 參數值提供不同級別的保護。 通過使用SSL證書對移動資料進行加密，有助於防止「中間人」(MITM)攻擊、竊聽和模擬。 下表提供了可用的不同SSL模式及其提供的保護級別的劃分。

>[!NOTE]
>
> SSL值 `disable` 由於符合必要的資料保護規範，Adobe Experience Platform不支援。

| sslmode | 竊聽保護 | MITM保護 | 說明 |
|---|---|---|---|
| `allow` | 部分 | 無 | 安全性不是優先順序，速度和低處理開銷更重要。 此模式僅在伺服器堅持加密時選擇加密。 |
| `prefer` | 部分 | 無 | 加密不是必需的，但如果伺服器支援，通信將被加密。 |
| `require` | 是 | 無 | 所有通信都需要加密。 信任網路連接到正確的伺服器。 不需要伺服器SSL憑證驗證。 |
| `verify-ca` | 是 | 取決於CA政策 | 所有通信都需要加密。 共用資料之前需要進行伺服器驗證。 這需要您在 [!DNL PostgreSQL] 首頁目錄。 [詳情如下](#instructions) |
| `verify-full` | 是 | 是 | 所有通信都需要加密。 共用資料之前需要進行伺服器驗證。 這需要您在 [!DNL PostgreSQL] 首頁目錄。 [詳情如下](#instructions). |

>[!NOTE]
>
>兩者的差異 `verify-ca` 和 `verify-full` 取決於根證書頒發機構(CA)的策略。 如果您已建立自己的本地CA，為您的應用程式頒發專用證書，請使用 `verify-ca` 通常提供足夠的保護。 如果使用公用CA, `verify-ca` 允許連接到其他人可能已向CA註冊的伺服器。 `verify-full` 應一律搭配公用根CA使用。

建立與Platform資料庫的協力廠商連線時，建議您使用 `sslmode=require` 至少要確保資料的安全連線。 此 `verify-full` 建議在大多數安全敏感型環境中使用SSL模式。

## 設定根證書以進行伺服器驗證 {#root-certificate}

為確保安全連線，必須先在用戶端和伺服器上設定SSL使用，才能進行連線。 如果SSL僅在伺服器上配置，則客戶端可能會在建立伺服器需要高度安全性之前發送敏感資訊（如密碼）。

依預設， [!DNL PostgreSQL] 不執行伺服器證書的任何驗證。 在傳送任何敏感資料之前（作為SSL的一部分），驗證伺服器的身分並確保安全連線 `verify-full` 模式)，您必須在本機電腦(`root.crt`)和由伺服器上的根憑證簽署的葉憑證。

若 `sslmode` 參數設為 `verify-full`, libpq會檢查儲存在用戶端上的根憑證上的憑證鏈，以確認伺服器是否可信。 然後，它會驗證主機名稱是否與伺服器憑證中儲存的名稱相符。

若要允許伺服器憑證驗證，您必須放置一或多個根憑證(`root.crt`) [!DNL PostgreSQL] 檔案。 檔案路徑類似於 `~/.postgresql/root.crt`.

## 啟用驗證完全的SSL模式，以便與第三方一起使用 [!DNL Query Service] 連接 {#instructions}

如果你比 `sslmode=require`，您可以依照醒目提示的步驟，將協力廠商用戶端連線至 [!DNL Query Service] 使用 `verify-full` SSL模式。

>[!NOTE]
>
>取得SSL憑證有許多選項。 由於無管理證書的趨勢日益增長，本指南中使用DigiCert，因為它們是高保證TLS/SSL、PKI、IoT和簽名解決方案的可信全局提供者。

1. 導覽至 [可用的DigiCert根證書清單](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. 搜索「[!DNL DigiCert Global Root CA]」（從可用證書清單中）。
1. 選擇 [!DNL **下載PEM**] 將檔案下載到本地電腦。
   ![已反白顯示「下載PEM」的可用DigiCert根憑證清單。](../images/clients/ssl-modes/digicert.png)
1. 將安全證書檔案更名為 `root.crt`.
1. 將檔案複製到 [!DNL PostgreSQL] 檔案夾。 必要的檔案路徑會因作業系統而異。 如果資料夾尚未存在，請建立資料夾。
   - 如果您使用macOS，路徑為 `/Users/<username>/.postgresql`
   - 如果您使用Windows，則路徑為 `%appdata%\postgresql`

>[!TIP]
>
>若要尋找 `%appdata%` 在Windows作業系統上的檔案位置，按⊞ **Win + R** 輸入 `%appdata%` 填入搜尋欄位。

在 [!DNL DigiCert Global Root CA] CRT檔案在 [!DNL PostgreSQL] 資料夾，您可以 [!DNL Query Service] 使用 `sslmode=verify-full` 或 `sslmode=verify-ca` 選項。

## 後續步驟

閱讀本檔案，您便能更清楚了解將協力廠商用戶端連線至 [!DNL Query Service]，以及如何啟用 `verify-full` SSL選項，可加密正在移動的資料。

如果您尚未這麼做，請遵循 [將第三方客戶端連接到 [!DNL Query Service]](./overview.md).
