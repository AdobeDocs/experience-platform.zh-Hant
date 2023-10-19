---
title: 刪除記錄
description: 瞭解如何刪除Adobe Experience Platform UI中的記錄。
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 6e97b3a6b3830cf88802a8dd89944b6ce8791f02
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 8%

---

# [!BADGE 測試版]{type=Informative}刪除記錄 {#record-delete}

使用 [[!UICONTROL 資料生命週期] 工作區](./overview.md) 根據主要身分刪除Adobe Experience Platform中的記錄。 這些記錄可以與個別消費者或包含在身分圖表中的任何其他實體繫結。

>[!IMPORTANT]
> 
>記錄刪除功能目前在Beta版中提供，且僅適用於 **限量發行**. 並非所有客戶都可使用。 記錄刪除請求僅適用於有限版本中的組織。
> 
> 
>記錄刪除旨在用於資料清理、匿名資料移除或資料最小化。 它們是 **非** 用於資料主體權利要求（法規遵循），如一般資料保護規範(GDPR)等隱私權法規。 對於所有合規性使用案例，請使用 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 而非。

## 先決條件 {#prerequisites}

刪除記錄需要實際瞭解身分欄位在Experience Platform中的運作方式。 具體來說，您必須知道要刪除其記錄之實體的主要身分值，視您要從中刪除這些記錄的資料集（或資料集）而定。

請參閱下列檔案，以取得有關Platform中身分的詳細資訊：

* [Adobe Experience Platform Identity服務](../../identity-service/home.md)：跨裝置和系統橋接身分，根據資料集符合的XDM結構描述所定義的身分欄位將其連結在一起。
* [身分名稱空間](../../identity-service/namespaces.md)：身分名稱空間會定義與單一人員相關的不同型別的身分資訊，且是每個身分欄位的必要元件。
* [即時客戶個人檔案](../../profile/home.md)：使用身分圖表，根據來自多個來源的彙總資料提供統一的消費者個人檔案，並近乎即時更新。
* [體驗資料模型(XDM)](../../xdm/home.md)：透過使用結構描述，提供Platform資料的標準定義和結構。 所有Platform資料集都符合特定的XDM結構描述，而結構描述會定義哪些欄位是身分。
* [身分欄位](../../xdm/ui/fields/identity.md)：瞭解身分欄位如何在XDM結構描述中定義。

## 建立請求 {#create-request}

若要啟動程式，請選取 **[!UICONTROL 資料生命週期]** （在Platform UI的左側導覽器中）。 此 [!UICONTROL 資料生命週期請求] 工作區隨即顯示。 接下來，選取 **[!UICONTROL 建立請求]** 從工作區的主要頁面。

![此 [!UICONTROL 資料生命週期請求] 工作區，使用 [!UICONTROL 建立請求] 已選取。](../images/ui/record-delete/create-request-button.png)

此時會出現請求建立工作流程。 根據預設， **[!UICONTROL 刪除記錄]** 已選取「 」選項中的 **[!UICONTROL 請求的動作]** 區段。 保留選取此選項。

