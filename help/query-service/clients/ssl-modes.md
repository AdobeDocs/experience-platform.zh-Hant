---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；連線；連線到查詢服務；SSL；ssl；sslmode；
title: 查詢服務SSL選項
description: 瞭解協力廠商連線至Adobe Experience Platform查詢服務的SSL支援，以及如何使用驗證完整SSL模式連線。
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 37c30fc1a040efbce0c221c10b36e105d5b1a962
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 1%

---

# [!DNL Query Service] SSL選項

為了提高安全性，Adobe Experience Platform [!DNL Query Service]提供SSL連線的原生支援，以加密使用者端/伺服器通訊。 本文介紹協力廠商使用者端連線至[!DNL Query Service]的可用SSL選項，以及如何使用`verify-full` SSL引數值連線。

## 先決條件

本檔案假設您已下載協力廠商案頭使用者端應用程式，以便與您的Platform資料搭配使用。 在各自的連線指南檔案中可找到有關如何在與協力廠商使用者端連線時整合SSL安全性的特定指示。 如需所有[!DNL Query Service]受支援使用者端的清單，請參閱[使用者端連線總覽](./overview.md)。

## 可用的SSL選項 {#available-ssl-options}

Platform支援各種SSL選項，以符合您的資料安全性需求，並平衡加密和金鑰交換的處理開銷。

不同的`sslmode`引數值提供不同的保護等級。 使用SSL憑證即時加密資料，有助於防止「中間人」(MITM)攻擊、竊聽和模擬。 下表提供可用不同SSL模式的明細，及其提供的保護等級。

>[!NOTE]
>
> 由於符合必要的資料保護規範，Adobe Experience Platform不支援SSL值`disable`。

| sslmode | 竊聽保護 | MITM保護 | 說明 |
|---|---|---|---|
| `allow` | 是 | 無 | 所有通訊都需要加密。 信任網路可連線到正確的伺服器。 |
| `prefer` | 是 | 無 | 所有通訊都需要加密。 信任網路可連線到正確的伺服器。 |
| `require` | 是 | 無 | 所有通訊都需要加密。 信任網路可連線到正確的伺服器。 不需要伺服器SSL憑證驗證。 |
| `verify-ca` | 是 | 取決於CA原則 | 所有通訊都需要加密。 必須先進行伺服器驗證，才能共用資料。 這要求您在[!DNL PostgreSQL]主目錄中設定根憑證。 [詳情如下](#instructions) |
| `verify-full` | 是 | 是 | 所有通訊都需要加密。 必須先進行伺服器驗證，才能共用資料。 這要求您在[!DNL PostgreSQL]主目錄中設定根憑證。 [詳情如下](#instructions)。 |

>[!NOTE]
>
>`verify-ca`與`verify-full`之間的差異取決於根憑證授權單位(CA)的原則。 如果您已建立自己的本機CA來發行應用程式的私密憑證，則使用`verify-ca`通常可提供足夠的保護。 如果使用公用CA，`verify-ca`會允許連線到其他人可能已向CA註冊的伺服器。 `verify-full`應一律搭配公用根CA使用。

建立與Platform資料庫的協力廠商連線時，建議您至少使用`sslmode=require`，以確保移動中的資料有安全的連線。 建議將`verify-full` SSL模式用於大多數安全性敏感型環境。

## 設定伺服器驗證的根憑證 {#root-certificate}

>[!IMPORTANT]
>
>查詢服務互動式Postgres API的生產環境上的TLS/SSL憑證於2024年1月24日星期三更新。<br>雖然這是年度需求，但這次鏈結中的根憑證也已變更，因為Adobe的TLS/SSL憑證提供者已更新其憑證階層。 如果某些Postgres使用者端的憑證授權單位清單遺失根憑證，這可能會影響這些使用者端。 例如，PSQL CLI使用者端可能需要將根憑證新增至明確檔案`~/postgresql/root.crt`，否則可能會導致錯誤。 例如 `psql: error: SSL error: certificate verify failed`。如需此問題的詳細資訊，請參閱[正式的PostgreSQL檔案](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES)。<br>可以從[https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem)下載要新增的根憑證。

為了確保安全連線，在進行連線之前，必須在使用者端和伺服器上設定SSL使用方式。 如果只在伺服器上設定SSL，使用者端可能會先傳送機密資訊（例如密碼），然後才確定伺服器需要高安全性。

依預設，[!DNL PostgreSQL]不會執行伺服器憑證的任何驗證。 若要驗證伺服器的識別碼，並確保在傳送任何敏感資料之前有安全連線（作為SSL `verify-full`模式的一部分），您必須在本機電腦(`root.crt`)上放置根（自我簽署）憑證，並在伺服器上放置由根憑證簽署的葉憑證。

如果`sslmode`引數設為`verify-full`，libpq會檢查憑證鏈結是否連至儲存在使用者端上的根憑證，以確認伺服器是否可信。 接著會驗證主機名稱是否符合儲存在伺服器憑證中的名稱。

若要允許伺服器憑證驗證，您必須在主目錄的[!DNL PostgreSQL]檔案中放置一或多個根憑證(`root.crt`)。 檔案路徑類似於`~/.postgresql/root.crt`。

## 啟用驗證完整SSL模式以搭配協力廠商[!DNL Query Service]連線使用 {#instructions}

如果您需要比`sslmode=require`更嚴格的安全性控制，您可以依照醒目提示的步驟，使用`verify-full` SSL模式將協力廠商使用者端連線至[!DNL Query Service]。

>[!NOTE]
>
>要取得SSL憑證，有許多可用選項。 由於Rogue憑證愈演愈烈的趨勢，本指南會使用DigiCert，因為他們是高保證TLS/SSL、PKI、IoT和簽署解決方案的可信全球提供者。

1. 瀏覽至[可用的DigiCert根憑證清單](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. 從可用憑證清單中搜尋&quot;[!DNL DigiCert Global Root G2]&quot;。
1. 選取&#x200B;[!DNL **下載PEM**]以將檔案下載到您的本機電腦。
   ![已反白顯示[下載PEM]的可用DigiCert根憑證清單。](../images/clients/ssl-modes/digicert.png)
1. 將安全性憑證檔案重新命名為`root.crt`。
1. 將檔案複製到[!DNL PostgreSQL]資料夾。 必要的檔案路徑會因您的作業系統而異。 如果該資料夾尚不存在，請建立該資料夾。
   - 如果您使用macOS，路徑為`/Users/<username>/.postgresql`
   - 如果您使用Windows，路徑為`%appdata%\postgresql`

>[!TIP]
>
>若要在Windows作業系統上尋找您的`%appdata%`檔案位置，請按⊞ **Win + R**&#x200B;並在搜尋欄位中輸入`%appdata%`。

在您的[!DNL PostgreSQL]資料夾中有[!DNL DigiCert Global Root G2] CRT檔案之後，您可以使用`sslmode=verify-full`或`sslmode=verify-ca`選項連線到[!DNL Query Service]。

## 後續步驟

閱讀本檔案後，您將會更瞭解將協力廠商使用者端連線至[!DNL Query Service]時可用的SSL選項，以及如何啟用`verify-full` SSL選項以動態加密您的資料。

如果您尚未這樣做，請依照[將協力廠商使用者端連線至 [!DNL Query Service]](./overview.md)的指南操作。
