---
title: 在UI中建立Google PubSub Source Connection
description: 了解如何使用Platform使用者介面建立Google PubSub來源連接器。
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: f56cdc2dc67f2d4820d80d8e5bdec8306d852891
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 1%

---

# 建立 [!DNL Google PubSub] UI中的源連接

本教學課程提供建立 [!DNL Google PubSub] (下稱「[!DNL PubSub]&quot;)使用Platform使用者介面。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

如果您已有有效 [!DNL PubSub] 連線，您可以略過本檔案的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/batch/cloud-storage.md).

### 收集所需憑據

為了連接 [!DNL PubSub] 若要使用Platform，您必須為下列憑證提供有效值：

| 憑據 | 說明 |
| ---------- | ----------- |
| 專案 ID | 驗證所需的專案ID [!DNL PubSub]. |
| 憑證 | 驗證所需的憑據或私鑰ID [!DNL PubSub]. |
| 主題ID | 的ID [!DNL PubSub] 代表訊息摘要的資源。 如果要提供對中特定資料流的存取權，必須指定主題ID [!DNL Google PubSub] 來源。 |

如需這些值的詳細資訊，請參閱下列內容 [PubSub驗證](https://cloud.google.com/pubsub/docs/authentication) 檔案。 如果您使用服務帳戶型驗證，請參閱下列內容 [PubSub指南](https://cloud.google.com/docs/authentication/production#create_service_account) 以取得如何產生憑證的步驟。

>[!TIP]
>
>如果您使用服務帳戶型驗證，請確定您已授予您服務帳戶的足夠使用者存取權，且複製和貼上憑證時，JSON中沒有額外的空格。

收集完所需憑證後，您可以依照下列步驟連結您的 [!DNL PubSub] 帳戶至Platform。

## 連接您的 [!DNL PubSub] 帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 [!UICONTROL 雲端儲存空間] 類別，選擇 **[!UICONTROL Google PubSub]**，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/google-pubsub/catalog.png)

此 **[!UICONTROL 連線至Google PubSub]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL PubSub] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/google-pubsub/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選用說明，以及 [!DNL PubSub] 輸入表單上的驗證憑據。 在此步驟中，您可以提供主題ID，以定義您的帳戶可存取的資料。 只能存取與該主題ID相關聯的訂閱。

>[!NOTE]
>
>指派給發佈子專案的承擔者（角色）會繼承在 [!DNL PubSub] 專案。 如果要添加主體（角色）以訪問特定主題，則該主體（角色）也必須添加到主題的相應訂閱中。 如需詳細資訊，請閱讀 [[!DNL PubSub] 存取控制檔案](https://cloud.google.com/pubsub/docs/access-control).

完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## 後續步驟

依照本教學課程，您可以在 [!DNL PubSub] 帳戶和平台。 您現在可以繼續下一個教學課程，以及 [配置資料流，將雲儲存中的資料流導入Platform](../../dataflow/streaming/cloud-storage-streaming.md).
