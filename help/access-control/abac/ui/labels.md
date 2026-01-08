---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制
title: 以屬性為基礎的存取控制管理標籤
description: 透過Adobe Experience Cloud中的許可權介面管理標籤。
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: 855f0a1384f658d39aa9d4fbb6bcb032933e59db
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 11%

---

# 管理標籤

您可以使用標籤，根據資料使用情況和以屬性為基礎的存取控制原則，將資料集和欄位分類。 標籤可隨時套用，提供您選擇控管資料方式的靈活性。 最佳實務建議在資料內嵌至Adobe Experience Platform後，或資料可供使用時，立即為資料加上標籤。 請閱讀本檔案，瞭解如何在許可權UI中管理標籤。

如需完整的標籤清單及其對應的治理原則，請閱讀[核心資料使用標籤](../../../data-governance/labels/reference.md){target="_blank"}的指南。

>[!NOTE]
>
>若要使用包含指定標籤的欄位來建立或檢視[運算屬性](../../../profile/computed-attributes/overview.md){target="_blank"}，您必須擁有該標籤的存取權。

## 探索標籤 {#explore-labels}

若要檢視所有可用的標籤，請在&#x200B;**[!UICONTROL Permissions]** Adobe Experience Cloud[中導覽至](https://experience.adobe.com/){target="_blank"}。 從左側面板中選取&#x200B;**[!UICONTROL Labels]**。

![在許可權內的標籤工作區中，標籤在左側面板中反白顯示。](../../images/ui/labels/labels-home.png){zoomable="yes"}

標籤會依型別分類，且屬於下列類別之一：

| 類型 | 說明 |
| --- | --- |
| [合約](../../../data-governance/labels/reference.md#contract){target="_blank"} | 此類別可用於分類具有合約義務或與貴組織的資料治理原則相關的資料。 |
| [身分識別](../../../data-governance/labels/reference.md#identity){target="_blank"} | 此類別用於分類可直接或間接識別個人的資料。 |
| [敏感](../../../data-governance/labels/reference.md#sensitive){target="_blank"} | 此類別是用來分類貴組織認為敏感的資料。 |
| [合作夥伴生態系統](../../../data-governance/labels/reference.md#partner){target="_blank"} | 此類別可用於分類從組織外部的來源取得的資料。 |
| 負責任的參與 | 此類別包含單一標籤&#x200B;**[!UICONTROL Potential for Bias]**，其反映有可能引入偏差的資料。 |
| 自訂 | 此類別包含貴組織建立的標籤。 |

若要篩選標籤，請選取篩選圖示（![篩選圖示](/help/images/icons/filter.png)），然後從&#x200B;**[!UICONTROL Type]**&#x200B;下拉式清單中選取您想要的標籤型別。

![標籤工作區已展開篩選選項，並反白顯示型別下拉式清單。](../../images/ui/labels/label-filter.png){zoomable="yes"}

若要檢視個別標籤，請從清單中選取標簽名稱。 標籤的詳細資訊頁面隨即顯示。 Adobe的核心標籤&#x200B;**無法**&#x200B;編輯。

![個別標籤的詳細資料頁面。](../../images/ui/labels/label-details.png){zoomable="yes"}

## 建立自訂標籤 {#create-custom-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="標籤使用"
>abstract="您可以使用自訂標籤，將資料控管和存取權控制的設定套用至您的資料。"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="建立新標籤"
>abstract="您可以建立適合您組織需求的自訂標籤。自訂標籤可用於資料控管和存取控制設定套用到您的資料。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html#manage-labels" text="管理自訂標籤"

>[!NOTE]
>
>若要建立自訂標籤，您需要一個包含&#x200B;**[!UICONTROL Manage Usage Labels]**&#x200B;許可權和`Prod`沙箱的角色。

若要建立新標籤，請從&#x200B;**[!UICONTROL Labels]**&#x200B;工作區的左側面板中選取&#x200B;**[!UICONTROL Permissions]**，然後選取&#x200B;**[!UICONTROL Create label]**。

![標籤工作區中反白顯示[建立標籤]選項。](../../images/ui/labels/create-label.png){zoomable="yes"}

**[!UICONTROL Create new label]**&#x200B;對話方塊會出現，提示您輸入&#x200B;**[!UICONTROL Name]**、**[!UICONTROL Friendly name]**&#x200B;和&#x200B;**[!UICONTROL Description]**。

>[!IMPORTANT]
>
> 建立標籤後無法變更標籤的[!UICONTROL Name]，目前不支援刪除標籤。

選取&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成建立標籤。

![已填入「名稱」、「好記名稱」和「說明」的「建立新標籤」對話方塊，並反白顯示「確認」選項。](../../images/ui/labels/create-new-label.png){zoomable="yes"}

## 編輯自訂標籤 {#edit-custom-label}

雖然您無法編輯自訂標籤的&#x200B;**[!UICONTROL Name]**，但可以編輯&#x200B;**[!UICONTROL Friendly name]**&#x200B;和&#x200B;**[!UICONTROL Description]**。 若要編輯自訂標籤，請從&#x200B;**[!UICONTROL Labels]**&#x200B;工作區內的清單中選取標籤。

![標籤反白顯示的標籤工作區。](../../images/ui/labels/select-label.png){zoomable="yes"}

編輯任一欄位，然後按一下文字方塊之外的任意位置以儲存變更。 畫面會顯示確認訊息，**[!UICONTROL Modified by]**&#x200B;名稱和&#x200B;**[!UICONTROL Modified]**&#x200B;日期將會變更。

![標籤詳細資訊頁面顯示「已成功更新」訊息。](../../images/ui/labels/edit-label.png){zoomable="yes"}

## 後續步驟

現在您已更深入瞭解標籤，可以開始[將它們套用至結構描述](../../../xdm/tutorials/labels.md)。
