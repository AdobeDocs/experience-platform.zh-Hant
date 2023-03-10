---
keywords: Experience Platform；首頁；熱門主題；匯出；匯出
solution: Experience Platform
title: 在Privacy ServiceUI中管理隱私權作業
description: 了解如何使用Privacy Service使用者介面協調及監控各種Experience Cloud應用程式的隱私權要求。
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: e539b1e165227d9a888bfe12d8205e285b3ce259
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---

# 在Privacy ServiceUI中管理隱私權作業 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="說明"
>abstract=""

本檔案提供使用 [!DNL Privacy Service] 使用者介面。

## 瀏覽 [!DNL Privacy Service] UI控制面板

的控制面板 [!DNL Privacy Service] UI提供兩個小工具，可讓您檢視隱私權工作的狀態：&quot;[!UICONTROL 狀態報表]&quot;和&quot;[!UICONTROL 工作請求]」。 控制面板也會顯示所顯示作業的目前選取規則。

![UI控制面板](../images/user-guide/dashboard.png)

### 規範類型

[!DNL Privacy Service] 支援數個隱私權法規的工作要求。 下表列出UI中顯示的支援的法規及其對應標籤：

| UI標籤 | 規範 |
| --- | --- |
| [!UICONTROL CCPA] | 此 [!DNL California Consumer Privacy Act] |
| [!UICONTROL GDPR] | 歐盟 [!DNL General Data Protection Regulation] |
| [!UICONTROL PDPA_THA] | 泰國 [!DNL Personal Data Protection Act] |
| [!UICONTROL LGPD_BRA] | 巴西 [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL NZPA_NZL] | 紐西蘭 [!DNL Privacy Act] |
| [!UICONTROL VCDPA_USA] | 此 [!DNL Virginia Consumer Data Protection Act] |
| [!UICONTROL CPRA_USA] | 此 [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL APA_AUS] | 此 [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL HIPAA_AUS] | 此 [!DNL Health Insurance Portability and Accountability Act] |

{style="table-layout:auto"}

>[!NOTE]
>
>請參閱 [支援的隱私權法規](../regulations/overview.md) ，以了解有關各條例的法律背景的更多資訊。

每個規則類型的作業將單獨跟蹤。 若要在規則類型之間切換，請選取 **[!UICONTROL 規範類型]** 下拉式選單中，然後從清單中選取所需的規則。

![規則類型下拉式清單](../images/user-guide/regulation.png)

更改規則類型後，控制面板將更新，以顯示適用於所選規則的所有操作、篩選器、小部件和職務建立對話框。

![更新的控制面板](../images/user-guide/dashboard-update.png)

### 狀態報表

狀態報表Widget左側的圖形會追蹤已提交的作業，以針對可能回報有錯誤的任何作業。 右側的圖表會追蹤接近30天法規遵循期間結尾的工作。

選取圖形上方的兩個切換按鈕之一，以顯示或隱藏其個別的量度。

![](../images/user-guide/hide-errors.png)

您可以將滑鼠移至相關資料點上，即可檢視與圖形上任何資料點相關聯的確切作業數量。

![滑鼠移過資料點](../images/user-guide/mouse-over.png)

若要檢視特定資料點的詳細資訊，請選取相關資料點，以在「工作請求」介面工具集中顯示相關作業。 記下剛在工作清單上方套用的篩選器。

