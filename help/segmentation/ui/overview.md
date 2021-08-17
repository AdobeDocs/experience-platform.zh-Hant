---
keywords: Experience Platform；首頁；熱門主題；分段服務；分段服務；使用手冊；ui指南；分段ui指南；區段產生器；區段產生器；已實現；現有；退出；
solution: Experience Platform
title: 區段服務UI指南
topic-legacy: ui guide
description: Adobe Experience Platform區段服務提供建立和管理區段定義的使用者介面。
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: b7392596c7ed96032dc8ad6bb8e423640f562394
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 0%

---

# 區段服務UI指南

[!DNL Adobe Experience Platform Segmentation Service] 提供建立和管理區段定義的使用者介面。

## 快速入門

使用區段定義需要了解與區段相關的各種[!DNL Experience Platform]服務。 閱讀本使用手冊之前，請查閱以下服務的文檔：

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] 可讓您將儲存在中、與 [!DNL Experience Platform] 個人（例如客戶、潛在客戶、使用者或組織）相關的資料分割為較小的群組。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):可借由將擷取到的不同資料來源的身分橋接至，來建立客戶設 [!DNL Platform]定檔。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

此外，還必須了解本檔案中使用的兩個重要術語，並了解它們之間的差異：
- **區段定義**:用於描述目標受眾的關鍵特徵或行為的規則集。
- **對象**:符合區段定義條件的產生設定檔集。

## 概覽

在Experience PlatformUI中，在左側導覽中選取&#x200B;**[!UICONTROL 區段]**&#x200B;以開啟顯示[!UICONTROL 區段]控制面板的&#x200B;**[!UICONTROL 概述]**&#x200B;標籤。

>[!NOTE]
>
>如果您的組織是初次使用Platform，且尚未建立作用中的設定檔資料集或合併原則，則不會顯示[!UICONTROL Segments]控制面板。 反之， [!UICONTROL 概述]標籤會顯示可協助您開始使用區段的連結和檔案。

###  區段控制面板 {#segments-dashboard}

**[!UICONTROL 區段]**&#x200B;控制面板概述與貴組織的區段資料相關的關鍵量度。

若要深入了解，請造訪[區段控制面板指南](../../dashboards/guides/segments.md)。

![](../../dashboards/images/segments/dashboard-overview.png)

## 瀏覽

選取&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤，查看您IMS組織的所有區段定義清單。

![](../images/ui/overview/segment-browse-all.png)

此檢視會列出區段定義的相關資訊，包括劃分、流失、設定檔計數、評估方法、建立日期和上次修改日期。

劃分會顯示橫條圖，概述屬於下列各種狀態的設定檔百分比：[!UICONTROL 已實現]、[!UICONTROL 現有]和[!UICONTROL 正在退出]。

![](../images/ui/overview/segment-browse-breakdown.png)

| 狀態 | 說明 |
| ------ | ----------- |
| 已實現 | 區段內的新設定檔。 |
| 現有 | 保留在區段內的現有設定檔。 |
| 退出 | 離開區段的現有設定檔。 |

流失率代表與上次執行區段工作相比，在區段定義中變更之設定檔的百分比，而設定檔計數則代表符合區段資格的設定檔總數。

評估方法可以是流式或批次。 資料進入系統時，會持續評估串流區段。 系統會根據設定的排程來評估批次區段。

![](../images/ui/overview/segment-browse-segments.png)

頁面頂端有選項可新增所有區段至排程和建立新區段。

切換&#x200B;**[!UICONTROL 新增所有區段至排程]**&#x200B;將啟用排程的分段。 如需排程分段的詳細資訊，請參閱本使用手冊](#scheduled-segmentation)的「排程分段」區段。[

選取&#x200B;**[!UICONTROL 建立區段]**&#x200B;後，您就會前往區段產生器。 若要進一步了解如何建立區段，請閱讀使用手冊](#create-segment)中[建立區段的相關章節。

