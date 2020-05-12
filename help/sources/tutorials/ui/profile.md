---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 啟用傳入來源資料以填入客戶個人檔案
topic: overview
translation-type: tm+mt
source-git-commit: 3e43e043df296c29cafb4c6933c8be1105c985ab
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# 啟用傳入來源資料以填入客戶個人檔案

來自來源連接器的傳入資料可用於豐富和填入即時客戶個人檔案資料。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [體驗資料模型(XDM)系統](../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   - [架構構成基礎](../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
- [即時客戶個人檔案](../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

此外，本教學課程要求您已建立並設定來源連接器。  如需在UI中建立不同連接器的教學課程清單，請參閱來源連 [接器概觀](../../home.md)。

## 填入您的即時客戶個人檔案資料

為了豐富客戶個人檔案，目標資料集的來源結構必須相容，才能用於即時客戶個人檔案。 相容的架構符合下列需求：

- 架構至少有一個屬性指定為標識屬性。
- 架構具有定義為主標識的身份屬性。
- 資料流記憶體在映射，其中主標識是目標屬性。

在「來源」工作區中，按一下「 **瀏覽** 」標籤以列出您的基本連線。 在顯示的清單中，查找包含要填充配置檔案的資料流的連接。 按一下連接的名稱以訪問其詳細資訊。

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

此時將顯示連 *接的「源」活動* 螢幕，顯示連接正在將源資料收錄到的資料集。 按一下您要啟用描述檔的資料集名稱。

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

此時會 *顯示「資料集* 」活動畫面。 畫面 *右側的***** 「屬性」欄會顯示資料集的詳細資料，並包含「描述檔」切換器和資料集所遵守之架構的連結。 按一下架構的名稱可查看其構成。

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

此時 *會出現* 「架構編輯器」，在中央畫布中顯示架構的結構。 在畫布中，選取要設為主要身分的欄位。 在出現的 *欄位屬性* (Field properties **)標籤下，選取「** Identity **」核取方塊，然後選取「** Primary identity」。 最後，選取適當的 **Identity命名空間**，然後按一下 **套用**。

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

按一下方案結構的頂級對象，並顯示「方 *案屬性* 」列。 通過切換配置式交換機為配置式啟 **用** 架構。 按一 **下「儲存** 」以完成變更。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

現在已為Profile啟用架構，請返回 *Dataset活動螢幕，並通過按一下Properties（屬性）列中的* Profile **（配置檔案）切換來啟用Profile（配置檔案）的** 資料集 ** 。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

在「描述檔」啟用架構和資料集後，該資料集中的資料現在也會填入客戶描述檔。

>[!NOTE] 描述檔不會使用最近啟用的資料集內的現有資料

## 後續步驟

遵循本教學課程，您已成功啟用描述檔填入的傳入資料。 如需詳細資訊，請參 [閱即時客戶個人檔案總覽](../../../profile/home.md)。