---
title: 在UI中建立Marketo Engage來源連線和資料流
description: 本教學課程提供在UI中建立Marketo Engage來源連線和資料流的步驟，以便將B2B資料引進Adobe Experience Platform。
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 744098777141c61ac27fe6f150c05469d5705dee
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 2%

---

# 建立 [!DNL Marketo Engage] UI中的來源連線和資料流

>[!IMPORTANT]
>
>建立之前 [!DNL Marketo Engage] 來源連線和資料流，您必須先確定 [已對應您的Adobe組織ID](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html) 在 [!DNL Marketo]. 此外，您也必須確保已完成 [自動填入 [!DNL Marketo] B2B名稱空間和結構描述](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) 建立來源連線和資料流之前。

本教學課程提供建立 [!DNL Marketo Engage] (以下稱「[!DNL Marketo]&quot;) UI中的來源聯結器，可將B2B資料帶入Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [B2B名稱空間和結構描述自動產生公用程式](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md)：B2B名稱空間和結構描述自動產生公用程式可讓您使用 [!DNL Postman] 自動產生B2B名稱空間和結構描述的值。 您必須先完成B2B名稱空間和結構描述，才能建立 [!DNL Marketo] 來源連線和資料流。
* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [體驗資料模型(XDM)](../../../../../xdm/home.md)：Experience Platform組織客戶體驗資料的標準化架構。
   * [在UI中建立和編輯方案](../../../../../xdm/ui/resources/schemas.md)：瞭解如何在UI中建立和編輯方案。
* [身分名稱空間](../../../../../identity-service/features/namespaces.md)：身分名稱空間是元件，屬於 [!DNL Identity Service] 作為身分相關內容的指示器。 完整身分包含ID值和名稱空間。
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 收集必要的認證

為了存取您的 [!DNL Marketo] account onExperience Platform，您必須提供下列值：

| 認證 | 說明 |
| ---- | ---- |
| `munchkinId` | Munchkin ID是特定「 」的唯一識別碼 [!DNL Marketo] 執行個體。 |
| `clientId` | 您的唯一使用者端ID [!DNL Marketo] 執行個體。 |
| `clientSecret` | 您專屬的使用者端密碼 [!DNL Marketo] 執行個體。 |

如需取得這些值的詳細資訊，請參閱 [[!DNL Marketo] 驗證指南](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

收集完所需的認證後，您可以依照下一節中的步驟操作。

## 連線您的 [!DNL Marketo] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在 *Adobe應用程式* 類別，選取 **[!UICONTROL Marketo Engage]**，然後選取 **[!UICONTROL 新增資料]**.

>[!TIP]
>
>來源目錄中的來源會顯示 **[!UICONTROL 設定]** 選項，當指定的來源尚未擁有已驗證的帳戶時。 一旦驗證帳戶存在，此選項就會變更為 **[!UICONTROL 新增資料]**.

![已選取Marketo Engage來源的來源目錄。](../../../../images/tutorials/create/marketo/catalog.png)

此 **[!UICONTROL 連線Marketo Engage帳戶]** 頁面便會顯示。 在此頁面中，您可以使用新帳戶或存取現有帳戶。

>[!BEGINTABS]

>[!TAB 建立新帳戶]

若要建立新帳戶，請選取 **[!UICONTROL 新帳戶]** 並提供名稱、選擇性說明和您的認證。

完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![用於驗證新Marketo帳戶的新帳戶介面。](../../../../images/tutorials/create/marketo/new.png)

>[!TAB 使用現有帳戶]

若要使用現有帳戶，請選取 **[!UICONTROL 現有帳戶]** 然後從現有帳戶目錄中選取您要使用的帳戶。

選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有的帳戶介面，您可在此選取現有的Marketo帳戶。](../../../../images/tutorials/create/marketo/existing.png)

>[!ENDTABS]

## 選取資料集

建立您的 [!DNL Marketo] 帳戶，下一個步驟會提供介面供您探索 [!DNL Marketo] 資料集。

介面的左半部分是目錄瀏覽器，顯示10 [!DNL Marketo] 資料集。 功能齊全的 [!DNL Marketo] 來源連線需要擷取九個不同的資料集。 如果您也使用 [!DNL Marketo] 帳戶型行銷(ABM)功能後，您還必須建立第10個資料流以擷取 [!UICONTROL 具名帳戶] 資料集。

