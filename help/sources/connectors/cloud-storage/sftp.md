---
keywords: Experience Platform；首頁；熱門主題；SFTP;sftp
solution: Experience Platform
title: SFTP源連接器概述
description: 瞭解如何使用API或用戶介面將SFTP伺服器連接到Adobe Experience Platform。
exl-id: d5bced3d-cd33-40ea-bce0-32c76ecd2790
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# SFTP連接器

Adobe Experience Platform提供本地連接，如AWS, [!DNL Google Cloud Platform], [!DNL Azure]，允許您從這些系統中獲取資料。

雲儲存源可以將您自己的資料 [!DNL Platform] 無需下載、格式化或上載。 所攝取的資料可以格式化為XDM JSON、XDM Parke或分隔。 流程的每個步驟都整合到「源」工作流中。 [!DNL Platform] 允許您通過批處理從FTP或SFTP伺服器導入資料。

## IP地址允許清單

在使用源連接器之前，必須將IP地址清單添加到允許清單。 如果無法將特定於區域的IP地址添加到允許清單，則在使用源時可能會導致錯誤或效能不佳。 查看 [IP地址允許清單](../../ip-address-allow-list.md) 的子菜單。

## 檔案和目錄的命名約束

以下是命名雲儲存檔案或目錄時必須考慮的約束條件清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名不能以正斜槓結尾(`/`)。 如果提供，將自動刪除。
- 必須正確轉義以下保留URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用以下字元： `" \ / : | < > * ?`。
- 不允許使用非法的URL路徑字元。 代碼點類似 `\uE000`，但在NTFS檔案名中有效，則不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，如控制字元（0x00到0x1F、\u0081等）。 有關HTTP/1.1中Unicode字串的規則，請參見 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許使用下列檔案名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM9、COM9prn、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 設定Base64編碼的OpenSSH私鑰 [!DNL SFTP]

的 [!DNL SFTP] 源支援驗證 [!DNL Base64]-encoded OpenSSH私鑰。 有關如何生成Base64編碼的OpenSSH私鑰並連接的資訊，請參閱以下步驟 [!DNL SFTP] 到平台。

### [!DNL Windows] 用戶

如果使用 [!DNL Windows] 機器，開啟 **開始** ，然後選擇 **設定**。

![設定](../../images/tutorials/create/sftp/settings.png)

從 **設定** 菜單，選擇 **應用**。

![應用](../../images/tutorials/create/sftp/apps.png)

下一步，選擇 **可選功能**。

![可選功能](../../images/tutorials/create/sftp/optional-features.png)

此時將顯示可選功能的清單。 如果 **OpenSSH客戶端** 已預裝到您的電腦中，然後將包含在 **已安裝的功能** 清單 **可選功能**。

![open ssh](../../images/tutorials/create/sftp/open-ssh.png)

如果未安裝，請選擇 **安裝** 然後開啟 **[!DNL Powershell]** 並運行以下命令以生成私鑰：

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

接下來，在提供私鑰的檔案路徑時運行以下命令，將私鑰編碼到 [!DNL Base64]:

```shell
C:\Users\lucy> [convert]::ToBase64String((Get-Content -path "C:\Users\lucy\.ssh\id_rsa" -Encoding byte)) > C:\Users\lucy\.ssh\id_rsa_base64
```

以上命令保存 [!DNL Base64]指定的檔案路徑中的 — encoded私鑰。 然後，您可以使用該私鑰進行身份驗證 [!DNL SFTP] 並連接到平台。

### [!DNL Mac] 用戶

如果使用 [!DNL Mac]開啟 **終端** 並運行以下命令以生成私鑰(在這種情況下，私鑰將保存在 `/Documents/id_rsa`):

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

接下來，運行以下命令將私鑰編碼到 [!DNL Base64]:

