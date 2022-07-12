---
keywords: SFTP;SFTP
title: SFTP連接
description: 建立到SFTP伺服器的即時出站連接，以定期從Adobe Experience Platform導出分隔的資料檔案。
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---

# SFTP連接

## 總覽 {#overview}

建立到SFTP伺服器的即時出站連接，以定期從Adobe Experience Platform導出分隔的資料檔案。

>[!IMPORTANT]
>
> 雖然Experience Platform支援向SFTP伺服器導出資料，但建議的用於導出資料的雲儲存位置 [!DNL Amazon S3] 和 [!DNL Azure Blob]。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 批]** | 批處理目標將檔案以3、6、8、12或24小時的增量導出到下游平台。 閱讀有關 [基於批檔案的目標](/help/destinations/destination-types.md#file-based)。 |

{style=&quot;table-layout:auto&quot;}

![基於SFTP配置檔案的導出類型](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

### 驗證資訊 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA公鑰"
>abstract="或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 公鑰必須寫為Base64編碼字串。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="專用SSH密鑰"
>abstract="專用SSH密鑰必須格式化為Base64編碼的字串，且不得受密碼保護。"

如果選擇 **[!UICONTROL 基本身份驗證]** 鍵入以連接到SFTP位置：

![SFTP目標基本身份驗證](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL 主機]**:SFTP儲存位置的地址；
* **[!UICONTROL 用戶名]**:登錄SFTP儲存位置的用戶名；
* **[!UICONTROL 密碼]**:登錄SFTP儲存位置的密碼。
* **[!UICONTROL 加密密鑰]**:或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公鑰必須寫為 [!DNL Base64] 編碼字串。
   * 範例: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. 請參見下面一個正確格式的PGP鍵示例，其中中間部分縮短為簡短。

      ![PGP鍵](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)


如果選擇 **[!UICONTROL 帶SSH密鑰的SFTP]** 連接到SFTP位置的驗證類型：

![SFTP目標SSH密鑰驗證](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL 域]**:填寫SFTP帳戶的IP地址或域名
* **[!UICONTROL 埠]**:SFTP儲存位置使用的埠；
* **[!UICONTROL 用戶名]**:登錄SFTP儲存位置的用戶名；
* **[!UICONTROL SSH密鑰]**:用於登錄到SFTP儲存位置的專用SSH密鑰。 私鑰必須格式化為Base64編碼的字串，且不得受密碼保護。
* **[!UICONTROL 加密密鑰]**:或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公鑰必須寫為 [!DNL Base64] 編碼字串。
   * 範例: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. 請參見下面一個正確格式的PGP鍵示例，其中中間部分縮短為簡短。

      ![PGP鍵](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 目標詳細資訊 {#destination-details}

在建立到SFTP位置的身份驗證連接後，請提供目標的以下資訊：

![SFTP目標的可用目標詳細資訊](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL 名稱]**:在Experience Platform用戶介面中輸入有助於識別此目標的名稱；
* **[!UICONTROL 說明]**:輸入此目標的說明；
* **[!UICONTROL 資料夾路徑]**:在SFTP位置輸入檔案導出位置的資料夾路徑。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md) 有關激活此目標受眾段的說明。

## 導出的資料 {#exported-data}

對於 [!DNL SFTP] 目標，平台建立 `.csv` 檔案。 有關檔案的詳細資訊，請參見 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md) 在段激活教程中。

## IP地址允許清單

請參閱 [雲儲存目標的IP地址允許清單](ip-address-allow-list.md) 如果需要將AdobeIP添加到允許清單。
