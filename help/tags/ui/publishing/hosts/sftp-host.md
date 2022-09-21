---
title: SFTP 主機
description: 了解如何在Adobe Experience Platform中設定標籤，將程式庫組建傳送至安全、自行托管的SFTP伺服器。
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 19%

---

# SFTP主機

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

Adobe Experience Platform可讓您將標籤程式庫組建傳送至托管的安全SFTP伺服器，進一步掌控組建的儲存和管理方式。 本指南說明如何在Experience PlatformUI或資料收集UI中為標籤屬性設定SFTP主機。

>[!NOTE]
>
>您也可以選擇使用由Adobe管理的主機。 請參閱 [Adobe管理主機](./managed-by-adobe-host.md) 以取得更多資訊。
>
>如需自行托管程式庫的優點和限制的相關資訊，請參閱 [自行托管指南](./self-hosting-libraries.md).

## 設定伺服器的存取金鑰 {#access-key}

Platform 使用加密的金鑰連線至您的 SFTP 網站。正確設定此項目的幾個步驟：

### 建立公開/私密金鑰組

您的 SFTP 伺服器上必須安裝公開/私密金鑰組。您可以在伺服器上產生這些金鑰，或在其他位置產生金鑰，再安裝在伺服器上。 請參閱GitHub檔案，了解 [如何產生SSH金鑰](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) 以取得更多資訊。

### 加密您的金鑰

私密金鑰用於加密公開金鑰。 在SFTP主機建立程式期間，您需要提供私密金鑰。 請參閱 [加密值](../../../api/guides/encrypting-values.md) 請參閱Reactor API指南，取得加密公開金鑰的相關指示。 除非您確定需要特定金鑰，否則請使用生產環境的GPG金鑰。 最後，您可以從任何電腦加密私密金鑰，因此不需要在伺服器上安裝 GPG，即可完成此步驟。

### 允許清單平台IP地址

您可能需要核准要在公司防火牆內使用的一組IP位址，才能讓Platform連線您的SFTP伺服器並連線至它。 這些IP位址包括：

* `184.72.239.68`
* `23.20.85.113`
* `54.226.193.184`

>[!NOTE]
>
>標籤組建的結構已隨著時間而變更。 組建內部使用符號連結 (symlink) 來維持回溯相容性，以便舊版內嵌程式碼繼續與最新的組建結構搭配使用。您的SFTP伺服器必須支援使用symlink，才能作為標籤組建的有效目的地。

有關更多詳細資訊，請參閱以下的中文文章： [如何設定SFTP伺服器以傳送組建](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## 建立 SFTP 主機 {#create}

選擇 **[!UICONTROL 主機]** 在左側導覽器中，隨後 **[!UICONTROL 添加主機]**.

![在UI中顯示「新增主機」按鈕的影像](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

主機建立對話框隨即顯示。 提供主機的名稱，並在 **[!UICONTROL 類型]**，選取 **[!UICONTROL SFTP]**.

![顯示所選SFTP托管選項的影像](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### 設定SFTP主機 {#configure}

對話方塊會展開，加入SFTP主機的其他設定選項。 以下說明。

![顯示SFTP主機連線所需詳細資訊的影像](../../../images/ui/publishing/sftp-hosts/host-details.png)

| 配置欄位 | 說明 |
| --- | --- |
| [!UICONTROL 不使用Symlink] | 依預設，所有SFTP主機都使用符號連結（符號連結）來參考程式庫 [建置](../builds.md) 會儲存至伺服器。 但是，並非所有伺服器都支援使用symlink。 選取此選項時，主機會使用複製操作直接更新建置資產，而非使用符號連結。 |
| [!UICONTROL SFTP伺服器URL] | 伺服器的URL基礎路徑。 |
| [!UICONTROL 路徑] | 要附加到此主機的基本伺服器URL的路徑。 |
| [!UICONTROL 埠] | 連接埠必須為下列任一項：<ul><li>`21`</li><li>`22`</li><li>`80`</li><li>`200-299`</li><li>`443`</li><li>`2000-2999`</li><li>`4343`</li><li>`8080`</li><li>`8888`</li></ul>Adobe 會限制可用於傳出流量的連接埠數量，當作安全性最佳實務。選定的埠通常可通過公司防火牆，並包括一些範圍以實現靈活性。 |
| [!UICONTROL 使用者名稱] | 存取伺服器時要使用的使用者名稱。 |
| [!UICONTROL 加密的私密金鑰] | 您在 [上一步](#access-key). |

選擇 **[!UICONTROL 儲存]** 使用所選配置建立主機。

![顯示正在儲存的SFTP主機的影像](../../../images/ui/publishing/sftp-hosts/save-host.png)

選取 **[!UICONTROL 儲存]**，則會測試連線以及將檔案傳送至SFTP伺服器的能力。 Platform會建立資料夾、在該資料夾中寫入檔案、檢查檔案是否確實存在，然後自行清除。 如果您SFTP伺服器上的使用者帳戶（與您提供給Platform的安全憑證連結的帳戶）沒有執行此動作的必要權限，則主機會進入「失敗」狀態。

## 後續步驟

本指南說明如何設定自行托管的SFTP伺服器，以便用於標籤。 建立主機後，您就可以將其與一或多個 [環境](../environments.md) ，以發佈標籤程式庫。 如需在您的網頁或行動屬性上啟用標籤功能的高階程式詳細資訊，請參閱 [發佈概述](../overview.md).
