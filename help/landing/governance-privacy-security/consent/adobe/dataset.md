---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 設定資料集以擷取同意和偏好設定資料
topic-legacy: getting started
description: 了解如何設定Experience Data Model(XDM)結構和資料集，以在Adobe Experience Platform中擷取同意和偏好設定資料。
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: da7696d288543abd21ff8a1402e81dcea32efbc2
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 0%

---

# 設定資料集以擷取同意和偏好設定資料

為了讓Adobe Experience Platform處理您的客戶同意/偏好設定資料，該資料必須傳送至資料集，其結構包含與同意和其他權限相關的欄位。 具體而言，此資料集必須以[!DNL XDM Individual Profile]類別為基礎，並啟用以在[!DNL Real-time Customer Profile]中使用。

本檔案提供設定資料集以處理Experience Platform中同意資料的步驟。 如需在Platform中處理同意/偏好設定資料的完整工作流程的概觀，請參閱[同意處理概述](./overview.md)。

>[!IMPORTANT]
>
>本指南中的範例使用標準化的欄位集來表示客戶同意值，如[[!UICONTROL 同意和偏好設定]結構欄位群組](../../../../xdm/field-groups/profile/consents.md)所定義。 這些欄位的結構旨在提供有效的資料模型，以涵蓋許多常見的同意收集使用案例。
>
>不過，您也可以定義自己的欄位群組，以根據自己的資料模型來表示同意。 請洽詢您的法律團隊，根據下列選項，取得符合您業務需求的同意資料模型的核准：
>
>* 標準化同意欄位群組
>* 貴組織建立的自訂同意欄位群組
>* 標準化同意欄位群組和自訂同意欄位群組提供之其他欄位的組合


