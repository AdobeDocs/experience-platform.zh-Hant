---
title: 即時CDP B2B版的分段使用案例
description: 概述各種可用的即時CDP B2B版使用案例。
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: 6a108a0bfde3c8f44c1a1221b06581f0f69b5203
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---

# Real-time Customer Data PlatformB2B版的切分用例

本文檔提供了即時CDP B2B版中段定義的示例，以及如何針對常見的B2B使用情形組合不同類型的屬性。 要瞭解目標在B2B工作流中的適應性，請參閱 [端到端教程](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data)。

>[!NOTE]
>
>這些細分使用案例所需的屬性僅對Real-time Customer Data PlatformB2B版客戶可用。 如果您未使用Real-time Customer Data PlatformB2B版，請參閱 [分段概述](./segmentation-overview.md) 的雙曲餘切值。

## 先決條件 {#prerequisites}

在為B2B類使用分段屬性之前，必須完成以下步驟：

1. 建立使用B2B類的架構。 B2B版本類包括Account 、 Campaign 、 Opportunity 、 Marketing List等。 有關 [如何設定用於B2B類的架構](../schemas/b2b.md) 請參閱架構文檔。
1. 在體驗資料模型(XDM)B2B架構之間建立關係。 基於B2B版本屬性的段要求類之間的關係才能充分利用擴展的B2B分段功能。 請參閱 [如何定義兩個B2B架構之間的關係](../../xdm/tutorials/relationship-b2b.md) 的子菜單。
1. 使用基於B2B架構的資料集來接收資料。 請參閱的源文檔 [關於如何攝取資料的資訊](../../sources/connectors/adobe-applications/marketo/marketo.md)。
1. 閱讀 [段生成器使用手冊](../../segmentation/ui/segment-builder.md) 獲取有關如何構建段的更詳細的指導。

滿足這些要求後，您就可以將這些屬性組合用於常見的B2B使用情形。

## 快速入門 {#getting-started}

一旦B2B類的聯合架構建立了關係並已用於接收資料，它們的屬性就可以在段生成器的左滑軌中使用。

B2B類及其屬性附加有 `B2B` 「分段」工作區中的標籤，以區別於Real-time Customer Data Platform中的標準。

為了有效地為B2B使用情形建立段，必須深入瞭解模式並瞭解資料模型的外觀。 瞭解資料從一個資料對象到另一個資料對象的路徑也很有用。

下圖說明了即時CDP B2B版中可用的B2B類之間的關係。

![B2B類ERD](../assets/segmentation/b2b-classes.png)

由於資料模型可能很複雜，因此您可以使用平台UI查看資料模型的更詳細的可視表示形式，以幫助查找用例的相關屬性。 要啟動，請轉到平台UI並在左側導航中選擇架構。

從可用清單中選擇相應的架構，然後從 [!UICONTROL 組合] 側軌。 在以下示例中，選擇「人員」關係可顯示當前架構中引用相關「人員」架構（如果它是關係中的源架構）的屬性，或者「人員」架構引用的屬性（如果它是關係中的目標架構）。

![source-key示例在架構工作區中使用people關係](../assets/segmentation/source-key-schema-relationship-example.png)

此關係通過使用 `Key` 資料夾，如下圖所示。

![source-key在分段工作區中使用段生成器的示例](../assets/segmentation/source-key-segmentation-example.png)

請參閱 [Real-time Customer Data PlatformB2B版文檔中的架構](../schemas/b2b.md) 的子菜單。

下面的使用案例提供了有關哪些類用於建立不同架構之間的關係以實現這些結果的資訊。 這些示例可幫助您建立自己的段。

## 不同分段使用案例的示例 {#use-cases}

以下使用案例可用於B2B版的分段。 每個示例都提供段的操作說明以及用於建立段的類的說明。 提供的影像突出顯示 [!UICONTROL 屬性] 反映架構結構的側軌。 的 [!UICONTROL 段屬性] 顯示右側的部分包含段屬性的書面細分。

### 示例1:為B2B機會尋找「決策者」 {#find-decision-maker}

