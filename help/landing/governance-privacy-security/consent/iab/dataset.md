---
keywords: Experience Platform；首頁；IAB;IAB 2.0；同意；同意
solution: Experience Platform
title: 建立資料集以擷取IAB TCF 2.0同意資料
topic-legacy: privacy events
description: 本檔案提供設定兩個必要資料集以收集IAB TCF 2.0同意資料的步驟。
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: 9b75a69cc6e31ea0ad77048a6ec1541df2026f27
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# 建立資料集以擷取IAB TCF 2.0同意資料

為了讓Adobe Experience Platform依照IAB [!DNL Transparency & Consent Framework](TCF)2.0處理客戶同意資料，該資料必須傳送至其結構包含TCF 2.0同意欄位的資料集。

具體來說，擷取TCF 2.0同意資料需要兩個資料集：

* 以[!DNL XDM Individual Profile]類別為基礎的資料集，可在[!DNL Real-time Customer Profile]中使用。
* 以[!DNL XDM ExperienceEvent]類別為基礎的資料集。

>[!IMPORTANT]
>
>Platform只會強制收集到個別設定檔資料集中的TCF字串。 雖然在此工作流程中仍需要ExperienceEvent資料集來建立資料流，但您只需將資料內嵌至設定檔資料集即可。 如果您想要追蹤一段時間內的同意變更事件，仍可使用ExperienceEvent資料集，但在強制啟用區段時，不會使用這些值。

本檔案提供設定這兩個資料集的步驟。 如需針對TCF 2.0設定平台資料作業完整工作流程的概述，請參閱[IAB TCF 2.0法規遵循概述](./overview.md)。

## 先決條件

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [Experience Data Model(XDM)](../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [結構構成基本概念](../../../../xdm/schema/composition.md):了解XDM結構的基本建置組塊。
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md):可讓您跨裝置和系統，從不同的資料來源橋接客戶身分。
   * [身分識別命名空間](../../../../identity-service/namespaces.md):客戶身分資料必須以Identity Service所識別的特定身分命名空間提供。
* [即時客戶個人檔案](../../../../profile/home.md):利 [!DNL Identity Service] 用可讓您即時從資料集建立詳細的客戶設定檔。[!DNL Real-time Customer Profile] 從資料湖提取資料，並將客戶設定檔保存在其自己的個別資料存放區中。

## TCF 2.0欄位組 {#field-groups}

[!UICONTROL IAB TCF 2.0同意]結構欄位群組提供TCF 2.0支援所需的客戶同意欄位。 此欄位群組有兩個版本：一個與[!DNL XDM Individual Profile]類相容，另一個與[!DNL XDM ExperienceEvent]類相容。

以下各節說明每個欄位群組的結構，包括擷取期間預期的資料。

### 設定檔欄位群組 {#profile-field-group}

針對以[!DNL XDM Individual Profile]為基礎的結構， [!UICONTROL IAB TCF 2.0同意]欄位群組提供單一對應類型欄位`identityPrivacyInfo`，可將客戶身分對應至其TCF同意偏好設定。 此欄位群組必須包含在為「即時客戶設定檔」啟用的記錄型結構中，才能自動執行。

請參閱此欄位組的[參考指南](../../../../xdm/field-groups/profile/iab.md)以深入了解其結構和使用案例。

### 事件欄位組 {#event-field-group}

如果您想要追蹤隨時間變化的同意變更事件，可將[!UICONTROL IAB TCF 2.0同意]欄位群組新增至您的[!UICONTROL XDM ExperienceEvent]結構。

