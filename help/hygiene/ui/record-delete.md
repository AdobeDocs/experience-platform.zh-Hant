---
title: 刪除記錄
description: 瞭解如何刪除Adobe Experience PlatformUI中的記錄。
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
hide: true
hidefromtoc: true
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 10%

---

# 刪除記錄

的 [[!UICONTROL 資料衛生] 工作區](./overview.md) 在Adobe Experience PlatformUI中，您可以刪除參與身份服務和即時客戶配置檔案的記錄。 這些記錄可以與單個消費者或包含在身份圖中的任何其他實體相關聯。

>[!IMPORTANT]
>
>記錄刪除請求僅適用於已購買的組織 **Adobe醫療保健盾**。
>
>
>記錄刪除旨在用於資料清除、刪除匿名資料或資料最小化。 他們 **不** 用於與隱私法規(如一般資料保護法規(GDPR))相關的資料主題權限請求（合規性）。 對於所有符合性使用案例，使用 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 的雙曲餘切值。

## 先決條件

刪除記錄需要瞭解身份欄位在Experience Platform中的作用。 具體來說，您必須瞭解要刪除其記錄的實體的主要標識值，具體取決於要從中刪除這些記錄的資料集（或資料集）。

有關平台中標識的詳細資訊，請參閱以下文檔：

* [Adobe Experience Platform身份服務](../../identity-service/home.md):跨設備和系統橋接身份，根據它們遵循的XDM架構定義的身份欄位將資料集連結在一起。
   * [標識命名空間](../../identity-service/namespaces.md):標識名稱空間定義可與單個人相關的不同類型的標識資訊，並且是每個標識欄位的必需元件。
* [即時客戶配置檔案](../../profile/home.md):利用身份圖表，根據來自多個來源的聚合資料提供統一的用戶配置檔案，這些資料幾乎即時更新。
* [體驗資料模型(XDM)](../../xdm/home.md):通過使用架構為平台資料提供標準定義和結構。 所有平台資料集都符合特定的XDM架構，並且該架構定義哪些欄位是標識。
   * [標識欄位](../../xdm/ui/fields/identity.md):瞭解如何在XDM架構中定義標識欄位。

## 建立新請求

要啟動流程，請選擇 **[!UICONTROL 建立請求]** 的下界。

![顯示 [!UICONTROL 建立請求] 按鈕](../images/ui/record-delete/create-request-button.png)

此時將出現請求建立對話框。 預設情況下， **[!UICONTROL 刪除使用者]** 選項 **[!UICONTROL 請求的操作]** 的子菜單。 保留此選項。

![顯示在建立對話框中選擇的刪除使用者選項的影像](../images/ui/record-delete/consumer-action.png)

## 選擇資料集

在 **[!UICONTROL 消費者詳細資訊]** 部分，下一步是確定要從單個資料集還是所有資料集中刪除記錄。

如果您選擇 **[!UICONTROL 選擇資料集]**，選擇資料庫表徵圖(![資料庫表徵圖的影像](../images/ui/record-delete/database-icon.png))，並出現一個對話框，允許您從清單中選擇所需的資料集。

![顯示資料集選擇對話框的影像](../images/ui/record-delete/select-dataset.png)

如果要從所有資料集中刪除記錄，請選擇 **[!UICONTROL 所有資料集]**。

