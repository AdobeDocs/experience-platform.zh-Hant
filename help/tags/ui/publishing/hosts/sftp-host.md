---
title: SFTP 主機
description: 了解如何在Adobe Experience Platform中設定標籤，將程式庫組建傳送至安全、自行托管的SFTP伺服器。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 39%

---

# SFTP主機

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../../term-updates.md)。

若您不希望讓 Adobe 管理您的託管程式庫，另一個選項是讓 Adobe Experience Platform 將組建傳送至您自行託管的安全 SFTP 伺服器。

Platform 使用加密的金鑰連線至您的 SFTP 網站。正確設定此項目的幾個步驟：

1. 您的 SFTP 伺服器上必須安裝公開/私密金鑰組。您可以在伺服器上產生這些金鑰，或在其他位置產生金鑰，再安裝在伺服器上。 如需詳細資訊，請參閱[如何產生SSH金鑰](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key)的GitHub檔案。
1. 私密金鑰用來加密公開GPG金鑰。 在SFTP主機建立程式期間，您需要提供私密金鑰。 請參閱Reactor API檔案中的[Encrypt values](https://developer.adobelaunch.com/api/guides/encrypting_values/)一節，了解加密公用GPG金鑰的相關說明。 除非您確定需要特定金鑰，否則請使用生產環境的GPG金鑰。 最後，您可以從任何電腦加密私密金鑰，因此不需要在伺服器上安裝 GPG，即可完成此步驟。
1. 您公司防火牆使用的IP位址可能需經過核准，才能讓Platform連線您的SFTP伺服器並加以連線。 這些 IP 位址包括：
   * `184.72.239.68`
   * `23.20.85.113`
   * `54.226.193.184`

>[!NOTE]
>
>標籤組建的結構已隨著時間而變更。 組建內部使用符號連結 (symlink) 來維持回溯相容性，以便舊版內嵌程式碼繼續與最新的組建結構搭配使用。您的SFTP伺服器必須支援使用symlink，才能作為標籤組建的有效目的地。

如需詳細資訊，請參閱以下關於[如何設定SFTP伺服器以傳送組建](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6)的中文。

## 建立 SFTP 主機

1. 開啟[!UICONTROL Hosts]標籤。
1. 建立新主機。
1. 為主機命名。
1. 選擇&#x200B;**[!UICONTROL SFTP]**&#x200B;作為主機類型。
1. 輸入主機、路徑、連接埠、使用者名稱和加密的私密金鑰。

   連接埠必須為下列任一項：

   * 21
   * 22
   * 80
   * 200-299
   * 443
   * 2000-2999
   * 4343
   * 8080
   * 8888

   >[!NOTE]
   >
   >Adobe 會限制可用於傳出流量的連接埠數量，當作安全性最佳實務。系統通常會允許所選連接埠通過公司防火牆，這些連接埠還有一些範圍，更加彈性。

1. 選取&#x200B;**[!UICONTROL 「儲存」]**。

當您選取&#x200B;**[!UICONTROL Save]**&#x200B;時，會測試連線和將檔案傳送至SFTP伺服器的能力。 Platform會建立資料夾、在該資料夾中寫入檔案、檢查檔案是否確實存在，然後自行清除。 如果您SFTP伺服器上的使用者帳戶（與您提供給Platform的安全憑證連結的帳戶）沒有執行此動作的必要權限，則主機會進入「失敗」狀態。
