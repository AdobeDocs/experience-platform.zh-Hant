---
keywords: Experience Platform;home;IAB;IAB 2.0；同意；同意
solution: Experience Platform
title: 建立用於捕獲IAB TCF 2.0許可資料的資料集
topic-legacy: privacy events
description: 本文檔提供了設定兩個收集IAB TCF 2.0許可資料所需資料集的步驟。
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 0%

---

# 建立資料集，以擷取IAB TCF 2.0同意資料

為了讓Adobe Experience Platform按照IAB [!DNL Transparency & Consent Framework](TCF)2.0處理客戶同意資料，必須將該資料發送到方案包含TCF 2.0同意欄位的資料集。

具體來說，捕獲TCF 2.0許可資料需要兩個資料集：

* 基於[!DNL XDM Individual Profile]類的資料集，可用於[!DNL Real-time Customer Profile]。
* 基於[!DNL XDM ExperienceEvent]類的資料集。

本文檔提供了設定這兩個資料集以收集IAB TCF 2.0許可資料的步驟。 有關為TCF 2.0配置平台資料操作的完整工作流程的概述，請參閱[IAB TCF 2.0合規性概述](./overview.md)。

## 先決條件

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [體驗資料模型(XDM)](../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [架構構成基礎](../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊。
* [Adobe Experience Platform身分服務](../../../../identity-service/home.md):可讓您跨裝置和系統，從不同的資料來源橋接客戶身份。
   * [身分名稱空間](../../../../identity-service/namespaces.md):客戶身分資料必須以Identity Service所識別的特定身分名稱空間提供。
* [即時客戶個人檔案](../../../../profile/home.md):利用 [!DNL Identity Service] 這些工具，您可以即時從資料集建立詳細的客戶個人檔案。[!DNL Real-time Customer Profile] 從資料湖提取資料，並將客戶個人檔案保留在其個別的資料儲存中。

## [!UICONTROL Privacy Details] 欄位組結構  {#structure}

[!UICONTROL Privacy Details]模式欄位組提供TCF 2.0支援所需的客戶許可欄位。 此欄位組有兩個版本：一個與[!DNL XDM Individual Profile]類別相容，另一個與[!DNL XDM ExperienceEvent]類別相容。

以下各節將說明每個欄位群組的結構，包括擷取期間預期的資料。

### 配置檔案欄位組{#profile-field-group}

對於基於[!DNL XDM Individual Profile]的方案，[!UICONTROL Privacy Details]欄位組提供單個映射類型欄位`xdm:identityPrivacyInfo`，該欄位將客戶身份映射到其TCF許可偏好。 以下JSON是資料擷取時`xdm:identityPrivacyInfo`所需資料類型的範例：

```json
{
  "xdm:identityPrivacyInfo": {
      "ECID": {
        "13782522493631189": {
          "xdm:identityIABConsent": {
            "xdm:consentTimestamp": "2020-04-11T05:05:05Z",
            "xdm:consentString": {
              "xdm:consentStandard": "IAB TCF",
              "xdm:consentStandardVersion": "2.0",
              "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
              "xdm:gdprApplies": true,
              "xdm:containsPersonalData": false
            }
          }
        }
      }
    }
}
```

如示例所示，`xdm:identityPrivacyInfo`的每個根級別密鑰都與Identity Service所識別的身份名稱空間相對應。 反過來，每個namespace屬性至少必須有一個子屬性，其索引鍵與該namespace的客戶對應識別值相符。 在此範例中，客戶的Experience CloudID(`ECID`)值為`13782522493631189`。

>[!NOTE]
>
>雖然上述範例使用單一名稱空間／值對來表示客戶的身分，但您可以為其他名稱空間新增額外的索引鍵，而且每個名稱空間都可以有多個識別值，每個值都有其專屬的TCF同意偏好設定集。

身分值物件中是單一欄位`xdm:identityIABConsent`。 此物件會擷取客戶指定身分命名空間和值的TCF同意值。 此欄位包含的子屬性列於下列：

| 屬性 | 說明 |
| --- | --- |
| `xdm:consentTimestamp` | TCF許可值更改時的[ISO 8601](https://www.ietf.org/rfc/rfc3339.txt)時間戳。 |
| `xdm:consentString` | 包含客戶的更新同意資料和其他上下文資訊的對象。 請參閱[同意字串屬性](#consent-string)一節，瞭解此物件的必要子屬性。 |

### 事件欄位組{#event-field-group}

對於基於[!DNL XDM ExperienceEvent]的方案，[!UICONTROL Privacy Details]欄位組提供單個陣列類型欄位：`xdm:consentStrings`。 此陣列中的每個項目都必須是包含TCF許可字串必要屬性的對象，類似於配置檔案欄位組中的`xdm:consentString`欄位。 有關這些子屬性的詳細資訊，請參閱[下一節](#consent-string)。

```json
{
  "xdm:consentStrings": [
    {
      "xdm:consentStandard": "IAB TCF",
      "xdm:consentStandardVersion": "2.0",
      "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
      "xdm:gdprApplies": true,
      "xdm:containsPersonalData": false
    }
  ]
}
```

### 許可字串屬性{#consent-string}

[!UICONTROL Privacy Details]欄位組的兩個版本都要求至少有一個對象，該對象捕獲描述客戶TCF許可字串的必要欄位。 這些屬性說明如下：

| 屬性 | 說明 |
| --- | --- |
| `xdm:consentStandard` | 資料適用的同意框架。 對於TCF合規性，值必須為`IAB TCF`。 |
| `xdm:consentStandardVersion` | `xdm:consentStandard`所指示之同意框架的版本號。 對於TCF 2.0合規性，值必須為`2.0`。 |
| `xdm:consentStringValue` | 由許可管理平台(CMP)根據客戶的選定設定生成的許可字串。 |
| `xdm:gdprApplies` | 一個布爾值，指示GDPR是否適用於此客戶。 必須將值設定為`true` ，才能執行TCF 2.0。 如果未包含，則預設為`true`。 |
| `xdm:containsPersonalData` | 指示許可更新是否包含個人資料的布爾值。 如果未包含，則預設為`false`。 |

## 建立客戶許可方案{#create-schemas}

為了建立捕獲許可資料的資料集，您必須首先建立XDM架構以基於這些資料集。

在平台UI中，選擇左側導覽中的&#x200B;**[!UICONTROL Schemas]**&#x200B;以開啟[!UICONTROL Schemas]工作區。 從這裡，請依照下列各節中的步驟建立每個必要的架構。

>[!NOTE]
>
>如果您有想要用來擷取同意資料的現有XDM結構，您可以編輯這些結構，而不是建立新的結構。 但是，如果現有結構已啟用在即時客戶描述檔中使用，其主要識別碼不能是直接可識別的欄位，而無法用於喜好式廣告，例如電子郵件地址。 如果您不確定哪些欄位受限制，請洽詢您的法律顧問。
>
>此外，編輯現有結構描述時，只能進行加法（非中斷）變更。 如需詳細資訊，請參閱[架構演化原則](../../../../xdm/schema/composition.md#evolution)一節。

### 建立基於記錄的許可方案{#profile-schema}

在&#x200B;**[!UICONTROL Schemas]**&#x200B;工作區中，選擇&#x200B;**[!UICONTROL Create schema]**，然後從下拉式清單中選擇&#x200B;**[!UICONTROL XDM Individual Profile]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

出現[!DNL Schema Editor]，顯示畫布中的架構結構。 使用右側欄來提供架構的名稱和說明，然後在畫布左側的&#x200B;**[!UICONTROL Field groups]**&#x200B;區段下選取&#x200B;**[!UICONTROL Add]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

出現&#x200B;**[!UICONTROL Add field groups]**&#x200B;對話框。 從這裡，從清單中選擇&#x200B;**[!UICONTROL Privacy Details]**。 您可以選擇使用搜尋列縮小結果，以更輕鬆地找到欄位群組。 選擇欄位組後，選擇&#x200B;**[!UICONTROL Add field groups]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

畫布會重新出現，顯示`identityPrivacyInfo`欄位已新增至架構結構。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

從這裡，重複上述步驟，將下列其他欄位群組新增至架構：

* [!UICONTROL IdentityMap]
* [!UICONTROL Data capture region for Profile]
* [!UICONTROL Demographic Details]
* [!UICONTROL Personal Contact Details]

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-all-field-groups.png)

如果您正在編輯已啟用在[!DNL Real-time Customer Profile]中使用的現有模式，請選擇&#x200B;**[!UICONTROL Save]**&#x200B;以確認您所做的更改，然後跳到[中基於您的同意模式](#dataset)建立資料集的部分。 如果要建立新模式，請繼續遵循下面子部分中概述的步驟。

#### 啟用方案以用於[!DNL Real-time Customer Profile]

為了讓平台將其接收的許可資料與特定客戶配置檔案關聯，必須啟用許可方案以便在[!DNL Real-time Customer Profile]中使用。

>[!NOTE]
>
>本節中顯示的示例方案使用其`identityMap`欄位作為其主要標識。 如果您想要將另一個欄位設為主要身分識別，請確定您使用的是Cookie ID等間接識別碼，而不是禁止在喜好式廣告（例如電子郵件地址）中使用的直接識別欄位。 如果您不確定哪些欄位受限制，請洽詢您的法律顧問。
>
>有關如何為方案設定主標識欄位的步驟，請參見[方案建立教程](../../../../xdm/tutorials/create-schema-ui.md#identity-field)。

要啟用[!DNL Profile]的架構，請在左側導軌中選擇架構的名稱，以開啟右側導軌中的&#x200B;**[!UICONTROL Schema properties]**&#x200B;對話框。 從這裡，選擇&#x200B;**[!UICONTROL Profile]**&#x200B;切換按鈕。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

出現一個快顯視窗，指出遺失主要識別。 選中用於使用備用主標識的複選框，因為主標識將包含在`identityMap`欄位中。

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

最後，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以確認您所做的變更。

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### 建立基於時間序列的許可方案{#event-schema}

在&#x200B;**[!UICONTROL Schemas]**&#x200B;工作區中，選擇&#x200B;**[!UICONTROL Create schema]**，然後從下拉式清單中選擇&#x200B;**[!UICONTROL XDM ExperienceEvent]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

出現[!DNL Schema Editor]，顯示畫布中的架構結構。 使用右側欄來提供架構的名稱和說明，然後在畫布左側的&#x200B;**[!UICONTROL Field groups]**&#x200B;區段下選取&#x200B;**[!UICONTROL Add]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

出現&#x200B;**[!UICONTROL Add field groups]**&#x200B;對話框。 從這裡，從清單中選擇&#x200B;**[!UICONTROL Privacy Details]**。 您可以選擇使用搜尋列縮小結果，以更輕鬆地找到欄位群組。 選擇欄位組後，選擇&#x200B;**[!UICONTROL Add field groups]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

畫布會重新出現，顯示`consentStrings`陣列已新增至架構結構。

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

從這裡，重複上述步驟，將下列其他欄位群組新增至架構：

* [!UICONTROL IdentityMap]
* [!UICONTROL Environment Details]
* [!UICONTROL Web Details]
* [!UICONTROL Implementation Details]

新增欄位群組後，請選取&#x200B;**[!UICONTROL Save]**&#x200B;以完成。

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## 根據您的許可方案建立資料集{#datasets}

對於上述每個必要的結構描述，您必須建立資料集，以最終收錄客戶的同意資料。 必須為[!DNL Real-time Customer Profile]啟用基於記錄模式的資料集，而基於時間序列模式&#x200B;**的資料集不應**&#x200B;啟用[!DNL Profile]。

若要開始，請在左側導覽中選取&#x200B;**[!UICONTROL Datasets]**，然後在右上角選取&#x200B;**[!UICONTROL Create dataset]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

在下一頁，選擇&#x200B;**[!UICONTROL Create dataset from schema]**。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

將顯示&#x200B;**[!UICONTROL Create dataset from schema]**&#x200B;工作流，從&#x200B;**[!UICONTROL Select schema]**&#x200B;步驟開始。 在提供的清單中，找出您先前建立的其中一個同意方案。 您可以選擇使用搜尋列來縮小結果範圍，並更輕鬆地尋找結構。 選擇所需方案旁的單選按鈕，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

出現&#x200B;**[!UICONTROL Configure dataset]**&#x200B;步驟。 在選擇&#x200B;**[!UICONTROL Finish]**&#x200B;之前，請為資料集提供唯一、可輕鬆識別的名稱和說明。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

此時會顯示新建立資料集的詳細資料頁面。 如果資料集是以您的時間序列模式為基礎，則程式已完成。 如果資料集是以您的記錄架構為基礎，則程式的最後步驟是啟用資料集以用於[!DNL Real-time Customer Profile]。

在右側邊欄中，選擇&#x200B;**[!UICONTROL Profile]**&#x200B;切換，然後在確認快顯視窗中選擇&#x200B;**[!UICONTROL Enable]**，以啟用[!DNL Profile]的方案。

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

請再次遵循上述步驟，以建立符合TCF 2.0規範的其他必要資料集。

## 後續步驟

按照本教程，您已建立了兩個資料集，現在可用於收集客戶同意資料：

* 可在即時客戶個人檔案中使用的記錄型資料集。
* 未為[!DNL Profile]啟用的基於時間序列的資料集。

您現在可以返回[IAB TCF 2.0概觀](./overview.md#merge-policies)以繼續配置平台以符合TCF 2.0。
