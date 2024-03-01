---
keywords: Experience Platform；首頁；熱門主題；匯出；匯出
solution: Experience Platform
title: 管理Privacy Service UI中的隱私權工作
description: 瞭解如何使用Privacy Service使用者介面來協調及監控各種Experience Cloud應用程式的隱私權請求。
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: b16eae9698de6c20022fdf1a3ff659df35e440f6
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 14%

---

# 管理 Privacy Service UI 中的隱私權作業 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="執行資料主體隱私權要求"
>abstract="<h2>說明</h2><p>Adobe Experience Platform Privacy Service 可讓您代表想要存取或刪除其個人資料的客戶，根據隱私權法規建立和管理隱私權要求。</p>"

本檔案提供使用建立及管理隱私權請求的步驟。 [!DNL Privacy Service] 使用者介面。

>[!IMPORTANT]
>
>Privacy Service僅適用於資料主體和消費者權利要求。 不支援或允許將Privacy Service用於資料清理或維護的任何其他用途。 Adobe有法定義務須及時履行。 因此，不允許在Privacy Service上進行負載測試，因為這是僅限生產的環境，且會為有效隱私權請求建立不必要的待處理專案。
>
>現已設定每日硬性上傳限制，以協助防止濫用服務。 發現濫用系統的使用者將會停用其服務的存取權。 隨後將與他們舉行會議，討論他們的動作，並討論可接受的Privacy Service用途。

## 瀏覽 [!DNL Privacy Service] UI儀表板

的儀表板 [!DNL Privacy Service] UI提供兩個可讓您檢視隱私權工作狀態的Widget： &quot;[!UICONTROL 狀態報表]「和」[!UICONTROL 工作請求]「。 控制面板也會針對顯示的作業顯示目前選取的規則。

![UI儀表板](../images/user-guide/dashboard.png)

### 法規型別

[!DNL Privacy Service] 支援數項隱私權法規的工作要求。 下表列出支援的法規及其在UI中顯示的對應標籤：