![](../images/ui/overview/segment-browse-top.png)

右側邊欄包含IMS組織內所有區段的相關資訊，列出區段總數、上次評估日期、下次評估日期，以及依評估方法劃分的區段。

![](../images/ui/overview/segment-browse-segment-info.png)

選取區段定義的列可提供區段定義的摘要，包括可編輯或刪除區段的選項、區段的合格對象、總對象大小，以及區段的名稱、說明、評估方法、建立日期和上次修改日期。

>[!NOTE]
>
> 您將能夠刪除目標啟動中使用的區段&#x200B;**not**。

![](../images/ui/overview/segment-browse-details.png)

## 區段定義詳細資料 {#segment-details}

若要查看有關特定區段定義的詳細資訊，請在&#x200B;**[!UICONTROL Browse]**&#x200B;標籤內選取區段名稱。

區段詳細資料頁面隨即顯示。 頂端是區段定義的摘要、合格對象大小的相關資訊，以及區段已啟動的目的地。

![](../images/ui/overview/segment-details-summary.png)

### 區段摘要

**[!UICONTROL 區段摘要]**&#x200B;區段提供諸如屬性的ID、名稱、說明和詳細資訊。

此外，您也可以選擇編輯區段。 選擇&#x200B;**[!UICONTROL 編輯段]**&#x200B;將帶您進入[!DNL Segment Builder]。 有關使用[!DNL Segment Builder]工作區的更多詳細資訊，請參閱[[!DNL Segment Builder] 使用手冊](./segment-builder.md)。

### 區段中的總受眾

區段&#x200B;]**中的**[!UICONTROL &#x200B;受眾總計區段會顯示符合區段資格的設定檔總數。

