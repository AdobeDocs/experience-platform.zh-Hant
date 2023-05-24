---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；連接；連接到查詢服務；SSL;sslmode;
title: 查詢服務SSL選項
description: 瞭解對與Adobe Experience Platform查詢服務的第三方連接的SSL支援，以及如何使用驗證完全SSL模式進行連接。
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 1%

---

# [!DNL Query Service] SSL選項

為了加強安全，Adobe Experience Platform [!DNL Query Service] 為加密客戶端/伺服器通信提供本機SSL連接支援。 本文檔介紹第三方客戶端連接到的可用SSL選項 [!DNL Query Service] 以及如何使用 `verify-full` SSL參數值。

## 先決條件

本文檔假定您已經下載了第三方案頭客戶端應用程式以用於您的平台資料。 有關在與第三方客戶端連接時如何結合SSL安全性的具體說明，請參見其各自的連接指南文檔。 用於所有清單 [!DNL Query Service] 支援的客戶端，請參見 [客戶端連接概述](./overview.md)。

## 可用SSL選項 {#available-ssl-options}

平台支援各種SSL選項，以滿足您的資料安全需求，並平衡加密和密鑰交換的處理開銷。

不同 `sslmode` 參數值提供不同級別的保護。 通過使用SSL證書對移動資料進行加密，它有助於防止「中間人」(MITM)攻擊、竊聽和模擬。 下表提供了可用的不同SSL模式及其提供的保護級別的細目。

>[!NOTE]
>
> SSL值 `disable` 由於必需的資料保護符合性，Adobe Experience Platform不支援。

| sslmode | 竊聽保護 | MITM保護 | 說明 |
|---|---|---|---|
| `allow` | 部分 | 無 | 安全性不是優先事項，速度和低處理開銷更為重要。 此模式僅在伺服器堅持加密時才會選擇加密。 |
| `prefer` | 部分 | 無 | 不需要加密，但如果伺服器支援，通信將被加密。 |
| `require` | 是 | 無 | 所有通信都需要加密。 信任網路可以連接到正確的伺服器。 不需要伺服器SSL證書驗證。 |
| `verify-ca` | 是 | 取決於CA策略 | 所有通信都需要加密。 共用資料之前需要伺服器驗證。 這要求您在 [!DNL PostgreSQL] 主目錄。 [詳情如下](#instructions) |
| `verify-full` | 是 | 是 | 所有通信都需要加密。 共用資料之前需要伺服器驗證。 這要求您在 [!DNL PostgreSQL] 主目錄。 [詳情如下](#instructions)。 |

>[!NOTE]
>
>兩者之差 `verify-ca` 和 `verify-full` 取決於根證書頒發機構(CA)的策略。 如果您已建立自己的本地CA來為您的應用程式頒發專用證書，請使用 `verify-ca` 通常提供足夠的保護。 如果使用公共CA, `verify-ca` 允許連接到其他人可能已向CA註冊的伺服器。 `verify-full` 應始終與公共根CA一起使用。

在與平台資料庫建立第三方連接時，建議您使用 `sslmode=require` 至少要確保移動資料的安全連接。 的 `verify-full` 建議在大多數安全敏感環境中使用SSL模式。

## 設定用於伺服器驗證的根證書 {#root-certificate}

為確保安全連接，必須在建立連接之前在客戶端和伺服器上配置SSL使用。 如果SSL僅在伺服器上配置，則客戶機可能會在確定伺服器需要高安全性之前發送密碼等敏感資訊。

預設情況下， [!DNL PostgreSQL] 不對伺服器證書執行任何驗證。 在發送任何敏感資料之前（作為SSL的一部分）驗證伺服器的身份並確保安全連接 `verify-full` 模式)，您必須在本地電腦(`root.crt`)和由伺服器上的根證書籤名的葉證書。

如果 `sslmode` 參數設定為 `verify-full`, libpq將通過檢查儲存在客戶端上的根證書上的證書鏈來驗證伺服器是否可信。 然後驗證主機名是否與儲存在伺服器證書中的名稱匹配。

要允許伺服器證書驗證，必須放置一個或多個根證書(`root.crt`) [!DNL PostgreSQL] 檔案。 檔案路徑類似於 `~/.postgresql/root.crt`。

## 啟用驗證完全SSL模式，以便與第三方一起使用 [!DNL Query Service] 連接 {#instructions}

如果你需要更嚴格的安全控制 `sslmode=require`，您可以按照突出顯示的步驟將第三方客戶端連接到 [!DNL Query Service] 使用 `verify-full` SSL模式。

>[!NOTE]
>
>有許多選項可用於獲取SSL證書。 由於無管理證書的趨勢日益增長，本指南中使用DigiCert，因為它們是高保證TLS/SSL、PKI、IoT和簽名解決方案的可信全球提供商。

1. 導航到 [可用DigiCert根證書清單](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. 搜索「」[!DNL DigiCert Global Root CA]」。
1. 選擇 [!DNL **下載PEM**] 將檔案下載到本地電腦。
   ![突出顯示了帶有下載PEM的可用DigiCert根證書的清單。](../images/clients/ssl-modes/digicert.png)
1. 將安全證書檔案更名為 `root.crt`。
1. 將檔案複製到 [!DNL PostgreSQL] 的子菜單。 必要的檔案路徑因作業系統而異。 如果資料夾不存在，請建立該資料夾。
   - 如果你用macOS，那麼 `/Users/<username>/.postgresql`
   - 如果使用Windows，路徑是 `%appdata%\postgresql`

>[!TIP]
>
>查找 `%appdata%` 檔案位置，按⊞ **Win + R** 輸入 `%appdata%` 的下界。

在 [!DNL DigiCert Global Root CA] CRT檔案在您的 [!DNL PostgreSQL] 資料夾，您可以 [!DNL Query Service] 使用 `sslmode=verify-full` 或 `sslmode=verify-ca` 的雙曲餘切值。

## 後續步驟

通過閱讀本文檔，您可以更好地瞭解將第三方客戶端連接到 [!DNL Query Service]，以及如何啟用 `verify-full` SSL選項，用於加密移動中的資料。

如果尚未執行此操作，請按照 [將第三方客戶端連接到 [!DNL Query Service]](./overview.md)。
