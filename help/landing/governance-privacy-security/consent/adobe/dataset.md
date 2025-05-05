---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 設定資料集以擷取同意和偏好設定資料
description: 瞭解如何設定Experience Data Model (XDM)結構描述和資料集，以擷取Adobe Experience Platform中的同意和偏好設定資料。
role: Developer
feature: Consent, Schemas, Datasets
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---

# 設定資料集以擷取同意和偏好設定資料

為了讓Adobe Experience Platform處理您的客戶同意/偏好設定資料，該資料必須傳送至其結構描述包含與同意和其他許可權相關欄位的資料集。 具體而言，此資料集必須以[!DNL XDM Individual Profile]類別為基礎，並啟用以在[!DNL Real-Time Customer Profile]中使用。

本檔案提供在Experience Platform中設定資料集以處理同意資料的步驟。 如需Experience Platform中處理同意/偏好設定資料的完整工作流程總覽，請參閱[同意處理總覽](./overview.md)。

>[!IMPORTANT]
>
>本指南中的範例使用標準化的欄位集來表示客戶同意值，如[[!UICONTROL 同意和偏好設定詳細資料]結構描述欄位群組](../../../../xdm/field-groups/profile/consents.md)所定義。 這些欄位的結構旨在提供有效的資料模型，以涵蓋許多常見的同意收集使用案例。
>
>不過，您也可以定義自己的欄位群組，以根據自己的資料模型表示同意。 請洽詢您的法律團隊，以根據下列選項取得符合您業務需求的同意資料模型核准：
>
>* 標準化的同意欄位群組
>* 由您的組織建立的自訂同意欄位群組
>* 標準化同意欄位群組和自訂同意欄位群組提供的其他欄位的組合

