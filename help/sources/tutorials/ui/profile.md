---
keywords: Experience Platform；主題；熱門主題；激活入站資料；填充配置檔案；填充rtcp；填充的統一配置檔案
solution: Experience Platform
title: 激活入站源資料以在UI中填充客戶配置檔案
type: Tutorial
description: 來自源連接器的入站資料可用於豐富和填充即時客戶配置檔案資料。
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# 激活入站源資料以填充客戶配置檔案

來自源連接器的入站資料可用於豐富和填充 [!DNL Real-Time Customer Profile] 資料。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

- [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   - [架構組合的基礎](../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   - [架構編輯器教程](../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

此外，本教程要求您已建立並配置了源連接器。  有關在UI中建立不同連接器的教程清單，請參見 [源連接器概述](../../home.md)。

## 填充 [!DNL Real-Time Customer Profile] 資料

為了豐富客戶配置檔案，目標資料集的源架構必須相容，以便在 [!DNL Real-Time Customer Profile]。 相容架構滿足以下要求：

- 架構至少有一個屬性指定為標識屬性。
- 架構具有定義為主標識的標識屬性。
- 資料流記憶體在映射，其中主標識是目標屬性。

在「源」工作區中，按一下 **[!UICONTROL 瀏覽]** 按鈕。 在顯示的清單中，查找包含要用填充配置檔案的資料流的連接。 按一下連接的名稱以訪問其詳細資訊。

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

連接 **[!UICONTROL 源活動]** 螢幕，顯示連接正在將源資料插入的資料集。 按一下要為其啟用的資料集的名稱 [!DNL Profile]。

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

的 **[!UICONTROL 資料集活動]** 的上界。 的 **[!UICONTROL 屬性]** 螢幕右側的列顯示資料集的詳細資訊，並包括 **[!UICONTROL 配置檔案]** 切換和指向資料集所遵守的模式的連結。 按一下架構的名稱以查看其組成。

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

的 **[!UICONTROL 架構編輯器]** 顯示中心畫布中架構的結構。 在畫布中，選擇要設定為主標識的欄位。 在 **[!UICONTROL 欄位屬性]** 頁籤，選擇 **[!UICONTROL 身份]** 複選框 **[!UICONTROL 主標識]**。 最後，選擇適當的 **[!UICONTROL 標識命名空間]**，然後按一下 **[!UICONTROL 應用]**。

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

按一下架構結構的頂級對象， **[!UICONTROL 架構屬性]** 的雙曲餘切值。 為 [!DNL Profile] 通過切換 **[!UICONTROL 配置檔案]** 按鈕 按一下 **[!UICONTROL 保存]** 完成更改。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

現在，已為 [!DNL Profile]，返回 **[!UICONTROL 資料集活動]** 螢幕和啟用資料集 [!DNL Profile] 按一下 **[!UICONTROL 配置檔案]** 在 **[!UICONTROL 屬性]** 的雙曲餘切值。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

同時啟用架構和資料集 [!DNL Profile]，現在將接收到該資料集的資料也填充客戶配置檔案。

>[!NOTE]
>
>最近啟用的資料集中的現有資料不由 [!DNL Profile]。

## 後續步驟

按照本教程，您已成功激活了 [!DNL Profile] 人口。 有關詳細資訊，請參見 [[!DNL Real-Time Customer Profile] 概述](../../../profile/home.md)。