>[!IMPORTANT]
> 
>為了提高效率並降低資料集作業成本，進行中的變更包括，已移至Delta格式的組織可從Identity Service、即時客戶設定檔和資料湖中刪除資料。 此型別的使用者稱為差異移轉使用者。 已進行差異移轉的組織之使用者，可選擇從單一或所有資料集中刪除記錄。 來自尚未進行差異移轉之組織的使用者，無法選擇從單一或所有資料集中刪除記錄，如下圖所示。 在此情況下，請繼續執行 [提供身分](#provide-identities) 部分。

![使用的請求建立工作流程 [!UICONTROL 刪除記錄] 選項已選取並反白顯示。](../images/ui/record-delete/delete-record.png)

## 選取資料集 {#select-dataset}

下一步是決定您要從單一資料集還是所有資料集中刪除記錄。 如果您無法使用此選項，請繼續瀏覽 [提供身分](#provide-identities) 部分。

在 **[!UICONTROL 記錄詳細資料]** 區段，使用選項按鈕在特定資料集和所有資料集之間選取。 如果您選擇 **[!UICONTROL 選取資料集]**，繼續選取資料庫圖示(![資料庫圖示](../images/ui/record-delete/database-icon.png))以開啟提供可用資料集清單的對話方塊。 從清單中選取所需的資料集，然後按一下 **[!UICONTROL 完成]**.

![此 [!UICONTROL 選取資料集] 對話方塊，其中已選取資料集並 [!UICONTROL 完成] 反白顯示。](../images/ui/record-delete/select-dataset.png)

如果您想要刪除所有資料集中的記錄，請選取 **[!UICONTROL 所有資料集]**.

![此 [!UICONTROL 選取資料集] 對話方塊 [!UICONTROL 所有資料集] 已選取選項。](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>選取 **[!UICONTROL 所有資料集]** 選項可能會導致刪除操作花費更長的時間，並且可能不會導致準確的記錄刪除。

## 提供身分 {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="主要身分識別"
>abstract="主要身分識別指將記錄和 Experience Platform 中的消費者設定檔繫結的屬性。資料集的主要身分識別欄位由資料集建立基礎的方案定義。在此欄中，您必須提供記錄的主要身分識別的類型 (或命名空間)，例如用於電子郵件地址的 `email`，以及用於 Experience Cloud ID 的 `ecid`。若要了解詳細資訊，請查看「資料生命週期 UI 指南」。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="身分識別值"
>abstract="在此欄中，您必須提供記錄的主要身分識別的值，該值必須和左欄中提供的身分識別類型相對應。如果主要身分識別類型是 `email`，則該值應該是記錄的電子郵件地址。若要了解詳細資訊，請查看「資料生命週期 UI 指南」。"

刪除記錄時，您必須提供身分資訊，讓系統能夠決定要刪除哪些記錄。 對於Platform中的任何資料集，記錄會根據 **主要身分** 由資料集結構描述定義的欄位。

和Platform中的所有身分欄位一樣，主要身分也由兩部分組成： **type** （有時稱為身分名稱空間）和 **值**. 身分型別提供欄位如何識別記錄的上下文（例如電子郵件地址），值代表該型別記錄的特定身分(例如， `jdoe@example.com` 針對 `email` 身分型別)。 做為身分識別的常見欄位包括帳戶資訊、裝置ID和Cookie ID。

>[!TIP]
>
>如果您不知道特定資料集的主要身分，可以在Platform UI中找到。 在 **[!UICONTROL 資料集]** 從工作區中，選取有問題的資料集。 在資料集的詳細資訊頁面上，將滑鼠移至右側邊欄中資料集的結構描述名稱上。 主要身分會與結構描述名稱和說明一起顯示。
>
>![資料集控制面板，已選取資料集，並從資料集詳細資料面板開啟結構描述對話方塊。 資料集的主要ID會反白顯示。](../images/ui/record-delete/dataset-primary-identity.png)

如果您要從單一資料集中刪除記錄，您提供的所有身分都必須有相同的型別，因為資料集只能有一個主要身分。 如果您要從所有資料集中刪除，則可以包含多個身分型別，因為不同的資料集可能具有不同的主要身分。

刪除記錄時，有兩個選項可提供身分識別：

* [上傳JSON檔案](#upload-json)
* [手動輸入身分值](#manual-identity)

### 上傳JSON檔案 {#upload-json}

若要上傳JSON檔案，您可以將檔案拖放至提供的區域，或選取 **[!UICONTROL 選擇檔案]** 瀏覽並從您的本機目錄中選取。

![要求建立工作流程中，針對上傳JSON檔案的選擇檔案和拖放介面已反白顯示。](../images/ui/record-delete/upload-json.png)

JSON檔案必須格式化為物件陣列，每個物件代表一個身分。

```json
[
  {
    "namespaceCode": "email",
    "value": "jdoe@example.com"
  },
  {
    "namespaceCode": "email",
    "value": "san.gray@example.com"
  }
]
```

| 屬性 | 說明 |
| --- | --- |
| `namespaceCode` | 身分型別。 |
| `value` | 型別所表示的身分值。 |

上傳檔案後，您可以繼續 [提交請求](#submit).

### 手動輸入身分 {#manual-identity}

若要手動輸入身分，請選取 **[!UICONTROL 新增身分]**.

![使用的請求建立工作流程 [!UICONTROL 新增身分] 選項會醒目提示。](../images/ui/record-delete/add-identity.png)

顯示的控制項可讓您一次輸入一個身分。 在 **[!UICONTROL 主要身分]**，使用下拉式選單來選取身分型別。 在 **[!UICONTROL 身分值]**，提供記錄的主要身分值。

![已手動新增包含身分欄位的請求建立工作流程。](../images/ui/record-delete/identity-added.png)

若要新增更多身分，請選取加號圖示(![加號圖示。](../images/ui/record-delete/plus-icon.png))或選取 **[!UICONTROL 新增身分]**.

![要求建立工作流程中，會以加號圖示及新增身分圖示強調顯示。](../images/ui/record-delete/more-identities.png)

## 提交請求 {#submit}

當您完成新增身分到請求時，請在底下 **[!UICONTROL 請求設定]**，在選取之前提供請求的名稱和選擇性說明 **[!UICONTROL 提交]**.

>[!IMPORTANT]
> 
>每個月可提交的不重複身分記錄刪除總數有不同的限制。 這些限制是以您的授權合約為基礎。 已購買Adobe Real-time Customer Data Platform和Adobe Journey Optimizer所有版本的組織，每個月最多可提交100,000筆身分記錄刪除。 已購買的組織 **AdobeHealthcare Shield** 或 **Adobe隱私權與安全防護板** 每月最多可提交600,000筆身分記錄刪除。<br>透過UI的單一記錄刪除請求可讓您一次提交10,000個ID。 此 [刪除記錄的API方法](../api/workorder.md#create) 允許一次提交100,000個ID。<br>最佳實務是每個請求提交儘可能多的ID，以您的ID限製為上限。 當您要刪除大量ID時，應避擴音交小量ID或每個記錄刪除請求使用一個單一ID。

![請求設定的 [!UICONTROL 名稱] 和 [!UICONTROL 說明] 欄位和 [!UICONTROL 提交] 反白顯示。](../images/ui/record-delete/submit.png)

A [!UICONTROL 確認請求] 對話方塊似乎表示身分在刪除後就無法復原。 選取 **[!UICONTROL 提交]** 以確認您要刪除其資料的身分清單。

![此 [!UICONTROL 確認請求] 對話方塊。](../images/ui/record-delete/confirm-request.png)

提交請求後，即會建立工單並顯示在 [!UICONTROL 記錄] 的標籤 [!UICONTROL 資料生命週期] 工作區。 從這裡，您可以在工單處理請求時監視工單的狀態。

>[!NOTE]
>
>請參閱的概觀區段： [時間軸和透明度](../home.md#record-delete-transparency) 以瞭解記錄刪除執行後如何處理的詳細資訊。

![此 [!UICONTROL 記錄] 的標籤 [!UICONTROL 資料生命週期] 工作區中醒目提示新請求。](../images/ui/record-delete/request-log.png)

## 後續步驟

本檔案說明如何刪除Experience Platform UI中的記錄。 有關如何在UI中執行其他資料生命週期管理任務的資訊，請參閱 [資料生命週期UI總覽](./overview.md).

若要瞭解如何使用資料衛生API刪除記錄，請參閱 [工單端點指南](../api/workorder.md).