估計值是使用當天樣本資料的樣本大小產生。 如果您的設定檔存放區中實體少於100萬個，則會使用完整資料集；100萬至2000萬個實體使用100萬個實體；超過2,000萬個實體，佔實體總數的5%。 有關生成段估計的更多資訊，請參見段建立教程的[估計生成部分](../tutorials/create-a-segment.md#estimate-and-preview-an-audience)。

### 已啟動的目的地

**[!UICONTROL 已啟用的目的地]**&#x200B;區段顯示已啟用此區段的目的地。

>[!NOTE]
>
> 目標是[!DNL Real-time Customer Data Platform]提供的功能，可讓您將資料匯出至外部平台。 如需目的地的詳細資訊，請參閱[目的地概述](../../destinations/home.md)。 若要了解如何對目的地啟用區段，請參閱[啟用概述](../../destinations/ui/activation-overview.md)。

### 設定檔範例

底下是符合區段資格的設定檔取樣，其中詳細說明資訊，包括[!DNL Profile] ID、名字、姓氏和個人電子郵件。

資料取樣的觸發方式取決於擷取方法。

對於批次內嵌，設定檔存放區會每十五分鐘自動掃描一次，以查看自上次執行取樣工作以來是否已成功內嵌新批次。 如果是，隨後會掃描設定檔存放區，以查看記錄數量是否至少有5%的變更。 如果滿足這些條件，則會觸發新的取樣工作。

若是串流內嵌，系統會每小時自動掃描設定檔存放區，以查看記錄數量是否至少有5%的變更。 若符合此條件，則會觸發新的取樣工作。

掃描的樣本大小取決於設定檔存放區中的整體數量。 下表顯示以下樣本大小：

| 設定檔存放區中的實體 | 樣本大小 |
| ------------------------- | ----------- |
| 不到100萬 | 完整資料集 |
| 1000至2000萬 | 100萬 |
| 2000多萬 | 總共5% |

若要查看有關每個[!DNL Profile]的更多詳細資訊，請選取[!DNL Profile] ID。 若要進一步了解設定檔的詳細資訊，請參閱[[!DNL Real-time Customer Profile] 使用手冊](../../profile/ui/user-guide.md#profile-detail)。

![](../images/ui/overview/segment-details-profiles.png)

## 建立區段 {#create-segment}

選取右上角的&#x200B;**[!UICONTROL 建立區段]**&#x200B;會開啟[!DNL Segment Builder]工作區，您可在此處開始建立區段定義。

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] 工作區

[!DNL Segment Builder] 提供豐富的工作區，可讓您與資料元素 [!DNL Profile] 互動。工作區提供建立和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖磚。

有關使用[!DNL Segment Builder]工作區的更多詳細資訊，請參閱[[!DNL Segment Builder] 使用手冊](./segment-builder.md)。

![](../images/ui/overview/segment-builder.png)

## 排程分段 {#scheduled-segmentation}

建立區段定義後，您就可以依需求或排程（持續）評估來評估它們。 評估是指透過區段定義來移動[!DNL Real-time Customer Profile]資料，以產生對應的受眾。 建立後，會儲存和儲存對象，以便使用[!DNL Experience Platform] API匯出對象。

隨需評估包括視需要使用API來執行評估並建立受眾，而排程評估（也稱為「已排程區段」）可讓您建立週期性排程，以在特定時間（最多每天一次）評估區段定義。

### 啟用排程的細分 {#enable-scheduled-segmentation}

您可以使用UI或API，為排程評估啟用區段定義。 在UI中，返回&#x200B;**[!UICONTROL Segments]**&#x200B;內的&#x200B;**[!UICONTROL Browse]**&#x200B;標籤，並開啟&#x200B;**[!UICONTROL 新增所有區段至排程]**。 這會導致根據貴組織設定的排程評估所有區段。

>[!NOTE]
>
>對於[!DNL XDM Individual Profile]，最多可為五(5)個合併原則的沙箱啟用排程評估。 如果貴組織在單一沙箱環境中有超過五個[!DNL XDM Individual Profile]的合併原則，則無法使用排程的評估。

目前只能使用API建立排程。 有關使用API建立、編輯和使用排程的詳細步驟，請參閱評估和存取區段結果的教學課程，尤其是使用API](../tutorials/evaluate-a-segment.md#scheduled-evaluation)排程評估的[區段。

![](../images/ui/overview/segment-browse-scheduled.png)

## 串流細分 {#streaming-segmentation}

串流細分是即時對[!DNL Platform]執行近乎即時的細分，同時專注於資料的豐富度。 透過串流細分，區段資格現在會在資料進入[!DNL Platform]時進行，以緩解排程和執行區段工作的需求。

如需串流分段的詳細資訊，請參閱[串流分段使用手冊](./streaming-segmentation.md)。

>[!NOTE]
>
>為了讓串流區段正常運作，您需要為組織啟用已排程的區段。 如需啟用排程分段的詳細資訊，請參閱本使用手冊中的[串流分段區段](#scheduled-segmentation)。

## 邊緣分割 {#edge-segmentation}

邊緣分段是即時在邊緣上評估Platform中區段的功能，可啟用相同的頁面和下一頁個人化使用案例。

如需邊緣劃分的詳細資訊，請參閱[邊緣劃分UI指南](./edge-segmentation.md)

## 違反策略

>[!NOTE]
>
>只有當您建立已指派給目的地的區段時，才會套用原則違規。

建立完區段後，Adobe Experience Platform資料控管會分析區段，以確保區段內沒有違反政策的情況。 如需詳細資訊，請參閱[[!DNL Data Governance] 概述](../../data-governance/home.md) 。

![](../images/ui/overview/segment-dule-policy-violations.png)

## 後續步驟和其他資源 {#next-steps}

[!DNL Segmentation Service] UI提供豐富的工作流程，可讓您將有價對象與[!DNL Real-time Customer Profile]資料隔離。

若要進一步了解[!DNL Segmentation Service]，請繼續閱讀本檔案。 若要了解如何使用[!DNL Segmentation Service] API，請參閱[[!DNL Segmentation Service] 開發人員指南](../api/overview.md)。