## 先決條件

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [體驗資料模型(XDM)](../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊。
* [即時客戶個人檔案](../../../../profile/home.md)：將不同來源的客戶資料整合至完整、統一的檢視中，並針對每個客戶互動提供可採取行動且附有時間戳記的帳戶。

>[!IMPORTANT]
>
>本教學課程假設您知道Experience Platform中要用來擷取客戶屬性資訊的[!DNL Profile]結構描述。 無論您使用何種方法來收集同意資料，此結構描述都必須針對Real-time Customer Profile[&#128279;](../../../../xdm/ui/resources/schemas.md#profile)啟用。 此外，結構描述的主要身分不能是禁止用於興趣型廣告（例如電子郵件地址）的直接可識別欄位。 如果您不確定哪些欄位受到限制，請諮詢法律顧問。

## [!UICONTROL 同意和偏好設定詳細資料]欄位群組結構 {#structure}

[!UICONTROL 同意和偏好設定詳細資料]欄位群組為結構描述提供標準化的同意欄位。 目前，此欄位群組僅與以[!DNL XDM Individual Profile]類別為基礎的結構描述相容。

欄位群組提供單一物件型別欄位`consents`，其子屬性會擷取一組標準化的同意欄位。 下列JSON為`consents`在資料擷取時所期望的資料型別範例：

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "idSpecific": {
      "email": {
        "jdoe@example.com": {
          "marketing": {
            "email": {
              "val": "n"
            }
          }
        }
      }
    }
  },
  "metadata": {
    "time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>如需有關`consents`中子屬性的結構和意義的詳細資訊，請參閱[[!UICONTROL 同意和偏好設定詳細資料]欄位群組](../../../../xdm/field-groups/profile/consents.md)的概觀。

## 新增必要欄位群組至您的[!DNL Profile]結構描述 {#add-field-group}

為了使用Adobe標準收集同意資料，您必須具備已啟用設定檔的結構描述，包含下列兩個欄位群組：

* [[!UICONTROL 同意和偏好設定詳細資料]](../../../../xdm/field-groups/profile/consents.md)
* [[!UICONTROL IdentityMap]](../../../../xdm/field-groups/profile/identitymap.md) (若使用Experience Platform Web或Mobile SDK傳送同意訊號則為必要)

在Experience Platform UI中，選取左側導覽中的&#x200B;**[!UICONTROL 結構描述]**，然後選取&#x200B;**[!UICONTROL 瀏覽]**&#x200B;索引標籤以顯示現有結構描述清單。 從這裡，選取您要新增同意欄位的[!DNL Profile]啟用結構描述的名稱。 本節中的熒幕擷取畫面以[方案建立教學課程](../../../../xdm/tutorials/create-schema-ui.md)中內建的「忠誠會員」方案為例。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>您可以使用工作區的搜尋和篩選功能來協助您更輕鬆地尋找結構描述。 如需詳細資訊，請參閱[探索XDM資源](../../../../xdm/ui/explore.md)的指南。

[!DNL Schema Editor]出現，顯示畫布中的結構描述結構。 在畫布的左側，選取&#x200B;**[!UICONTROL 欄位群組]**&#x200B;區段下的&#x200B;**[!UICONTROL 新增]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

**[!UICONTROL 新增欄位群組]**&#x200B;對話方塊就會顯示。 從這裡，從清單中選取&#x200B;**[!UICONTROL 同意和偏好設定詳細資料]**。 您可以選擇使用搜尋列來縮小結果，以便更輕鬆地找到欄位群組。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

接著，從清單中尋找&#x200B;**[!UICONTROL IdentityMap]**&#x200B;欄位群組並加以選取。 兩個欄位群組都列在右邊欄後，請選取&#x200B;**[!UICONTROL 新增欄位群組]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/identitymap.png)

畫布會重新出現，顯示`consents`和`identityMap`欄位已新增至結構描述結構。 如果您需要標準欄位群組未擷取的其他同意和偏好設定欄位，請參閱[將自訂同意和偏好設定欄位新增到結構描述](#custom-consent)的附錄區段。 否則，請選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以完成結構描述的變更。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

>[!IMPORTANT]
>
>如果您要建立新的結構描述，或編輯尚未為設定檔啟用的現有結構描述，您必須在儲存之前[為設定檔](../../../../xdm/ui/resources/schemas.md#profile)啟用結構描述。

如果您編輯的結構描述是由Experience Platform Web SDK資料流中指定的[!UICONTROL 設定檔資料集]使用，該資料集現在會包含新的同意欄位。 您現在可以返回[同意處理指南](./overview.md#merge-policies)，繼續設定Experience Platform以處理同意資料的程式。 如果您尚未為此結構描述建立資料集，請依照下一節中的步驟操作。

## 根據您的同意結構描述建立資料集 {#dataset}

使用同意欄位建立結構描述後，您必須建立資料集，以便最終擷取客戶的同意資料。 必須為[!DNL Real-Time Customer Profile]啟用此資料集。

若要開始，請在左側導覽中選取&#x200B;**[!UICONTROL 資料集]**，然後在右上角選取&#x200B;**[!UICONTROL 建立資料集]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

在下一頁，選取&#x200B;**[!UICONTROL 從結構描述建立資料集]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

**[!UICONTROL 從結構描述]**&#x200B;建立資料集工作流程隨即出現，從&#x200B;**[!UICONTROL 選取結構描述]**&#x200B;步驟開始。 在提供的清單中，找出您先前建立的其中一個同意結構描述。 您可以選擇使用搜尋列來縮小結果範圍，並更輕鬆地找到您的結構描述。 選取所需結構描述旁邊的圓鈕，然後選取[下一步] **[!UICONTROL 以繼續。]**

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

**[!UICONTROL 設定資料集]**&#x200B;步驟隨即顯示。 在選取&#x200B;**[!UICONTROL 完成]**&#x200B;之前，為資料集提供唯一、易於識別的名稱和描述。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

新建立資料集的詳細資訊頁面隨即顯示。 如果資料集是以您的時間序列結構描述為基礎，則程式已完成。 如果資料集是以您的記錄結構描述為基礎，程式中的最後一個步驟是啟用資料集以在[!DNL Real-Time Customer Profile]中使用。

在右邊欄中，選取&#x200B;**[!UICONTROL 設定檔]**&#x200B;切換按鈕。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

最後，在確認彈出視窗中選取&#x200B;**[!UICONTROL 啟用]**&#x200B;以啟用[!DNL Profile]的結構描述。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

資料集現已儲存並啟用以用於[!DNL Profile]。 如果您打算使用Experience Platform Web SDK傳送同意資料至設定檔，在設定[資料流](../../../../datastreams/overview.md)時，您必須選取此資料集作為[!UICONTROL 設定檔資料集]。

## 後續步驟

依照本教學課程，您已新增同意欄位至已啟用[!DNL Profile]的結構描述，其資料集將用來使用Experience Platform Web SDK或直接XDM擷取來擷取同意資料。

您現在可以返回[同意處理概述](./overview.md#merge-policies)，繼續設定Experience Platform以處理同意資料。

## 附錄

下節包含有關建立資料集以擷取客戶同意和偏好設定資料的其他資訊。

### 將自訂同意和偏好設定欄位新增到結構描述 {#custom-consent}

如果您需要擷取標準[!UICONTROL 同意和偏好設定詳細資料]欄位群組所代表以外的其他同意訊號，您可以使用自訂XDM元件來增強您的同意結構描述，以符合您的特定業務需求。 本節概述如何自訂同意綱要的基本原則，以便將這些訊號擷取至設定檔中。

>[!IMPORTANT]
>
>Experience Platform Web和Mobile SDK的同意變更命令不支援自訂欄位。 目前將自訂同意欄位擷取到設定檔的唯一方式是透過[批次擷取](../../../../ingestion/batch-ingestion/overview.md)或[來源連線](../../../../sources/home.md)。

強烈建議您使用[!UICONTROL 同意和偏好設定詳細資料]欄位群組作為同意資料結構的基準，並視需要新增其他欄位，而不是嘗試從頭開始建立整個結構。

若要將自訂欄位新增至標準欄位群組的結構，您必須先建立自訂欄位群組。 將[!UICONTROL 同意和偏好設定詳細資料]欄位群組新增到結構描述之後，請在&#x200B;**[!UICONTROL 欄位群組]**&#x200B;區段中選取&#x200B;**加號(+)**&#x200B;圖示，然後選取&#x200B;**[!UICONTROL 建立新欄位群組]**。 提供欄位群組的名稱和選擇性描述，然後選取&#x200B;**[!UICONTROL 新增欄位群組]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

[!DNL Schema Editor]會重新出現，並在左側邊欄中選取新的自訂欄位群組。 在畫布中顯示可讓您將自訂欄位新增到結構描述結構的控制項。 若要新增同意或偏好設定欄位，請選取`consents`物件旁的&#x200B;**加號(+)**&#x200B;圖示。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

新欄位會出現在`consents`物件中。 由於您要將自訂欄位新增到標準XDM物件，新欄位會在命名為租使用者ID的物件下建立。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

在&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;下的右側邊欄中，提供欄位的名稱和描述。 選取欄位的&#x200B;**[!UICONTROL 型別]**&#x200B;時，您必須針對自訂同意或偏好設定欄位使用適當的標準資料型別：

* [[!UICONTROL 一般同意欄位]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL 通用的行銷偏好設定欄位]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL 訂閱通用的行銷偏好設定欄位]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL 一般Personalization喜好設定欄位]](../../../../xdm/data-types/personalization-field.md)

完成後，選取&#x200B;**[!UICONTROL 套用]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

同意或偏好設定欄位會新增至結構描述結構。 請注意，右側邊欄中顯示的[!UICONTROL 路徑]包含`_tenantId`名稱空間。 每當您在資料作業中參照此欄位的路徑時，都必須包含此名稱空間。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

按照上述步驟繼續新增您需要的同意和偏好設定欄位。 完成時，選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以確認您的變更。

如果您尚未為此結構描述建立資料集，請繼續前往[建立資料集](#dataset)的區段。