![從介面工具集套用篩選](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>當篩選器已套用至「工作請求」介面工具集時，您可以選取 **X** 吃過濾藥。 接著，工作請求會返回預設追蹤清單。

### 工作請求

「工作請求」小工具集會列出您組織中所有可用的工作請求，包括請求類型、當前狀態、到期日和請求者電子郵件等詳細資訊。

>[!NOTE]
>
>先前建立之作業的資料僅可在完成日期後30天記憶體取。

您可以在「工作請求」標題下方的搜尋列中輸入關鍵字，以篩選清單。 清單會在您輸入時自動篩選，顯示包含符合您搜尋詞之值的請求。 您也可以使用 **[!UICONTROL 請求日期]** 下拉式功能表，選取列出作業的時間範圍。

![作業請求搜索選項](../images/user-guide/job-search.png)

要查看特定作業請求的詳細資訊，請從清單中選擇請求的作業ID以開啟 **[!UICONTROL 作業詳細資訊]** 頁面。

![GDPR UI工作詳細資訊](../images/user-guide/job-details.png)

此對話框包含有關每個 [!DNL Experience Cloud] 解決方案及其當前狀態。 由於每個隱私權工作都為非同步作業，因此頁面會顯示每個解決方案的最新通訊日期和時間(GMT)，因為有些解決方案處理請求所需的時間會比其他解決方案多。

如果解決方案已提供任何其他資料，則可在此對話方塊中檢視該資料。 您可以選取個別產品列，以檢視此資料。

若要以CSV檔案格式下載完整的作業資料，請選取 **[!UICONTROL 匯出至CSV]** 對話框的右上角。

## 建立新的隱私權工作請求 {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="說明"
>abstract=""

>[!NOTE]
>
>若要建立隱私權工作請求，您必須為要存取或刪除其資料的特定客戶提供身分資訊。 請查閱 [隱私權要求的身分資料](../identity-data.md) ，再繼續使用本小節。

此 [!DNL Privacy Service] UI提供兩種建立新作業請求的方法：

* [使用請求產生器](#request-builder)
* [上傳JSON檔案](#json)

以下各節將提供使用這些方法的步驟。

### 使用請求產生器 {#request-builder}

您可以使用「請求產生器」，在使用者介面中手動建立新的隱私權工作請求。 請求產生器最適合用於較簡單和較小的請求集，因為請求產生器會限制每個使用者的請求只有ID類型。 對於更複雜的請求，最好 [上傳JSON檔案](#json) 。

若要開始使用請求產生器，請選取 **[!UICONTROL 建立請求]** 位於畫面右側的「狀態報表」介面工具集下方。

![選擇建立請求](../images/user-guide/create-request.png)

此 **[!UICONTROL 建立請求]** 對話框開啟，顯示用於提交當前所選規則類型的隱私權作業請求的可用選項。

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

選取 **[!UICONTROL 作業類型]** （「刪除」或「存取」），以及清單中的一或多個可用產品。

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

在 **[!UICONTROL 命名空間類型]**，請為要傳送至的客戶ID選取適當的命名空間類型 [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

使用標準命名空間類型時，請從下拉式選單（電子郵件、ECID或AAID）中選取命名空間，然後在右側的文字方塊中輸入ID值，按 **\&lt;enter>** 將每個ID新增至清單。

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

使用自訂命名空間類型時，您必須先手動輸入命名空間，才能提供下列ID值。

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

完成後，請選取 **[!UICONTROL 建立]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

對話方塊會消失，新作業（或作業）會列在「作業請求」Widget中，及其目前的處理狀態。

### 上傳JSON檔案 {#json}

建立更複雜的請求時（例如對每個處理中的資料主體使用多個ID類型的請求），您可以上傳JSON檔案來建立請求。

選取旁邊的箭頭 **[!UICONTROL 建立請求]**，位於畫面右側的「狀態報表」介面工具集下方。 從顯示的選項清單中，選取 **[!UICONTROL 上傳JSON]**.

![請求建立選項](../images/user-guide/create-options.png)

此 **[!UICONTROL 上傳JSON]** 對話方塊，提供視窗供您將JSON檔案拖放至。

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

如果您沒有要上傳的JSON檔案，請選取 **[!UICONTROL 下載Adobe-GDPR-Request.json]** 下載範本，您可以根據從資料主體收集的值填入。


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


在電腦上找出JSON檔案，並將其拖曳至對話方塊視窗中。 如果上傳成功，檔案名稱會顯示在對話方塊中。 您可以視需要將JSON檔案拖曳至對話方塊中，以繼續新增更多JSON檔案。

完成後，請選取 **[!UICONTROL 建立]**. 對話方塊會消失，新作業（或作業）會列在「作業請求」Widget中，及其目前的處理狀態。

### 後續步驟

閱讀本檔案，您已學會如何使用 [!DNL Privacy Service] UI可建立隱私權工作、檢視工作的詳細資訊並監控其處理狀態，並在完成後下載結果。

有關如何以程式設計方式使用 [!DNL Privacy Service] API，請參閱 [API指南](../api/overview.md).
