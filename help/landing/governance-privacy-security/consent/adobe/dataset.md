---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 配置資料集以捕獲同意和首選項資料
description: 瞭解如何配置體驗資料模型(XDM)架構和資料集以捕獲Adobe Experience Platform的同意和偏好資料。
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# 配置資料集以捕獲同意和首選項資料

為了讓Adobe Experience Platform處理您的客戶同意/首選項資料，必須將該資料發送到其架構包含與同意和其他權限相關欄位的資料集。 具體而言，此資料集必須基於 [!DNL XDM Individual Profile] 類，並啟用 [!DNL Real-Time Customer Profile]。

本文檔提供了配置資料集以處理Experience Platform中的同意資料的步驟。 有關在平台中處理同意/首選項資料的完整工作流的概述，請參閱 [同意處理概述](./overview.md)。

>[!IMPORTANT]
>
>本指南中的示例使用一組標準化欄位來表示客戶同意值，如 [[!UICONTROL 同意和首選項詳細資訊] 架構欄位組](../../../../xdm/field-groups/profile/consents.md)。 這些欄位的結構旨在提供一個有效的資料模型，以涵蓋許多常見的同意收集使用案例。
>
>但是，您也可以根據自己的資料模型定義自己的欄位組來表示同意。 請咨詢您的法律團隊，以獲得符合您業務需要的同意資料模型的批准，具體選項如下：
>
>* 標準化同意現場小組
>* 由您的組織建立的自定義同意欄位組
>* 標準化同意欄位組和由自定義同意欄位組提供的附加欄位的組合


