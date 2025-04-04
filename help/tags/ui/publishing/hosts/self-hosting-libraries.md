---
title: 自行託管程式庫
description: 瞭解如何在Adobe Experience Platform中實施標籤程式庫組建的自家託管。
exl-id: 8c3bf202-de7a-46e0-801f-0cede24865fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 72%

---

# 自行託管程式庫

>[!NOTE]
>
>Adobe Experience Platform Launch 已進行品牌重塑，現在是 Adobe Experience Platform 中的一套資料彙集技術。 因此，這些產品文件都推出多項幾術語變更。如需術語變更的彙整參考資料，請參閱以下[文件](../../../term-updates.md)。

Adobe Experience Platform中的標籤允許產生一組稱為[組建](../builds.md)的檔案。 這組檔案控制應用程式在執行階段的行為。

組建需要在某處託管，用戶端裝置才能在需要時於執行階段擷取這些組建。

Experience Platform可以管理這些檔案的託管，或由您親自管理。

## Managed by Adobe {#managed-by-adobe}

Adobe不從事Web託管業務。 如果您選擇交由 Adobe 管理託管作業，系統會將您的組建傳送給與我們簽約的第三方內容傳送網路 (CDN)。

目前主要的 CDN 提供廠商為 Akamai。由 Akamai 託管的檔案是使用 `assets.adobedtm.com` 網域。

### 為何使用受管式託管？

使用受管式託管的主要原因是便利性。可更輕鬆建立所需主機，且不必擔心維護作業。

## 自行託管

若您不希望 Adobe 管理您的託管檔案，您必須自行託管。若要託管您的檔案，您必須從Experience Platform取得完成的組建，並負責透過公司的發行週期將檔案發佈到公司管理的伺服器上。

### 為何要使用自行託管？

選擇託管您自己的組建檔案有許多理由。

* 有些瀏覽器會根據終端使用者設定的隱私權設定，封鎖 assets.adobedtm.com 網域
* 自行託管可減少所需的 DNS 查閱數
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

組建也可以直接傳送至您建立的SFTP伺服器。 您有責任將這些組建歸檔到您的發行週期中，並推動其上線。

若要執行直接傳送，您應建立 [SFTP 主機](sftp-host.md)，並將該主機指派給您的環境。每當您在該環境中建立程式庫，檔案都會傳送至您的 SFTP 伺服器。
