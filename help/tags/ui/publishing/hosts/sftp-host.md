---
title: SFTP 主機
description: 瞭解如何在Adobe Experience Platform配置標籤，以將庫構建交付到安全、自主承載的SFTP伺服器。
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: a0f22bad4a18936ba7c59d3747f8dd34f3de5ca4
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 19%

---

# SFTP主機

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

Adobe Experience Platform允許您將標籤庫生成提交到您托管的安全SFTP伺服器，從而讓您能夠更好地控制生成的儲存和管理方式。 本指南介紹如何在資料收集UI中為標籤屬性設定SFTP主機。

>[!NOTE]
>
>您也可以選擇使用由Adobe管理的主機。 請參閱上的指南 [Adobe管理的主機](./managed-by-adobe-host.md) 的子菜單。
>
>有關自主托管庫的優點和限制的資訊，請參見 [自主引導](./self-hosting-libraries.md)。

## 為伺服器設定訪問密鑰 {#access-key}

Platform 使用加密的金鑰連線至您的 SFTP 網站。正確設定此項目的幾個步驟：

### 建立公共/私鑰對

您的 SFTP 伺服器上必須安裝公開/私密金鑰組。您可以在伺服器上生成這些密鑰，或在其他位置生成這些密鑰，然後在伺服器上安裝它們。 有關 [如何生成SSH密鑰](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) 的子菜單。

### 加密密鑰

私鑰用於加密公鑰。 在SFTP主機建立過程中，您需要提供您的私鑰。 請參閱 [加密值](../../../api/guides/encrypting-values.md) 的API指南。 使用「生產環境」的GPG鍵，除非您知道需要特定的密鑰。 最後，您可以從任何電腦加密私密金鑰，因此不需要在伺服器上安裝 GPG，即可完成此步驟。

### 允許清單平台IP地址

您可能需要批准在公司防火牆內使用的一組IP地址，以便平台能夠訪問SFTP伺服器並連接到它。 這些IP地址是：

* `184.72.239.68`
* `23.20.85.113`
* `54.226.193.184`

>[!NOTE]
>
>標籤生成的結構已隨時間而改變。 組建內部使用符號連結 (symlink) 來維持回溯相容性，以便舊版內嵌程式碼繼續與最新的組建結構搭配使用。SFTP伺服器必須支援使用符號連結才能作為標籤生成的有效目標。

有關更多詳細資訊，請參閱以下中介文章 [如何設定SFTP伺服器以交付生成](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6)。

## 建立 SFTP 主機 {#create}

在資料收集UI中，選擇 **[!UICONTROL 主機]** 在左側導航中，然後 **[!UICONTROL 添加主機]**。

![顯示在UI中選擇的「添加主機」按鈕的影像](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

將出現主機建立對話框。 為主機提供名稱，並在 **[!UICONTROL 類型]**&#x200B;選中 **[!UICONTROL SFTP]**。

![顯示正在選擇的SFTP托管選項的影像](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### 配置SFTP主機 {#configure}

該對話框將展開，以包括SFTP主機的其他配置選項。 下文對此作了說明。

![顯示SFTP主機連接所需詳細資訊的影像](../../../images/ui/publishing/sftp-hosts/host-details.png)

| 配置欄位 | 說明 |
| --- | --- |
| [!UICONTROL 不使用符號連結] | 預設情況下，所有SFTP主機都使用符號連結（符號連結）來引用庫 [構建](../builds.md) 保存到伺服器。 但是，並非所有伺服器都支援使用符號連結。 選擇此選項後，主機將使用複製操作直接更新生成資產，而不是使用符號連結。 |
| [!UICONTROL SFTP伺服器URL] | 伺服器的URL基路徑。 |
| [!UICONTROL 路徑] | 附加到此主機的基本伺服器URL的路徑。 |
| [!UICONTROL 埠] | 連接埠必須為下列任一項：<ul><li>`21`</li><li>`22`</li><li>`80`</li><li>`200-299`</li><li>`443`</li><li>`2000-2999`</li><li>`4343`</li><li>`8080`</li><li>`8888`</li></ul>Adobe 會限制可用於傳出流量的連接埠數量，當作安全性最佳實務。所選埠通常允許通過公司防火牆，並包括一些靈活性範圍。 |
| [!UICONTROL 用戶名] | 訪問伺服器時使用的用戶名。 |
| [!UICONTROL 加密的私鑰] | 您在 [上一步](#access-key)。 |

選擇 **[!UICONTROL 保存]** 建立具有選定配置的主機。

![顯示正在保存的SFTP主機的影像](../../../images/ui/publishing/sftp-hosts/save-host.png)

選擇時 **[!UICONTROL 保存]**，已測試將檔案傳送到SFTP伺服器的連接和能力。 平台建立資料夾，在該資料夾中寫入檔案，檢查檔案是否在該資料夾中，然後自行清除。 如果SFTP伺服器上的用戶帳戶（連接到您提供給平台的安全證書的用戶帳戶）沒有執行此操作所需的權限，則主機將進入「失敗」狀態。

## 後續步驟

本指南介紹了如何設定自主承載的SFTP伺服器以用於標籤。 主機建立後，您可以將其與 [環境](../environments.md) 用於發佈標籤庫。 有關在Web或移動屬性上激活標籤功能的高級過程的詳細資訊，請參閱 [發佈概述](../overview.md)。