>[!NOTE]
>
>為了簡單起見，下列教學課程使用 [!UICONTROL 機會] 例如，以下概述的步驟適用於10個步驟中的任一個 [!DNL Marketo] 資料集。

選取您要擷取的資料集。 這會更新介面，以顯示資料集的預覽。 完成後，選取 **[!UICONTROL 下一個]**.

![預覽介面](../../../../images/tutorials/create/marketo/preview.png)

## 提供資料集和資料流詳細資料 {#provide-dataset-and-dataflow-details}

接下來，您必須提供有關資料集和資料流的資訊。

### 資料集詳細資訊 {#dataset-details}

資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 成功擷取到Experience Platform的資料會以資料集的形式儲存在資料湖中。 在此步驟中，您可以建立新資料集或使用現有資料集。

>[!BEGINTABS]

>[!TAB 使用新資料集]

若要使用新資料集，請選取「 」 **[!UICONTROL 新資料集]** 然後為您的資料集提供名稱和說明（選用）。 您也必須選取您的資料集所要遵守的Experience Data Model (XDM)結構。

![新的資料集選取介面。](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!TAB 使用現有的資料集]

如果您已有現有的資料集，請選取「 」 **[!UICONTROL 現有資料集]** 然後使用 **[!UICONTROL 進階搜尋]** 用於檢視貴組織中所有資料集視窗的選項，包括其個別詳細資訊，例如是否啟用這些資料集以擷取至即時客戶設定檔。

![現有的資料集選取介面。](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!ENDTABS]

### 資料流設定 {#dataflow-configurations}

>[!IMPORTANT]
>
>此 [!DNL Marketo] 來源會使用批次擷取來擷取所有歷史記錄，並使用串流擷取來即時更新。 這可讓來源在擷取任何錯誤記錄時繼續串流。 啟用 **[!UICONTROL 部分擷取]** 切換，然後設定 [!UICONTROL 錯誤臨界值%] 達到最大值，以防止資料流失敗。

如果您的資料集已啟用即時客戶個人檔案，那麼在此步驟中，您可以切換 **[!UICONTROL 設定檔資料集]** 啟用您的資料以供設定檔擷取。 您也可以使用此步驟來啟用 **[!UICONTROL 錯誤診斷]** 和 **[!UICONTROL 部分擷取]**.

* **[!UICONTROL 錯誤診斷]**：選取 **[!UICONTROL 錯誤診斷]** 指示來源產生錯誤診斷，以便您稍後在監控資料集活動和資料流狀態時參考。
* **[!UICONTROL 部分擷取]**： [部分批次擷取](../../../../../ingestion/batch-ingestion/partial.md) 能夠內嵌包含錯誤的資料，上限為特定可設定的臨界值。 此功能可讓您將所有精確資料成功擷取到Experience Platform，同時所有不正確的資料會個別批次處理，並提供無效原因的資訊。

在此步驟中，您可以啟用 **[!UICONTROL 範例資料流]** 可限制資料擷取，並避免擷取所有歷史資料（包括個人身分）所產生的額外成本。

>[!BEGINSHADEBOX]

**使用範例資料流的快速指南**

範例資料流是您可以為設定的設定 [!DNL Marketo] 資料流來限制您的擷取率，然後嘗試Experience Platform功能而不需要擷取大量資料。

* 啟用範例資料流，可在回填工作期間擷取最多10萬筆記錄（從最大的記錄ID）或最多10天的活動，以限制歷史資料。
* 針對所有B2B實體使用範例資料流設定時，您必須考慮到某些相關記錄可能會遺失，因為系統不會擷取來源資料的整個歷史記錄。

>[!ENDSHADEBOX]

![「資料流詳細資料」頁面的「資料流組態」段落。](../../../../images/tutorials/create/marketo/dataflow-configurations.png)

此外，如果您從公司資料集中擷取資料，則可啟用 **[!UICONTROL 排除無人認領的帳戶]** 將無人認領的帳戶排除在擷取之外。

