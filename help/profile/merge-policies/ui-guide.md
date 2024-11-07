---
title: 合併原則UI指南
type: Documentation
description: 瞭解如何使用Adobe Experience Platform使用者介面處理合併原則。
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: 400b20578e9a13fa2f41462b188707a34a462ea9
workflow-type: tm+mt
source-wordcount: '2455'
ht-degree: 2%

---


# 合併原則 UI 指南

Adobe Experience Platform可讓您將多個來源的資料片段彙整在一起，並將它們合併，以便檢視每個個別客戶的完整檢視。 將這個資料集合在一起時，合併原則是[!DNL Platform]用來決定資料優先順序的方式以及將合併哪些資料以建立統一檢視的規則。

使用RESTful API或使用者介面，您可以建立新的合併原則、管理現有原則，並為您的組織設定預設合併原則。 本指南提供使用Adobe Experience Platform使用者介面(UI)處理合併原則的逐步指示。

若要進一步瞭解合併原則及其在Experience Platform中所扮演的角色，請先閱讀[合併原則概觀](overview.md)。

## 快速入門

本指南需要您實際瞭解幾項重要的[!DNL Experience Platform]功能。 在遵循本指南之前，請檢視以下服務的檔案：

* [即時客戶個人檔案](../home.md)：根據來自多個來源的彙總資料，提供統一的即時客戶個人檔案。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md)：透過橋接擷取到[!DNL Platform]中的不同資料來源的身分，啟用即時客戶個人檔案。
* [體驗資料模型(XDM)](../../xdm/home.md)： [!DNL Platform]用來組織客戶體驗資料的標準化架構。

## 檢視合併原則 {#view-merge-policies}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_101221_404"
>title="找不到合併原則"
>abstract="這代表平台無法找到所要求的合併原則。若要解決此錯誤，請嘗試以下其中一項解決方案：<ul><li>確保 URL 中列出正確的合併原則 ID。</li><li>根據您正在嘗試存取的合併原則，確認您擁有正確的組織和沙箱組合。</li></ul>"

在[!DNL Experience Platform] UI中，您可以透過選取左側導覽中的&#x200B;**[!UICONTROL 設定檔]**，然後選取&#x200B;**[!UICONTROL 合併原則]**&#x200B;索引標籤，開始使用合併原則。

此索引標籤包含貴組織的所有現有合併原則清單，以及每個合併原則的詳細資訊，包括原則名稱、合併原則是否為預設合併原則，以及合併原則相關的結構描述類別。

![顯示合併原則瀏覽頁面。](../images/merge-policies/landing.png)

若要選取顯示哪些詳細資訊，或新增其他資料行至顯示，請選取![資料行設定圖示](../../images/icons/column-settings.png)並選取資料行名稱，以新增或移除檢視中的資料行。

![顯示可用於自訂合併原則瀏覽頁面的選項。](../images/merge-policies/adjust-view.png)

## 建立合併原則 {#create-a-merge-policy}

若要建立新的合併原則，請選取[合併原則]索引標籤上的[建立合併原則] ****，以輸入新的合併原則工作流程。

![醒目提示建立按鈕的合併原則登陸頁面。](../images/merge-policies/create-new.png)

**[!UICONTROL 新合併原則]**&#x200B;工作流程需要您透過一系列引導式步驟，為您的新合併原則提供重要資訊。 以下各節將概述這些步驟。

![新的合併原則工作流程。](../images/merge-policies/create.png)

## [!UICONTROL 設定] {#configure}

工作流程的第一步可讓您提供基本資訊，以設定合併原則。 此資訊包括：

* **[!UICONTROL 名稱]**：您的合併原則名稱應該要有描述性但簡潔。
* **[!UICONTROL 結構描述類別]**：與合併原則關聯的XDM結構描述類別。 這會指定建立此合併原則的結構描述類別。 組織可以針對每個結構描述類別建立多個合併原則。 目前UI中只有[!UICONTROL XDM個別設定檔]類別可用。 您可以選取&#x200B;**[!UICONTROL 檢視聯合結構描述]**&#x200B;來預覽結構描述類別的聯合結構描述。 如需詳細資訊，請參閱後面有關[檢視聯合結構描述](#view-union-schema)的章節。
* **[!UICONTROL ID拼接]**：此欄位定義如何判斷客戶的相關身分。 身分拼接有兩個可能的值，瞭解您選取的身分拼接型別將如何影響您的資料非常重要。 若要深入瞭解，請參閱[合併原則概述](overview.md)。
   * **[!UICONTROL 無]**：不執行身分拼接。
   * **[!UICONTROL 私人身分圖表]**：根據您的私人身分圖表執行身分拼接。
