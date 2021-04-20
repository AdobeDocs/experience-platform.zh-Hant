---
keywords: Experience Platform;home；熱門主題；Oracle Object Storage;Oracle對象儲存
solution: Experience Platform
title: 在UI中建立Oracle對象儲存源連接
topic: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Oracle Object Storage來源連線。
translation-type: tm+mt
source-git-commit: c1453a9f0be42f834d35af871051324df8dadf80
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---


# 在UI中建立[!DNL Oracle Object Storage]源連接

本教學課程提供使用Adobe Experience Platform UI建立[!DNL Oracle Object Storage]來源連線的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

### 收集必要的認證

在中，要連接到[!DNL Oracle Object Storage]，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `serviceUrl` | 驗證所需的[!DNL Oracle Object Storage]端點。 端點格式為：`https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 驗證所需的[!DNL Oracle Object Storage]訪問密鑰ID。 |
| `secretKey` | 驗證需要[!DNL Oracle Object Storage]密碼。 |
| `bucketName` | 如果使用者有限制的存取權，則需要允許的儲存貯體名稱。 貯體名稱必須在3到63個字元之間，且必須以字母或數字開頭和結尾，且只能包含小寫字母、數字或連字型大小(`-`)。 貯體名稱的格式不能與IP位址相同。 |
| `folderPath` | 如果使用者有限制存取權，則需要允許的資料夾路徑。 |

有關如何獲取這些值的詳細資訊，請參閱[《Oracle Object Storage Authentication Guide》](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)。

收集到所需的憑據後，您可以按照以下步驟建立新的Oracle對象儲存帳戶以連接到平台。

## 連接到Oracle對象儲存

在平台UI中，從左側導覽器選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL Catalog]畫面會顯示多種來源，您可以使用這些來源建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列，找到您要使用的特定來源。

在[!UICONTROL 雲儲存]類別下，選擇&#x200B;**[!UICONTROL Oracle對象儲存]** ，然後選擇&#x200B;**[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### 現有帳戶

要使用現有帳戶，請選擇要建立新資料流的[!DNL Oracle Object Storage]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![現有](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇&#x200B;**[!UICONTROL 新建帳戶]**，然後提供名稱、可選說明和[!DNL Oracle Object Storage]憑據。 完成後，選擇&#x200B;**[!UICONTROL 連接到源]** ，然後允許新連接建立一段時間。

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## 後續步驟

在本教學課程之後，您已建立與[!DNL Oracle Object Storage]帳戶的連線。 您現在可以繼續下一個有關[配置資料流的教程，以便將雲儲存中的資料帶入Platform](../../dataflow/batch/cloud-storage.md)。
