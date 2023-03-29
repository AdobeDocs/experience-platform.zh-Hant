---
keywords: 啟用設定檔目的地；啟用目的地；啟用資料；啟用電子郵件行銷目的地；啟用雲端儲存目的地
title: 啟用受眾資料以批次設定檔匯出目的地
type: Tutorial
description: 了解如何將區段傳送至批次設定檔式型目的地，以啟動Adobe Experience Platform中的受眾資料。
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '3629'
ht-degree: 10%

---

# 啟用受眾資料以批次設定檔匯出目的地

>[!IMPORTANT]
> 
> * 啟用資料並啟用 [對應步驟](#mapping) 工作流程中，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions).
> * 若要啟動資料，而不要透過 [對應步驟](#mapping) 工作流程中，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟用區段而不對應]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions).
> 
> 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。
>
> 參與改善檔案匯出功能測試版的部分客戶看到新的 **[!UICONTROL 對應]** 作為其啟動工作流程的一部分 [全新測試版雲端儲存目的地](/help/release-notes/2022/october-2022.md#destinations). 另請注意 [已知限制](#known-limitations) 做為版本的一部分。

## 總覽 {#overview}

本文說明在Adobe Experience Platform批次設定檔型目的地（例如雲端儲存空間和電子郵件行銷目的地）中啟用受眾資料所需的工作流程。

## 先決條件 {#prerequisites}

若要將資料啟用至目的地，您必須成功 [連接到目的地](./connect-destination.md). 如果尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地，並設定您要使用的目的地。

## 選取您的目的地 {#select-destination}

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![影像醒目提示如何前往目的地目錄標籤](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. 選擇 **[!UICONTROL 啟用區段]** 在與您要啟用區段的目的地對應的卡片上，如下圖所示。

   ![突出顯示「激活段」按鈕的影像](../assets/ui/activate-batch-profile-destinations/activate-segments-button.png)

1. 選取您要用來啟用區段的目的地連線，然後選取 **[!UICONTROL 下一個]**.

   ![影像醒目提示如何選取一或多個目的地以啟用區段至](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. 移至下一節，以 [選取區段](#select-segments).

## 選取您的區段 {#select-segments}

使用區段名稱左側的核取方塊，選取您要啟用至目的地的區段，然後選取 **[!UICONTROL 下一個]**.

![影像醒目提示如何選取一或多個要啟用的區段](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## 排程區段匯出 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_schedule"
>title="排程"
>abstract="使用鉛筆圖示設定檔案匯出類型 (完整檔案或增量檔案) 和匯出頻率。"

[!DNL Adobe Experience Platform] 以 [!DNL CSV] 檔案。 在 **[!UICONTROL 排程]** 頁面，您可以為要匯出的每個區段設定排程和檔案名稱。 必須設定排程，但設定檔案名稱為選用。

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] 會自動分割每個檔案500萬筆記錄（列）的匯出檔案。 每一列代表一個設定檔。
>
>拆分檔案名後附加一個數字，表示該檔案是較大導出的一部分，例如： `filename.csv`, `filename_2.csv`, `filename_3.csv`.

選取 **[!UICONTROL 建立排程]** 按鈕（與您要傳送至目的地的區段對應）。

![突出顯示「建立計畫」按鈕的影像](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### 導出完整檔案 {#export-full-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exportoptions"
>title="檔案匯出選項 "
>abstract="選取&#x200B;**匯出完整檔案**&#x200B;以匯出符合區段資格的所有設定檔的完整快照。選取&#x200B;**匯出增量檔案**，僅匯出上次匯出後符合區段資格的設定檔。<br> 第一個增量檔案匯出包括符合區段資格的所有設定檔，充當回填。未來的增量檔案僅包括第一次增量檔案匯出後符合區段資格的設定檔。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#export-incremental-files" text="匯出增量檔案"

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_aftersegmentevaluation"
>title="區段評估後啟動"
>abstract="每日分段作業完成後立即執行啟動。這可確保匯出最新的設定檔。"

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_scheduled"
>title="排程啟動"
>abstract="在一天中的固定時間執行啟動。"

選擇 **[!UICONTROL 導出完整檔案]** 觸發匯出檔案，該檔案包含所選區段之所有設定檔資格的完整快照。

![選取「匯出完整檔案」時的UI影像。](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. 使用 **[!UICONTROL 頻率]** 選取器以選取匯出頻率：

   * **[!UICONTROL 一次]**:排程一次性的隨選完整檔案匯出。
   * **[!UICONTROL 每日]**:在您指定的時間，每天排程完整檔案匯出一次。

1. 使用 **[!UICONTROL 時間]** 切換，選取匯出應在區段評估後立即進行，或在指定時間依排程進行。 選取 **[!UICONTROL 已排程]** 選項，您可以使用選取器來選擇一天中的時間，位於 [!DNL UTC] 格式，導出時間。

   >[!NOTE]
   >
   >此 **[!UICONTROL 區段評估後]** 下列說明的選項目前僅供選取測試版客戶使用。

   使用 **[!UICONTROL 區段評估後]** 選項，在每日Platform批次劃分作業完成後，立即執行啟動工作。 這可確保在啟動工作執行時，最新的設定檔會匯出至您的目的地。

   <!-- Batch segmentation currently runs at {{insert time of day}} and lasts for an average {{x hours}}. Adobe reserves the right to modify this schedule. -->

   ![影像醒目提示批次目的地啟動流程中的「區段評估後」選項。](../assets/ui/activate-batch-profile-destinations/after-segment-evaluation-option.png)
使用 **[!UICONTROL 已排程]** 選項，讓啟動工作在固定時間執行。 這可確保Experience Platform設定檔資料會每天同時匯出，但您匯出的設定檔可能不是最新的，具體取決於啟動工作開始前批次分段工作是否已完成。

   ![影像醒目提示批次目的地啟動流程中的「已排程」選項，並顯示時間選取器。](../assets/ui/activate-batch-profile-destinations/scheduled-option.png)

   >[!IMPORTANT]
   >
   >由於內部Experience Platform進程的配置方式，第一個增量或完整檔案導出可能不包含所有回填資料。 <br> <br> 為確保完整檔案和增量檔案都能匯出完整且最新的回填資料，Adobe建議在次日中午12點後設定第一次檔案匯出時間。 未來版本將會解決此限制。

1. 使用 **[!UICONTROL 日期]** 選取器，以選擇應進行匯出的日期或間隔。 對於每日匯出，最佳實務是設定您的開始和結束日期，以符合下游平台中促銷活動的持續時間。

   >[!IMPORTANT]
   >
   > 選取匯出間隔時，匯出中不會包含間隔的最後一天。 例如，如果選取1月4日到11日的間隔，最後一次檔案匯出將於1月10日進行。

1. 選擇 **[!UICONTROL 建立]** 以儲存排程。

### 匯出增量檔案 {#export-incremental-files}

選擇 **[!UICONTROL 導出增量檔案]** 觸發導出，其中第一個檔案是選定段的所有配置檔案資格的完整快照，而後續檔案是自上次導出以來的增量配置檔案資格。

>[!IMPORTANT]
>
>第一個匯出的增量檔案包含所有符合區段資格的設定檔，可作為回填。

![已選取「匯出增量檔案」的UI影像。](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. 使用 **[!UICONTROL 頻率]** 選取器以選取匯出頻率：

   * **[!UICONTROL 每日]**:在您指定的時間，每天計劃一次增量檔案導出。
   * **[!UICONTROL 每小時]**:計畫每3、6、8或12小時導出增量檔案。

1. 使用 **[!UICONTROL 時間]** 選取器以選擇一天中的時間，位於 [!DNL UTC] 格式，導出時間。

   >[!IMPORTANT]
   >
   >由於內部Experience Platform進程的配置方式，第一個增量或完整檔案導出可能不包含所有回填資料。 <br> <br> 為確保完整檔案和增量檔案都能匯出完整且最新的回填資料，Adobe建議在次日中午12點後設定第一次檔案匯出時間。 未來版本將會解決此限制。

1. 使用 **[!UICONTROL 日期]** 選取器，以選擇應進行匯出的間隔。 最佳實務是設定您的開始和結束日期，以符合下游平台中促銷活動的持續時間。

   >[!IMPORTANT]
   >
   >匯出中不會包含間隔的最後一天。 例如，如果選取1月4日到11日的間隔，最後一次檔案匯出將於1月10日進行。

1. 選擇 **[!UICONTROL 建立]** 以儲存排程。

### 配置檔案名 {#file-names}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_filename"
>title="設定檔案名稱"
>abstract="若是檔案型目的地，會對每個區段產生唯一的檔案名稱。使用檔案名稱編輯器建立和編輯唯一的檔案名稱或保留預設名稱。"

對於大多數目的地，預設檔案名稱包含目的地名稱、區段ID以及日期和時間指標。 例如，您可以編輯匯出的檔案名稱以區分不同的促銷活動，或將資料匯出時間附加至檔案。 請注意，某些目的地開發人員可能會選取為其目的地顯示不同的預設檔案名稱附加選項。

選取鉛筆圖示以開啟強制回應視窗並編輯檔案名稱。 檔案名限制為255個字元。

>[!NOTE]
>
>下圖顯示如何為 [!DNL Amazon S3] 但所有批次目的地的程式都相同(例如SFTP、 [!DNL Azure Blob Storage]，或 [!DNL Google Cloud Storage])。

![用於配置檔案名的鉛筆表徵圖突出顯示影像。](../assets/ui/activate-batch-profile-destinations/configure-name.png)

在檔案名稱編輯器中，可以選取不同的元件以新增至檔案名稱。

![顯示所有可用檔案名選項的影像。](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

無法從檔案名稱中移除目的地名稱和區段ID。 除了這些外，您還可以新增下列項目：

| 檔案名選項 | 說明 |
|---------|----------|
| **[!UICONTROL 區段名稱]** | 匯出的區段名稱。 |
| **[!UICONTROL 日期和時間]** | 在新增 `MMDDYYYY_HHMMSS` 格式或Unix 10位數的檔案生成時間時間戳。 如果希望檔案在每次增量導出時都生成動態檔案名，請選擇以下選項之一。 |
| **[!UICONTROL 自訂文字]** | 要添加到檔案名的任何自定義文本。 |
| **[!UICONTROL 目的地ID]** | 用於導出段的目標資料流的ID。 <br> **附註**:此檔案名稱附加選項僅適用於參與改善的檔案匯出功能測試版程式的測試版客戶。 如果您想要存取測試版計畫，請連絡您的Adobe代表或客戶服務。 |
| **[!UICONTROL 目的地名稱]** | 用於導出段的目標資料流的名稱。 <br> **附註**:此檔案名稱附加選項僅適用於參與改善的檔案匯出功能測試版程式的測試版客戶。 如果您想要存取測試版計畫，請連絡您的Adobe代表或客戶服務。 |
| **[!UICONTROL 組織名稱]** | 您的組織名稱Experience Platform。 <br> **附註**:此檔案名稱附加選項僅適用於參與改善的檔案匯出功能測試版程式的測試版客戶。 如果您想要存取測試版計畫，請連絡您的Adobe代表或客戶服務。 |
| **[!UICONTROL 沙箱名稱]** | 您用來匯出區段的沙箱ID。 <br> **附註**:此檔案名稱附加選項僅適用於參與改善的檔案匯出功能測試版程式的測試版客戶。 如果您想要存取測試版計畫，請連絡您的Adobe代表或客戶服務。 |

{style="table-layout:auto"}

選擇 **[!UICONTROL 套用變更]** 以確認您的選取。

>[!IMPORTANT]
> 
>如果您未選取 **[!UICONTROL 日期和時間]** 元件，則檔案名將為靜態，而新導出的檔案將用每次導出覆蓋儲存位置中以前的檔案。 將循環匯入工作從儲存位置執行至電子郵件行銷平台時，建議使用此選項。

完成所有區段的設定後，請選取 **[!UICONTROL 下一個]** 繼續。

## 選取設定檔屬性 {#select-attributes}

針對以設定檔為基礎的目的地，您必須選取要傳送至目標目的地的設定檔屬性。

1. 在 **[!UICONTROL 選擇屬性]** 頁面，選取 **[!UICONTROL 新增欄位]**.

   ![突出顯示「添加新欄位」按鈕的影像。](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. 選取 **[!UICONTROL 結構欄位]** 的下界。

   ![影像突出顯示如何選擇源欄位。](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. 在 **[!UICONTROL 選擇欄位]** 頁面，選取您要傳送至目的地的XDM屬性或身分命名空間，然後選擇 **[!UICONTROL 選擇]**.

   ![此影像顯示了作為源欄位可用的各種欄位。](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

1. 若要新增更多對應，請重複步驟一至三。

>[!NOTE]
>
> Adobe Experience Platform會從您的架構中，使用四個建議且常用的屬性來填入您的選取項目： `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

>[!IMPORTANT]
>
>由於已知限制，您目前無法使用 **[!UICONTROL 選擇欄位]** 窗口 `segmentMembership.status` 檔案匯出。 而是需要手動貼上值 `xdm: segmentMembership.status` 填入架構欄位，如下所示。
>
>![螢幕記錄顯示啟動工作流程對應步驟中的區段成員資格因應措施。](/help/destinations/assets/ui/activate-batch-profile-destinations/segment-membership.gif)

檔案匯出會依下列方式而異，具體取決於 `segmentMembership.status` 已選取：
* 若 `segmentMembership.status` 欄位，導出的檔案包括 **[!UICONTROL 作用中]** 初始完整快照和 **[!UICONTROL 作用中]** 和 **[!UICONTROL 過期]** 成員。
* 若 `segmentMembership.status` 欄位未選中，導出的檔案僅包括 **[!UICONTROL 作用中]** 初始完整快照和後續增量導出中的成員。

![在區段啟動工作流程的對應步驟中顯示預先填入的建議屬性的影像。](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### 強制屬性 {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="關於強制屬性"
>abstract="選取所有匯出的設定檔應包含的 XDM 方案屬性。沒有強制金鑰的設定檔不會匯出到目的地。未選取強制金鑰會匯出所有合格的設定檔，無論其屬性如何。"

強制屬性是啟用使用者的核取方塊，可確保所有設定檔記錄都包含選取的屬性。 例如：所有匯出的設定檔都包含電子郵件地址&#x200B;。

您可以將屬性標示為必填，以確保 [!DNL Platform] 僅匯出包含特定屬性的設定檔。 因此，它可作為額外的篩選形式使用。 將屬性標示為必要屬性 **not** 必填。

不選擇強制屬性會匯出所有符合資格的設定檔（無論其屬性為何）。

建議其中一個屬性是 [唯一識別碼](../../destinations/catalog/email-marketing/overview.md#identity) 從您的架構。 如需強制屬性的詳細資訊，請參閱 [電子郵件行銷目的地](../../destinations/catalog/email-marketing/overview.md#identity) 檔案。

### 重複資料刪除密鑰 {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="關於去重複化索引鍵"
>abstract="選取去重複化索引鍵，以消除匯出檔案中同一設定檔的多筆記錄。選取單一命名空間或最多兩個 XDM 方案屬性作為去重複化索引鍵。未選取去重複化索引鍵可能會導致匯出檔案中出現重複的設定檔項目。"

重複資料刪除金鑰是使用者定義的主金鑰，可決定使用者要依此身分對其設定檔進行重複資料刪除的&#x200B;身分。

重複資料刪除索引鍵消除了在一個匯出檔案中有多個相同設定檔記錄的可能性。

在中，有三種使用重複資料刪除密鑰的方式 [!DNL Platform]:

* 使用單一身分命名空間作為 [!UICONTROL 去重複化金鑰]
* 使用 [!DNL XDM] 設定檔作為 [!UICONTROL 去重複化金鑰]
* 使用 [!DNL XDM] 設定檔作為複合鍵

>[!IMPORTANT]
>
> 您可以將單一身分命名空間匯出至目的地，命名空間會自動設為重複資料刪除索引鍵。 不支援將多個命名空間傳送至目的地。
> 
> 您無法使用身分命名空間和設定檔屬性的組合作為重複資料刪除索引鍵。

### 重複資料刪除範例 {#deduplication-example}

此示例說明重複資料消除的工作方式，具體取決於所選的重複資料消除密鑰。

讓我們考慮下列兩個設定檔。

**設定檔A**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-03-10 10:03:08"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "Doe",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

**設定檔B**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-04-10 11:33:28"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "D",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

### 重複資料刪除使用案例1:無重複資料消除 {#deduplication-use-case-1}

若不使用重複資料刪除，匯出檔案將包含下列項目。

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | 約翰 | Doe |
| johndoe@example.com | 約翰 | D |


### 重複資料刪除使用案例2:基於身份命名空間的重複資料消除 {#deduplication-use-case-2}

假設重複資料刪除由 [!DNL Email] 命名空間，匯出檔案將包含下列項目。 設定檔B是符合區段資格的最新一個，因此是唯一一個匯出的設定檔。

| 電子郵件* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | 約翰 | D |
| johndoe_2@example.com | johndoe@example.com | 約翰 | D |

### 重複資料刪除使用案例3:基於單一設定檔屬性的重複資料刪除 {#deduplication-use-case-3}

假設重複資料刪除由 `personal Email` 屬性，則匯出檔案將包含下列項目。 設定檔B是符合區段資格的最新一個，因此是唯一一個匯出的設定檔。

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | 約翰 | D |


### 重複資料刪除使用案例4:基於兩個配置檔案屬性的重複資料消除 {#deduplication-use-case-4}

假設使用複合鍵重複資料刪除 `personalEmail + lastName`，則匯出檔案將包含下列項目。

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | 約翰 |
| johndoe@example.com | Doe | 約翰 |


Adobe建議您選取身分命名空間，例如 [!DNL CRM ID] 或電子郵件地址作為重複資料刪除金鑰，以確保所有設定檔記錄都經過唯一識別。

>[!NOTE]
> 
>如果資料集（而非整個資料集）中的某些欄位已套用任何資料使用標籤，則在啟用時，會在下列條件下強制執行這些欄位層級標籤：
>
>* 欄位會用於區段定義中。
>* 欄位會設定為目標目的地的預計屬性。
>
> 例如，如果欄位 `person.name.firstName` 具有與目的地的行銷動作相衝突的特定資料使用標籤，則您會在審核步驟中顯示資料使用政策違規。 如需詳細資訊，請參閱 [Adobe Experience Platform中的資料控管](../../rtcdp/privacy/data-governance-overview.md#destinations).

## （測試版）對應 {#mapping}

>[!IMPORTANT]
> 
>精選測試版客戶可檢視 **[!UICONTROL 對應]** 取代 [選取設定檔屬性](#select-attributes) 上述步驟。 這個新 **[!UICONTROL 對應]** 步驟可讓您將匯出檔案的標題編輯為任何您想要的自訂名稱。
> 
> 功能和檔案可能會有所變更。 如果您想要存取此測試版計畫，請連絡您的Adobe代表或客戶服務。

在此步驟中，您必須選取要新增至匯出至目標目的地之檔案的設定檔屬性。 若要選取要匯出的設定檔屬性和身分：

1. 在 **[!UICONTROL 對應]** 頁面，選取 **[!UICONTROL 新增欄位]**.

   ![在對應工作流程中反白顯示新增欄位控制項。](../assets/ui/activate-batch-profile-destinations/add-new-field-mapping.png)

1. 選取 **[!UICONTROL 源欄位]** 的下界。

   ![選擇映射工作流中突出顯示的源欄位控制項。](../assets/ui/activate-batch-profile-destinations/select-source-field.png)

1. 在 **[!UICONTROL 選擇源欄位]** 頁，選擇要包含在導出到目標的檔案中的配置檔案屬性和標識，然後選擇 **[!UICONTROL 選擇]**.

   >[!TIP]
   > 
   >您可以使用搜尋欄位來縮小選取範圍，如下圖所示。

   ![強制回應視窗，顯示可匯出至目的地的設定檔屬性。](../assets/ui/activate-batch-profile-destinations/select-source-field-modal.png)


1. 您選取要匯出的欄位現在會顯示在對應檢視中。 如果您願意，可以編輯導出檔案中的標題名稱。 要執行此操作，請在目標欄位上選取圖示。

   ![強制回應視窗，顯示可匯出至目的地的設定檔屬性。](../assets/ui/activate-batch-profile-destinations/mapping-step-select-target-field.png)

1. 在 **[!UICONTROL 選擇目標欄位]** 頁，在導出的檔案中鍵入所需的標題名稱，然後選擇 **[!UICONTROL 選擇]**.

   ![強制回應視窗中顯示標題的輸入好記名稱。](../assets/ui/activate-batch-profile-destinations/select-target-field-mapping.png)

1. 您選取要匯出的欄位現在會顯示在對應檢視中，並在匯出的檔案中顯示已編輯的標題。

   ![強制回應視窗，顯示可匯出至目的地的設定檔屬性。](../assets/ui/activate-batch-profile-destinations/select-target-field-updated.png)

1. （選用）您可以選取匯出的欄位為 [必填金鑰](#mandatory-keys) 或 [去重複化金鑰](#deduplication-keys).

   ![強制回應視窗，顯示可匯出至目的地的設定檔屬性。](../assets/ui/activate-batch-profile-destinations/select-mandatory-deduplication-key.png)

1. 若要新增更多要匯出的欄位，請重複上述步驟。

### 已知限制 {#known-limitations}

新 **[!UICONTROL 對應]** 頁面有下列已知限制：

#### 無法通過映射工作流選擇段成員資格屬性

由於已知限制，您目前無法使用 **[!UICONTROL 選擇欄位]** 窗口 `segmentMembership.status` 檔案匯出。 而是需要手動貼上值 `xdm: segmentMembership.status` 填入架構欄位，如下所示。

![螢幕記錄顯示啟動工作流程對應步驟中的區段成員資格因應措施。](/help/destinations/assets/ui/activate-batch-profile-destinations/segment-membership-mapping-step.gif)

檔案匯出會依下列方式而異，具體取決於 `segmentMembership.status` 已選取：
* 若 `segmentMembership.status` 欄位，導出的檔案包括 **[!UICONTROL 作用中]** 初始完整快照和 **[!UICONTROL 作用中]** 和 **[!UICONTROL 過期]** 成員。
* 若 `segmentMembership.status` 欄位未選中，導出的檔案僅包括 **[!UICONTROL 作用中]** 初始完整快照和後續增量導出中的成員。

#### 目前無法為匯出選取身分命名空間

目前不支援選取要匯出的身分命名空間，如下圖所示。 選取要匯出的任何身分命名空間，將會導致 **[!UICONTROL 檢閱]** 步驟。

![不支援的映射顯示身份導出](/help/destinations/assets/ui/activate-batch-profile-destinations/unsupported-identity-mapping.png)

如果您在測試期間需要將身分識別命名空間新增至匯出的檔案，可做為暫時因應措施，您可以：
* 對於要在匯出內容中包含身分命名空間的資料流，請使用舊版雲端儲存目標
* 將身分上傳至Experience Platform中，然後將其匯出至雲端儲存空間目的地。

## 請檢閱 {#review}

在 **[!UICONTROL 檢閱]** 頁面，您可以看到您所選內容的摘要。 選擇 **[!UICONTROL 取消]** 來分解流， **[!UICONTROL 返回]** 修改設定，或 **[!UICONTROL 完成]** 確認您的選擇並開始將資料傳送至目的地。

![審核步驟中的選擇摘要。](/help/destinations/assets/ui/activate-batch-profile-destinations/review.png)

### 同意政策評估 {#consent-policy-evaluation}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_viewApplicableConsentPolicies"
>title="檢視適用的同意原則"
>abstract="如果您的組織購買了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，請選取&#x200B;**[!UICONTROL 檢視適用的同意原則]**，以查看套用了哪些同意原則以及由於這些原則啟動中包含了多少個設定檔。如果您的公司無權存取上述 SKU，則會停用此控制項。"

如果您的組織購買了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，請選取&#x200B;**[!UICONTROL 檢視適用的同意原則]**，以查看套用了哪些同意原則以及由於這些原則啟動中包含了多少個設定檔。閱讀 [同意政策評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 以取得更多資訊。

### 資料使用原則檢查 {#data-usage-policy-checks}

在 **[!UICONTROL 檢閱]** 步驟中，Experience Platform也會檢查是否有任何資料使用策略違規。 以下顯示違反原則的範例。 除非您解決違規，否則無法完成區段啟用工作流程。 有關如何解決策略違規的資訊，請參閱 [資料使用策略違規](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) （位於資料控管檔案一節）。

![資料策略違規](../assets/common/data-policy-violation.png)

### 篩選區段 {#filter-segments}

此外，在此步驟中，您也可以使用頁面上的可用篩選器，以僅顯示排程或對應已隨此工作流程更新的區段。 您也可以切換要查看的表格欄。

![顯示審核步驟中可用區段篩選的螢幕記錄。](/help/destinations/assets/ui/activate-batch-profile-destinations/filter-segments-batch-review.gif)

如果您對您的選擇感到滿意，並且未檢測到任何違反策略的情況，請選擇 **[!UICONTROL 完成]** 確認您的選擇並開始將資料傳送至目的地。

## 驗證區段啟用 {#verify}

對於電子郵件行銷目的地和雲端儲存空間目的地，Adobe Experience Platform會建立 `.csv` 檔案。 預期會根據您在工作流程中設定的排程，在儲存位置中建立新檔案。 預設檔案格式如下所示，但您可以 [編輯檔案名的元件](#file-names):
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

例如，如果您選取每日匯出頻率，您會連續三天收到的檔案可能如下所示：

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

儲存位置中是否存在這些檔案是成功激活的確認。 若要了解匯出的檔案的結構，您可以 [下載範例.csv檔案](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). 此範例檔案包含設定檔屬性 `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`，和 `personalEmail.address`.
