---
keywords: Experience Platform；首頁；熱門主題；Oracle物件儲存；oracle物件儲存
solution: Experience Platform
title: 在UI中建立Oracle對象儲存源連接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立Oracle物件儲存來源連線。
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# 建立 [!DNL Oracle Object Storage] UI中的來源連線

本教學課程提供建立 [!DNL Oracle Object Storage] 來源連線。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 收集所需憑據

在中以連接到 [!DNL Oracle Object Storage]，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `serviceUrl` | 此 [!DNL Oracle Object Storage] 驗證所需的端點。 端點格式為： `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 此 [!DNL Oracle Object Storage] 驗證所需的訪問密鑰ID。 |
| `secretKey` | 此 [!DNL Oracle Object Storage] 驗證所需的密碼。 |
| `bucketName` | 如果使用者具有限制存取權，則需要允許的貯體名稱。 貯體名稱必須介於3到63個字元之間，其開頭和結尾必須是字母或數字，並且只能包含小寫字母、數字或連字型大小(`-`)。 儲存貯體名稱的格式無法與IP位址相同。 |
| `folderPath` | 如果用戶具有受限訪問權，則需要允許的資料夾路徑。 |

如需如何取得這些值的詳細資訊，請參閱 [Oracle對象儲存身份驗證指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

收集到所需的憑據後，您可以按照以下步驟建立新的Oracle對象儲存帳戶以連接到平台。

## 連接到Oracle對象儲存

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列找到您要使用的特定來源。

在 [!UICONTROL 雲端儲存空間] 類別，選擇 **[!UICONTROL Oracle對象儲存]** 然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Oracle Object Storage] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選用說明，以及 [!DNL Oracle Object Storage] 憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## 後續步驟

依照本教學課程，您已建立與 [!DNL Oracle Object Storage] 帳戶。 您現在可以繼續下一個教學課程，以了解 [配置資料流，將資料從雲儲存導入平台](../../dataflow/batch/cloud-storage.md).
