---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Google雲端儲存空間連接器
topic: overview
translation-type: tm+mt
source-git-commit: 0ed2ed3b08f262100746f255a78c248a1748eb5e
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Google雲端儲存空間連接器

Adobe Experience Platform為AWS、Google Cloud Platform和Azure等雲端供應商提供原生連接功能，讓您能夠從這些系統中取用資料。

雲端儲存來源可將您自己的資料匯入平台，而不需下載、格式化或上傳。 收錄的資料可格式化為XDM JSON、XDM鑲木地板或分隔字元。 此程式的每個步驟都會整合至Sources工作流程中。 平台可讓您透過批次從Google雲端儲存區匯入資料。

## 連接Google雲端儲存空間帳戶的先決條件設定

若要連線至平台，您必須先啟用Google雲端儲存空間帳戶的互操作性。 若要存取互操作性設定，請開啟Google Cloud Platform，然後從導覽面板的「 **[!UICONTROL 儲存]** 」選 **[!UICONTROL 項中選取「設定]** 」。

![](../../images/tutorials/create/google-cloud-storage/nav.png)

此時會 **[!UICONTROL 顯示]** 「設定」頁面。 從這裡，您可以看到有關您Google專案ID的資訊，以及您Google雲端儲存空間帳戶的詳細資訊。 要訪問互操作性設定，請從 **[!UICONTROL 頂部標題中]** 選擇「互操作性」。

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

「互 **[!UICONTROL 操作性]** 」頁包含有關驗證、訪問密鑰和與用戶帳戶關聯的預設項目的資訊。 如果尚未建立可互操作訪問的預設項目，則可在「預設項目」( *[!UICONTROL Default project)中設定一個可互操作訪問]* 。 如果已建立預設專案，則區段會顯示專案已設為預設的確認。

若要為您的使用者帳戶產生新的存取金鑰ID和機密存取金鑰，請選取「 **[!UICONTROL 建立金鑰]**」。

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新產生的存取金鑰ID和機密存取金鑰，將您的Google雲端儲存帳戶連接至平台。

以下檔案提供如何使用API或使用者介面將Google雲端儲存空間連接至平台的資訊：

## 將Google雲端儲存空間連接至平台

以下檔案提供如何使用API或使用者介面將Google雲端儲存空間連接至平台的資訊：

### 使用API

- [使用Flow Service API建立Google雲端儲存連接器](../../tutorials/api/create/cloud-storage/google.md)
- [使用Flow Service API探索雲端儲存系統](../../tutorials/api/explore/cloud-storage.md)
- [使用Flow Service API收集雲端儲存空間資料](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中建立Google Cloud儲存空間來源連接器](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [在UI中為雲端儲存連接器設定資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)