---
title: SFTP Source聯結器概述
description: 瞭解如何使用API或使用者介面將SFTP伺服器連線至Adobe Experience Platform。
exl-id: d5bced3d-cd33-40ea-bce0-32c76ecd2790
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 0%

---

# SFTP聯結器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

閱讀本檔案以瞭解成功將[!DNL SFTP]帳戶連線至Experience Platform所需完成的先決條件步驟。

>[!TIP]
>
>在連線之前，您必須先停用SFTP伺服器設定中的鍵盤互動式驗證。 停用此設定將允許手動輸入密碼，而不是透過服務或程式輸入。

## 先決條件 {#prerequisites}

請參閱本節，瞭解您必須完成的先決條件步驟，才能成功將您的[!DNL SFTP]來源連線至Experience Platform。

### IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

### 檔案和目錄的命名限制

以下是在命名雲端儲存空間檔案或目錄時必須考慮的限制清單。

* 目錄和檔案元件名稱不能超過255個字元。
* 目錄和檔案名稱不能以正斜線(`/`)結尾。 如果提供，則會自動移除。
* 必須正確逸出下列保留的URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
* 不允許下列字元： `" \ / : | < > * ?`。
* 不允許非法URL路徑字元。 類似`\uE000`的程式碼點雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的規則，請參閱[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
* 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

### 設定[!DNL SFTP]的Base64編碼OpenSSH私密金鑰

[!DNL SFTP]來源支援使用[!DNL Base64]編碼的OpenSSH私密金鑰進行驗證。 如需有關如何產生Base64編碼的OpenSSH私密金鑰以及如何將[!DNL SFTP]連線至Experience Platform的資訊，請參閱下列步驟。

>[!BEGINTABS]

>[!TAB Windows]

### [!DNL Windows]位使用者

如果您使用[!DNL Windows]電腦，請開啟&#x200B;**開始**&#x200B;功能表，然後選取&#x200B;**設定**。

![設定](../../images/tutorials/create/sftp/settings.png)

從出現的&#x200B;**設定**&#x200B;功能表中，選取&#x200B;**應用程式**。

![個應用程式](../../images/tutorials/create/sftp/apps.png)

接著，選取&#x200B;**選用功能**。

![選用功能](../../images/tutorials/create/sftp/optional-features.png)

選擇性功能清單隨即顯示。 如果您的電腦已預先安裝&#x200B;**OpenSSH使用者端**，則會包含在&#x200B;**選用功能**&#x200B;下的&#x200B;**已安裝功能**&#x200B;清單中。

![open-ssh](../../images/tutorials/create/sftp/open-ssh.png)

如果未安裝，請選取&#x200B;**安裝**，然後開啟&#x200B;**[!DNL Powershell]**&#x200B;並執行下列命令以產生您的私密金鑰：

```shell
PS C:\Users\lucy> ssh-keygen -t rsa -m pem
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\lucy/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\lucy/.ssh/id_rsa.
Your public key has been saved in C:\Users\lucy/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:osJ6Lg0TqK8nekNQyZGMoYwfyxNc+Wh0hYBtBylXuGk lucy@LAPTOP-FUJT1JEC
The key's randomart image is:
+---[RSA 3072]----+
|.=.*+B.o.        |
|=.O.O +          |
|+o+= B           |
|+o +E .          |
|.o=o  . S        |
|+... . .         |
| *o .            |
|o.B.             |
|=O..             |
+----[SHA256]-----+
```

接下來，在提供私密金鑰的檔案路徑時執行以下命令，將您的私密金鑰編碼為[!DNL Base64]：

```shell
C:\Users\lucy> [convert]::ToBase64String((Get-Content -path "C:\Users\lucy\.ssh\id_rsa" -Encoding byte)) > C:\Users\lucy\.ssh\id_rsa_base64
```

上述命令會將[!DNL Base64]編碼的私密金鑰儲存在您指定的檔案路徑中。 然後，您可以使用該私密金鑰來驗證[!DNL SFTP]並連線到Experience Platform。

>[!TAB Mac]

### [!DNL Mac]位使用者

如果您使用[!DNL Mac]，請開啟&#x200B;**終端機**&#x200B;並執行下列命令以產生私密金鑰（在此案例中，私密金鑰將會儲存在`/Documents/id_rsa`）：

```shell
ssh-keygen -t rsa -m pem -f ~/Documents/id_rsa
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/vrana/Documents/id_rsa.
Your public key has been saved in /Users/vrana/Documents/id_rsa.pub.
The key fingerprint is:
SHA256:s49PCaO4a0Ee8I7OOeSyhQAGc+pSUQnRii9+5S7pp1M vrana@vrana-macOS
The key's randomart image is:
+---[RSA 2048]----+
|o ==..           |
|.+..o            |
|oo.+             |
|=.. +            |
|oo = .  S        |
|+.+ +E . = .     |
|o*..*.. . o      |
|.o*=.+   +       |
|.oo=Oo  ..o      |
+----[SHA256]-----+
```

接下來，執行以下命令來編碼[!DNL Base64]中的私密金鑰：

```shell
base64 ~/Documents/id_rsa > ~/Documents/id_rsa_base64
 
 
# Print Content of base64 encoded file
cat ~/Documents/id_rsa_base64
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUJGd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFRRUF0cWFYczlXOUF1ZmtWazUwSXpwNXNLTDlOMU9VYklaYXVxbVM0Q0ZaenI1NjNxUGFuN244CmFxZWdvQTlCZnVnWDJsTVpGSFl5elEzbnp6NXdXMkdZa1hkdjFjakd0elVyNyt1NnBUeWRneGxrOGRXZWZsSzBpUlpYWW4KVFRwS0E5c2xXaHhjTXg3R2x5ejdGeDhWSzI3MmdNSzNqY1d1Q0VIU3lLSFR5SFFwekw0MEVKbGZJY1RGR1h1dW1LQjI5SwpEakhwT1grSDdGcG5Gd1pabTA4Uzc2UHJveTVaMndFalcyd1lYcTlyUDFhL0E4ejFoM1ZLdllzcG53c2tCcHFQSkQ1V3haCjczZ3M2OG9sVllIdnhWajNjS3ZsRlFqQlVFNWRNUnB2M0I5QWZ0SWlrYmNJeUNDaXV3UnJmbHk5eVNPQ2VlSEc0Z2tUcGwKL3V4YXNOT0h1d0FBQThqNnF6R1YrcXN4bFFBQUFBZHpjMmd0Y25OaEFBQUJBUUMycHBlejFiMEM1K1JXVG5Rak9ubXdvdgowM1U1UnNobHE2cVpMZ0lWbk92bnJlbzlxZnVmeHFwNkNnRDBGKzZCZmFVeGtVZGpMTkRlZlBQbkJiWVppUmQyL1Z5TWEzCk5TdnY2N3FsUEoyREdXVHgxWjUrVXJTSkZsZGlkTk9rb0QyeVZhSEZ3ekhzYVhMUHNYSHhVcmJ2YUF3cmVOeGE0SVFkTEkKb2RQSWRDbk12alFRbVY4aHhNVVplNjZZb0hiMG9PTWVrNWY0ZnNXbWNYQmxtYlR4THZvK3VqTGxuYkFTTmJiQmhlcjJzLwpWcjhEelBXSGRVcTlpeW1mQ3lRR21vOGtQbGJGbnZlQ3pyeWlWVmdlL0ZXUGR3cStVVkNNRlFUbDB4R20vY0gwQiswaUtSCnR3aklJS0s3Qkd0K1hMM0pJNEo1NGNiaUNST21YKzdGcXcwNGU3QUFBQUF3RUFBUUFBQVFBcGs0WllzMENSRnNRTk9WS0sKYWxjazlCVDdzUlRLRjFNenhrSGVydmpJYk9kL0lvRXpkcHlVa28rbm41RmpGK1hHRnNCUXZnOFdTaUlJTk1oU3BNYWI1agpvWXlka2gvd0ovWElOaDlZaE5QVXlURi9NNkFnMkNYd21KS2RxN1VKWjZyNjloV3V0VVN6U05QbkVYWTZLc29GeVUwTEFvCko0OHJMT1pMZldtMHFhWDBLNUgzNmJPaHFXSWJwMDNoZk94eno5M0MrSDM5MFJkRkp4bzJVZ0FVY3UvdHREb0REVldBdmEKVkVyMWEzak9LenVHbThrK21WeXpPZERjVFY4ckZIT0pwRnRBU3l6Q24yVld1MjV0TWtrcGRPRjNKcVdMZHdOY3loeG1URApXZGVDNWh4V0Fiano0WDZ5WXpHcFcwTmptVkFoWUVVZGNBSVlXWWM3OGEvQkFBQUFnRm8wakl4aGhwZkJ6QjF6b09FMDJBClpjTC9hcUNuYysrdmJ1a2V0aFg5Zzhlb0xQMTQyeUgzdlpLczl3c1RtbVVsZ0prZURaN2hUcklwOGY2eEwzdDRlMXByY1kKb2ZLd0gwckNGOTFyaldPbGZOUmxEempoR1NTTEVMczZoNlNzMEdBQXE2Z0ZQTVF2dTB4TDlQUTlGQ21YZVVKazJpRm1MWgpEWWJGc0NyVUxEQUFBQWdRRGF0a1pMamJaSTBFM0ZuY2dTOVF5Y3lVWmtkZ1dVNjBQcG9ud3BMQXdUdHRpOG1EQXE5cHYwClEvUlk1WE9UeGF3VXNHa0tYMjNtV1BYR0grdUlBSzhrelVVM2dGM1dRWGVkTWw4NHVCVFZCTEtUdStvVVAvZmIvMEE0dE0KSE9BSythbXZPMkZuYzFiSmVwd05USTE2cjZXWk9sZWV2ZklJQVpXcEgxVVpIdkVRQUFBSUVBMWNwcStDNUVXSFJwbnVPZQpiNHE4T0tKTlJhSUxIRUN6U0twWlFpZDFhRmJYWlVKUXpIQU85YzhINVZMcjBNUjFkcW1ORkNja2ZsZzI2Y3BEUEl3TjBYCm5HMFBxcmhKbXp0U3ZQZ3NGdkNPallncXF6U0RYUjkxd1JQTEN5cU8zcGMyM2kzZnp2WkhtMGhIdWdoNVJqV0loUlFZVkwKZUpDWHRqM08vY3p1SWdzQUFBQVJkbkpoYm1GQWRuSmhibUV0YldGalQxTUJBZz09Ci0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=
```

將[!DNL Base64]編碼的私密金鑰儲存在您指定的資料夾後，您必須將公開金鑰檔案的內容新增至[!DNL SFTP]主機授權金鑰中的新行。 在命令列上執行下列命令：

```shell
cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
```

若要確認您的公開金鑰是否已正確新增，您可以在命令列上執行下列動作：

```shell
more ~/.ssh/authorized_keys
```

>[!ENDTABS]

### 收集必要的認證 {#credentials}

您必須提供下列認證的值，才能將您的[!DNL SFTP]伺服器連線至Experience Platform。

>[!BEGINTABS]

>[!TAB 基本驗證]

為下列認證提供適當的值，以使用基本驗證來驗證您的[!DNL SFTP]伺服器。

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | 與您的[!DNL SFTP]伺服器關聯的名稱或IP位址。 |
| `port` | 您正在連線的[!DNL SFTP]伺服器連線埠。 如果未提供，則值預設為`22`。 |
| `username` | 可存取您[!DNL SFTP]伺服器的使用者名稱。 |
| `password` | [!DNL SFTP]伺服器的密碼。 |
| `maxConcurrentConnections` | 此引數可讓您指定Experience Platform在連線至您的SFTP伺服器時，將建立的同時連線數目上限。 您必須將此值設定為小於SFTP設定的限制。 **注意**：為現有SFTP帳戶啟用此設定時，只會影響未來的資料流，不會影響現有的資料流。 |
| `folderPath` | 您要提供存取權的資料夾路徑。 [!DNL SFTP]來源，您可以提供資料夾路徑，以指定使用者對您所選子資料夾的存取權。 |
| `disableChunking` | 在資料擷取期間，[!DNL SFTP]來源可以先擷取檔案長度、將檔案分割成多個部分，然後並行讀取。 您可以啟用或停用這個值，以指定您的[!DNL SFTP]伺服器是否可以從特定位移擷取檔案長度或讀取資料。 |
| `connectionSpec.id` | （僅限API）連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL SFTP]的連線規格識別碼為： `b7bf2577-4520-42c9-bae9-cad01560f7bc`。 |