如果您不打算隨著時間追蹤同意變更事件，則不需要將此欄位群組納入事件結構。 自動強制執行TCF同意值時，Experience Platform只會使用擷取至[設定檔欄位群組](#profile-field-group)的最新同意資訊。 事件擷取的同意值不會參與自動執行工作流程。

有關此欄位組的結構和使用案例的詳細資訊，請參閱[參考指南](../../../../xdm/field-groups/event/iab.md)。

## 建立客戶同意結構 {#create-schemas}

若要建立擷取同意資料的資料集，您必須先建立XDM結構，才能將這些資料集建立在上。

在Platform UI中，選取左側導覽中的&#x200B;**[!UICONTROL 結構]**&#x200B;以開啟[!UICONTROL 結構]工作區。 從這裡，請依照以下各節中的步驟，建立每個必要的架構。

>[!NOTE]
>
>如果您有想要用來擷取同意資料的現有XDM結構，您可以編輯這些結構，而非建立新結構。 不過，如果現有結構已啟用在即時客戶設定檔中使用，其主要身分不能是禁止在興趣型廣告（例如電子郵件地址）中使用的可直接識別欄位。 如果您不確定哪些欄位受限，請洽詢您的法律顧問。
>
>此外，編輯現有結構時，只能進行加法（非中斷）變更。 如需詳細資訊，請參閱[架構演化原則](../../../../xdm/schema/composition.md#evolution)一節。

### 建立設定檔同意結構 {#profile-schema}

選擇「**[!UICONTROL 建立架構]**」，然後從下拉菜單中選擇「**[!UICONTROL XDM單個配置檔案]**」。

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

此時將顯示&#x200B;**[!UICONTROL 添加欄位組]**&#x200B;對話框，允許您立即開始向架構添加欄位組。 從此處，從清單中選取&#x200B;**[!UICONTROL IAB TCF 2.0同意]**。 您可以選擇使用搜尋列來縮小結果，以便更輕鬆地找出欄位群組。 選擇欄位組後，選擇&#x200B;**[!UICONTROL 添加欄位組]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

畫布會重新顯示，顯示`identityPrivacyInfo`欄位已新增至架構結構。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

在將更多欄位新增至架構之前，請選取根欄位，以在右側邊欄中顯示&#x200B;**[!UICONTROL 架構屬性]**，您可在此提供架構的名稱和說明。

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

提供名稱和說明後，請在畫布左側的&#x200B;**[!UICONTROL 欄位群組]**&#x200B;區段下選取&#x200B;**[!UICONTROL 新增]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

從此處，使用對話框將以下其他欄位組添加到架構中：

* [!UICONTROL IdentityMap]
* [!UICONTROL 設定檔的資料擷取區域]
* [!UICONTROL 人口統計詳細資料]
* [!UICONTROL 個人聯繫人詳細資訊]

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-all-field-groups.png)

如果您正在編輯已啟用在[!DNL Real-time Customer Profile]中使用的現有架構，請選擇&#x200B;**[!UICONTROL Save]**&#x200B;以確認更改，然後跳到[基於您的同意架構](#dataset)建立資料集的部分。 如果要建立新架構，請繼續執行以下小節中概述的步驟。

#### 啟用架構以用於[!DNL Real-time Customer Profile]

為了讓Platform將其收到的同意資料與特定客戶設定檔建立關聯，必須啟用同意結構以用於[!DNL Real-time Customer Profile]。

>[!NOTE]
>
>本節中顯示的範例架構使用其`identityMap`欄位作為其主要身分。 如果您想要將另一個欄位設為主要身分，請確定您使用的是間接識別碼，如Cookie ID，而非不得在以興趣為基礎的廣告（例如電子郵件地址）中使用的直接識別欄位。 如果您不確定哪些欄位受限，請洽詢您的法律顧問。
>
>有關如何為架構設定主要身份欄位的步驟，請參見[架構建立教程](../../../../xdm/tutorials/create-schema-ui.md#identity-field)。

若要啟用[!DNL Profile]的架構，請在左側邊欄中選取該架構的名稱，以開啟&#x200B;**[!UICONTROL Schema properties]**&#x200B;區段。 從此處，選擇&#x200B;**[!UICONTROL Profile]**&#x200B;切換按鈕。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

畫面隨即顯示彈出視窗，指出遺失主要身分。 選中使用替代主標識的複選框，因為主標識將包含在`identityMap`欄位中。

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

最後，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以確認更改。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### 建立事件同意結構 {#event-schema}

在&#x200B;**[!UICONTROL 結構]**&#x200B;工作區中，選擇&#x200B;**[!UICONTROL 建立結構]**，然後從下拉式清單中選擇&#x200B;**[!UICONTROL XDM ExperienceEvent]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

此時將顯示&#x200B;**[!UICONTROL 添加欄位組]**&#x200B;對話框。 從此處，從清單中選取&#x200B;**[!UICONTROL IAB TCF 2.0同意]**。 您可以選擇使用搜尋列來縮小結果，以便更輕鬆地找出欄位群組。 選擇欄位組後，選擇&#x200B;**[!UICONTROL 添加欄位組]**。

>[!NOTE]
>
>只有在您打算隨時間追蹤同意變更事件時，才需要在事件結構中加入此欄位群組。 若您不想追蹤這些事件，可在設定Web SDK時，使用不含這些欄位的事件結構。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

畫布會重新顯示，顯示`consentStrings`欄位已新增至架構結構。

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

在將更多欄位新增至架構之前，請選取根欄位，以在右側邊欄中顯示&#x200B;**[!UICONTROL 架構屬性]**，您可在此提供架構的名稱和說明。

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

提供名稱和說明後，請在畫布左側的&#x200B;**[!UICONTROL 欄位群組]**&#x200B;區段下選取&#x200B;**[!UICONTROL 新增]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

在此，重複上述步驟，將下列其他欄位群組新增至架構：

* [!UICONTROL IdentityMap]
* [!UICONTROL 環境詳細資訊]
* [!UICONTROL Web詳細資訊]
* [!UICONTROL 實作詳細資料]

新增欄位群組後，請選取&#x200B;**[!UICONTROL Save]**&#x200B;以完成。

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## 根據同意結構建立資料集 {#datasets}

您必須針對上述每個必要結構建立資料集，以最終內嵌客戶的同意資料。 必須為[!DNL Real-time Customer Profile]啟用以記錄架構為基礎的資料集，而以時間序列架構&#x200B;**為基礎的資料集不應**&#x200B;啟用[!DNL Profile]。

若要開始，請在左側導覽中選取「**[!UICONTROL 資料集]**」，然後選取右上角的「**[!UICONTROL 建立資料集]**」。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

在下一頁，選擇「從架構&#x200B;]**建立資料集」。**[!UICONTROL 

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

從&#x200B;**[!UICONTROL 選擇架構]**&#x200B;步驟開始，將顯示&#x200B;**[!UICONTROL 從架構]**&#x200B;建立資料集工作流。 在提供的清單中，找出您先前建立的其中一個同意結構。 您可以選擇使用搜尋列來縮小結果範圍，並更輕鬆地找出您的結構。 選擇所需架構旁的單選按鈕，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

此時會出現「**[!UICONTROL 設定資料集]**」步驟。 在選擇&#x200B;**[!UICONTROL Finish]**&#x200B;之前，為資料集提供可輕鬆識別的唯一名稱和說明。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

隨即顯示新建立資料集的詳細資訊頁面。 如果資料集以您的時間序列結構為基礎，則程式會完成。 如果資料集以您的記錄結構為基礎，則此程式的最後一步是啟用資料集以用於[!DNL Real-time Customer Profile]。

在右側邊欄中，選取&#x200B;**[!UICONTROL Profile]**&#x200B;切換，然後在確認彈出視窗中選取&#x200B;**[!UICONTROL Enable]**&#x200B;以啟用[!DNL Profile]的結構。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

請再次遵循上述步驟，建立符合TCF 2.0規範的其他必要資料集。

## 後續步驟

依照本教學課程，您已建立兩個資料集，現在可用來收集客戶同意資料：

* 以記錄為基礎的資料集，可在「即時客戶個人檔案」中使用。
* 未為[!DNL Profile]啟用的時間序列資料集。

您現在可以返回[IAB TCF 2.0概述](./overview.md#merge-policies)以繼續設定符合TCF 2.0的平台程式。