* **[!UICONTROL 預設合併原則]**：可讓您選取此合併原則是否為貴組織預設的切換按鈕。 如果選取器已開啟，系統會顯示警告以要求您確認要變更組織的預設合併原則。 請參閱[合併原則概述](overview.md)，深入瞭解預設合併原則。
  ![說明當合併原則設定為預設合併原則時所發生情形的彈出視窗。](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Active-On-Edge合併原則]**：可讓您選取此合併原則在Edge上是否有效的切換按鈕。 為確保所有設定檔消費者在邊緣上使用相同的檢視，可將邊緣上的合併原則標籤為使用中。 為了在Edge上啟用對象（標示為Edge對象），該對象必須繫結至Edge上標示為「作用中」的合併原則。 如果對象是&#x200B;**非**，繫結至在Edge上標示為「作用中」的合併原則，則該對象不會在Edge上標示為「作用中」，而會標示為串流對象。 此外，組織中的每個沙箱只能有&#x200B;**一個**&#x200B;在邊緣上有效的合併原則。

必填欄位完成後，您可以選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續工作流程。

![已完成的[設定]畫面，顯示[下一步]按鈕。](../images/merge-policies/create-complete.png)

## [!UICONTROL 檢視聯合結構描述] {#view-union-schema}

在建立或編輯合併原則時，您可以選取&#x200B;**[!UICONTROL 檢視聯合結構描述]**，以檢視所選結構描述類別的聯合結構描述。

![新合併原則工作流程上會醒目顯示[檢視聯合結構描述]按鈕。](../images/merge-policies/view-union-schema.png)

這會開啟[!UICONTROL 檢視聯合結構描述]對話方塊，顯示與聯合結構描述相關的所有貢獻結構描述、身分和關係。 您可以使用此對話方塊來探索聯合結構描述，其方式與存取Platform UI [!UICONTROL 設定檔]區段中的[!UICONTROL 聯合結構描述]索引標籤相同。

如需有關聯合結構描述的詳細資訊，包括如何在合併原則工作流程中顯示的[!UICONTROL 聯合結構描述]索引標籤或[!UICONTROL 檢視聯合結構描述]對話方塊中與它們互動，請造訪[聯合結構描述UI指南](../ui/union-schema.md)。