>[!TAB SSH公開金鑰驗證]

為下列認證提供適當的值，以使用SSH公開金鑰驗證來驗證您的[!DNL SFTP]伺服器。

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | 與您的[!DNL SFTP]伺服器關聯的名稱或IP位址。 |
| `port` | 您正在連線的[!DNL SFTP]伺服器連線埠。 如果未提供，則值預設為`22`。 |
| `username` | 可存取您[!DNL SFTP]伺服器的使用者名稱。 |
| `password` | [!DNL SFTP]伺服器的密碼。 |
| `privateKeyContent` | Base64編碼的SSH私密金鑰內容。 支援的OpenSSH金鑰型別為`ed25519`、`RSA`和`DSA`。 |
| `passPhrase` | 如果金鑰檔案或金鑰內容受密語保護，則將私密金鑰解密的密語或密碼。 如果PrivateKeyContent受密碼保護，此引數必須搭配PrivateKeyContent的密碼短語作為值使用。 |
| `maxConcurrentConnections` | 此引數可讓您指定Experience Platform在連線至您的SFTP伺服器時，將建立的同時連線數目上限。 您必須將此值設定為小於SFTP設定的限制。 **注意**：為現有SFTP帳戶啟用此設定時，只會影響未來的資料流，不會影響現有的資料流。 |
| `folderPath` | 您要提供存取權的資料夾路徑。 [!DNL SFTP]來源，您可以提供資料夾路徑，以指定使用者對您所選子資料夾的存取權。 |
| `disableChunking` | 在資料擷取期間，[!DNL SFTP]來源可以先擷取檔案長度、將檔案分割成多個部分，然後並行讀取。 您可以啟用或停用這個值，以指定您的[!DNL SFTP]伺服器是否可以從特定位移擷取檔案長度或讀取資料。 |
| `connectionSpec.id` | （僅限API）連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL SFTP]的連線規格識別碼為： `b7bf2577-4520-42c9-bae9-cad01560f7bc`。 |

>[!ENDTABS]

## 將SFTP連線至Experience Platform

以下檔案提供如何使用API或使用者介面將SFTP伺服器連線至Experience Platform的資訊：

### 使用API

* [使用流量服務API建立SFTP基本連線](../../tutorials/api/create/cloud-storage/sftp.md)
* [使用流量服務API探索雲端儲存空間來源的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
* [使用流量服務API為雲端儲存空間來源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

* [在使用者介面中建立SFTP來源連線](../../tutorials/ui/create/cloud-storage/sftp.md)
* [在UI中為雲端儲存空間連線建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