![顯示 [!UICONTROL 所有資料集] 選項](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>選擇 **[!UICONTROL 所有資料集]** 選項會導致刪除操作花費更長的時間，並且不會導致準確的記錄刪除。

## 提供身份 {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="主要身分識別"
>abstract="主要身分識別指將記錄和 Experience Platform 中的消費者設定檔繫結的屬性。資料集的主要身分識別欄位由資料集建立基礎的方案定義。在此欄中，您必須提供記錄的主要身分識別的類型 (或命名空間)，例如用於電子郵件地址的 `email`，以及用於 Experience Cloud ID 的 `ecid`。若要了解詳細資訊，請查看資料檢疫 UI 指南。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="身分識別值"
>abstract="在此欄中，您必須提供記錄的主要身分識別的值，該值必須和左欄中提供的身分識別類型相對應。如果主要身分識別類型是 `email`，則該值應該是記錄的電子郵件地址。若要了解詳細資訊，請查看資料檢疫 UI 指南。"

刪除記錄時，必須提供身份資訊，以便系統能夠確定必須刪除哪些記錄。 對於平台中的任何資料集，記錄將根據 **主身份** 由資料集的架構定義的欄位。

與Platform中的所有標識欄位一樣，主標識由兩部分組成：a **類型** （有時稱為標識命名空間）和 **值**。 標識類型提供了有關欄位如何標識記錄（如電子郵件地址）的上下文，並且該值表示該類型的記錄的特定標識(例如， `jdoe@example.com` 為 `email` 標識類型)。 用作標識的常用欄位包括帳戶資訊、設備ID和cookieID。

>[!TIP]
>
>如果您不知道特定資料集的主標識，可以在平台UI中找到它。 在 **[!UICONTROL 資料集]** 工作區，從清單中選擇有關的資料集。 在資料集的詳細資訊頁面上，將滑鼠懸停在右欄中資料集的架構名稱上。 主標識與架構名稱和說明一起顯示。
>
>![顯示在UI中突出顯示的資料集的主標識的影像](../images/ui/record-delete/dataset-primary-identity.png)

如果從單個資料集中刪除記錄，則您提供的所有標識必須具有相同的類型，因為資料集只能有一個主標識。 如果要從所有資料集中刪除，則可以包括多個標識類型，因為不同的資料集可能具有不同的主標識。

在刪除記錄時提供標識有兩個選項：

* [上載JSON檔案](#upload-json)
* [手動輸入標識值](#manual-identity)

### 上載JSON檔案 {#upload-json}

要上載JSON檔案，可以將檔案拖放到提供區域，或選擇 **[!UICONTROL 選擇檔案]** 瀏覽並從本地目錄中進行選擇。

![顯示在UI中上載JSON方法的影像](../images/ui/record-delete/upload-json.png)

JSON檔案必須格式化為對象陣列，每個對象都表示標識。

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
| `namespaceCode` | 標識類型。 |
| `value` | 由類型表示的標識值。 |

上載檔案後，您可以繼續 [提交請求](#submit)。

### 手動輸入標識 {#manual-identity}

要手動輸入標識，請選擇 **[!UICONTROL 添加標識]**。

![顯示 [!UICONTROL 添加標識] 按鈕](../images/ui/record-delete/add-identity.png)

顯示允許您一次輸入一個標識的控制項。 下 **[!UICONTROL 主標識]**，使用下拉菜單選擇標識類型。 下 **[!UICONTROL 標識值]**，為記錄提供主標識值。

![顯示手動添加的標識欄位的影像](../images/ui/record-delete/identity-added.png)

要添加更多標識，請選擇加號表徵圖(![加號表徵圖的影像](../images/ui/record-delete/plus-icon.png))，或選擇 **[!UICONTROL 添加標識]**。

![顯示如何向請求添加更多標識的影像](../images/ui/record-delete/more-identities.png)

## 提交請求(#submit)

完成向請求添加標識後，在 **[!UICONTROL 請求設定]**，在選擇前為請求提供名稱和可選說明 **[!UICONTROL 提交]**。

![顯示 [!UICONTROL 提交] 按鈕](../images/ui/record-delete/submit.png)

系統將要求您確認要刪除其資料的身份清單。 選擇 **[!UICONTROL 提交]** 確認您的選擇。

![顯示確認對話框的影像](../images/ui/record-delete/confirm-request.png)

在提交請求後，將建立工作單並顯示在 [!UICONTROL 消費者] 頁籤 [!UICONTROL 資料衛生] 工作區。 在此處，您可以監視工作單處理請求時的狀態。

>[!NOTE]
>
>請參閱上的概述部分 [時間表和透明度](../home.md#record-delete-transparency) 有關執行記錄刪除後如何處理記錄刪除的詳細資訊。

## 後續步驟

本文檔介紹了如何刪除Experience PlatformUI中的記錄。 有關如何在UI中執行其他資料衛生任務的資訊，請參閱 [資料衛生UI概述](./overview.md)。

要瞭解如何使用資料衛生API刪除記錄，請參閱 [工作單終結點指南](../api/workorder.md)。
