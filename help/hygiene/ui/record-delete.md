---
title: 刪除記錄
description: 瞭解如何刪除Adobe Experience Platform UI中的記錄。
badgeBeta: label="Beta" type="Informative"
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 9981f35732b041a92c5a371e727a8facb6636cf5
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 8%

---

# 刪除記錄 {#record-delete}

使用[[!UICONTROL 資料生命週期]工作區](./overview.md)，根據其主要身分刪除Adobe Experience Platform中的記錄。 這些記錄可以與個別消費者或包含在身分圖表中的任何其他實體繫結。

>[!IMPORTANT]
> 
>「記錄刪除」功能目前在Beta中，僅可在&#x200B;**限定的版本**&#x200B;中使用。 並非所有客戶都可使用。 記錄刪除請求僅適用於有限版本中的組織。
> 
> 
>記錄刪除旨在用於資料清理、匿名資料移除或資料最小化。 它們&#x200B;**不**&#x200B;用於資料主體權利要求（法規遵循），因為與一般資料保護規範(GDPR)等隱私權法規相關。 對於所有規範使用案例，請改用[Adobe Experience Platform Privacy Service](../../privacy-service/home.md)。

## 先決條件 {#prerequisites}

刪除記錄需要實際瞭解身分欄位在Experience Platform中的運作方式。 具體來說，您必須知道要刪除其記錄的實體的身分名稱空間值，端視您要從中刪除這些記錄的資料集（或資料集）而定。

請參閱下列檔案，以取得有關Platform中身分的詳細資訊：

* [Adobe Experience Platform Identity服務](../../identity-service/home.md)：跨裝置和系統橋接身分，根據資料集所符合的XDM結構描述所定義的身分欄位，將資料集連結在一起。
* [身分識別名稱空間](../../identity-service/features/namespaces.md)：身分識別名稱空間會定義與單一人員相關的不同身分識別資訊型別，而且是每個身分識別欄位的必要元件。
* [即時客戶個人檔案](../../profile/home.md)：使用身分圖表，根據來自多個來源的彙總資料提供統一的消費者個人檔案，近乎即時更新。
* [體驗資料模型(XDM)](../../xdm/home.md)：透過使用結構描述為Platform資料提供標準定義和結構。 所有Platform資料集都符合特定的XDM結構描述，而結構描述會定義哪些欄位是身分。
* [身分欄位](../../xdm/ui/fields/identity.md)：瞭解身分欄位在XDM結構描述中的定義方式。

## 建立請求 {#create-request}

若要啟動程式，請在Platform UI的左側導覽中選取&#x200B;**[!UICONTROL 資料生命週期]**。 [!UICONTROL 資料生命週期要求]工作區會出現。 接著，從工作區的首頁面選取&#x200B;**[!UICONTROL 建立請求]**。

![已選取[!UICONTROL 建立要求]的[!UICONTROL 資料生命週期要求]工作區。](../images/ui/record-delete/create-request-button.png)

此時會出現請求建立工作流程。 依預設，**[!UICONTROL 要求的動作]**&#x200B;區段底下會選取&#x200B;**[!UICONTROL 刪除記錄]**&#x200B;選項。 保留選取此選項。

