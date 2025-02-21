---
title: 帳戶對象
description: 瞭解如何建立和使用帳戶對象，以定位下游目的地中的帳戶設定檔。
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: 78cb7fd24b858859226c737affbb4e93783c884d
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 21%

---

# 帳戶客群

>[!AVAILABILITY]
>
>帳戶對象只能在Real-Time Customer Data Platform的[B2B edition](../../rtcdp/overview.md#rtcdp-b2b)和Real-Time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2p)的[B2P版本中使用。

透過帳戶細分，Adobe Experience Platform可讓您從以人物為基礎的受眾到以帳戶為基礎的受眾，使用完整且精密的行銷細分體驗。

帳戶對象可用於作為以帳戶為基礎的目的地的輸入，讓您在下游服務中鎖定這些帳戶內的人員。 例如，您可以使用以帳戶為基礎的受眾來擷取&#x200B;**不**&#x200B;擁有任何職銜為首席營運官(COO)或首席行銷官(CMO)之人員的聯絡資訊的所有帳戶記錄。

## 術語 {#terminology}

開始使用帳戶對象之前，請先檢閱不同對象型別之間的差異：

- **帳戶對象**：帳戶對象是使用&#x200B;**帳戶**&#x200B;設定檔資料建立的對象。 帳戶設定檔資料可用來建立受眾，將下游帳戶內的人員設為目標。 如需帳戶設定檔的詳細資訊，請閱讀[帳戶設定檔總覽](../../rtcdp/accounts/account-profile-overview.md)。
- **People對象**： People對象是使用&#x200B;**客戶**&#x200B;設定檔資料建立的對象。 客戶設定檔資料可用來建立以您企業的客戶為目標之對象。 如需客戶設定檔的詳細資訊，請閱讀[即時客戶設定檔總覽](../../profile/home.md)。
- **潛在客戶對象**：潛在客戶對象是使用&#x200B;**潛在客戶**&#x200B;設定檔資料建立的對象。 潛在客戶設定檔資料可用來從未經驗證的使用者建立對象。 如需潛在客戶設定檔的詳細資訊，請閱讀[潛在客戶設定檔概觀](../../profile/ui/prospect-profile.md)。

## 存取 {#access}

若要存取帳戶對象，請在&#x200B;**[!UICONTROL 帳戶]**&#x200B;區段中選取&#x200B;**[!UICONTROL 對象]**。

![[帳戶]區段中的[對象]按鈕會反白顯示。](../images/types/account/select.png)

顯示[!UICONTROL 瀏覽]頁面，顯示組織所有帳戶對象的清單。

![顯示屬於組織的帳戶對象。](../images/types/account/browse.png)

此檢視會列出對象的相關資訊，包括名稱、設定檔計數、來源、生命週期狀態、建立日期和上次更新日期。

您也可以使用搜尋和篩選功能，快速搜尋及排序特定帳戶對象。 如需有關此功能的詳細資訊，請參閱[對象入口網站概觀](../ui/audience-portal.md#manage-audiences)。

## 建立客群 {#create}

>[!NOTE]
>
>帳戶對象是使用&#x200B;**批次**&#x200B;細分評估，每24小時評估一次。

若要建立帳戶對象，請在[!UICONTROL 瀏覽]頁面上選取&#x200B;**[!UICONTROL 建立對象]**。

![帳戶對象瀏覽頁面會醒目顯示[!UICONTROL 建立對象]按鈕。](../images/types/account/select-create-audience.png)

「區段產生器」隨即顯示。 帳戶屬性和對象會顯示在左側導覽列上。 在[!UICONTROL 屬性]標籤下，您可以同時新增Platform建立和自訂屬性。

![會顯示區段產生器。 請注意，只會顯示屬性和對象。](../images/types/account/segment-builder.png)

建立帳戶對象時，請注意，事件列在&#x200B;**[!UICONTROL 人員]**&#x200B;下，而不是作為自己的標籤，因為這些屬性與人員相關聯。

![在[!UICONTROL People]資料夾中尋找事件的位置會反白顯示。](../images/types/account/attributes.png)

在[!UICONTROL 對象]標籤下方，您可以新增先前建立的以人物為基礎的對象，以便在建立您自己的帳戶對象時建置。

![區段產生器內的「對象」索引標籤會醒目提示。](../images/types/account/audiences.png)

如需使用區段產生器的詳細資訊，請參閱[區段產生器UI指南](../ui/segment-builder.md)。

### 建立關係 {#relationships}

依預設，帳戶對象的「區段產生器」UI會顯示帳戶和個人之間的直接關係。 不過，帳戶對象可使用其他關係型別。

若要使用替代關聯性型別，請選取![設定圖示](../../images/icons/settings.png)。

![設定圖示會在[欄位]區段上反白顯示。](../images/types/account/select-settings.png)

在[!UICONTROL 設定]標籤上，選取&#x200B;**[!UICONTROL 欄位關聯性]**&#x200B;區段中的&#x200B;**[!UICONTROL 顯示關聯性選取器]**。

![在[設定]索引標籤的[欄位關聯性]區段內已選取[顯示關聯性選取器]切換按鈕。](../images/types/account/show-relation-selectors.png)

再次選取![設定圖示](../../images/icons/settings.png)以返回[!UICONTROL 欄位]索引標籤。 您現在可以看到&#x200B;**[!UICONTROL 建立關係]**&#x200B;區段，讓您建立帳戶與個人的連線方式以及個人與機會的連線方式。

![「建立關係」區段會反白顯示，顯示如何將帳戶與個人連線以及如何將個人與機會連線的選項。](../images/types/account/establish-relationships.png)

將帳戶連線至人員時，您可以選擇下列選項：

| 選項 | 說明 |
| ------ | ----------- |
| 直接關係 | 帳戶和個人之間的直接連線。 這會指定每個人員透過人員結構描述上`personComponents`陣列中的`accountID`值陣列所連結的帳戶。 此路徑是最常使用的路徑。 |
| 帳戶 — 個人關係 | 帳戶和個人之間的關係，由`accountPersonRelation`物件定義。 此路徑也可讓每個人連線至多個帳戶。 當您的組織從您的來源資料中定義明確的關係表時，就會使用它。 |
| 機會 — 個人關係 | 機會和個人之間的關係，由`opportunityPersonRelation`物件定義。 這會將個人從機會個人連結至帳戶，將個人連結至帳戶。 這可讓您說明哪些公司已將人員附加至商機。 |

將商機連線到個人時，您可以從下列選項中選擇：

| 選項 | 說明 |
| ------ | ----------- |
| 帳戶 | 帳戶與機會之間的直接連線。 當您在帳戶對象中使用此專案時，此路徑會將公司的所有人員連結至該機會。 |
| 機會 — 個人關係 | 機會和個人之間的關係，其基礎為機會 — 個人物件。 此路徑只會將已被明確識別為參與商機的人員連結到該商機。 |

建立所需的關係後，您可以將必要的人員 — 對象新增至您的區段定義。

## 啟用客群 {#activate}

>[!NOTE]
>
>只有有限數量的目的地可支援帳戶對象。 在繼續此程式之前，請確定您要啟用的目的地可支援帳戶對象。

建立帳戶對象後，您可以對其他下游服務啟用對象。

選取您要啟用的對象，然後選取&#x200B;**[!UICONTROL 啟用到目的地]**。

![在選取對象的快速動作功能表中，[!UICONTROL 啟用至目的地]按鈕會醒目提示。](../images/types/account/activate.png)

[!UICONTROL 啟用目的地]頁面隨即顯示。 如需啟動程式的詳細資訊，包括支援的目的地以及欄位對應的詳細資訊，請參閱[啟動帳戶對象](/help/destinations/ui/activate-account-audiences.md)教學課程。

## 後續步驟 {#next-steps}

閱讀本指南後，您現在已更瞭解如何在Adobe Experience Platform中建立和使用您的帳戶對象。 若要瞭解如何在Platform中使用其他型別的對象，請閱讀[對象型別概觀](./overview.md)。

## 附錄 {#appendix}

下節提供有關帳戶對象的額外資訊。

### 帳戶分段驗證 {#validation}

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_eventLookbackWindow"
>title="回顧期間上限錯誤"
>abstract="體驗事件的回顧期間上限為 30 天。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxDepth"
>title="巢狀容器深度上限錯誤"
>abstract="巢狀容器深度上限為 **5**。這表示建立對象時，**不能**&#x200B;有超過五個巢狀容器。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxBreadth"
>title="規則數上限錯誤"
>abstract="單一容器內規則數上限為 **5**。這表示建立對象時，**不能**&#x200B;在單一容器中有超過五個規則。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_crossEntityMaxDepth"
>title="跨實體數上限錯誤"
>abstract="單一對象中可以進行的跨實體數上限為 **5**。跨實體是指您在對象內不同實體之間進行切換。例如，從帳戶到人員再到行銷清單。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowCustomEntity"
>title="自訂實體錯誤"
>abstract="**不**&#x200B;允許自訂實體。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_b2bBuiltInEntities"
>title="B2B 實體無效錯誤"
>abstract="僅允許使用下列 B2B 實體：`_xdm.context.account`、`_xdm.content.opportunity`、`_xdm.context.profile`、`_xdm.context.experienceevent`、`_xdm.context.account-person`、`_xdm.classes.opportunity-person`、`_xdm.classes.marketing-list-member`、`_xdm.classes.marketing-list`、`_xdm.context.campaign-member` 和 `_xdm.classes.campaign`。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_rhsMaxOptions"
>title="值數量上限錯誤"
>abstract="單一欄位可以檢查的值數量上限為 **50**。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByReference"
>title="inSegment 事件錯誤"
>abstract="**不**&#x200B;允許 inSegment 事件。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByValue"
>title="inSegment 事件錯誤"
>abstract="**不**&#x200B;允許 inSegment 事件。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowSequentialEvents"
>title="Sequential 事件錯誤"
>abstract="**不**&#x200B;允許 Sequential 事件。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowMaps"
>title="Map-type 屬性錯誤"
>abstract="**不**&#x200B;允許 Map-type 屬性。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxNestedAggregationDepth"
>title="巢狀實體深度上限錯誤"
>abstract="巢狀陣列深度上限為 **5**。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxObjectNestingLevel"
>title="巢狀物件數上限錯誤"
>abstract="允許的巢狀物件數上限為 **10**。"

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_generic"
>title="違反限制"
>abstract="對象違反限制。請閱讀連結的文件以了解更多詳細資訊。"

使用帳戶對象時，對象&#x200B;**必須**&#x200B;符合下列限制：

- 體驗事件的回顧期間上限為&#x200B;**30天**。
- 巢狀容器的最大深度為&#x200B;**5**。
   - 這表示建立對象時，**不能**&#x200B;有超過五個巢狀容器。
- 單一容器內的規則數目上限為&#x200B;**5**。
   - 這表示您的對象&#x200B;**不能**&#x200B;有超過五個規則組成您的對象。
- 可使用的跨實體數目上限為&#x200B;**5**。
   - 跨實體是指您在對象內不同實體之間進行切換。例如，從帳戶到人員再到行銷清單。
- 無法使用自訂實體&#x200B;****。
- 單一欄位可以檢查的值數量上限為 **50**。
   - 例如，如果您有「城市名稱」欄位，您可以根據50個城市名稱檢查該值。
- 帳戶對象&#x200B;**無法**&#x200B;使用`inSegment`個事件。
- 帳戶對象&#x200B;**不能**&#x200B;使用循序事件。
- 帳戶對象&#x200B;**無法**&#x200B;使用地圖。
- 巢狀陣列深度上限為 **5**。
- 巢狀物件的數量上限為&#x200B;**10**。
