---
keywords: SFTP;sftp
title: SFTP連線
description: 建立與SFTP伺服器的即時傳出連線，以定期從Adobe Experience Platform匯出分隔的資料檔案。
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 1dd87ce19c3d9f4eb07c49968754ab979b4dee5c
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# SFTP連線

## 總覽 {#overview}

建立與SFTP伺服器的即時傳出連線，以定期從Adobe Experience Platform匯出分隔的資料檔案。

>[!IMPORTANT]
>
> 雖然Experience Platform支援將資料匯出至SFTP伺服器，但建議的雲端儲存空間位置會匯出資料 [!DNL Amazon S3] 和 [!DNL Azure Blob].

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取設定檔屬性」畫面中所選 [目的地啟動工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以3、6、8、12或24小時為增量將檔案匯出至下游平台。 深入了解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![SFTP設定檔匯出類型](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

### 驗證資訊 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA公鑰"
>abstract="或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公開金鑰必須寫入為Base64編碼字串。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="私密SSH金鑰"
>abstract="私有SSH金鑰的格式必須為Base64編碼字串，且不得受密碼保護。"

如果您選取 **[!UICONTROL 基本驗證]** 類型以連線至您的SFTP位置：

![SFTP目的地基本驗證](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL 主機]**:SFTP儲存位置的位址；
* **[!UICONTROL 使用者名稱]**:要登入您SFTP儲存位置的使用者名稱；
* **[!UICONTROL 密碼]**:登入您SFTP儲存位置的密碼。
* **[!UICONTROL 加密密鑰]**:或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公開金鑰必須寫入 [!DNL Base64-encoded] 字串。 在以下說明檔案連結中檢視格式正確且以base64編碼的鍵的範例。 中間部縮短為簡潔。

![此影像顯示UI中格式正確且以base64加密的PGP金鑰範例](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


如果您選取 **[!UICONTROL 具有SSH金鑰的SFTP]** 要連線至您SFTP位置的驗證類型：

![SFTP目的地SSH金鑰驗證](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL 網域]**:填入您的SFTP帳戶的IP位址或網域名稱
* **[!UICONTROL 埠]**:您的SFTP儲存位置所使用的連接埠；
* **[!UICONTROL 使用者名稱]**:要登入您SFTP儲存位置的使用者名稱；
* **[!UICONTROL SSH金鑰]**:用來登入您SFTP儲存位置的私密SSH金鑰。 私密金鑰必須格式化為Base64編碼字串，且不得受密碼保護。
* **[!UICONTROL 加密密鑰]**:或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公開金鑰必須寫入 [!DNL Base64] 編碼字串。
   * 範例: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. 請參閱以下格式正確的PGP金鑰範例，其中中間部分縮短，以求簡潔。

      ![PGP金鑰](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 目的地詳細資訊 {#destination-details}

建立與SFTP位置的驗證連線後，請為目的地提供下列資訊：

![SFTP目的地的可用目的地詳細資訊](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL 名稱]**:在「Experience Platform」用戶介面中輸入有助於標識此目標的名稱；
* **[!UICONTROL 說明]**:輸入此目的地的說明；
* **[!UICONTROL 資料夾路徑]**:在要匯出檔案的SFTP位置中，輸入資料夾的路徑。

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 匯出的資料 {#exported-data}

針對 [!DNL SFTP] 目的地，平台會建立 `.csv` 檔案。 如需檔案的詳細資訊，請參閱 [啟用受眾資料以批次設定檔匯出目的地](../../ui/activate-batch-profile-destinations.md) 在區段啟用教學課程中。

## IP位址允許清單

請參閱 [雲端儲存目的地的IP位址允許清單](ip-address-allow-list.md) 如果您需要將AdobeIP新增至允許清單。
