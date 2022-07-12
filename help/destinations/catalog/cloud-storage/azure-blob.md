---
keywords: Azure Blob;Blob目標；s3;azure Blob目標
title: Azure Blob連接
description: 建立到Azure Blob儲存的即時出站連接以定期從Adobe Experience Platform導出CSV資料檔案。
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 1%

---

# [!DNL Azure Blob] 連接

## 總覽 {#overview}

[!DNL Azure Blob] (以下簡稱： [!DNL Blob])是Microsoft的雲對象儲存解決方案。 本教程提供建立 [!DNL Blob] 目標使用 [!DNL Platform] 用戶介面。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-time Customer Profile]](../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有 [!DNL Blob] 目標，您可以跳過本文檔的其餘部分，繼續學習有關 [將段激活到目標](../../ui/activate-batch-profile-destinations.md)。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 批]** | 批處理目標將檔案以3、6、8、12或24小時的增量導出到下游平台。 閱讀有關 [基於批檔案的目標](/help/destinations/destination-types.md#file-based)。 |

{style=&quot;table-layout:auto&quot;}

## 支援的檔案格式 {#file-formats}

[!DNL Experience Platform] 支援要導出到的以下檔案格式 [!DNL Azure Blob]:

* 逗號分隔值(CSV):當前，對導出資料檔案的支援僅限於逗號分隔的值。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在目標配置工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="RSA公鑰"
>abstract="或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公鑰必須寫為 [!DNL Base64-encoded] 的下界。 在下面的文檔連結中查看正確格式鍵的示例。"

要驗證到目標，請填寫必填欄位並選擇 **[!UICONTROL 連接到目標]**。

* **[!UICONTROL 連接字串]**:訪問Blob儲存中的資料需要連接字串。 的 [!DNL Blob] 連接字串模式以以下方式開頭： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。
   * 有關配置的詳細資訊 [!DNL Blob] 連接字串，請參見 [為Azure儲存帳戶配置連接字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) 在Microsoft檔案里。
* **[!UICONTROL 加密密鑰]**:或者，您可以附加RSA格式的公鑰，以將加密添加到導出的檔案中。 您的公鑰必須寫為 [!DNL Base64-encoded] 的下界。
   * 範例: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. 請參見下面一個正確格式的PGP鍵示例，其中中間部分縮短為簡短。

      ![PGP鍵](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:輸入一個名稱，以幫助您標識此目標。
* **[!UICONTROL 說明]**:輸入此目標的說明。
* **[!UICONTROL 資料夾路徑]**:輸入將承載導出檔案的目標資料夾的路徑。
* **[!UICONTROL 容器]**:輸入 [!DNL Azure Blob Storage] 要由此目標使用的容器。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md) 有關激活此目標受眾段的說明。

## 導出的資料 {#exported-data}

對於 [!DNL Azure Blob Storage] 目的地， [!DNL Platform] 建立 `.csv` 檔案。 有關檔案的詳細資訊，請參見 [將受眾資料激活到批配置檔案導出目標](../../ui/activate-batch-profile-destinations.md) 在段激活教程中。