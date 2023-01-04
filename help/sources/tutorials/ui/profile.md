---
keywords: Experience Platform；首頁；熱門主題；啟用傳入資料；填入設定檔；填入rtcp；填入的統一設定檔
solution: Experience Platform
title: 啟動傳入來源資料，以在UI中填入客戶設定檔
topic-legacy: overview
type: Tutorial
description: 來自來源連接器的傳入資料可用來擴充和填入您的即時客戶設定檔資料。
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# 啟動傳入來源資料以填入客戶設定檔

來自來源連接器的傳入資料可用於擴充和填入 [!DNL Real-Time Customer Profile] 資料。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   - [結構構成基本概念](../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   - [結構編輯器教學課程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

此外，本教學課程要求您已建立並設定來源連接器。  若需在UI中建立不同連接器的教學課程清單，請參閱 [來源連接器概觀](../../home.md).

## 填入 [!DNL Real-Time Customer Profile] 資料

為了讓客戶設定檔更加豐富，目標資料集的來源結構必須相容，才能用於 [!DNL Real-Time Customer Profile]. 相容的架構符合下列需求：

- 架構至少有一個屬性被指定為標識屬性。
- 架構具有定義為主要身分的身分屬性。
- 資料流記憶體在映射，其中主標識為目標屬性。

在來源工作區中，按一下 **[!UICONTROL 瀏覽]** 頁簽，列出基本連接。 在顯示的清單中，查找包含要用填充配置檔案的資料流的連接。 按一下連線的名稱以存取其詳細資訊。

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

連接 **[!UICONTROL 來源活動]** 畫面隨即顯示，顯示連線正在擷取來源資料的資料集。 按一下您要啟用的資料集名稱 [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

此 **[!UICONTROL 資料集活動]** 畫面。 此 **[!UICONTROL 屬性]** 畫面右側的欄會顯示資料集的詳細資訊，並包含 **[!UICONTROL 設定檔]** 切換並連結至資料集所隸屬的結構。 按一下結構的名稱以檢視其組成。

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

此 **[!UICONTROL 結構編輯器]** 顯示，顯示中央畫布中架構的結構。 在畫布中，選取要設定為主要身分的欄位。 在 **[!UICONTROL 欄位屬性]** 頁簽，選擇 **[!UICONTROL 身分]** 核取方塊，然後 **[!UICONTROL 主要身分]**. 最後，選取適當的 **[!UICONTROL 身分命名空間]**，然後按一下 **[!UICONTROL 套用]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

按一下結構的頂層物件，然後 **[!UICONTROL 架構屬性]** 欄。 為 [!DNL Profile] 通過切換 **[!UICONTROL 設定檔]** 切換。 按一下 **[!UICONTROL 儲存]** 完成變更。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

架構已啟用 [!DNL Profile]，返回 **[!UICONTROL 資料集活動]** 畫面並啟用資料集 [!DNL Profile] 按一下 **[!UICONTROL 設定檔]** 在 **[!UICONTROL 屬性]** 欄。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

同時啟用結構和資料集後， [!DNL Profile]，內嵌至該資料集的資料現在也會填入客戶設定檔。

>[!NOTE]
>
>最近啟用的資料集內的現有資料不會由 [!DNL Profile].

## 後續步驟

依照本教學課程，您已成功啟用 [!DNL Profile] 人口。 如需詳細資訊，請參閱 [[!DNL Real-Time Customer Profile] 概述](../../../profile/home.md).
