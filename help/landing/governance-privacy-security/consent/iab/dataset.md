---
keywords: Experience Platform；首頁；IAB;IAB 2.0；同意；同意
solution: Experience Platform
title: 建立資料集以擷取IAB TCF 2.0同意資料
topic-legacy: privacy events
description: 本檔案提供設定兩個必要資料集以收集IAB TCF 2.0同意資料的步驟。
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 0%

---

# 建立資料集以擷取IAB TCF 2.0同意資料

為了讓Adobe Experience Platform依照IAB處理客戶同意資料 [!DNL Transparency & Consent Framework] (TCF)2.0，該資料必須傳送至其結構包含TCF 2.0同意欄位的資料集。

具體來說，擷取TCF 2.0同意資料需要兩個資料集：

* 以 [!DNL XDM Individual Profile] 類別，啟用，在 [!DNL Real-Time Customer Profile].
* 以 [!DNL XDM ExperienceEvent] 類別。

>[!IMPORTANT]
>
>Platform只會強制收集到個別設定檔資料集中的TCF字串。 雖然在此工作流程中仍需要ExperienceEvent資料集來建立資料流，但您只需將資料內嵌至設定檔資料集即可。 如果您想要追蹤一段時間內的同意變更事件，仍可使用ExperienceEvent資料集，但在強制啟用區段時，不會使用這些值。

本檔案提供設定這兩個資料集的步驟。 如需設定TCF 2.0之平台資料作業完整工作流程的概述，請參閱 [IAB TCF 2.0法規遵循概述](./overview.md).

## 先決條件

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [Experience Data Model(XDM)](../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../xdm/schema/composition.md):了解XDM結構的基本建置組塊。
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md):可讓您跨裝置和系統，從不同的資料來源橋接客戶身分。
   * [身分識別命名空間](../../../../identity-service/namespaces.md):客戶身分資料必須以Identity Service所識別的特定身分命名空間提供。
* [即時客戶個人檔案](../../../../profile/home.md):利用 [!DNL Identity Service] 可讓您即時從資料集建立詳細的客戶設定檔。 [!DNL Real-Time Customer Profile] 從資料湖提取資料，並將客戶設定檔保存在其自己的個別資料存放區中。

## TCF 2.0欄位組 {#field-groups}

此 [!UICONTROL IAB TCF 2.0同意詳細資訊] 架構欄位群組提供TCF 2.0支援所需的客戶同意欄位。 此欄位群組有兩個版本：與 [!DNL XDM Individual Profile] 類別，而另一個 [!DNL XDM ExperienceEvent] 類別。

以下各節說明每個欄位群組的結構，包括擷取期間預期的資料。

### 設定檔欄位群組 {#profile-field-group}

結構依 [!DNL XDM Individual Profile], [!UICONTROL IAB TCF 2.0同意詳細資訊] 欄位組提供單一映射類型欄位， `identityPrivacyInfo`，會將客戶身分對應至其TCF同意偏好設定。 此欄位群組必須包含在為「即時客戶設定檔」啟用的記錄型結構中，才能自動執行。

請參閱 [參考指南](../../../../xdm/field-groups/profile/iab.md) 讓此欄位群組進一步了解其結構和使用案例。

### 事件欄位組 {#event-field-group}

如果您想要追蹤一段時間的同意變更事件，可以新增 [!UICONTROL IAB TCF 2.0同意詳細資訊] 欄位群組 [!UICONTROL XDM ExperienceEvent] 綱要。

