---
title: 使用沙箱工具啟用卓越中心
description: 透過建立「黃金沙箱」套件，以標準化多個沙箱的最佳做法，使用沙箱工具啟用卓越中心。
source-git-commit: f0cbee2663682f0afae6d7e4b174f250fcb3df53
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 7%

---

# 使用沙箱工具啟用卓越中心

透過建立「黃金沙箱」套件，以標準化多個沙箱的最佳做法，使用沙箱工具啟用卓越中心。

![跨不同組織匯出套件的概觀](../images/use-cases/packages-across-orgs.png)

## 為何考慮此使用案例 {#why-this-use-case}

許多大型公司或企業針對不同的組織、團隊、地區或開發環境使用多個沙箱。 利用[沙箱工具](../ui/sandbox-tooling.md)的強大功能，您可以建立黃金沙箱套件，以確保多個沙箱之間組織標準的一致性、合規性和一致性。

此金色沙箱套件可建立卓越中心，以有效共用關鍵設定。 使用沙箱工具，您可以輕鬆地跨多個沙箱匯入套件。 您也可以將您的套件分享給其他組織，以確保廣泛的一致性。

請依照此使用案例中所述的步驟，建立您自己的Golden Sandbox套件。

## 行業範例 {#industry-example}

舉例來說，假設一家銀行橫跨北美、歐洲及非洲等不同地區營運。 每個市場或地區都有自己的Adobe Experience Platform例項。 這家銀行想要維持由全球架構師團隊管理的集中式資料模型，讓單一版本的資料模型能夠推廣到所有市場。

本銀行選擇運用沙箱工具來建立及維護黃金沙箱套件。 這有助於提高開發效率、允許一致的資料模型，並確保所有區域的一致性。

## 必要條件和規劃 {#prerequisites-and-planning}

當您計畫在組織內建立自己的卓越中心時，請在計畫處理中考慮下列必要條件：

- 識別要包含在套件中的最佳實務和設定。
- 建立沙箱，並包含所有將設定為黃金沙箱的相關和已驗證設定。
- 如有需要，請取得利害關係人的意見，並同意您的基準標準。

### 您將使用的 UI 功能、平台元件和 Experience Cloud 產品 {#ui-functionality-and-elements}

若要成功實作此使用案例，您必須使用Adobe Experience Platform的多個區域。 請確定您擁有這些區域所需的[屬性型存取控制許可權](../../access-control/abac/overview.md)，或要求系統管理員授與您必要的許可權。

- [沙箱工具](../ui/sandbox-tooling.md)
- [沙箱管理](../ui/user-guide.md)
- [資料集](../../catalog/datasets/overview.md)
- [結構描述](../../xdm//home.md)
- [客群](../../segmentation/home.md)
- 來自Adobe Journey Optimizer的[歷程](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

## 如何實現使用案例：高層級概觀 {#achieve-the-use-case-high-level}

1. 建立基線設定，代表您在Golden Sandbox中的最佳實務。 這可能包括資料集、結構描述、對象或歷程等物件。
2. 使用沙箱工具，將設定匯出至套件。
3. 將此套件匯入至所有相關沙箱。
4. 如果您有多個組織，請在您的組織間共用此套件。
5. 監控匯入和匯出，並透過稽核記錄追蹤變更。
6. 隨著標準的演化，定期更新您的黃金沙箱，確保所有沙箱符合最佳實務。

## 如何實現使用案例：逐步說明 {#step-by-step-instructions}

詳閱以下章節，其中包含指向更多文件的連結，以完成上述高層級概觀中的每個步驟。

### 建立您的黃金沙箱

啟用卓越中心的第一步，就是建立您的黃金沙箱。 此沙箱應包含代表您最佳實務的基準設定。 若要建立此Golden沙箱，請依照[在Experience Platform中建立新沙箱](../ui/user-guide.md#create-a-new-sandbox)的指南操作。

建立沙箱之後，請開始建立基準物件設定，例如[結構描述](../../xdm/ui/resources/schemas.md#create-a-new-schema)、[資料集](../../catalog/datasets/user-guide.md#create-a-dataset)或[對象](../../segmentation/ui/segment-builder.md)。 在繼續之前，請務必檢閱您的設定。

### 將沙箱匯出至套件

現在您的沙箱包含基準物件設定，您可以使用沙箱工具將其匯出到套件中。 請依照[匯出整個沙箱](../ui/sandbox-tooling.md#export-an-entire-sandbox)上的指南操作，以建立您的黃金沙箱套件。

### 將您的套件匯入相關的沙箱

現在您的封裝已建立，您可以將此封裝匯入您的相關沙箱。 最佳實務是將包含整個沙箱的套件匯入到空沙箱中。 使用沙箱工具，您可以輕鬆地將整個沙箱套件](../../sandboxes/ui/sandbox-tooling.md#import-the-entire-sandbox-package)直接匯入Experience Platform中的沙箱。[

### 跨組織共用套件

沙箱工具可讓您分享在不同組織間建立的套件。 依照[封裝共用指南](../../sandboxes/ui/sharing-packages-across-orgs.md)來共用您的Golden Sandbox封裝。

### 透過稽核記錄監控匯入和匯出

當您匯入或匯出套件時，可以使用Experience Platform中的&#x200B;**[!UICONTROL 工作]**&#x200B;儀表板來監視工作的狀態。 若要深入瞭解監視工作，請閱讀[監視匯入詳細資料](../../sandboxes/ui/sandbox-tooling.md#monitor-import-details)的指南。

### 定期更新黃金沙箱

現在您的Golden Sandbox套件已完成，您已建立標準化的卓越中心，您可以繼續匯入沙箱或跨組織共用。 隨著最佳實務的變更和開發，請務必定期更新金色沙箱中的基準物件設定。 當您更新沙箱時，可以依照此相同程式建立金色沙箱套件的新反複專案。

>[!NOTE]
>
> 上述步驟遵循Experience Platform使用者介面中的程式。 您可以透過各種端點使用API來遵循相同的步驟。 如需透過API提出每個要求的資訊，請參閱`sandboxes` [端點指南](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/api/sandboxes#create)和`packages` [端點指南](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages)。

## 其他透過合作夥伴資料支援封存的使用案例 {#other-use-cases}

進一步探索透過沙箱工具啟用的使用案例：

- [使用沙箱工具的備份物件設定](./backup-object-configuration.md)
