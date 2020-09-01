---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Google雲端儲存空間連接器
topic: overview
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Google雲端儲存空間連接器

Adobe Experience Platform為AWS等雲端提供商提供原生連接 [!DNL Google Cloud Platform]功能 [!DNL Azure]，讓您能夠從這些系統中取得資料。

雲端儲存來源可將您自己的資料匯入 [!DNL Platform] 其中，而不需下載、格式化或上傳。 收錄的資料可格式化為XDM JSON、XDM鑲木地板或分隔字元。 此程式的每個步驟都會整合至Sources工作流程中。 [!DNL Platform] 允許您從批中導入 [!DNL Google Cloud Storage] 資料。

## IP位址允許清單

在使用源連接器之前，必須將下列IP位址新增至允許清單。 若未將您地區專屬的IP位址新增至您的允許清單，在使用來源時可能會導致錯誤或效能不佳。

### 美國東部地區

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### 西歐地區

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### 澳洲東部

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

## 連線帳戶的先決條件設 [!DNL Google Cloud Storage] 定

為了連接至，您必 [!DNL Platform]須先啟用您帳戶的互用 [!DNL Google Cloud Storage] 性。 要訪問互操作性設定，請打 [!DNL Google Cloud Platform] 開並從導航面 **[!UICONTROL 板的「存]** 儲 **** 」選項中選擇「設定」。

![](../../images/tutorials/create/google-cloud-storage/nav.png)

此時會 **[!UICONTROL 顯示]** 「設定」頁面。 從這裡，您可以看到有關您的專案ID [!DNL Google] 的資訊，以及您帳戶的詳 [!DNL Google Cloud Storage] 細資訊。 要訪問互操作性設定，請從 **[!UICONTROL 頂部標題中]** 選擇「互操作性」。

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

「互 **[!UICONTROL 操作性]** 」頁包含有關驗證、訪問密鑰和與用戶帳戶關聯的預設項目的資訊。 如果尚未建立可互操作訪問的預設項目，則可在「預設項目」( **[!UICONTROL Default project)中設定一個可互操作訪問]** 。 如果已建立預設專案，則區段會顯示專案已設為預設的確認。

若要為您的使用者帳戶產生新的存取金鑰ID和機密存取金鑰，請選取「 **[!UICONTROL 建立金鑰]**」。

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新產生的存取金鑰ID和機密存取金鑰，將您的帳戶連 [!DNL Google Cloud Storage] 接至 [!DNL Platform]。

## 連線 [!DNL Google Cloud Storage] 至 [!DNL Platform]

以下檔案提供如何連線至使用API [!DNL Google Cloud Storage] 或使 [!DNL Platform] 用者介面的資訊：

### 使用API

- [使用Flow Service API建立Google雲端儲存連接器](../../tutorials/api/create/cloud-storage/google.md)
- [使用Flow Service API探索雲端儲存系統](../../tutorials/api/explore/cloud-storage.md)
- [使用Flow Service API收集雲端儲存空間資料](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立Google Cloud儲存空間來源連接器](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [在UI中為雲端儲存連接器設定資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)