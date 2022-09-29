---
title: 刪除消費者記錄
description: 了解如何在Adobe Experience Platform UI中刪除消費者記錄。
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: e4cc78591d0d3b4abd660956b1263092697d63d5
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 0%

---

# 刪除消費者記錄

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料衛生功能目前僅適用於已購買AdobeHealthcare Shield或Privacy Shield的組織。

此 [[!UICONTROL 資料衛生] 工作區](./overview.md) 在Adobe Experience Platform UI中，您可以刪除參與Identity Service和即時客戶設定檔的消費者記錄。

## 先決條件

刪除消費者記錄需要認真了解身分欄位在Experience Platform中的運作方式。 具體來說，您必須知道要刪除其記錄的使用者的主要身分值，具體取決於您要從中刪除的資料集（或資料集）。

如需Platform中身分識別的詳細資訊，請參閱下列檔案：

* [Adobe Experience Platform Identity Service](../../identity-service/home.md):橋接跨裝置和系統的身分，根據資料集所遵循的XDM結構所定義的身分欄位，將資料集連結在一起。
   * [身分識別命名空間](../../identity-service/namespaces.md):身分識別命名空間會定義可與單一人員相關的不同身分資訊類型，且是每個身分欄位的必要元件。
* [即時客戶個人檔案](../../profile/home.md):利用消費者身分圖表，根據來自多個來源的匯總資料提供統一的消費者設定檔，且幾乎即時更新。
* [Experience Data Model(XDM)](../../xdm/home.md):透過使用結構，提供Platform資料的標準定義和結構。 所有Platform資料集都符合特定XDM結構，且結構會定義哪些欄位為身分。
   * [身分欄位](../../xdm/ui/fields/identity.md):了解如何在XDM架構中定義身分欄位。

## 建立新請求

要啟動進程，請選擇 **[!UICONTROL 建立請求]** 從工作區的主要頁面。

![顯示 [!UICONTROL 建立請求] 按鈕](../images/ui/delete-consumer/create-request-button.png)

請求建立對話方塊隨即顯示。 依預設， **[!UICONTROL 消費者]** 選項 **[!UICONTROL 請求的操作]** 區段。 保留此選項。

![顯示在建立對話方塊中選取的使用者選項的影像](../images/ui/delete-consumer/consumer-action.png)

## 選取資料集

在 **[!UICONTROL 消費者詳細資訊]** 區段，下一步是決定要從單一資料集或所有資料集中刪除消費者資料。

如果您選擇 **[!UICONTROL 選取資料集]**，請選取資料庫圖示(![資料庫表徵圖的影像](../images/ui/delete-consumer/database-icon.png))，此時會出現對話方塊，讓您從清單中選取所需的資料集。

![顯示資料集選取對話方塊的影像](../images/ui/delete-consumer/select-dataset.png)

如果要從所有資料集中刪除消費者資料，請選擇 **[!UICONTROL 所有資料集]**.

![顯示 [!UICONTROL 所有資料集] 已選取](../images/ui/delete-consumer/all-datasets.png)

>[!NOTE]
>
>選取 **[!UICONTROL 所有資料集]** 選項可能會導致刪除操作花費更長時間，並且可能不會導致正確刪除記錄。

## 提供消費者身分識別 {#provide-consumer-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="主要身分"
>abstract="主要身分是將記錄系結至Experience Platform中消費者設定檔的屬性。 資料集的主要身分欄位由資料集所依據的結構所定義。 在此欄中，您必須提供消費者主要身分的類型（或命名空間），例如 `email` 對於電子郵件地址和 `ecid` Experience CloudID。 若要進一步了解，請參閱資料衛生UI指南。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="身分值"
>abstract="在此欄中，您必須提供消費者主要身分的值，其必須與左欄中提供的身分類型相對應。 如果主要身分類型為 `email`，值應為消費者的電子郵件地址。 若要進一步了解，請參閱資料衛生UI指南。"

刪除消費者資料時，您必須提供身分資訊，以便系統能夠確定必須刪除哪些記錄。 若是Platform中的任何資料集，記錄會根據 **主要身分** 由資料集結構定義的欄位。