>[!IMPORTANT]
> 
>為了提高效率並降低資料集操作的成本，已移至Delta格式的組織可以刪除Identity Service、即時客戶設定檔和資料湖中的資料。 此型別的使用者稱為差異移轉使用者。 已進行差異移轉的組織之使用者，可選擇從單一或所有資料集中刪除記錄。 來自未曾進行差異移轉之組織的使用者，無法從單一資料集或所有資料集中選擇性地刪除記錄，如下圖所示。 在此情況下，請繼續前往指南的[提供身分](#provide-identities)區段。

![已選取並反白具有[!UICONTROL 刪除記錄]選項的請求建立工作流程。](../images/ui/record-delete/delete-record.png)

## 選取資料集 {#select-dataset}

下一步是決定您要從單一資料集還是所有資料集中刪除記錄。 如果您無法使用此選項，請繼續前往指南的[提供身分識別](#provide-identities)區段。

在&#x200B;**[!UICONTROL 記錄詳細資料]**&#x200B;區段下，使用選項按鈕在特定資料集與所有資料集之間選取。 如果您選擇&#x200B;**[!UICONTROL 選取資料集]**，請繼續選取資料庫圖示（![資料庫圖示](../images/ui/record-delete/database-icon.png)）以開啟提供可用資料集清單的對話方塊。 從清單中選取所需的資料集，然後選取&#x200B;**[!UICONTROL 完成]**。

![已選取資料集並醒目提示[!UICONTROL 完成]的[!UICONTROL 選取資料集]對話方塊。](../images/ui/record-delete/select-dataset.png)

若要刪除所有資料集中的記錄，請選取&#x200B;**[!UICONTROL 所有資料集]**。

![已選取[!UICONTROL 所有資料集]選項的[!UICONTROL 選取資料集]對話方塊。](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>選取&#x200B;**[!UICONTROL 所有資料集]**&#x200B;選項可能會導致刪除作業花費更長的時間，並且可能不會導致精確的記錄刪除。

## 提供身分 {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="身分命名空間"
>abstract="身分命名空間指將記錄和 Experience Platform 中的消費者設定檔繫結的屬性。資料集的身分命名空間欄位由資料集建立基礎的方案定義。在此欄中，您必須提供記錄的身分命名空間的類型 (或命名空間)，例如用於電子郵件地址的 `email`，以及用於 Experience Cloud ID 的 `ecid`。若要了解詳細資訊，請查看「資料生命週期 UI 指南」。"

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="主要身分值"
>abstract="在此欄中，您必須提供記錄的身分命名空間的值，該值必須和左欄中提供的身分識別類型相對應。如果身分命名空間類型是 `email`，則該值應該是記錄的電子郵件地址。若要了解詳細資訊，請查看「資料生命週期 UI 指南」。"

刪除記錄時，您必須提供身分資訊，讓系統能夠決定要刪除哪些記錄。 對於Platform中的任何資料集，會根據資料集結構描述所定義的&#x200B;**身分名稱空間**&#x200B;欄位來刪除記錄。

和Platform中的所有身分識別欄位一樣，身分識別名稱空間是由兩部分組成： **型別** （有時稱為身分識別名稱空間）和&#x200B;**值**。 身分型別提供欄位如何識別記錄的上下文（例如電子郵件地址）。 值代表該型別的記錄特定身分（例如，`email`身分型別的`jdoe@example.com`）。 做為身分識別的常見欄位包括帳戶資訊、裝置ID和Cookie ID。

>[!TIP]
>
>如果您不知道特定資料集的身分名稱空間，可以在Platform UI中找到。 在&#x200B;**[!UICONTROL 資料集]**&#x200B;工作區中，從清單中選取有問題的資料集。 在資料集的詳細資訊頁面上，將滑鼠移至右側邊欄中資料集的結構描述名稱上。 身分名稱空間會與結構描述名稱和說明一起顯示。
>
>![已選取資料集的資料集控制面板，並從資料集詳細資料面板開啟結構描述對話方塊。 資料集的主要ID已反白顯示。](../images/ui/record-delete/dataset-primary-identity.png)

如果您要從單一資料集中刪除記錄，您提供的所有身分都必須有相同的型別，因為資料集只能有一個身分名稱空間。 如果您要從所有資料集中刪除，則可以包含多個身分型別，因為不同的資料集可能具有不同的主要身分。

刪除記錄時，有兩個選項可提供身分識別：

* [上傳JSON檔案](#upload-json)
* [手動輸入主要身分值](#manual-identity)

### 上傳JSON檔案 {#upload-json}

若要上傳JSON檔案，您可以將檔案拖放至提供的區域，或選取&#x200B;**[!UICONTROL 選擇檔案]**&#x200B;以瀏覽並從本機目錄中選取。

![要求建立工作流程，其中包含反白顯示的選擇檔案和拖放介面以上傳JSON檔案。](../images/ui/record-delete/upload-json.png)

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
| `value` | 型別所代表的主要身分值。 |

上傳檔案後，您就可以繼續[提交要求](#submit)。

### 手動輸入身分 {#manual-identity}

若要手動輸入身分，請選取&#x200B;**[!UICONTROL 新增身分]**。

![要求建立工作流程中反白顯示[!UICONTROL 新增身分]選項。](../images/ui/record-delete/add-identity.png)

顯示的控制項可讓您一次輸入一個身分。 在&#x200B;**[!UICONTROL 身分名稱空間]**&#x200B;下，使用下拉式功能表選取身分型別。 在&#x200B;**[!UICONTROL 主要身分值]**&#x200B;下，提供記錄的身分名稱空間值。

![已手動新增包含身分欄位的要求建立工作流程。](../images/ui/record-delete/identity-added.png)

若要新增更多身分，請選取加號圖示(![A加號圖示。](../images/ui/record-delete/plus-icon.png))，或選取&#x200B;**[!UICONTROL 新增身分]**。

![要求建立工作流程中會顯示加號圖示和醒目提示的新增身分圖示。](../images/ui/record-delete/more-identities.png)

## 提交請求 {#submit}

完成新增身分到要求之後，在&#x200B;**[!UICONTROL 要求設定]**&#x200B;下，在選取&#x200B;**[!UICONTROL 提交]**&#x200B;之前，提供要求的名稱和選擇性描述。

>[!IMPORTANT]
> 
>每個月可提交的不重複身分記錄刪除總數有不同的限制。 這些限制是以您的授權合約為基礎。 已購買所有Adobe Real-time Customer Data Platform或Adobe Journey Optimizer版本的組織，每個月最多可提交100,000筆身分記錄刪除。 已購買&#x200B;**AdobeHealthcare Shield**&#x200B;或&#x200B;**AdobePrivacy &amp; Security Shield**&#x200B;的組織每個月最多可提交600,000個身分記錄刪除。<br>透過UI的單一記錄刪除請求可讓您一次提交10,000個ID。 刪除記錄的[API方法](../api/workorder.md#create)允許一次提交100,000個ID。<br>最佳實務是每個請求提交儘可能多的ID，以您的ID限製為限。 當您要刪除大量ID時，應避擴音交小量ID或每個記錄刪除請求使用一個單一ID。

![要求設定的[!UICONTROL 名稱]和[!UICONTROL 描述]欄位，並反白顯示[!UICONTROL 提交]。](../images/ui/record-delete/submit.png)

出現[!UICONTROL Confirm要求]對話方塊，表示刪除後無法復原身分。 選取&#x200B;**[!UICONTROL 提交]**&#x200B;以確認您要刪除其資料的身分清單。

![ [!UICONTROL 確認要求]對話方塊。](../images/ui/record-delete/confirm-request.png)

提交要求後，工作單即建立並顯示在[!UICONTROL 資料生命週期]工作區的[!UICONTROL 記錄]索引標籤上。 從這裡，您可以在工單處理請求時監視工單的狀態。

>[!NOTE]
>
>如需記錄刪除執行後如何處理的詳細資訊，請參閱[時間表與透明度](../home.md#record-delete-transparency)的概觀區段。

![ [!UICONTROL 資料生命週期]工作區的[!UICONTROL 記錄]索引標籤中反白顯示新要求。](../images/ui/record-delete/request-log.png)

## 後續步驟

本檔案說明如何刪除Experience Platform UI中的記錄。 有關如何在UI中執行其他資料生命週期管理工作的資訊，請參閱[資料生命週期UI概觀](./overview.md)。

若要瞭解如何使用資料衛生API刪除記錄，請參閱[工單端點指南](../api/workorder.md)。