找到所有機會的「決策者」。 此段要求在 [!UICONTROL XDM個人配置檔案] 類和 [!UICONTROL XDM業務機會人員關係] 類。

![顯示示例1設定的UI](../assets/segmentation/example-1.png)

### 示例2:查找分配給業務機會的B2B配置檔案，金額超過一定 {#find-opportunities-amount}

查找直接分配給任何業務機會且業務機會金額大於指定金額（100萬美元）的所有人員。 此段要求在 [!UICONTROL XDM個人配置檔案] 類， [!UICONTROL XDM業務機會人員關係] 類和 [!UICONTROL XDM業務機會] 類。

![顯示示例2設定的UI](../assets/segmentation/example-2.png)

### 示例3:按地點查找分配給業務機會的B2B配置檔案 {#find-opportunities-location}

查找直接分配給帳戶位於指定位置的任何業務機會的所有人員（加拿大）。 此段要求在 [!UICONTROL XDM個人配置檔案] 類， [!UICONTROL XDM業務機會人員關係] 類， [!UICONTROL XDM業務機會] 類和 [!UICONTROL XDM業務客戶] 類。

![顯示示例3設定的UI](../assets/segmentation/example-3.png)

### 示例4:按行業和瀏覽行為查找機會的「決策者」 {#find-industry-browsing-behavior}

查找客戶在「金融」行業中的任何機會的「決策者」，並在最近三天訪問了定價頁。 此段要求在 [!UICONTROL XDM個人配置檔案] 類， [!UICONTROL XDM業務機會人員關係] 類， [!UICONTROL XDM業務機會] 類和 [!UICONTROL XDM業務客戶] 類和 [!UICONTROL XDM體驗事件] 類。

![顯示示例4設定的UI](../assets/segmentation/example-4.png)

### 示例5:按部門名稱和業務機會金額查找業務機會的B2B配置檔案 {#find-department-opportunity-amount}

查找在人力資源(HR)部門工作且與任何帳戶相關的所有人員，這些帳戶至少有一個價值指定金額（100萬美元）或更多的未結機會。 此段要求在 [!UICONTROL XDM個人配置檔案] 類， [!UICONTROL XDM業務客戶] 類和 [!UICONTROL XDM業務機會] 類。

![顯示示例5設定的UI](../assets/segmentation/example-5.png)

### 示例6:按職務和年度帳戶收入查找B2B配置檔案 {#find-by-job-title-and-revenue}

查找其職務為副總裁且與任何年收入達指定金額（1億美元）或以上且在上個月至少訪問過3次定價頁的帳戶相關的所有人員。 此段要求在 [!UICONTROL XDM個人配置檔案] 類， [!UICONTROL XDM業務客戶] 類和 [!UICONTROL XDM體驗事件] 類。

![顯示示例6設定的UI](../assets/segmentation/example-6.png)

### 示例7:按機會狀態和瀏覽行為查找「決策者」 {#find-by-opportunity-status-and-browsing-behavior}

查找所有作為任何已關閉的丟失機會的「決策者」的人員，並在上週訪問了定價頁。 此段要求在 [!UICONTROL XDM個人配置檔案] 類， [!UICONTROL XDM業務機會人員關係] 類， [!UICONTROL XDM業務機會] 類和 [!UICONTROL XDM體驗事件] 類。

![顯示示例7設定的UI](../assets/segmentation/example-7.png)

### 示例8:使用相關帳戶擴展細分範圍 {#related-accounts}

查找在人力資源(HR)部門工作且與任何帳戶相關的所有人員 *或者任何一個賬戶的相關賬戶* 至少有一次機會，價值達到規定數額（100萬美元）或以上。 此段要求在 [!UICONTROL XDM個人配置檔案] 類， [!UICONTROL XDM業務客戶] 類和 [!UICONTROL XDM業務機會] 類。

![顯示相關帳戶的分段的UI](../assets/segmentation/segmentation-related-accounts.png)

## 後續步驟 {#next-steps}

在閱讀此概述後，您現在瞭解了使用即時CDP B2B Edition提供的分段可能性。 有關分段服務的詳細資訊，請閱讀 [分段文檔](../../segmentation/home.md)。