```shell
base64 ~/Documents/id_rsa > ~/Documents/id_rsa_base64
 
 
# Print Content of base64 encoded file
cat ~/Documents/id_rsa_base64
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUJGd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFRRUF0cWFYczlXOUF1ZmtWazUwSXpwNXNLTDlOMU9VYklaYXVxbVM0Q0ZaenI1NjNxUGFuN244CmFxZWdvQTlCZnVnWDJsTVpGSFl5elEzbnp6NXdXMkdZa1hkdjFjakd0elVyNyt1NnBUeWRneGxrOGRXZWZsSzBpUlpYWW4KVFRwS0E5c2xXaHhjTXg3R2x5ejdGeDhWSzI3MmdNSzNqY1d1Q0VIU3lLSFR5SFFwekw0MEVKbGZJY1RGR1h1dW1LQjI5SwpEakhwT1grSDdGcG5Gd1pabTA4Uzc2UHJveTVaMndFalcyd1lYcTlyUDFhL0E4ejFoM1ZLdllzcG53c2tCcHFQSkQ1V3haCjczZ3M2OG9sVllIdnhWajNjS3ZsRlFqQlVFNWRNUnB2M0I5QWZ0SWlrYmNJeUNDaXV3UnJmbHk5eVNPQ2VlSEc0Z2tUcGwKL3V4YXNOT0h1d0FBQThqNnF6R1YrcXN4bFFBQUFBZHpjMmd0Y25OaEFBQUJBUUMycHBlejFiMEM1K1JXVG5Rak9ubXdvdgowM1U1UnNobHE2cVpMZ0lWbk92bnJlbzlxZnVmeHFwNkNnRDBGKzZCZmFVeGtVZGpMTkRlZlBQbkJiWVppUmQyL1Z5TWEzCk5TdnY2N3FsUEoyREdXVHgxWjUrVXJTSkZsZGlkTk9rb0QyeVZhSEZ3ekhzYVhMUHNYSHhVcmJ2YUF3cmVOeGE0SVFkTEkKb2RQSWRDbk12alFRbVY4aHhNVVplNjZZb0hiMG9PTWVrNWY0ZnNXbWNYQmxtYlR4THZvK3VqTGxuYkFTTmJiQmhlcjJzLwpWcjhEelBXSGRVcTlpeW1mQ3lRR21vOGtQbGJGbnZlQ3pyeWlWVmdlL0ZXUGR3cStVVkNNRlFUbDB4R20vY0gwQiswaUtSCnR3aklJS0s3Qkd0K1hMM0pJNEo1NGNiaUNST21YKzdGcXcwNGU3QUFBQUF3RUFBUUFBQVFBcGs0WllzMENSRnNRTk9WS0sKYWxjazlCVDdzUlRLRjFNenhrSGVydmpJYk9kL0lvRXpkcHlVa28rbm41RmpGK1hHRnNCUXZnOFdTaUlJTk1oU3BNYWI1agpvWXlka2gvd0ovWElOaDlZaE5QVXlURi9NNkFnMkNYd21KS2RxN1VKWjZyNjloV3V0VVN6U05QbkVYWTZLc29GeVUwTEFvCko0OHJMT1pMZldtMHFhWDBLNUgzNmJPaHFXSWJwMDNoZk94eno5M0MrSDM5MFJkRkp4bzJVZ0FVY3UvdHREb0REVldBdmEKVkVyMWEzak9LenVHbThrK21WeXpPZERjVFY4ckZIT0pwRnRBU3l6Q24yVld1MjV0TWtrcGRPRjNKcVdMZHdOY3loeG1URApXZGVDNWh4V0Fiano0WDZ5WXpHcFcwTmptVkFoWUVVZGNBSVlXWWM3OGEvQkFBQUFnRm8wakl4aGhwZkJ6QjF6b09FMDJBClpjTC9hcUNuYysrdmJ1a2V0aFg5Zzhlb0xQMTQyeUgzdlpLczl3c1RtbVVsZ0prZURaN2hUcklwOGY2eEwzdDRlMXByY1kKb2ZLd0gwckNGOTFyaldPbGZOUmxEempoR1NTTEVMczZoNlNzMEdBQXE2Z0ZQTVF2dTB4TDlQUTlGQ21YZVVKazJpRm1MWgpEWWJGc0NyVUxEQUFBQWdRRGF0a1pMamJaSTBFM0ZuY2dTOVF5Y3lVWmtkZ1dVNjBQcG9ud3BMQXdUdHRpOG1EQXE5cHYwClEvUlk1WE9UeGF3VXNHa0tYMjNtV1BYR0grdUlBSzhrelVVM2dGM1dRWGVkTWw4NHVCVFZCTEtUdStvVVAvZmIvMEE0dE0KSE9BSythbXZPMkZuYzFiSmVwd05USTE2cjZXWk9sZWV2ZklJQVpXcEgxVVpIdkVRQUFBSUVBMWNwcStDNUVXSFJwbnVPZQpiNHE4T0tKTlJhSUxIRUN6U0twWlFpZDFhRmJYWlVKUXpIQU85YzhINVZMcjBNUjFkcW1ORkNja2ZsZzI2Y3BEUEl3TjBYCm5HMFBxcmhKbXp0U3ZQZ3NGdkNPallncXF6U0RYUjkxd1JQTEN5cU8zcGMyM2kzZnp2WkhtMGhIdWdoNVJqV0loUlFZVkwKZUpDWHRqM08vY3p1SWdzQUFBQVJkbkpoYm1GQWRuSmhibUV0YldGalQxTUJBZz09Ci0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=
```

一旦 [!DNL Base64]-encoded私鑰保存在您指定的資料夾中，然後必須將公鑰檔案的內容添加到 [!DNL SFTP] 主機授權密鑰。 在命令行上運行以下命令：

```shell
cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
```

要確認是否正確添加了公鑰，可以在命令行上運行以下命令：

```shell
more ~/.ssh/authorized_keys
```

## 將SFTP連接到 [!DNL Platform]

>[!IMPORTANT]
>
>在連接之前，用戶必須在SFTP伺服器配置中禁用鍵盤交互身份驗證。 禁用此設定將允許手動輸入密碼，而不是通過服務或程式輸入密碼。 查看 [元件Pro文檔](https://doc.componentpro.com/ComponentPro-Sftp/authenticating-with-a-keyboard-interactive-authentication) 的子菜單。

下面的文檔提供了有關如何將SFTP伺服器連接到 [!DNL Platform] 使用API或用戶介面：

### 使用API

- [使用流服務API建立SFTP基連接](../../tutorials/api/create/cloud-storage/sftp.md)
- [使用流服務API瀏覽雲儲存源的資料結構和內容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服務API為雲儲存源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立SFTP源連接](../../tutorials/ui/create/cloud-storage/sftp.md)
- [在UI中為雲儲存連接建立資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
