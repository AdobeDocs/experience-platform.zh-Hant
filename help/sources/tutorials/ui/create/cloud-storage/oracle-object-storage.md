---
keywords: Experience Platform；首頁；熱門主題；Oracle對象儲存；oracle對象儲存
solution: Experience Platform
title: 在UI中建立Oracle對象儲存源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Oracle對象儲存源連接。
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---

# 在UI中建立[!DNL Oracle Object Storage]源連接

本教學課程提供使用Adobe Experience PlatformUI建立[!DNL Oracle Object Storage]源連接的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示並增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

### 收集必要的認證

在中，要連接到[!DNL Oracle Object Storage]，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `serviceUrl` | 驗證所需的[!DNL Oracle Object Storage]端點。 端點格式為：`https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 驗證所需的[!DNL Oracle Object Storage]訪問密鑰ID。 |
| `secretKey` | 驗證需要[!DNL Oracle Object Storage]密碼。 |
| `bucketName` | 如果使用者有限制的存取權，則需要允許的儲存貯體名稱。 貯體名稱必須在3到63個字元之間，且必須以字母或數字開頭和結尾，且只能包含小寫字母、數字或連字型大小(`-`)。 貯體名稱的格式不能與IP位址相同。 |
| `folderPath` | 如果使用者有限制存取權，則需要允許的資料夾路徑。 |

有關如何獲取這些值的詳細資訊，請參閱[Oracle對象儲存身份驗證指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)。

收集完所需的憑據後，您可以按照以下步驟建立新的Oracle對象儲存帳戶以連接到平台。

## 連接到Oracle對象儲存

在平台UI中，從左側導覽器選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL Catalog]畫面會顯示多種來源，您可以使用這些來源建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列，找到您要使用的特定來源。

在[!UICONTROL Cloud storage]類別下，選擇&#x200B;**[!UICONTROL Oracle Object Storage]**，然後選擇&#x200B;**[!UICONTROL Add data]**。

![目錄](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### 現有帳戶

要使用現有帳戶，請選擇要建立新資料流的[!DNL Oracle Object Storage]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![現有](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇&#x200B;**[!UICONTROL New account]**，然後提供名稱、可選說明和[!DNL Oracle Object Storage]憑據。 完成後，選擇&#x200B;**[!UICONTROL Connect to source]** ，然後允許一些時間建立新連接。

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## 後續步驟

在本教學課程之後，您已建立與[!DNL Oracle Object Storage]帳戶的連線。 您現在可以繼續下一個有關[配置資料流的教程，以便將雲儲存中的資料帶入Platform](../../dataflow/batch/cloud-storage.md)。