當個人填寫表單時， [!DNL Marketo] 根據不含其他資料的公司名稱建立虛擬帳戶記錄。 對於新的資料流，預設會啟用排除無人認領帳戶的切換按鈕。 對於現有的資料流，您可以啟用或停用此功能，而變更會套用至新擷取的資料，而非現有的資料。

![排除無人認領的帳戶](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## 對應您的 [!DNL Marketo] 目標XDM欄位的資料集來源欄位

此 [!UICONTROL 對應] 步驟隨即顯示，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

每個 [!DNL Marketo] 資料集有其專屬的對應規則要遵循。 如需如何對應的詳細資訊，請參閱下列內容 [!DNL Marketo] 資料集至XDM：

* [活動](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [方案](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [計畫成員資格](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [公司](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [靜態清單](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [靜態清單成員資格](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [具名帳戶](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [機會](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [機會聯絡人角色](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [人員](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

您可以根據自己的需求，選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算或計算的值。 如需使用對應介面的完整步驟，請參閱 [資料準備UI指南](../../../../../data-prep/ui/mapping.md).

![Marketo資料的對應介面。](../../../../images/tutorials/create/marketo/mapping.png)

對應集準備就緒後，選取 **[!UICONTROL 下一個]** 並留出一些時間建立新的資料流。

## 檢閱您的資料流

此 **[!UICONTROL 檢閱]** 步驟隨即顯示，可讓您在建立新資料流之前對其進行檢閱。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源實體的相關路徑，以及該來源實體中的欄數量。
* **[!UICONTROL 指派資料集並對映欄位]**：顯示要將來源資料擷取到哪個資料集中，包括資料集所堅持的結構描述。

檢閱資料流後，選取「 」 **[!UICONTROL 儲存並擷取]** 並留出一些時間建立資料流。

![此檢閱頁面可讓您在擷取之前確認資料流的詳細資訊。](../../../../images/tutorials/create/marketo/review.png)

## 監視資料流

建立資料流後，您可以監視透過該資料流擷取的資料，以檢視擷取率、成功和錯誤的資訊。 如需如何監視資料流的詳細資訊，請參閱以下教學課程： [在UI中監視資料流程](../../../../../dataflows/ui/monitor-sources.md).

## 刪除您的屬性

資料集中的自訂屬性無法回溯隱藏或移除。 如果您想從現有資料集中隱藏或移除自訂屬性，則必須建立不含此自訂屬性的新資料集、新的XDM結構，並為您建立的新資料集設定新的資料流。 您也必須停用或刪除包含資料集的原始資料流，該資料流具有您要隱藏或移除的自訂屬性。

## 刪除您的資料流

您可以刪除不再需要的資料流，或是使用建立的資料流不正確。 **[!UICONTROL 刪除]** 函式位於 [!UICONTROL 資料流] 工作區。 如需如何刪除資料流程的詳細資訊，請參閱以下教學課程： [在UI中刪除資料流](../../delete.md).

## 後續步驟

依照本教學課程中的指示，您已成功建立資料流以從擷取B2B資料 [!DNL Marketo Engage] 來源以Experience Platform。

## 附錄 {#appendix}

以下各節提供您在使用時，可能會遵循的其他准則。 [!DNL Marketo] 來源。

### ui中的錯誤訊息 {#error-messages}

當Platform偵測到您的設定發生問題時，UI中會顯示下列錯誤訊息：

#### [!DNL Munchkin ID] 未對應至適當的組織

若您的 [!DNL Munchkin ID] 不會對應至您正在使用的平台組織。 設定您與網站之間 [!DNL Munchkin ID] 以及您的組織，使用 [[!DNL Marketo] 介面](https://app-sjint.marketo.com/#MM0A1).

![錯誤訊息顯示Marketo執行個體未正確對應至Adobe組織。](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### 缺少主要身分

如果缺少主要身分，資料流將無法儲存和擷取。 確定 [您的XDM結構描述中存在主要身分](../../../../../xdm/tutorials/create-schema-ui.md)，然後再嘗試設定資料流。

![顯示主要身分從XDM結構描述中缺少的錯誤訊息。](../../../../images/tutorials/create/marketo/no-primary-identity.png)