![檢視聯合結構描述對話方塊。](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL 選取設定檔資料集] {#select-profile-datasets}

在&#x200B;**[!UICONTROL 選取設定檔資料集]**&#x200B;畫面上，您必須選取要用於合併原則的&#x200B;**[!UICONTROL 合併方法]**。 同樣顯示在熒幕上的是貴組織中，與上一個熒幕選取的結構描述類別相關的[!UICONTROL 設定檔資料集]總數。

根據您選擇的合併方法，所有設定檔資料集都將按其上次更新的順序（時間戳記排序）合併，否則您需要選取要納入合併原則的設定檔資料集，以及合併它們的順序（資料集優先順序）。

如需合併方法的詳細資訊，請參閱[合併原則概觀](overview.md)。

>[!BEGINTABS]

>[!TAB 已排序的時間戳記]

選取&#x200B;**[!UICONTROL 排序的時間戳記]**&#x200B;作為合併方法，表示最近更新的資料集中的屬性將取得優先權。 這適用於所有設定檔資料集。

>[!NOTE]
>
>**[!UICONTROL 設定檔資料集]**&#x200B;旁方括弧內的數字（例如顯示影像中的`(37)`）顯示將包含的設定檔資料集總數。

![顯示選取之時間戳記排序合併方法的影像。](../images/merge-policies/timestamp-ordered.png)

>[!TAB 資料集優先順序]

選取&#x200B;**[!UICONTROL 資料集優先順序]**&#x200B;做為合併方法需要您選取設定檔資料集，並手動排列其優先順序。 列出的每個資料集也會包含上次擷取批次的狀態，或顯示未擷取任何批次至該資料集的通知。

您可以從資料集清單中選取最多50個要納入合併原則的資料集。

>[!NOTE]
>
>**[!UICONTROL 設定檔資料集]**&#x200B;旁方括弧內的數字（例如顯示影像中的`(37)`）會顯示可供選取的設定檔資料集總數。

資料集經選取後，便會新增至&#x200B;**[!UICONTROL 選取資料集]**&#x200B;區段，讓您拖放資料集，並根據所需的優先順序進行排序。 當在清單中調整資料集時，資料集旁的序數（1、2、3等）將會更新，顯示優先順序（1會獲得最高優先順序，然後2接著再）。

選取資料集也會更新&#x200B;**[!UICONTROL 聯合結構描述]**&#x200B;區段，顯示每個資料集貢獻資料的聯合結構描述中的欄位。 如需聯合結構描述的詳細資訊，包括如何與UI中的視覺效果互動，請參考[聯合結構描述UI指南](../ui/union-schema.md)

![顯示已選取資料集優先順序的影像，以及您選取該選項時所需的對應設定。](../images/merge-policies/dataset-precedence.png)

>[!ENDTABS]

## [!UICONTROL 選取ExperienceEvent資料集] {#select-experienceevent-datasets}

工作流程的下一步需要您選取ExperienceEvent資料集。 此畫面受到您在[[!UICONTROL 選取設定檔資料集]](#select-profile-datasets)畫面上選取的合併方法影響。

>[!BEGINTABS]

>[!TAB 已排序的時間戳記]

如果您選取&#x200B;**[!UICONTROL 已排序的時間戳記]**&#x200B;作為設定檔資料集的合併方法，則最近更新的ExperienceEvent資料集中的屬性也會在這裡取得優先權。

>[!NOTE]
>
>**[!UICONTROL ExperienceEvent資料集]**&#x200B;旁方括弧內的數字（例如顯示影像中的`(1)`）顯示貴組織所建立的、與您在合併原則設定畫面中所選結構描述類別相關的ExperienceEvent資料集總數。

![會顯示與結構描述類別相關的ExperienceEvent資料集總數。](../images/merge-policies/timestamp-experienceevent.png)

>[!TAB 資料集優先順序]

如果您選取&#x200B;**[!UICONTROL 資料集優先順序]**&#x200B;作為設定檔資料集的合併方法，則需要選取要包含的ExperienceEvent資料集。 您可以從資料集清單中選取最多50個ExperienceEvent資料集。

>[!NOTE]
>
>**[!UICONTROL ExperienceEvent資料集]**&#x200B;旁方括弧內的數字（例如顯示影像中的`(1)`）顯示貴組織所建立的、與您在合併原則設定畫面中所選結構描述類別相關的ExperienceEvent資料集總數。

選取資料集後，這些資料集會顯示在[!UICONTROL 選取資料集]區段中。

ExperienceEvent資料集無法手動排序，如果ExperienceEvent資料集中的屬性屬於相同的設定檔片段，則會將其附加到設定檔資料集。

與選取設定檔資料集類似，選取ExperienceEvent資料集也會更新&#x200B;**[!UICONTROL 聯合結構描述]**&#x200B;區段，顯示每個資料集貢獻資料的聯合結構描述中的欄位。 如需聯合結構描述的詳細資訊，包括如何與UI中的視覺效果互動，請參考[聯合結構描述UI指南](../ui/union-schema.md)。

![會顯示可選取的ExperienceEvent資料集。](../images/merge-policies/dataset-precedence-experienceevent.png)

>[!ENDTABS]

## [!UICONTROL 檢閱] {#review}

工作流程的最後一步是檢閱合併原則。 **[!UICONTROL 檢閱]**&#x200B;畫面會顯示合併原則的相關資訊，包括選取的ID拼接方法、選取的合併方法，以及包含的資料集。 （若要檢視包含的所有設定檔或ExperienceEvent資料集，請選取資料集數量以展開下拉式清單。）

檢閱畫面中還包含&#x200B;**[!UICONTROL 預覽資料]**&#x200B;表格，其中顯示使用合併原則的範例設定檔記錄。 這可讓您在儲存合併原則之前，先預覽客戶設定檔的外觀。

在選取&#x200B;**[!UICONTROL 完成]**&#x200B;以完成建立工作流程之前，請務必仔細檢閱合併原則設定並預覽資料。

>[!BEGINTABS]

>[!TAB 已排序的時間戳記]

如果您選取&#x200B;**[!UICONTROL 排序的時間戳記]**&#x200B;作為合併原則的合併方法，設定檔資料集清單會依時間戳記順序，包含貴組織建立的所有與結構描述類別相關的資料集。 ExperienceEvent資料集清單包含貴組織針對所選結構描述類別建立的所有資料集，並將附加至設定檔資料集。

**[!UICONTROL 預覽資料]**&#x200B;資料表根據資料集的時間戳記順序顯示範例設定檔記錄。 這可讓您在儲存合併原則之前，先預覽客戶設定檔的外觀。

選取&#x200B;**[!UICONTROL 完成]**&#x200B;以建立新的合併原則。

![顯示[檢閱]頁面。 此頁面可讓您檢閱新建立的合併原則的詳細資料。](../images/merge-policies/timestamp-review.png)

>[!TAB 資料集優先順序]

如果您選取&#x200B;**[!UICONTROL 資料集優先順序]**&#x200B;作為合併原則的合併方法，Profile和ExperienceEvent資料集清單將分別只包含您在建立工作流程期間選取的Profile和ExperienceEvent資料集。 設定檔資料集的順序應與您在建立期間指定的優先順序相符。 如果沒有，請使用[!UICONTROL 上一步]按鈕返回上一個工作流程步驟並調整優先順序。

**[!UICONTROL 預覽資料]**&#x200B;表格顯示使用所選資料集的範例設定檔記錄。 這可讓您在儲存合併原則之前，先預覽客戶設定檔的外觀。

選取&#x200B;**[!UICONTROL 完成]**&#x200B;以建立新的合併原則。

![顯示[檢閱]頁面。 此頁面可讓您檢閱新建立的合併原則的詳細資料。](../images/merge-policies/dataset-precedence-review.png)

>[!ENDTABS]

## 編輯合併原則 {#edit}

從[!UICONTROL 合併原則]索引標籤中，您可以修改為[!DNL XDM Individual Profile]類別建立的現有合併原則，方法是選取您要編輯的合併原則的&#x200B;**[!UICONTROL 原則名稱]**。

當&#x200B;**[!UICONTROL 編輯合併原則]**&#x200B;畫面出現時，您可以變更名稱和[!UICONTROL ID拼接]方法，以及變更此原則是否為貴組織的預設合併原則。

選取&#x200B;**[!UICONTROL 下一步]**&#x200B;繼續完成合併原則工作流程，以更新合併原則中包含的合併方法和資料集。

![顯示編輯合併原則工作流程。](../images/merge-policies/edit-screen.png)

完成必要的變更後，請檢閱您的合併原則，並選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存您的變更並返回[!UICONTROL 合併原則]索引標籤。

>[!WARNING]
>
>變更合併原則可能會影響細分和設定檔結果，因為它將改變解決資料衝突的方式。 儲存合併原則之前，請務必仔細檢閱變更。

![顯示編輯原則工作流程的稽核頁面。](../images/merge-policies/edit-review.png)

## 資料治理原則違規

建立或更新合併原則時，會執行檢查以判斷合併原則是否違反貴組織定義的任何資料使用原則。 資料使用原則是Adobe Experience Platform資料控管的一部分，也是描述允許或限制您對特定[!DNL Platform]資料執行的行銷動作型別的規則。

例如，如果使用合併原則來建立啟用至協力廠商目的地的對象，而您的組織有資料使用原則來防止將特定資料匯出至協力廠商，則在嘗試儲存合併原則時，您將會收到&#x200B;**[!UICONTROL 偵測到資料治理原則違規]**&#x200B;的通知。

此通知包含已違反的資料使用原則清單，可讓您從清單中選取原則，檢視違規的詳細資訊。 選取違反的原則時，**[!UICONTROL 資料譜系]**&#x200B;索引標籤會提供違規的原因以及受影響的啟用，每個索引標籤都會提供資料使用原則如何違反的詳細資訊。

若要進一步瞭解如何在Adobe Experience Platform中執行資料控管，請先閱讀[資料控管概觀](../../data-governance/home.md)。

## 後續步驟

現在您已為組織建立並設定合併原則，您可以使用這些原則來調整Platform中客戶設定檔的檢視，以及從您的設定檔資料建立對象。 如需如何使用[!DNL Experience Platform] UI和API建立及使用對象的詳細資訊，請參閱[區段總覽](../../segmentation/home.md)。
