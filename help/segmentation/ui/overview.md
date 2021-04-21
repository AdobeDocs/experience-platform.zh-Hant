---
keywords: Experience Platform; home；熱門主題；分段服務；分段服務；使用手冊；ui指南；分段使用手冊；分段生成器；分段生成器；實現；現有；退出；
solution: Experience Platform
title: 區段服務UI指南
topic-legacy: ui guide
description: Adobe Experience Platform區段服務提供使用者介面，以建立和管理區段定義。
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 0%

---

# 區段服務UI指南

[!DNL Adobe Experience Platform Segmentation Service] 提供建立和管理區段定義的使用者介面。

## 快速入門

使用區段定義需要瞭解與區段相關的各種[!DNL Experience Platform]服務。 閱讀本使用指南之前，請先閱讀下列服務的說明檔案：

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] 可讓您將儲存在與個人( [!DNL Experience Platform] 如客戶、潛在客戶、使用者或組織)相關的資料分割為較小的群組。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md):借由將不同資料來源的身分整合到其中，以建立客戶個人檔案 [!DNL Platform]。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

此外，務必瞭解本檔案使用的兩個關鍵詞，並瞭解它們之間的差異：
- **區段定義**:用於描述目標對象的關鍵特性或行為的規則集。
- **觀眾**:符合區段定義條件的結果描述檔集。

## 概述

