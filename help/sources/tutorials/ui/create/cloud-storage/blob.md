---
title: 在UI中建立Azure Blob源連接
description: 瞭解如何使用平台用戶介面建立Azure Blob源連接器。
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 1%

---

# 建立 [!DNL Azure Blob] UI中的源連接

本教程提供建立 [!DNL Azure Blob] (以下簡稱：[!DNL Blob]&quot;)使用平台用戶介面進行源連接。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):在Experience Platform中組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有 [!DNL Blob] 連接，您可以跳過本文檔的其餘部分並繼續學習有關 [配置資料流](../../dataflow/batch/cloud-storage.md)。

### 支援的檔案格式

Experience Platform支援從外部儲存接收的以下檔案格式：

* 分隔符分隔的值(DSV):可以使用任何單列分隔符（如制表符、逗號、管道、分號或散列）來收集任何格式的平面檔案。
* JavaScript對象符號(JSON):JSON格式的資料檔案必須符合XDM。
* Apache Parke:拼花格式化資料檔案必須符合XDM。

### 收集所需憑據

為了訪問 [!DNL Blob] 在平台上儲存，必須為以下憑據提供有效值：

| 憑據 | 說明 |
| ---------- | ----------- |
| 連接字串 | 包含驗證所需的授權資訊的字串 [!DNL Blob] Experience Platform。 的 [!DNL Blob] 連接字串模式為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 有關連接字串的詳細資訊，請參閱 [!DNL Blob] 文檔 [配置連接字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)。 |
| SAS URI | 可用作連接的備用身份驗證類型的共用訪問簽名URI [!DNL Blob] 帳戶。 的 [!DNL Blob] SAS URI模式為： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` 有關詳細資訊，請參閱 [!DNL Blob] 文檔 [共用訪問簽名URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)。 |
| 容器 | 要指定訪問權限的容器的名稱。 使用 [!DNL Blob] 源，您可以提供容器名稱來指定用戶對所選子資料夾的訪問權限。 |
| 檔案夾路徑 | 要提供訪問權限的資料夾的路徑。 |

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL Blob] 帳戶到平台。

## 連接 [!DNL Blob] 帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左導航欄訪問 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索欄找到要使用的特定源。

在 [!UICONTROL 雲儲存] 類別，選擇 **[!UICONTROL Azure Blob儲存]**，然後選擇 **[!UICONTROL 添加資料]**。

![已選擇Azure Blob儲存源的Experience Platform源目錄。](../../../../images/tutorials/create/blob/catalog.png)

的 **[!UICONTROL 連接到Azure Blob儲存]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要使用現有帳戶，請選擇 [!DNL Blob] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/blob/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後提供新名稱和可選說明 [!DNL Blob] 帳戶。

![Azure Blob儲存源的新帳戶螢幕。](../../../../images/tutorials/create/blob/new.png)

的 [!DNL Blob] 源支援帳戶密鑰身份驗證和共用訪問簽名(SAS)身份驗證。 基於帳戶密鑰的身份驗證需要連接字串進行驗證，而SAS身份驗證則使用允許對帳戶進行安全委託授權的URI。

在此步驟中，您還可以通過定義容器名稱和子資料夾的路徑來指定帳戶可以訪問的子資料夾。

>[!BEGINTABS]

>[!TAB 連接字串]

要使用帳戶密鑰進行身份驗證，請選擇 **[!UICONTROL 帳戶密鑰身份驗證]** 並提供連接字串。 在此步驟中，還可以指定要訪問的子資料夾的容器名稱和路徑。 完成後，選擇 **[!UICONTROL 連接到源]**。

![連接字串](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB SAS URI]

您可以使用SAS建立不同訪問度的身份驗證憑據，因為基於SAS的身份驗證允許您設定權限、開始日期和到期日期以及對特定資源的設定。

要使用共用訪問簽名進行身份驗證，請選擇 **[!UICONTROL 共用訪問簽名驗證]** 然後提供SAS URI。 在此步驟中，還可以指定要訪問的子資料夾的容器名稱和路徑。 完成後，選擇 **[!UICONTROL 連接到源]**。

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## 後續步驟

按照本教程，您已建立到 [!DNL Blob] 帳戶。 現在，您可以繼續下一個教程， [配置資料流，將雲儲存中的資料引入平台](../../dataflow/batch/cloud-storage.md)。