## 先決條件

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [Experience Data Model(XDM)](../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [結構構成基本概念](../../../../xdm/schema/composition.md):了解XDM結構的基本建置組塊。
* [即時客戶個人檔案](../../../../profile/home.md):將不同來源的客戶資料整合為完整、統一的檢視，同時提供每個客戶互動的可操作、時間戳記帳戶。

>[!IMPORTANT]
>
>本教學課程假設您知道Platform中的[!DNL Profile]結構，而您想使用該架構來擷取客戶屬性資訊。 無論您使用何種方法收集同意資料，此結構都必須為「即時客戶設定檔」](../../../../xdm/ui/resources/schemas.md#profile)啟用[。 此外，結構的主要身分不能是禁止在以興趣為基礎的廣告（例如電子郵件地址）中使用的可直接識別欄位。 如果您不確定哪些欄位受限，請洽詢您的法律顧問。

## [!UICONTROL 同意和] 偏好欄位群組結構 {#structure}

[!UICONTROL 同意和偏好設定]欄位群組提供結構的標準化同意欄位。 目前，此欄位組僅與基於[!DNL XDM Individual Profile]類的架構相容。

欄位組提供單個對象類型欄位`consents`，其子屬性捕獲一組標準化的同意欄位。 以下JSON是資料擷取時`consents`所需資料類型的範例：

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
>有關`consents`中子屬性的結構和含義的詳細資訊，請參閱[[!UICONTROL Consents and Preferences]欄位組](../../../../xdm/field-groups/profile/consents.md)上的概述。

## 將[!UICONTROL 同意和偏好設定]欄位群組新增至[!DNL Profile]架構 {#add-field-group}

在Platform UI中，選取左側導覽中的&#x200B;**[!UICONTROL 結構]**，然後選取&#x200B;**[!UICONTROL Browse]**&#x200B;標籤以顯示現有結構的清單。 從此處，選擇要向其添加同意欄位的[!DNL Profile]啟用架構的名稱。 本節中的螢幕擷取畫面以[架構建立教學課程](../../../../xdm/tutorials/create-schema-ui.md)中建置的「忠誠會員」架構為範例。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>您可以使用工作區的搜尋和篩選功能，協助您更輕鬆找到您的結構。 如需詳細資訊，請參閱[探索XDM資源](../../../../xdm/ui/explore.md)的指南。

此時會出現[!DNL Schema Editor]，顯示畫布中架構的結構。 在畫布的左側，選取&#x200B;**[!UICONTROL 欄位群組]**&#x200B;區段下的&#x200B;**[!UICONTROL 新增]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

將顯示&#x200B;**[!UICONTROL 添加欄位組]**&#x200B;對話框。 從此處，從清單中選擇&#x200B;**[!UICONTROL Consensts and Preferences]**。 您可以選擇使用搜尋列來縮小結果，以便更輕鬆地找出欄位群組。 選擇欄位組後，選擇&#x200B;**[!UICONTROL 添加欄位組]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

畫布會重新顯示，顯示`consents`物件已新增至架構結構。 如果您需要其他未由標準欄位群組擷取的同意和偏好設定欄位，請參閱[上的附錄區段，將自訂同意和偏好設定欄位新增至架構](#custom-consent)。 否則，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以完成對架構的更改。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

如果您在Platform Web SDK資料流中指定的[!UICONTROL 設定檔資料集]使用您編輯的結構，該資料集現在會包含新的同意欄位。 您現在可以返回[同意處理指南](./overview.md#merge-policies)，繼續設定Experience Platform以處理同意資料的程式。

如果您尚未為此結構建立資料集，請依照下一節中的步驟操作。

## 根據您的同意結構建立資料集 {#dataset}

建立含同意欄位的結構後，您必須建立資料集，最終內嵌客戶的同意資料。 必須為[!DNL Real-time Customer Profile]啟用此資料集。

若要開始，請在左側導覽中選取「**[!UICONTROL 資料集]**」，然後選取右上角的「**[!UICONTROL 建立資料集]**」。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

在下一頁，選擇「從架構&#x200B;]**建立資料集」。**[!UICONTROL 

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

從&#x200B;**[!UICONTROL 選擇架構]**&#x200B;步驟開始，將顯示&#x200B;**[!UICONTROL 從架構]**&#x200B;建立資料集工作流。 在提供的清單中，找出您先前建立的其中一個同意結構。 您可以選擇使用搜尋列來縮小結果範圍，並更輕鬆地找出您的結構。 選擇所需架構旁的單選按鈕，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

此時會出現「**[!UICONTROL 設定資料集]**」步驟。 在選擇&#x200B;**[!UICONTROL Finish]**&#x200B;之前，為資料集提供可輕鬆識別的唯一名稱和說明。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

隨即顯示新建立資料集的詳細資訊頁面。 如果資料集以您的時間序列結構為基礎，則程式會完成。 如果資料集以您的記錄結構為基礎，則此程式的最後一步是啟用資料集以用於[!DNL Real-time Customer Profile]。

在右側邊欄中，選取&#x200B;**[!UICONTROL 設定檔]**&#x200B;切換。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

最後，在確認彈出視窗中選取&#x200B;**[!UICONTROL 啟用]**&#x200B;以啟用[!DNL Profile]的架構。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

資料集現在已儲存並啟用，以用於[!DNL Profile]。 如果您打算使用Platform Web SDK將同意資料傳送至設定檔，在設定[datastream](../../../../edge/fundamentals/datastreams.md)時，必須將此資料集選取為[!UICONTROL 設定檔資料集]。

## 後續步驟

依照本教學課程，您已將同意欄位新增至已啟用[!DNL Profile]的結構，其資料集將用來使用Platform Web SDK內嵌同意資料，或直接XDM內嵌。

您現在可以返回[同意處理概述](./overview.md#merge-policies)以繼續設定處理同意資料的Experience Platform。

## 附錄

以下章節包含建立資料集以擷取客戶同意和偏好設定資料的其他資訊。

### 將自訂同意和偏好設定欄位新增至結構 {#custom-consent}

如果您需要擷取標準[!UICONTROL 同意和偏好設定]欄位群組所代表以外的其他同意訊號，則可使用自訂XDM元件來增強同意結構，以符合您的特定業務需求。 本節概述如何自訂同意結構以將這些訊號內嵌至設定檔的基本原則。

>[!IMPORTANT]
>
>Platform Web和行動SDK不支援其同意變更命令中的自訂欄位。 目前，將自訂同意欄位內嵌至「設定檔」的唯一方式是透過[批次內嵌](../../../../ingestion/batch-ingestion/overview.md)或[來源連線](../../../../sources/home.md)。

強烈建議您使用[!UICONTROL 同意和偏好設定]欄位群組作為同意資料結構的基線，並視需要新增其他欄位，而非嘗試從頭建立整個結構。

若要將自訂欄位新增至標準欄位群組的結構，您必須先建立自訂欄位群組。 將[!UICONTROL 同意和首選項]欄位組添加到架構後，在&#x200B;**[!UICONTROL 欄位組]**&#x200B;區段中選擇&#x200B;**加號(+)**&#x200B;表徵圖，然後選擇&#x200B;**[!UICONTROL 建立新欄位組]**。 提供欄位組的名稱和可選說明，然後選擇&#x200B;**[!UICONTROL 添加欄位組]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

[!DNL Schema Editor]會重新顯示，並在左側邊欄中選取新的自訂欄位群組。 在畫布中，會顯示可讓您新增自訂欄位至架構結構的控制項。 若要新增同意或偏好設定欄位，請選取`consents`物件旁的&#x200B;**加號(+)**&#x200B;圖示。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

`consents`物件中會出現新欄位。 由於您要將自訂欄位新增至標準XDM物件，因此新欄位會建立在與租用戶ID命名的物件下。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

在右側欄的&#x200B;**[!UICONTROL 欄位屬性]**&#x200B;下，提供欄位的名稱和說明。 選取欄位的&#x200B;**[!UICONTROL Type]**&#x200B;時，您必須為自訂同意或偏好設定欄位使用適當的標準資料類型：

* [[!UICONTROL 一般同意欄位]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL 一般行銷偏好設定欄位]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL 具有訂閱的一般行銷偏好設定欄位]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL 一般個人化偏好設定欄位]](../../../../xdm/data-types/personalization-field.md)

完成後，選擇&#x200B;**[!UICONTROL Apply]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

同意或偏好設定欄位會新增至架構結構。 請注意，右側邊欄中顯示的[!UICONTROL Path]包含`_tenantId`命名空間。 每當您在資料操作中參考此欄位的路徑時，都必須包含此命名空間。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

請依照上述步驟，繼續新增您需要的同意和偏好設定欄位。 完成後，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以確認更改。

如果您尚未為此架構建立資料集，請繼續前往[建立資料集](#dataset)的區段。
