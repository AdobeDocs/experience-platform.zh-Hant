---
title: Real-time CDP B2B Edition的細分使用案例
description: 概述各種可用的即時CDP B2B Edition使用案例。
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: 9bd7434f2b224d76decac1e04d8491a6b3149a3a
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 1%

---

# Real-time Customer Data Platform B2B版的區段使用案例

本檔案提供即時CDP B2B Edition中區段定義的範例，以及如何針對常見B2B使用案例結合不同類型的屬性。 若要了解目的地與B2B工作流程有何不同，請參閱 [端對端教學課程](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>這些區段使用案例所需的屬性僅供Real-time Customer Data Platform B2B Edition客戶使用。 如果您未使用Real-time Customer Data Platform B2B Edition，請參閱 [細分概述](./segmentation-overview.md) 。

## 先決條件

您必須先完成下列步驟，才能使用B2B類別的分段屬性：

1. 建立使用B2B類的結構。 B2B版本類包括帳戶、促銷活動、機會、行銷清單等。 如需 [如何設定結構以用於B2B類](../schemas/b2b.md) 請參閱架構檔案。
1. 建立Experience Data Model(XDM)B2B結構之間的關係。 基於B2B版屬性的區段需要類別之間的關係，才能充分使用延伸的B2B分段功能。 請參閱 [如何定義兩個B2B架構之間的關係](../../xdm/tutorials/relationship-b2b.md) 以取得更多資訊。
1. 根據您的B2B結構使用資料集內嵌資料。 請參閱 [如何內嵌資料的資訊](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. 閱讀 [區段產生器使用手冊](../../segmentation/ui/segment-builder.md) 以取得如何建立區段的詳細指引。

滿足這些需求後，您就能針對常見的B2B使用案例結合這些屬性。

## 快速入門

一旦B2B類別的聯合結構建立關係並用於內嵌資料後，其屬性即可在區段產生器的左側邊欄中使用。

B2B類及其屬性會附加 `B2B` 標籤，以區別於Real-time Customer Data Platform中以標準形式提供的標籤。

為了有效建立B2B使用案例的區段，請務必熟悉結構，並了解資料模型的外觀。 另外，您也應留意資料從一個資料物件取往另一個資料物件的路徑。

下圖說明了Real-time CDP B2B Edition中可用的B2B類之間的關係。

![B2B類ERD](../assets/segmentation/b2b-classes.png)

由於您的資料模型可能很複雜，因此您可以使用Platform UI來檢視資料模型的更詳細視覺化呈現，以協助您找到使用案例的相關屬性。 若要開始，請前往Platform UI，然後選取左側導覽中的結構描述。

從可用清單中選擇適當的架構，然後從 [!UICONTROL 組合物] 側邊欄。 在以下示例中，選擇「人員」關係將顯示當前架構中引用相關「人員」架構的屬性（如果它是關係中的源架構），或者由「人員」架構引用（如果它是關係中的目標架構）。

![schema workspace中使用人員關係的來源索引鍵範例](../assets/segmentation/source-key-schema-relationship-example.png)

此關係會透過使用 `Key` 資料夾，如下圖所示。

![來源索引鍵範例，在區段工作區中使用區段產生器](../assets/segmentation/source-key-segmentation-example.png)

請參閱 [Real-time Customer Data Platform B2B版檔案的綱要](../schemas/b2b.md) 以取得可用B2B類別的詳細資訊。

下面的使用案例提供了資訊，說明使用哪些類來建立不同架構之間的關係，以實現這些結果。 這些範例可協助您建立自己的區段。

## 不同使用案例的範例

下列使用案例適用於B2B版的分段。 每個範例都提供區段功能的說明，以及用來建立區段的類別說明。 提供的影像會反白標示 [!UICONTROL 屬性] 會反映架構結構的側邊欄。 此 [!UICONTROL 區段屬性] 顯示右側的區段包含區段屬性的書面劃分。

### 範例 1

找到所有作為任何機會的「決策者」的人。 此區段需要 [!UICONTROL XDM個別設定檔] 類別和 [!UICONTROL XDM商機人員關係] 類別。

![顯示示例1設定的UI](../assets/segmentation/example-1.png)

### 範例 2

查找直接分配給任何業務機會的所有人員，其業務機會金額超過給定金額（100萬美元）。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商機人員關係] 類別，和 [!UICONTROL XDM業務機會] 類別。

![顯示示例2設定的UI](../assets/segmentation/example-2.png)

### 範例 3

查找直接分配給帳戶位於指定位置的任何業務機會的所有人員（加拿大）。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商機人員關係] 類別， [!UICONTROL XDM業務機會] 類別，和 [!UICONTROL XDM商業帳戶] 類別。

![顯示示例3設定的UI](../assets/segmentation/example-3.png)

### 範例 4

查找所有作為「決策者」的人員，了解客戶所在的「金融」行業中的任何機會，並在過去三天內訪問了定價頁。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商機人員關係] 類別， [!UICONTROL XDM業務機會] 類別，和 [!UICONTROL XDM商業帳戶] 類別，和 [!UICONTROL XDM ExperienceEvent] 類別。

![顯示示例4設定的UI](../assets/segmentation/example-4.png)

### 範例 5

查找所有在人力資源部(HR)工作的人員，這些人員與任何具有至少一個價值給定金額（100萬美元）或更多的開放機會的帳戶相關。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商業帳戶] 類別，和 [!UICONTROL XDM業務機會] 類別。

![顯示示例5設定的UI](../assets/segmentation/example-5.png)

### 範例 6

查找其職稱為副總裁且與任何年收入達指定金額（1億美元）或以上的帳戶相關的所有人員，並在上個月至少訪問過定價頁面3次。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商業帳戶] 類別，和 [!UICONTROL XDM ExperienceEvent] 類別。

![顯示示例6設定的UI](../assets/segmentation/example-6.png)

### 範例 7

查找所有作為任何已關閉的銷售機會的「決策者」，並在上週訪問了定價頁。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商機人員關係] 類別， [!UICONTROL XDM業務機會] 類別，和 [!UICONTROL XDM ExperienceEvent] 類別。

![顯示示例7設定的UI](../assets/segmentation/example-7.png)

## 後續步驟

閱讀本概述後，您現在已了解使用即時CDP B2B Edition可提供的分段可能性。 如需分段服務的詳細資訊，請參閱 [區段檔案](../../segmentation/home.md).