與Platform中的所有身分欄位一樣，主要身分由兩部分組成：a **type** （有時稱為身分命名空間）和 **value**. 身分類型提供欄位識別消費者的方式（例如電子郵件地址）的內容，而值代表該類型的消費者特定身分(例如， `jdoe@example.com` 針對 `email` 身分類型)。  用作身分的常見欄位包括帳戶資訊、裝置ID和Cookie ID。

>[!TIP]
>
>如果您不知道特定資料集的主要身分，可在Platform UI中找到。 在 **[!UICONTROL 資料集]** 工作區中，從清單中選取相關資料集。 在資料集的詳細資訊頁面上，將滑鼠移至右側邊欄中資料集結構名稱的上方。 主要身分會與架構名稱和說明一併顯示。
>
>![影像，顯示UI中強調顯示之資料集的主要身分](../images/ui/delete-consumer/dataset-primary-identity.png)

如果您從單一資料集刪除消費者記錄，您提供的所有身分識別都必須有相同的類型，因為資料集只能有一個主要身分識別。 如果您要從所有資料集刪除，可以包含多個身分類型，因為不同的資料集可能具有不同的主要身分。

刪除消費者記錄時，有兩個選項可提供消費者身分識別：

* [上傳JSON檔案](#upload-json)
* [手動輸入身分值](#manual-identity)

### 上傳JSON檔案 {#upload-json}

若要上傳JSON檔案，您可以將檔案拖放至提供區域，或選取 **[!UICONTROL 選擇檔案]** 瀏覽並從本地目錄中選擇。

![影像，顯示在UI中上傳JSON的方法](../images/ui/delete-consumer/upload-json.png)

JSON檔案必須格式化為物件陣列，每個物件都代表消費者身分。

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
| `namespaceCode` | 身分類型。 |
| `value` | 消費者的身分，如類型所表示。 |

上傳檔案後，您可以繼續 [提交請求](#submit).

### 手動輸入身分 {#manual-identity}

若要手動輸入身分，請選取 **[!UICONTROL 新增身分]**.

![顯示 [!UICONTROL 新增身分] 按鈕](../images/ui/delete-consumer/add-identity.png)

控制項可讓您一次輸入一個消費者身分。 在 **[!UICONTROL 主要身分]**，請使用下拉式功能表來選取身分類型。 在 **[!UICONTROL 身分值]**，提供消費者的主要身分值。

![顯示手動新增身分欄位的影像](../images/ui/delete-consumer/identity-added.png)

若要新增更多身分，請選取加號圖示(![加號圖示的影像](../images/ui/delete-consumer/plus-icon.png))，或選取 **[!UICONTROL 新增身分]**.

![影像，顯示如何新增更多身分至請求](../images/ui/delete-consumer/more-identities.png)

## 提交請求(#submit)

在您完成將身分新增至請求後，請在 **[!UICONTROL 請求設定]**，請在選取 **[!UICONTROL 提交]**.

![顯示 [!UICONTROL 提交] 按鈕](../images/ui/delete-consumer/submit.png)

系統會要求您確認您要刪除其資料的身分識別清單。 選擇 **[!UICONTROL 提交]** 以確認您的選取。

![顯示確認對話框的影像](../images/ui/delete-consumer/confirm-request.png)

提交請求後，會建立工作單並顯示在 [!UICONTROL 消費者] 的 [!UICONTROL 資料衛生] 工作區。 在此處，您可以在工作單處理請求時監控其狀態。

>[!NOTE]
>
>請參閱以下的概觀區段： [時間表和透明度](../home.md#consumer-delete-transparency) 有關執行消費者刪除後如何處理的詳細資訊。

## 後續步驟

本檔案說明如何在Experience PlatformUI中刪除消費者記錄。 有關如何在UI中執行其他資料衛生任務的資訊，請參閱 [資料衛生UI概述](./overview.md).

若要了解如何使用資料衛生API刪除消費者記錄，請參閱 [工作單端點指南](../api/workorder.md).
