---
keywords: Experience Platform；首頁；熱門主題；導出；導出
solution: Experience Platform
title: 在Privacy ServiceUI中管理隱私權工作
topic-legacy: UI guide
description: 瞭解如何使用Privacy Service使用者介面來協調和監控各種Experience Cloud應用程式的隱私權要求。
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 0%

---

# 在Privacy ServiceUI中管理隱私權工作

本檔案提供使用[!DNL Privacy Service]使用者介面建立和管理隱私權要求的步驟。

## 瀏覽[!DNL Privacy Service] UI儀表板

[!DNL Privacy Service] UI的控制面板提供兩個Widget，可讓您檢視隱私權工作的狀態：&quot;[!UICONTROL Status Report]&quot;和&quot;[!UICONTROL Job Requests]&quot;。 控制面板還顯示所顯示作業的當前選定規則。

![UI儀表板](../images/user-guide/dashboard.png)

### 規則類型

[!DNL Privacy Service] 支援數個隱私權規範的工作要求：

*  [!DNL California Consumer Privacy Act] ([!UICONTROL CCPA])
* 歐盟的[!DNL General Data Protection Regulation]([!UICONTROL GDPR])
* 泰國的[!DNL Personal Data Protection Act]([!UICONTROL PDPA_THA])
* 巴西的[!DNL Lei Geral de Proteção de Dados]([!UICONTROL LGPD_BRA])
* 紐西蘭[!DNL Privacy Act]([!UICONTROL NZPA_NZL])

每個規則類型的工作會個別追蹤。 要在規則類型之間切換，請選擇&#x200B;**[!UICONTROL Regulation Type]**&#x200B;下拉菜單並從清單中選擇所需的規則。

![規則類型下拉式清單](../images/user-guide/regulation.png)

變更規則類型時，控制面板會更新為顯示所有適用於所選規則的作業、篩選器、Widget和工作建立對話方塊。

![更新的控制面板](../images/user-guide/dashboard-update.png)

### 狀態報表

「狀態報表」介面工具集左側的圖表會追蹤任何已回報有錯誤的工作的已提交工作。 右側的圖表會追蹤接近30天相容性視窗結束的工作。

選取圖形上方的兩個切換按鈕之一，以顯示或隱藏其各自的量度。

![](../images/user-guide/hide-errors.png)

您可將滑鼠暫留在相關資料點上，即可檢視與圖形上任何資料點相關的確切作業數。

![將滑鼠移至資料點](../images/user-guide/mouse-over.png)

要查看有關給定資料點的詳細資訊，請選擇相關資料點以顯示「作業請求」構件中的相關作業。 請注意在工作清單上方套用的篩選。