在[[!DNL Experience Platform] UI](http://platform.adobe.com/)中，選擇左側導覽器中的&#x200B;**[!UICONTROL Segments]**&#x200B;以開啟&#x200B;**[!UICONTROL Overview]**&#x200B;標籤。 此標籤提供檔案和影片的連結，以協助您瞭解並開始使用區段。

![](../images/ui/overview/segment-overview.png)

## 瀏覽

選取&#x200B;**[!UICONTROL Browse]**&#x200B;標籤，查看IMS組織的所有區段定義清單。

![](../images/ui/overview/segment-browse-all.png)

此檢視會列出區段定義的相關資訊，包括劃分、流失、描述檔計數、評估方法、建立日期和上次修改日期。

劃分會顯示橫條圖，概述屬於下列各種狀態的描述檔百分比：[!UICONTROL Entered]、[!UICONTROL Realized]和[!UICONTROL Exiting]。

![](../images/ui/overview/segment-browse-breakdown.png)

| 狀態 | 說明 |
| ------ | ----------- |
| 已輸入 | 區段中的新描述檔。 |
| 已實現 | 保留在區段中的現有描述檔。 |
| 退出 | 離開區段的現有描述檔。 |

流失率代表在區段定義中變更的設定檔與上次執行區段作業時的百分比，而設定檔計數則代表符合區段資格的設定檔總數。

評估方法可以是流式或批式。 當資料進入系統時，會持續評估串流區段。 批次區段會根據設定的排程進行評估。

![](../images/ui/overview/segment-browse-segments.png)

頁面頂端有選項，可將所有區段新增至排程並建立新區段。

切換&#x200B;**[!UICONTROL Add all segments to schedule]**&#x200B;將啟用計劃分段。 有關排程分段的詳細資訊，請參閱本使用手冊](#scheduled-segmentation)的「排程分段」區段。[

選取&#x200B;**[!UICONTROL Create segment]**&#x200B;會帶您前往區段產生器。 若要進一步瞭解建立區段，請閱讀使用指南](#create-segment)中有關建立區段的章節。[

![](../images/ui/overview/segment-browse-top.png)

右側邊欄包含有關IMS組織內所有區段的資訊，列出區段總數、上次評估日期、下次評估日期，以及依評估方法劃分區段。

![](../images/ui/overview/segment-browse-segment-info.png)

選取區段定義的列可提供區段定義的摘要，包括編輯或刪除區段的選項、區段的合格對象、總對象大小，以及區段的名稱、說明、評估方法、建立日期和上次修改日期。

![](../images/ui/overview/segment-browse-details.png)

## 區段定義詳細資訊{#segment-details}

若要檢視特定區段定義的詳細資訊，請在&#x200B;**[!UICONTROL Browse]**&#x200B;標籤中選取區段名稱。

此時會顯示區段詳細資訊頁面。 在上方，有區段定義的摘要、符合資格對象大小的相關資訊，以及區段的啟動目標。

![](../images/ui/overview/segment-details-summary.png)

### 區段摘要

**[!UICONTROL Segment summary]**&#x200B;部分提供如屬性的ID、名稱、說明和詳細資訊等資訊。

此外，您也可以選擇編輯區段。 選擇&#x200B;**[!UICONTROL Edit segment]**&#x200B;將帶您進入[!DNL Segment Builder]。 有關使用[!DNL Segment Builder]工作區的更多詳細資訊，請閱讀[[!DNL Segment Builder] 使用手冊](./segment-builder.md)。

### 群體中的受眾總數

**[!UICONTROL Total audience in segment]**&#x200B;區段顯示符合區段資格的描述檔總數。

估計值是使用當天樣本資料的樣本大小產生。 如果您的描述檔儲存區中有少於100萬個實體，則會使用完整資料集；100萬到2000萬個單位使用100萬個單位；超過2000萬個單位，佔全部單位的5%。 有關產生區段估計的更多資訊，請參閱區段建立教學課程的[估計產生區段](../tutorials/create-a-segment.md#estimate-and-preview-an-audience)。

### 已啟動的目標

**[!UICONTROL Activated destinations]**&#x200B;區段顯示此段的激活目標。

>[!NOTE]
>
> 目標是[!DNL Real-time Customer Data Platform]提供的功能，可讓您將資料匯出至外部平台。 有關目標的詳細資訊，請閱讀[目標概述](../../destinations/home.md)。 若要瞭解如何啟用區段至目的地，請閱讀[指南，說明如何啟用區段至目的地](../../destinations/ui/activate-destinations.md)。

### 描述檔範例

下面是符合區段資格的設定檔範例，其中詳列資訊，包括[!DNL Profile] ID、名字、姓氏和個人電子郵件。

資料採樣觸發方式取決於提取方法。

對於批次擷取，描述檔存放區會每十五分鐘自動掃描一次，以查看自上次執行取樣工作以來是否成功擷取新批次。 如果是這樣，則隨後掃描配置檔案儲存，以查看記錄數是否至少有5%的變化。 如果滿足這些條件，則觸發新的採樣作業。

對於串流擷取，會每小時自動掃描描述檔存放區，以查看記錄數是否至少有5%的變更。 如果符合此條件，則會觸發新的取樣工作。

掃描的樣本大小取決於配置檔案儲存中的實體總數。 下表列出了這些樣本大小：

| 描述檔儲存中的實體 | 樣本大小 |
| ------------------------- | ----------- |
| 不到100萬 | 完整資料集 |
| 1000萬到2000萬 | 100萬 |
| 超過2000萬 | 總共5% |

有關每個[!DNL Profile]的更多詳細資訊，請選擇[!DNL Profile] ID。 若要進一步瞭解描述檔的詳細資訊，請閱讀[[!DNL Real-time Customer Profile] 使用指南](../../profile/ui/user-guide.md#profile-detail)。

![](../images/ui/overview/segment-details-profiles.png)

## 建立區段 {#create-segment}

選擇右上角的&#x200B;**[!UICONTROL Create segment]**&#x200B;會開啟[!DNL Segment Builder]工作區，您可在其中開始建立區段定義。

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] 工作區

[!DNL Segment Builder] 提供多樣化工作區，讓您與資料元素 [!DNL Profile] 互動。工作區提供建立和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖格。

有關使用[!DNL Segment Builder]工作區的更多詳細資訊，請閱讀[[!DNL Segment Builder] 使用手冊](./segment-builder.md)。

![](../images/ui/overview/segment-builder.png)

## 排程分段{#scheduled-segmentation}

建立區段定義後，您就可以透過隨選或排程（持續）評估來評估區段定義。 評估意指透過區段定義移動[!DNL Real-time Customer Profile]資料，以產生對應的觀眾。 建立後，會儲存觀眾，以便使用[!DNL Experience Platform] API匯出觀眾。

隨選評估包括視需要使用API來執行評估並建立觀眾，而排程評估（也稱為「排程區段」）可讓您建立循環排程，以評估特定時間（最多每天一次）的區段定義。

### 啟用計劃分段{#enable-scheduled-segmentation}

您可使用UI或API來啟用計畫評估的區段定義。 在UI中，返回&#x200B;**[!UICONTROL Segments]**&#x200B;內的&#x200B;**[!UICONTROL Browse]**&#x200B;標籤，並切換至&#x200B;**[!UICONTROL Add all segments to schedule]**。 這會導致根據您組織所設定的排程評估所有區段。

>[!NOTE]
>
>對於[!DNL XDM Individual Profile]最多可啟用五(5)個合併策略的沙盒，可啟用計畫評估。 如果您的組織在單一沙盒環境中有超過5個[!DNL XDM Individual Profile]的合併原則，您將無法使用排程的評估。

目前只能使用API建立排程。 有關使用API建立、編輯和使用排程的詳細步驟，請依照教學課程來評估和存取區段結果，尤其是使用API](../tutorials/evaluate-a-segment.md#scheduled-evaluation)排程評估的章節。[

![](../images/ui/overview/segment-browse-scheduled.png)

## 串流區段{#streaming-segmentation}

串流分段功能可讓您在[!DNL Platform]上幾乎即時進行分段，同時專注於資料的豐富性。 透過串流分段，區段資格現在會在資料進入[!DNL Platform]時進行，減輕排程和執行分段工作的需求。

有關串流分段的更多資訊，請參閱[串流分段使用指南](./streaming-segmentation.md)。

>[!NOTE]
>
>為了讓串流區段正常運作，您必須啟用組織的排程區段。 如需啟用排程分段的詳細資訊，請參閱本使用手冊](#scheduled-segmentation)中的[串流分段區段。

## 邊緣區段{#edge-segmentation}

邊緣區段是指能夠即時在邊緣上評估平台中的區段，讓相同的頁面和下一頁個人化使用案例。

有關邊緣分段的更多資訊，請參閱[邊緣分段UI指南](./edge-segmentation.md)

## 違反策略

>[!NOTE]
>
>只有當您建立已指派給目標的區段時，才會套用原則違規。

建立完區段後，Adobe Experience Platform資料管理會分析區段，以確保區段內沒有違反政策的情況。 如需詳細資訊，請參閱[[!DNL Data Governance] overview](../../data-governance/home.md)。

![](../images/ui/overview/segment-dule-policy-violations.png)

## 後續步驟和其他資源{#next-steps}

[!DNL Segmentation Service] UI提供豐富的工作流程，讓您將有價對象與[!DNL Real-time Customer Profile]資料隔離。

若要進一步瞭解[!DNL Segmentation Service]，請繼續閱讀檔案。 若要瞭解如何使用[!DNL Segmentation Service] API，請閱讀[[!DNL Segmentation Service] 開發人員指南](../api/overview.md)。
