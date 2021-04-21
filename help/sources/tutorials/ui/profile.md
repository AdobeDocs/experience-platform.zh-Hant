---
keywords: Experience Platform;home；熱門主題；激活入站資料；populate profile;populate rtcp;peltimed unified profile
solution: Experience Platform
title: 啟用傳入來源資料，在UI中填入客戶個人檔案
topic-legacy: overview
type: Tutorial
description: 來自來源連接器的傳入資料可用於豐富和填入即時客戶個人檔案資料。
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# 啟用傳入來源資料以填入客戶個人檔案

來自源連接器的入站資料可用於豐富和填充[!DNL Real-time Customer Profile]資料。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

- [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   - [架構構成基礎](../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

此外，本教學課程要求您已建立並設定來源連接器。  在[來源連接器概述](../../home.md)中，可找到在UI中建立不同連接器的教學課程清單。

## 填入您的[!DNL Real-time Customer Profile]資料

為了豐富客戶個人檔案，目標資料集的來源架構必須相容，才能用於[!DNL Real-time Customer Profile]。 相容的架構符合下列需求：

- 架構至少有一個屬性指定為標識屬性。
- 架構具有定義為主標識的身份屬性。
- 資料流記憶體在映射，其中主標識是目標屬性。

在「來源」工作區中，按一下&#x200B;**[!UICONTROL Browse]**&#x200B;標籤以列出基本連線。 在顯示的清單中，查找包含要填充配置檔案的資料流的連接。 按一下連接的名稱以訪問其詳細資訊。

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

此時將顯示連接的&#x200B;**[!UICONTROL Source activity]**&#x200B;螢幕，顯示連接正在將源資料收錄到的資料集。 按一下您要為[!DNL Profile]啟用的資料集名稱。

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

出現&#x200B;**[!UICONTROL Dataset activity]**&#x200B;螢幕。 畫面右側的&#x200B;**[!UICONTROL Properties]**&#x200B;欄會顯示資料集的詳細資料，並包含&#x200B;**[!UICONTROL Profile]**&#x200B;開關和資料集所依循之模式的連結。 按一下架構的名稱可查看其構成。

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

將出現&#x200B;**[!UICONTROL Schema Editor]**，顯示中央畫布中的架構結構。 在畫布中，選取要設為主要身分的欄位。 在出現的&#x200B;**[!UICONTROL Field properties]**&#x200B;頁籤下，選擇&#x200B;**[!UICONTROL Identity]**&#x200B;複選框，然後選擇&#x200B;**[!UICONTROL Primary identity]**。 最後，選取適當的&#x200B;**[!UICONTROL Identity namespace]**，然後按一下&#x200B;**[!UICONTROL Apply]**。

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

按一下架構結構的頂級對象，並顯示&#x200B;**[!UICONTROL Schema properties]**&#x200B;列。 通過切換&#x200B;**[!UICONTROL Profile]**&#x200B;交換機，為[!DNL Profile]啟用模式。 按一下&#x200B;**[!UICONTROL Save]**&#x200B;以完成變更。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

現在已為[!DNL Profile]啟用架構，請返回&#x200B;**[!UICONTROL Dataset activity]**&#x200B;畫面，並按一下&#x200B;**[!UICONTROL Profile]**&#x200B;在&#x200B;**[!UICONTROL Properties]**&#x200B;欄內切換，以啟用[!DNL Profile]的資料集。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

在[!DNL Profile]啟用架構和資料集後，內嵌至該資料集的資料現在也會填入客戶個人檔案。

>[!NOTE]
>
>[!DNL Profile]不會使用最近啟用的資料集內的現有資料。

## 後續步驟

按照本教程，您已成功激活[!DNL Profile]人口的入站資料。 如需詳細資訊，請參閱[[!DNL Real-time Customer Profile] overview](../../../profile/home.md)。
