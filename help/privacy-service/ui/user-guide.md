---
keywords: Experience Platform；首頁；熱門主題；導出；導出
solution: Experience Platform
title: 在Privacy ServiceUI中管理隱私作業
description: 瞭解如何使用Privacy Service用戶介面來協調和監視各種Experience Cloud應用程式的隱私請求。
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 14%

---

# 在Privacy ServiceUI中管理隱私作業 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="執行資料主體隱私權要求"
>abstract="<h2>說明</h2><p>Adobe Experience Platform Privacy Service 可讓您代表想要存取或刪除其個人資料的客戶，根據隱私權法規建立和管理隱私權要求。</p>"

本文檔提供了使用 [!DNL Privacy Service] 用戶介面。

>[!IMPORTANT]
>
>Privacy Service僅用於資料主題和消費者權利請求。 不支援或不允許使用Privacy Service進行資料清理或維護。 Adobe有法律義務及時履行這些義務。 因此，不允許對Privacy Service進行負載測試，因為它是僅生產環境，並會建立有效隱私請求的不必要的積壓。
>
>現在已設定硬性每日上載限制，以幫助防止濫用服務。 發現濫用系統的用戶將禁用其對服務的訪問權限。 隨後將與他們舉行會議，討論他們的行動並討論可接受的Privacy Service用途。

## 瀏覽 [!DNL Privacy Service] UI儀表板

用於 [!DNL Privacy Service] UI提供了兩個小部件，允許您查看隱私作業的狀態：&quot;[!UICONTROL 狀態報告]&quot;和&quot;[!UICONTROL 作業請求]。 控制板還顯示所顯示作業的當前選定規則。

![UI儀表板](../images/user-guide/dashboard.png)

### 規則類型

[!DNL Privacy Service] 支援多個隱私法規的作業請求。 下表列出了UI中表示的受支援的法規及其相應標籤：

| UI標籤 | 管制 |
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
>請參閱 [支援的隱私法規](../regulations/overview.md) 瞭解有關每個條例的法律背景的更多資訊。

對每種管制類型的作業分別進行跟蹤。 要在調節類型之間切換，請選擇 **[!UICONTROL 規則類型]** 下拉菜單，然後從清單中選擇所需的調節。

![「Regulation Type（調節類型）」下拉清單](../images/user-guide/regulation.png)

更改規則類型後，控制板將更新，以顯示應用於所選規則的所有操作、篩選器、小部件和職務建立對話框。

![已更新的儀表板](../images/user-guide/dashboard-update.png)

### 狀態報告

狀態報告構件左側的圖形跟蹤已提交的作業與可能已返回報告但出現錯誤的任何作業。 右側的圖表跟蹤接近30天符合性窗口結束的作業。

選擇圖形上方的兩個切換按鈕之一以顯示或隱藏各自的度量。

![](../images/user-guide/hide-errors.png)

通過將滑鼠懸停在有關的資料點上，可以查看與圖形上任何資料點關聯的作業的確切數量。

![滑鼠指針](../images/user-guide/mouse-over.png)

要查看有關給定資料點的詳細資訊，請選擇有關的資料點以顯示作業請求構件中的關聯作業。 請注意在作業清單上方應用的篩選器。

