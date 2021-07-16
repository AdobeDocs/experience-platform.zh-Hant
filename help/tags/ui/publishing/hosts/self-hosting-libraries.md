---
title: 自行托管程式庫
description: 了解如何在Adobe Experience Platform中為您的標籤程式庫組建實作自行托管。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 68%

---

# 自行託管程式庫

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../../term-updates.md)。

Adobe Experience Platform中的標籤可產生一組稱為[build](../builds.md)的檔案。 這組檔案控制應用程式在運行時的行為。

組建需要在某處託管，用戶端裝置才能在需要時於執行階段擷取這些組建。

Platform 可以管理這些檔案的託管，或由您親自管理。

## Managed by Adobe {#managed-by-adobe}

Adobe 不從事 Web 託管業務。如果您選擇交由 Adobe 管理託管作業，系統會將您的組建傳送給與我們簽約的第三方內容傳送網路 (CDN)。

目前主要的 CDN 提供廠商為 Akamai。由 Akamai 託管的檔案是使用 `assets.adobedtm.com` 網域。

### 為何使用受管式託管？

使用受管式託管的主要原因是便利性。可更輕鬆建立所需主機，且不必擔心維護作業。

## 自行託管

若您不希望 Adobe 管理您的託管檔案，您必須自行託管。若要托管您的檔案，您必須從Platform取得完成的組建，並負責透過公司的發行週期將檔案發佈至由公司管理的伺服器。

### 為何要使用自行託管？

選擇託管您自己的組建檔案有許多理由。

* 有些瀏覽器會根據終端使用者設定的隱私權設定，封鎖 assets.adobedtm.com 網域
* 自行託管可減少所需的 DNS 查閱數
* 您需要使用HTTP/2
* 您擁有設定安全性所需的特定標題
* 您的快取控制要求與Adobe預設設定不同
* 您希望更全面控制邊緣節點的位置
* 您的組織設有安全和法律規定，導致您無法使用由 Adobe 管理的選項

### 如何自行託管

您可透過兩種方法取得完成的組建，以便自行託管。

* 下載
* 直接傳送

#### 下載

組建可以封裝的.zip檔案傳送（可選擇加密）。 然後您可以將套件解壓縮並將內容插入至您的發行週期中，藉此將組建放置在您自己的伺服器上。

使用 [Managed by Adobe](self-hosting-libraries.md) 主機，並在您的環境中選取 [Archive](../environments.md) 選項。環境會提供下載連結。每當建立組建時，您都能透過環境的下載連結擷取該組建。

#### 直接傳送

組建也可直接傳送至您建立的SFTP伺服器。 您有責任將這些組建歸檔到您的發行週期中，並推動其上線。

若要執行直接傳送，您應建立 [SFTP 主機](sftp-host.md)，並將該主機指派給您的環境。每當您在該環境中建立程式庫，檔案都會傳送至您的 SFTP 伺服器。
