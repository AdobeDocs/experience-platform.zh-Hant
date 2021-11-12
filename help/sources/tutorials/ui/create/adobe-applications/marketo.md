---
keywords: Experience Platform；首頁；熱門主題；Marketo來源連接器；Marketo連接器；Marketo來源；Marketo
solution: Experience Platform
title: 在UI中建立Marketo Engage來源連接器
topic-legacy: overview
type: Tutorial
description: 本教學課程提供在UI中建立Marketo Engage來源連接器，將B2B資料匯入Adobe Experience Platform的步驟。
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 21617c6ec364fc05d7b8b6d00daa68608d1ed318
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 0%

---

# 建立 [!DNL Marketo Engage] UI中的來源連接器

本教學課程提供建立 [!DNL Marketo Engage] (下稱「[!DNL Marketo]&quot;)UI中的來源連接器，將B2B資料匯入Adobe Experience Platform。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [Experience Data Model(XDM)](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [在UI中建立和編輯結構](../../../../../xdm/ui/resources/schemas.md):了解如何在UI中建立和編輯結構描述。
* [身分識別命名空間](../../../../../identity-service/namespaces.md):身分識別命名空間是 [!DNL Identity Service] 作為身份相關背景的指標。 完全限定的身分包括ID值和命名空間。
* [[!DNL Real-time Customer Profile]](/help/profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 收集所需憑據

若要存取 [!DNL Marketo] 帳戶，您必須提供下列值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `munchkinId` | Munchkin ID是特定 [!DNL Marketo] 例項。 |
| `clientId` | 您的唯一用戶端ID [!DNL Marketo] 例項。 |
| `clientSecret` | 您的唯一用戶端密碼 [!DNL Marketo] 例項。 |

如需取得這些值的詳細資訊，請參閱 [[!DNL Marketo] 驗證指南](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

收集完所需憑證後，您就可以依照下一節中的步驟操作。

## 連接您的 [!DNL Marketo] 帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以為其建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列找到您要使用的特定來源。

在 [!UICONTROL Adobe應用程式] 類別，選擇 **[!UICONTROL Marketo Engage]**. 然後，選取 **[!UICONTROL 新增資料]** 建立新 [!DNL Marketo] 資料流。

![目錄](../../../../images/tutorials/create/marketo/catalog.png)

此 **[!UICONTROL 連接到Marketo Engage]** 頁。 在此頁面中，您可以使用新帳戶或存取現有帳戶。

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供帳戶名稱、選用說明和您的 [!DNL Marketo] 驗證憑據。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![新帳戶](../../../../images/tutorials/create/marketo/new.png)

### 現有帳戶

要使用現有帳戶建立資料流，請選擇 **[!UICONTROL 現有帳戶]** ，然後選取 [!DNL Marketo] 帳戶。 選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/marketo/existing.png)

## 選取資料集

建立 [!DNL Marketo] 帳戶，下一步提供介面供您探索 [!DNL Marketo] 資料集。

介面的左半部是目錄瀏覽器，顯示10 [!DNL Marketo] 資料集。 功能齊全 [!DNL Marketo] 來源連線需要擷取9個不同的資料集。 如果您也使用 [!DNL Marketo] 帳戶型行銷(ABM)功能，則您還必須建立第10個資料流來內嵌 [!UICONTROL 已命名帳戶] 資料集。

>[!NOTE]
>
>為了簡單起見，下列教學課程使用 [!UICONTROL 已命名帳戶] 例如，但下列步驟適用於10個 [!DNL Marketo] 資料集。

選取您要先擷取的資料集，然後選取 **[!UICONTROL 下一個]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## 地圖 [!DNL Marketo] 平台結構

此 [!UICONTROL 對應] 步驟，提供要映射的介面 [!DNL Marketo] 綱要到平台。

選擇要內嵌入的傳入資料的資料集。 您可以使用現有資料集或建立新資料集。

### 使用現有資料集

若要將資料內嵌至現有資料集，請選取 **[!UICONTROL 現有資料集]**，然後選取資料集圖示。

![現有資料集](../../../../images/tutorials/create/marketo/existing-dataset.png)

此 **[!UICONTROL 選取資料集]** 對話框。 找到包含您要使用之適當結構的資料集，選取該資料集，然後選取 **[!UICONTROL 確認]**.

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### 使用新資料集

若要將資料內嵌至新資料集，請選取 **[!UICONTROL 新資料集]** 並在提供的欄位中輸入資料集的名稱和說明。

您可以在 **[!UICONTROL 選擇架構]** 欄。 您也可以選取下拉式圖示，以查看現有結構的清單。 或者，您也可以選取 **[!UICONTROL 進階搜尋]** 若要存取現有結構的頁面，包括其各自的詳細資訊。

切換 **[!UICONTROL 設定檔資料集]** 按鈕，啟用目標資料集 [!DNL Profile]，可讓您建立實體屬性和行為的整體檢視。 所有資料 [!DNL Profile]啟用的資料集將包含在 [!DNL Profile] 和更改會在保存資料流時應用。

![create-new-dataset](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

選取架構後，向下捲動以檢視對應對話方塊，以開始對應您的 [!DNL Marketo] 資料集欄位中填入適當的目標XDM欄位。

### 對應您的 [!DNL Marketo] 以定位XDM欄位的資料集來源欄位

每個 [!DNL Marketo] 資料集有其專屬的對應規則可遵循。 如需如何對應的詳細資訊，請參閱下列內容 [!DNL Marketo] 資料集到XDM:

* [活動](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [計劃](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [方案成員資格](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [公司](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [靜態清單](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [靜態清單成員資格](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [已命名帳戶](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [機會](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [機會聯繫人角色](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [人員](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

選擇 **[!UICONTROL 預覽資料]** 查看根據所選資料集的映射結果。

![映射](../../../../images/tutorials/create/marketo/mapping.png)

此 [!UICONTROL 預覽] 彈出式視窗提供一個介面，讓您探索所選資料集中最多100列範例資料的對應結果。

![預覽](../../../../images/tutorials/create/marketo/mapping-preview.png)

將源欄位映射到適當的目標欄位後，請選擇 **[!UICONTROL 關閉]**.

## 提供資料流詳細資訊

此 [!UICONTROL 資料流詳細資訊] 步驟，允許您提供有關新資料流的名稱和簡要說明。

![dataflow detail](../../../../images/tutorials/create/marketo/dataflow-detail.png)

啟用 **[!UICONTROL 錯誤診斷]** 切換，允許針對新擷取的批次產生詳細的錯誤訊息，您可使用API下載。 如需詳細資訊，請參閱 [檢索資料獲取錯誤診斷](../../../../../ingestion/quality/error-diagnostics.md).

![錯誤](../../../../images/tutorials/create/marketo/errors.png)

此 [!DNL Marketo] 連接器使用批次內嵌來內嵌所有歷史記錄，並使用串流內嵌來進行即時更新。 這可讓連接器在擷取任何錯誤記錄時繼續串流。 啟用 **[!UICONTROL 部分擷取]** 切換，然後設定 [!UICONTROL 錯誤閾值%] 以防止資料流失敗。

**[!UICONTROL 部分擷取]** 提供內嵌包含錯誤且高達特定臨界值的資料的功能。 如需詳細資訊，請參閱 [部分批次內嵌概觀](../../../../../ingestion/batch-ingestion/partial.md).

提供資料流詳細資訊並將錯誤閾值設定為max後，請選擇 **[!UICONTROL 下一個]**.

![部分擷取](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## 查看資料流

此 **[!UICONTROL 檢閱]** 步驟顯示，允許您在建立新資料流之前對其進行查看。 詳細資料會分組為下列類別：

* **[!UICONTROL 連線]**:顯示源類型、所選源實體的相關路徑以及該源實體內的列數。
* **[!UICONTROL 指派資料集和對應欄位]**:顯示要擷取來源資料的資料集，包括資料集所遵守的結構。

審核資料流後，請選擇 **[!UICONTROL 完成]** 並允許建立資料流的時間。

![審查](../../../../images/tutorials/create/marketo/review.png)

## 監視資料流

建立資料流後，您可以監視正在通過資料流進行內嵌的資料，以查看有關內嵌率、成功和錯誤的資訊。 有關如何監視資料流的詳細資訊，請參閱 [監視UI中的資料流](../../../../../dataflows/ui/monitor-sources.md).

## 刪除屬性

資料集中的自訂屬性無法回溯隱藏或移除。 如果要隱藏或移除現有資料集中的自訂屬性，則必須建立沒有此自訂屬性的新資料集、新的XDM架構，並為您建立的新資料集配置新的資料流。 您還必須禁用或刪除包含資料集的原始資料流，該資料集包含要隱藏或刪除的自定義屬性。

## 刪除資料流

您可以刪除不再需要的資料流，或使用 **[!UICONTROL 刪除]** 函式 [!UICONTROL 資料流] 工作區。 有關如何刪除資料流的詳細資訊，請參閱 [刪除UI中的資料流](../../delete.md).

## 後續步驟

按照本教程，您已成功建立資料流以導入 [!DNL Marketo] 資料。 下游Platform服務(例如 [!DNL Real-time Customer Profile] 和 [!DNL Data Science Workspace]. 如需詳細資訊，請參閱下列檔案：

* [[!DNL Real-time Customer Profile] 概觀](/help/profile/home.md)
* [[!DNL Data Science Workspace] 概觀](/help/data-science-workspace/home.md)
