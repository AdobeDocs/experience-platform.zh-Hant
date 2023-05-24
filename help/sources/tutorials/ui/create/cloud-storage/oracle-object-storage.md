---
keywords: Experience Platform；首頁；熱門主題；Oracle對象儲存；oracle對象儲存
solution: Experience Platform
title: 在UI中建立Oracle對象儲存源連接
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Oracle對象儲存源連接。
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# 建立 [!DNL Oracle Object Storage] UI中的源連接

本教程提供建立 [!DNL Oracle Object Storage] 源連接使用Adobe Experience PlatformUI。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 收集所需憑據

連接到 [!DNL Oracle Object Storage]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `serviceUrl` | 的 [!DNL Oracle Object Storage] 驗證所需的終結點。 終結點格式為： `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 的 [!DNL Oracle Object Storage] 驗證所需的訪問密鑰ID。 |
| `secretKey` | 的 [!DNL Oracle Object Storage] 驗證所需的密碼。 |
| `bucketName` | 如果用戶具有限制訪問權限，則需要允許的儲存段名稱。 儲存桶名稱必須長3到63個字元，它必須以字母或數字開頭和結尾，並且只能包含小寫字母、數字或連字元(`-`)。 儲存段名稱的格式不能與IP地址相同。 |
| `folderPath` | 如果用戶具有限制訪問權限，則需要允許的資料夾路徑。 |

有關如何獲取這些值的詳細資訊，請參閱 [Oracle對象儲存身份驗證指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)。

收集了所需的憑據後，您可以按照以下步驟建立新的Oracle對象儲存帳戶以連接到平台。

## 連接到Oracle對象儲存

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索欄找到要使用的特定源。

在 [!UICONTROL 雲儲存] 類別，選擇 **[!UICONTROL Oracle對象儲存]** ，然後選擇 **[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### 現有帳戶

要使用現有帳戶，請選擇 [!DNL Oracle Object Storage] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後提供名稱、可選說明，以及 [!DNL Oracle Object Storage] 憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![新](../../../../images/tutorials/create/oracle-object-storage/new.png)

## 後續步驟

按照本教程，您已建立到 [!DNL Oracle Object Storage] 帳戶。 現在，您可以繼續下一個教程， [配置資料流以將雲儲存中的資料引入平台](../../dataflow/batch/cloud-storage.md)。