如果您不打算隨著時間追蹤同意變更事件，則不需要將此欄位群組納入事件結構。 自動強制執行TCF同意值時，Experience Platform只會使用擷取至 [設定檔欄位群組](#profile-field-group). 事件擷取的同意值不會參與自動執行工作流程。

請參閱 [參考指南](../../../../xdm/field-groups/event/iab.md) ，以了解其結構和使用案例的詳細資訊。

## 建立客戶同意結構 {#create-schemas}

若要建立擷取同意資料的資料集，您必須先建立XDM結構，才能將這些資料集建立在上。

如前一節所述，此結構使用 [!UICONTROL XDM個別設定檔] 為了在下游平台工作流程中強制同意，需要類別。 您也可以選擇根據 [!UICONTROL XDM ExperienceEvent] 如果您想要追蹤隨時間變更的同意。 兩個結構都必須包含 `identityMap` 欄位和適當的TCF 2.0欄位群組。

在平台UI中，選取 **[!UICONTROL 結構]** 在左側導覽中，開啟 [!UICONTROL 結構] 工作區。 從這裡，請依照以下各節中的步驟，建立每個必要的架構。

>[!NOTE]
>
>如果您有想要用來擷取同意資料的現有XDM結構，您可以編輯這些結構，而非建立新結構。 不過，如果現有結構已啟用在即時客戶設定檔中使用，其主要身分不能是禁止在興趣型廣告（例如電子郵件地址）中使用的可直接識別欄位。 如果您不確定哪些欄位受限，請洽詢您的法律顧問。
>
>此外，編輯現有結構時，只能進行加法（非中斷）變更。 請參閱 [圖式演化原則](../../../../xdm/schema/composition.md#evolution) 以取得更多資訊。

### 建立設定檔同意結構 {#profile-schema}

選擇 **[!UICONTROL 建立結構]**，然後選擇 **[!UICONTROL XDM個別設定檔]** 從下拉式功能表。

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

此 **[!UICONTROL 新增欄位群組]** 對話框，允許您立即開始向架構添加欄位組。 從此處，選擇 **[!UICONTROL IAB TCF 2.0同意詳細資訊]** 從清單中。 您可以選擇使用搜尋列來縮小結果，以便更輕鬆地找出欄位群組。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

接下來，找到 **[!UICONTROL IdentityMap]** 欄位群組，並加以選取。 將兩個欄位群組列於右側邊欄後，請選取 **[!UICONTROL 新增欄位群組]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-identitymap.png)

畫布會重新顯示，表示 `identityPrivacyInfo` 和 `identityMap` 欄位已新增至架構結構。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

將更多欄位新增至架構之前，請選取要顯示的根欄位 **[!UICONTROL 架構屬性]** 在右側邊欄中，您可以提供架構的名稱和說明。

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

提供名稱和說明後，您可以選取「 」，選擇新增更多欄位至結構 **[!UICONTROL 新增]** 在 **[!UICONTROL 欄位群組]** 區段。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

如果您正在編輯已啟用供使用的現有架構 [!DNL Real-Time Customer Profile]，選取 **[!UICONTROL 儲存]** 先確認您的變更，然後再跳到 [根據您的同意結構建立資料集](#dataset). 如果要建立新架構，請繼續執行以下小節中概述的步驟。

#### 啟用架構以用於 [!DNL Real-Time Customer Profile]

為了讓Platform將其收到的同意資料與特定客戶設定檔建立關聯，必須啟用同意結構以用於 [!DNL Real-Time Customer Profile].

>[!NOTE]
>
>本節中顯示的範例結構會使用其 `identityMap` 欄位作為其主要身分。 如果您想要將另一個欄位設為主要身分，請確定您使用的是間接識別碼，如Cookie ID，而非不得在以興趣為基礎的廣告（例如電子郵件地址）中使用的直接識別欄位。 如果您不確定哪些欄位受限，請洽詢您的法律顧問。
>
>有關如何為架構設定主要身分欄位的步驟，請參閱 [[!UICONTROL 結構] UI指南](../../../../xdm/ui/fields/identity.md).

為 [!DNL Profile]，請在左側邊欄中選取架構的名稱，以開啟 **[!UICONTROL 架構屬性]** 區段。 從此處，選取 **[!UICONTROL 設定檔]** 切換按鈕。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

畫面隨即顯示彈出視窗，指出遺失主要身分。 選取使用替代主要身分的核取方塊，因為主要身分將包含在 `identityMap` 欄位。

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

最後，選取 **[!UICONTROL 儲存]** 確認變更。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### 建立事件同意結構 {#event-schema}

>[!NOTE]
>
>事件同意結構僅用於追蹤一段時間內的同意變更事件，不參與下游實施工作流程。 如果您不想追蹤隨著時間的同意變更，可以跳至 [建立同意資料集](#datasets).

在 **[!UICONTROL 結構]** 工作區，選取 **[!UICONTROL 建立結構]**，然後選擇 **[!UICONTROL XDM ExperienceEvent]** 中。

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

此 **[!UICONTROL 新增欄位群組]** 對話框。 從此處，選擇 **[!UICONTROL IAB TCF 2.0同意詳細資訊]** 從清單中。 您可以選擇使用搜尋列來縮小結果，以便更輕鬆地找出欄位群組。


![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

接下來，找到 **[!UICONTROL IdentityMap]** 欄位群組，並加以選取。 將兩個欄位群組列於右側邊欄後，請選取 **[!UICONTROL 新增欄位群組]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-identitymap.png)

畫布會重新顯示，表示 `consentStrings` 和 `identityMap` 欄位已新增至架構結構。

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

將更多欄位新增至架構之前，請選取要顯示的根欄位 **[!UICONTROL 架構屬性]** 在右側邊欄中，您可以提供架構的名稱和說明。

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

提供名稱和說明後，您可以選取「 」，選擇新增更多欄位至結構 **[!UICONTROL 新增]** 在 **[!UICONTROL 欄位群組]** 區段。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

新增您需要的欄位群組後，請選取 **[!UICONTROL 儲存]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## 根據同意結構建立資料集 {#datasets}

您必須針對上述每個必要結構建立資料集，以最終內嵌客戶的同意資料。 必須針對 [!DNL Real-Time Customer Profile]，而資料集則以時間序列結構為基礎 **不應** be [!DNL Profile]-enabled。

若要開始，請選取 **[!UICONTROL 資料集]** 在左側導覽器中，然後選取 **[!UICONTROL 建立資料集]** 在右上角。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

在下一頁，選取 **[!UICONTROL 從結構建立資料集]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

此 **[!UICONTROL 從結構建立資料集]** 工作流程隨即顯示，從 **[!UICONTROL 選擇架構]** 步驟。 在提供的清單中，找出您先前建立的其中一個同意結構。 您可以選擇使用搜尋列來縮小結果範圍，並更輕鬆地找出您的結構。 選取所需結構旁的選項按鈕，然後選取 **[!UICONTROL 下一個]** 繼續。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

此 **[!UICONTROL 設定資料集]** 步驟。 在選取資料集前，提供可輕鬆識別的唯一名稱和說明 **[!UICONTROL 完成]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

隨即顯示新建立資料集的詳細資訊頁面。 如果資料集以您的時間序列結構為基礎，則程式會完成。 如果資料集以您的記錄結構為基礎，此程式的最後一步是啟用資料集以供 [!DNL Real-Time Customer Profile].

在右側邊欄中，選取 **[!UICONTROL 設定檔]** 切換，然後選取 **[!UICONTROL 啟用]** 在確認彈出視窗中，為 [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

如果您已建立事件型資料集的結構，請再按照上述步驟建立資料集。

## 後續步驟

依照本教學課程，您至少已建立一個資料集，現在可用來收集客戶同意資料：

* 以記錄為基礎的資料集，可在「即時客戶個人檔案」中使用。 **(必填)**
* 未啟用的時間序列資料集 [!DNL Profile]. (選填)

您現在可以返回 [IAB TCF 2.0概觀](./overview.md#merge-policies) 繼續為TCF 2.0法規遵循配置平台的流程。