![從介面工具集套用篩選](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>將篩選器套用至「工作請求」介面工具集後，您可以選取篩選藥丸上的&#x200B;**X**&#x200B;來移除篩選器。 然後，工作請求會返回預設追蹤清單。

### 工作請求

「工作請求」介面工具集會列出您組織中所有可用的工作請求，包括請求類型、目前狀態、到期日和申請人電子郵件等詳細資訊。

>[!NOTE]
>
>先前建立的工作資料僅能在完成日期後30天記憶體取。

您可以在「工作請求」標題下方的搜尋列中輸入關鍵字，以篩選清單。 清單會在您輸入時自動篩選，顯示包含符合您搜尋詞之值的請求。 您也可以使用&#x200B;**[!UICONTROL Requested on]**&#x200B;下拉式功能表，為列出的作業選擇時間範圍。

![作業請求搜索選項](../images/user-guide/job-search.png)

要查看特定作業請求的詳細資訊，請從清單中選擇該請求的作業ID以開啟&#x200B;**[!UICONTROL Job Details]**&#x200B;頁。

![GDPR UI工作詳細資訊](../images/user-guide/job-details.png)

此對話框包含有關每個[!DNL Experience Cloud]解決方案及其與整體作業相關的當前狀態的狀態資訊。 由於每個隱私權工作都是非同步的，因此頁面會顯示每個解決方案的最新通訊日期和時間(GMT)，因為有些解決方案需要比其他解決方案更多的時間來處理請求。

如果解決方案已提供任何其他資料，則可在此對話方塊中檢視。 您可以選取個別的產品列，以檢視此資料。

若要以CSV檔案形式下載完整的工作資料，請選取對話方塊右上角的&#x200B;**[!UICONTROL Export to CSV]**。

## 建立新的隱私權工作要求

>[!NOTE]
>
>為了建立隱私權工作要求，您必須為要存取或刪除其資料的特定客戶提供識別資訊。 請先閱讀有關[隱私權要求識別資料的檔案](../identity-data.md)，然後再繼續本節內容。

[!DNL Privacy Service] UI提供兩種建立新工作請求的方法：

* [使用請求產生器](#request-builder)
* [上傳JSON檔案](#json)

以下各節提供使用這些方法的步驟。

### 使用請求產生器{#request-builder}

使用「請求產生器」，您可以在使用者介面中手動建立新的隱私權工作請求。 「請求產生器」最適合用於較簡單和較小的請求集，因為「請求產生器」會限制每個使用者的請求只有ID類型。 對於更複雜的請求，請改為[上傳JSON檔案](#json)。

若要開始使用「請求產生器」，請在畫面右側的「狀態報表」介面工具集下方選取&#x200B;**[!UICONTROL Create Request]**。

![選擇建立請求](../images/user-guide/create-request.png)

將開啟&#x200B;**[!UICONTROL Create Request]**&#x200B;對話框，其中顯示針對當前選定的規則類型提交隱私作業請求的可用選項。

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

從清單中選取請求的&#x200B;**[!UICONTROL Job Type]**（「刪除」或「存取」）以及一或多個可用產品。

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

在&#x200B;**[!UICONTROL Namespace type]**&#x200B;下，為要傳送至[!DNL Privacy Service]的客戶ID選擇適當的名稱空間類型。

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

使用標準命名空間類型時，從下拉式選單（電子郵件、ECID或AAID）中選取命名空間，然後在文字方塊中的右側鍵入ID值，為每個ID按&#x200B;**\&lt;enter>**，將它新增至清單。

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

使用自訂命名空間類型時，您必須先在命名空間中手動輸入，才能提供下面的ID值。

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

完成後，選擇&#x200B;**[!UICONTROL Create]**。

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

對話方塊消失，新工作（或工作）會列在「工作請求」介面工具集中，以及其目前的處理狀態。

### 上傳JSON檔案{#json}

當建立更複雜的請求時（例如對每個正在處理的資料主體使用多個ID類型的請求），您可以上傳JSON檔案來建立請求。

在畫面右側的「狀態報表」介面工具集下方，選取&#x200B;**[!UICONTROL Create Request]**&#x200B;旁的箭頭。 從顯示的選項清單中，選擇&#x200B;**[!UICONTROL Upload JSON]**。

![請求建立選項](../images/user-guide/create-options.png)

此時會出現&#x200B;**[!UICONTROL Upload JSON]**&#x200B;對話方塊，提供您將JSON檔案拖放至其中的視窗。

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

如果您沒有要上傳的JSON檔案，請選取&#x200B;**[!UICONTROL Download Adobe-GDPR-Request.json]**&#x200B;以下載範本，您可以根據從資料主體收集到的值填入範本。


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


在您的電腦上找到JSON檔案，並將它拖曳至對話方塊視窗。 如果上載成功，則檔案名將出現在對話框中。 您可以視需要將更多JSON檔案拖放至對話方塊中，以繼續新增。

完成後，選擇&#x200B;**[!UICONTROL Create]**。 對話方塊消失，新工作（或工作）會列在「工作請求」介面工具集中，以及其目前的處理狀態。

### 後續步驟

閱讀本檔案後，您便瞭解如何使用[!DNL Privacy Service] UI來建立隱私權工作、檢視工作的詳細資料並監控其處理狀態，並在工作完成後下載結果。

有關如何使用[!DNL Privacy Service] API以程式設計方式執行這些作業的步驟，請參閱[開發人員指南](../api/getting-started.md)。