## 先決條件

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [體驗資料模型(XDM)](../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建塊。
* [即時客戶配置檔案](../../../../profile/home.md):將來自不同來源的客戶資料整合到一個完整、統一的視圖中，同時為每個客戶交互提供一個可操作且時間戳記的帳戶。

>[!IMPORTANT]
>
>本教程假定您知道 [!DNL Profile] 用於捕獲客戶屬性資訊的平台中的架構。 無論您使用何種方法收集同意資料，此架構必須 [為即時客戶配置檔案啟用](../../../../xdm/ui/resources/schemas.md#profile)。 此外，架構的主要身份不能是禁止在基於興趣的廣告中使用的直接可識別欄位，例如電子郵件地址。 如果您不確定哪些欄位受到限制，請咨詢您的法律顧問。

## [!UICONTROL 同意和首選項詳細資訊] 欄位組結構 {#structure}

的 [!UICONTROL 同意和首選項詳細資訊] 欄位組為架構提供標準化的同意欄位。 當前，此欄位組僅與基於 [!DNL XDM Individual Profile] 類。

欄位組提供單個對象類型欄位， `consents`，其子屬性捕獲一組標準化的同意欄位。 以下JSON是資料類型的示例 `consents` 預期在資料接收時：

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
>有關中子屬性的結構和含義的詳細資訊 `consents`，請參閱 [[!UICONTROL 同意和首選項詳細資訊] 欄位組](../../../../xdm/field-groups/profile/consents.md)。

## 將必填欄位組添加到 [!DNL Profile] 架構 {#add-field-group}

要使用Adobe標準收集同意資料，您必須具有啟用配置檔案的架構，該架構包含以下兩個欄位組：

* [!UICONTROL 同意和首選項詳細資訊]
* [!UICONTROL 標識映射] （如果使用平台Web或移動SDK發送同意信號，則為必需）

在平台UI中，選擇 **[!UICONTROL 架構]** 在左側導航中，選擇 **[!UICONTROL 瀏覽]** 頁籤，顯示現有架構的清單。 從此處，選擇 [!DNL Profile]-enabled方案，您要將同意欄位添加到其中。 此部分中的螢幕抓圖使用中內置的「會員」架構 [架構建立教程](../../../../xdm/tutorials/create-schema-ui.md) 例如，

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>可以使用工作區的搜索和篩選功能幫助更輕鬆地查找架構。 請參閱上的指南 [探索XDM資源](../../../../xdm/ui/explore.md) 的子菜單。

的 [!DNL Schema Editor] 顯示畫布中架構的結構。 在畫布的左側，選擇 **[!UICONTROL 添加]** 下 **[!UICONTROL 欄位組]** 的子菜單。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

的 **[!UICONTROL 添加欄位組]** 對話框。 從此處，選擇 **[!UICONTROL 同意和首選項詳細資訊]** 清單中。 您可以選擇使用搜索欄縮小結果範圍，以便更輕鬆地查找欄位組。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

接下來，查找 **[!UICONTROL 標識映射]** 欄位組，並選擇它。 在右滑軌中列出兩個欄位組後，選擇 **[!UICONTROL 添加欄位組]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/identitymap.png)

畫布重新出現，顯示 `consents` 和 `identityMap` 欄位已添加到架構結構中。 如果需要其他同意和未由標準欄位組捕獲的首選項欄位，請參閱附錄部分。 [將自定義同意和首選項欄位添加到架構](#custom-consent)。 否則，選擇 **[!UICONTROL 保存]** 完成對架構的更改。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

>[!IMPORTANT]
>
>如果要建立新架構或編輯尚未為配置檔案啟用的現有架構，則必須 [啟用配置檔案的架構](../../../../xdm/ui/resources/schemas.md#profile) 在保存之前。

如果您編輯的架構由 [!UICONTROL 配置檔案資料集] 在平台Web SDK資料流中指定，該資料集現在將包含新的同意欄位。 您現在可以返回 [同意處理指南](./overview.md#merge-policies) 繼續配置Experience Platform以處理同意資料的過程。 如果尚未為此架構建立資料集，請按照下一節中的步驟操作。

## 根據您的同意架構建立資料集 {#dataset}

建立具有同意欄位的架構後，必須建立最終將接收客戶同意資料的資料集。 必須為 [!DNL Real-Time Customer Profile]。

要開始，請選擇 **[!UICONTROL 資料集]** 在左側導航中，然後選擇 **[!UICONTROL 建立資料集]** 在右上角。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

在下一頁，選擇 **[!UICONTROL 從架構建立資料集]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

的 **[!UICONTROL 從架構建立資料集]** 工作流，從 **[!UICONTROL 選擇架構]** 的子菜單。 在提供的清單中，找到您以前建立的同意架構之一。 您可以選擇使用搜索欄縮小結果範圍，並更輕鬆地定位方案。 選擇所需方案旁邊的單選按鈕，然後選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

的 **[!UICONTROL 配置資料集]** 的上界。 在選擇之前，為資料集提供唯一且易於識別的名稱和說明 **[!UICONTROL 完成]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

此時將顯示新建立的資料集的詳細資訊頁面。 如果資料集基於您的時間序列模式，則該過程將完成。 如果資料集基於您的記錄模式，則此過程中的最後一步是啟用資料集，以便在 [!DNL Real-Time Customer Profile]。

在右滑軌中，選擇 **[!UICONTROL 配置檔案]** 切換。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

最後，選擇 **[!UICONTROL 啟用]** 在確認跨距中，為 [!DNL Profile]。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

資料集現在已保存並啟用，以供使用 [!DNL Profile]。 如果您計畫使用平台Web SDK向配置檔案發送同意資料，則必須選擇此資料集作為 [!UICONTROL 配置檔案資料集] 設定 [資料流](../../../../edge/datastreams/overview.md)。

## 後續步驟

通過學完本教程，您已將同意欄位添加到 [!DNL Profile]-enabled架構，其資料集將用於使用平台Web SDK或直接XDM接收來接收同意資料。

您現在可以返回 [同意處理概述](./overview.md#merge-policies) 繼續配置Experience Platform以處理同意資料。

## 附錄

以下部分包含有關建立資料集以接收客戶同意和首選項資料的其他資訊。

### 將自定義同意和首選項欄位添加到架構 {#custom-consent}

如果您需要捕獲標準所表示的之外的其他同意信號 [!UICONTROL 同意和首選項詳細資訊] 欄位組，您可以使用自定義XDM元件來增強您的同意模式，以滿足您的特定業務需要。 本節概述了如何自定義同意架構以便將這些信號輸入配置檔案的基本原則。

>[!IMPORTANT]
>
>平台Web和移動SDK不支援其concense-change命令中的自定義欄位。 當前將自定義同意欄位納入配置檔案的唯一方法是 [批處理](../../../../ingestion/batch-ingestion/overview.md) 或 [源連接](../../../../sources/home.md)。

強烈建議您使用 [!UICONTROL 同意和首選項詳細資訊] 欄位組作為同意資料結構的基線，並根據需要添加其他欄位，而不是嘗試從頭建立整個結構。

要將自定義欄位添加到標準欄位組的結構中，必須首先建立自定義欄位組。 添加 [!UICONTROL 同意和首選項詳細資訊] 欄位組到架構，選擇 **加(+)** 的 **[!UICONTROL 欄位組]** ，然後選擇 **[!UICONTROL 建立新欄位組]**。 為欄位組提供名稱和可選說明，然後選擇 **[!UICONTROL 添加欄位組]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

的 [!DNL Schema Editor] 在左滑軌中選定新的自定義欄位組後，重新顯示。 在畫布中，將顯示允許您向架構結構添加自定義欄位的控制項。 要添加新的同意或首選項欄位，請選擇 **加(+)** 表徵圖 `consents` 的雙曲餘切值。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

在 `consents` 的雙曲餘切值。 由於您正在向標準XDM對象添加自定義欄位，因此新欄位是在與租戶ID同名的對象下建立的。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

在右欄下 **[!UICONTROL 欄位屬性]**，提供欄位的名稱和說明。 選擇欄位時 **[!UICONTROL 類型]**，您必須為自定義同意或首選項欄位使用相應的標準資料類型：

* [[!UICONTROL 通用同意欄位]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL 一般市場營銷首選項欄位]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL 具有訂閱的一般市場營銷首選項欄位]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL 通用個性化首選項欄位]](../../../../xdm/data-types/personalization-field.md)

完成後，選擇 **[!UICONTROL 應用]**。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

同意或首選項欄位被添加到架構結構中。 請注意 [!UICONTROL 路徑] 顯示在右滑軌中的 `_tenantId` 命名空間。 無論何時在資料操作中引用此欄位的路徑，都必須包括此命名空間。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

按照上述步驟繼續添加所需的同意和首選項欄位。 完成後，選擇 **[!UICONTROL 保存]** 確認更改。

如果尚未為此架構建立資料集，請繼續上的部分 [建立資料集](#dataset)。