| UI標籤 | 法規 |
| --- | --- |
| [!UICONTROL APA_AUS] | 此 [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL CPA] | 此 [!DNL Colorado Privacy Act] |
| [!UICONTROL CCPA] | 此 [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPRA_USA] | 此 [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA] | 此 [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL GDPR] | 歐盟的 [!DNL General Data Protection Regulation] |
| [!UICONTROL HIPAA_AUS] | 此 [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL LGPD_BRA] | 巴西的 [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL MHMDA] | 此 [!DNL Washington My Health My Data Act] |
| [!UICONTROL NZPA_NZL] | 紐西蘭 [!DNL Privacy Act] |
| [!UICONTROL PDPA_THA] | 泰國的 [!DNL Personal Data Protection Act] |
| [!UICONTROL UCPA] | 此 [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA] | 此 [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

<!--Not released yet:
| [!UICONTROL PDPA_VNM] | Vietnam's [!DNL Personal Data Protection Decree] |
 -->

>[!NOTE]
>
>請參閱以下主題的概觀： [支援的隱私權法規](../regulations/overview.md) 以取得每項法規之法律內容的詳細資訊。

系統會分別追蹤每種規則型別的工作。 若要切換規則型別，請選取 **[!UICONTROL 法規型別]** 下拉式功能表，並從清單中選取所需的規則。

![具有「法規型別」下拉式清單的Privacy Service主控台。](../images/user-guide/regulation.png)

在變更法規型別後，儀表板會更新以顯示適用於所選法規的所有操作、篩選器、Widget和工作建立對話方塊。

![已更新儀表板](../images/user-guide/dashboard-update.png)

### 狀態報表

「狀態報表」Widget左側的圖形，會針對報表回傳時可能含有錯誤的任何工作，追蹤已提交的工作。 右側的圖表會追蹤接近30天規定期間結束的工作。

選取圖表上方的兩個切換按鈕之一，以顯示或隱藏其各自的量度。

![](../images/user-guide/hide-errors.png)

您可以將滑鼠停留在有問題的資料點上，以檢視與圖表上任何資料點相關聯的確切工作數目。

![將滑鼠移到資料點上方](../images/user-guide/mouse-over.png)

若要檢視指定資料點的進一步詳細資訊，請選取相關資料點，以在「工作請求」Widget中顯示相關工作。 記下套用至工作清單正上方的篩選器。

![從Widget套用的篩選器](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>將篩選器套用至工作請求Widget後，您可以選取 **X** 在過濾藥丸上。 接著，工作請求會傳回預設追蹤清單。

### 工作請求

工作請求Widget會列出組織中所有可用的工作請求，包括請求型別、目前狀態、到期日及請求者電子郵件等詳細資訊。

>[!NOTE]
>
>先前建立之工作的資料僅可在完成日期後30天記憶體取。

您可以在工作請求標題下方的搜尋列中鍵入關鍵字，以篩選清單。 清單會在您輸入時自動篩選，顯示包含符合搜尋詞之值的請求。 您也可以使用 **[!UICONTROL 申請時間]** 下拉式功能表，為列出的工作選取時間範圍。

![工作請求搜尋選項](../images/user-guide/job-search.png)

若要檢視特定工作請求的詳細資訊，請從清單中選取請求的工作ID以開啟 **[!UICONTROL 工作詳細資訊]** 頁面。

![GDPR UI工作詳細資料](../images/user-guide/job-details.png)

此對話方塊包含每個專案的狀態資訊 [!DNL Experience Cloud] 解決方案及其相對於整體工作的目前狀態。 由於每個隱私權工作非同步，頁面會顯示每個解決方案的最新通訊日期和時間(GMT)，因為有些解決方案需要的時間比其他解決方案長。

如果解決方案已提供任何其他資料，便可以在此對話方塊中檢視。 您可以選取個別產品列來檢視此資料。

若要將完整的工作資料下載為CSV檔案，請選取 **[!UICONTROL 匯出至CSV]** 位於對話方塊的右上角。

## 建立新的隱私權作業要求 {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="說明"
>abstract="<ul><li>在左側導覽中選取<a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=zh-Hant#logging-in-from-experience-platform">要求</a>以開啟隱私權 UI，然後選取<b>建立要求</b>。</li><li>從這裡您可以使用要求產生器或上傳資料主體的 JSON 檔案。</li><li>如果使用要求產生器，請選取工作類型 (存取和/或刪除)，然後選擇您提供的身分類型 (電子郵件、ECID 或 AAID) 或輸入自訂身分命名空間。為客戶輸入適當的身分值，完成後選取<b>建立</b>。</li><li>如果上傳 JSON 檔案，請選取「建立要求」旁邊的箭頭。從選項清單中，選取<b>上傳 JSON</b> 並上傳您的檔案。如果您沒有要上傳的 JSON 檔案，請選取<b>下載 Adobe-GDPR-Request.json</b> 以下載您可以填入的範本。完成後，上傳 JSON 並選取<b>建立</b>。</li><li>如需有關此功能的更多說明，請參閱 Experience League 上的 <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=zh-Hant">Privacy Service 使用手冊</a>。</li></ul>"

>[!NOTE]
>
>為了建立隱私權工作請求，您必須針對要存取或刪除其資料的特定客戶提供身分資訊。 請在以下位置檢閱檔案： [隱私權請求的身分資料](../identity-data.md) 再繼續本節。

此 [!DNL Privacy Service] UI提供兩種建立新工作請求的方法：

* [使用請求產生器](#request-builder)
* [上傳JSON檔案](#json)

以下各節提供使用其中每種方法的步驟。

### 使用請求產生器 {#request-builder}

使用「請求產生器」，您可以在使用者介面中手動建立新的隱私權工作請求。 請求產生器最適合用於較簡單且規模較小的請求集，因為請求產生器限制每個使用者的請求只能有ID型別。 若是更複雜的請求，最好是執行下列動作 [上傳JSON檔案](#json) 而非。

若要開始使用請求產生器，請選取「 」 **[!UICONTROL 建立請求]** 位於畫面右側的「狀態報表」Widget下方。

![選取建立請求](../images/user-guide/create-request.png)

此 **[!UICONTROL 建立請求]** 對話方塊隨即開啟，顯示可用選項，用於針對目前選取的法規型別提交隱私權工作請求。

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

選取 **[!UICONTROL 工作型別]** 請求（「刪除」或「存取」）以及清單中一個或多個可用產品的完整清單。

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

在 **[!UICONTROL 名稱空間型別]**，請為要傳送至的客戶ID選取適當的名稱空間型別 [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

使用標準名稱空間型別時，請從下拉式選單中選取名稱空間（電子郵件、ECID或AAID），然後在右側的文字方塊中輸入ID值，然後按 **\&lt;enter>** 以將每個ID新增至清單。

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

使用自訂名稱空間型別時，您必須手動輸入名稱空間，才能在下方提供ID值。

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

完成後，選取 **[!UICONTROL 建立]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

對話方塊會消失，而新工作（或多個工作）及其目前處理狀態會列在工作請求Widget中。

### 上傳JSON檔案 {#json}

建立更複雜的請求時（例如針對每個處理中的資料主體使用多個ID型別的請求），您可以透過上傳JSON檔案來建立請求。

選取旁的箭頭 **[!UICONTROL 建立請求]**，位於畫面右側的「狀態報表」Widget下方。 從出現的選項清單中，選取 **[!UICONTROL 上傳JSON]**.

![請求建立選項](../images/user-guide/create-options.png)

此 **[!UICONTROL 上傳JSON]** 對話方塊隨即出現，為您提供視窗，以便將JSON檔案拖放至中。

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

如果您沒有要上傳的JSON檔案，請選取「 」 **[!UICONTROL 下載Adobe-GDPR-Request.json]** 以下載範本，您可根據從資料主體收集的值填入。


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


在電腦上找到JSON檔案，並將其拖曳至對話方塊視窗。 如果上傳成功，檔案名稱會顯示在對話方塊中。 您可以視需要繼續新增更多JSON檔案，方法是將其拖放至對話方塊中。

完成後，選取 **[!UICONTROL 建立]**. 對話方塊會消失，而新工作（或多個工作）及其目前處理狀態會列在工作請求Widget中。

### 後續步驟

閱讀本檔案後，您已瞭解如何使用 [!DNL Privacy Service] UI以建立隱私權工作、檢視工作的詳細資訊和監視其處理狀態，並在完成後下載結果。

如需有關如何使用以程式設計方式執行這些操作的步驟， [!DNL Privacy Service] API，請參閱 [API指南](../api/overview.md).