![從小部件應用篩選器](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>將篩選器應用到作業請求構件後，可以通過選擇 **X** 在濾丸上。 然後，作業請求返回預設跟蹤清單。

### 作業請求

「作業請求」構件列出組織中的所有可用作業請求，包括請求類型、當前狀態、到期日期和申請人電子郵件等詳細資訊。

>[!NOTE]
>
>之前建立的作業的資料僅在完成日期後30天內可訪問。

您可以在「工作請求」標題下的搜索欄中鍵入關鍵字來篩選清單。 該清單在您鍵入時自動過濾，顯示包含與搜索項匹配值的請求。 您還可以使用 **[!UICONTROL 請求時間]** 下拉菜單，以選擇列出作業的時間範圍。

![作業請求搜索選項](../images/user-guide/job-search.png)

要查看特定作業請求的詳細資訊，請從清單中選擇該請求的作業ID以開啟 **[!UICONTROL 作業詳細資訊]** 的子菜單。

![GDPR UI作業詳細資訊](../images/user-guide/job-details.png)

此對話框包含有關每個 [!DNL Experience Cloud] 解決方案及其當前狀態。 由於每個隱私作業都是非同步的，因此該頁會顯示每個解決方案的最新通信日期和時間(GMT)，因為有些解決方案處理請求所需的時間比其他解決方案要長。

如果解決方案提供了任何附加資料，則可以在此對話框中查看。 您可以通過選擇單個產品行來查看此資料。

要將完整的作業資料作為CSV檔案下載，請選擇 **[!UICONTROL 導出為CSV]** 對話框的右上角。

## 建立新的隱私作業請求 {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="說明"
>abstract="<ul><li>在左側導覽中選取<a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html#logging-in-from-experience-platform">要求</a>以開啟隱私權 UI，然後選取<b>建立要求</b>。</li><li>從這裡您可以使用要求產生器或上傳資料主體的 JSON 檔案。</li><li>如果使用要求產生器，請選取工作類型 (存取和/或刪除)，然後選擇您提供的身分類型 (電子郵件、ECID 或 AAID) 或輸入自訂身分命名空間。為客戶輸入適當的身分值，完成後選取<b>建立</b>。</li><li>如果上傳 JSON 檔案，請選取「建立要求」旁邊的箭頭。從選項清單中，選取<b>上傳 JSON</b> 並上傳您的檔案。如果您沒有要上傳的 JSON 檔案，請選取<b>下載 Adobe-GDPR-Request.json</b> 以下載您可以填入的範本。完成後，上傳 JSON 並選取<b>建立</b>。</li><li>如需有關此功能的更多說明，請參閱 Experience League 上的 <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=zh-Hant">Privacy Service 使用手冊</a>。</li></ul>"

>[!NOTE]
>
>為了建立隱私作業請求，您必須為要訪問或刪除其資料的特定客戶提供身份資訊。 請在 [隱私請求的標識資料](../identity-data.md) 繼續本節。

的 [!DNL Privacy Service] UI提供了兩種建立新作業請求的方法：

* [使用請求生成器](#request-builder)
* [上載JSON檔案](#json)

以下各節提供了使用這些方法的步驟。

### 使用請求生成器 {#request-builder}

使用請求生成器，可以在用戶介面中手動建立新的隱私作業請求。 請求生成器最適合用於更簡單、更小的請求集，因為請求生成器將請求限制為每個用戶只具有ID類型。 對於更複雜的請求，最好是 [上載JSON檔案](#json) 的雙曲餘切值。

要開始使用請求生成器，請選擇 **[!UICONTROL 建立請求]** 位於螢幕右側的「狀態報告」小部件下。

![選擇建立請求](../images/user-guide/create-request.png)

的 **[!UICONTROL 建立請求]** 對話框開啟，其中顯示為當前選定的規則類型提交隱私作業請求的可用選項。

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

選擇 **[!UICONTROL 作業類型]** 請求（「刪除」或「訪問」）和清單中的一個或多個可用產品。

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

下 **[!UICONTROL 命名空間類型]**，為要發送到的客戶ID選擇相應的命名空間類型 [!DNL Privacy Service]。

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

使用標準命名空間類型時，從下拉菜單（電子郵件、ECID或AAID）中選擇一個命名空間，然後在文本框中的右鍵鍵入ID值，按 **\&lt;enter>** 將其添加到清單中。

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

使用自定義命名空間類型時，必須在提供以下ID值之前手動鍵入命名空間。

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

完成後，選擇 **[!UICONTROL 建立]**。

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

該對話框消失，新作業（或作業）隨其當前處理狀態一起列在作業請求構件中。

### 上載JSON檔案 {#json}

建立更複雜的請求時，可以通過上載JSON檔案來建立請求。

選擇旁邊的箭頭 **[!UICONTROL 建立請求]**，位於螢幕右側的「狀態報告」小部件下。 從顯示的選項清單中，選擇 **[!UICONTROL 上載JSON]**。

![請求建立選項](../images/user-guide/create-options.png)

的 **[!UICONTROL 上載JSON]** 對話框，提供一個窗口，可將JSON檔案拖放到其中。

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

如果沒有要上載的JSON檔案，請選擇 **[!UICONTROL 下載Adobe-GDPR-Request.json]** 下載模板，您可以根據從資料主題收集的值來填充該模板。


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


在電腦上找到JSON檔案，並將其拖入對話窗口。 如果上載成功，則檔案名將顯示在對話框中。 您可以根據需要將更多JSON檔案拖放到對話框中，以繼續添加。

完成後，選擇 **[!UICONTROL 建立]**。 該對話框消失，新作業（或作業）隨其當前處理狀態一起列在作業請求構件中。

### 後續步驟

通過閱讀此文檔，您已學會了如何使用 [!DNL Privacy Service] UI用於建立隱私作業、查看作業的詳細資訊並監視其處理狀態，並在完成後下載結果。

有關如何使用 [!DNL Privacy Service] API，請參閱 [API指南](../api/overview.md)。
