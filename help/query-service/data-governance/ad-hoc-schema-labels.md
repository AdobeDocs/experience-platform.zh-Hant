---
title: 基於屬性的Ad Hoc模式訪問控制支援
description: 用於限制訪問通過Adobe Experience Platform查詢服務生成的臨時架構中的資料欄位的指南。
exl-id: d675e3de-ab62-4beb-9360-1f6090397a17
source-git-commit: 91f318596bf268aa93e8b2df9c13774aab76d13a
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 2%

---

# 基於屬性的訪問控制支援ad hoc模式

引入Adobe Experience Platform的任何資料都由經驗資料模型(XDM)架構封裝，並可能受組織或法律法規定義的使用限制的約束。

通過在未指定架構時通過查詢服務執行CTAS查詢，自動生成ad hoc架構。 通常需要限制特定架構的某些欄位或資料集的使用，以控制對敏感個人資料和個人身份資訊的訪問。 Adobe Experience Platform通過允許您使用基於屬性的訪問控制功能通過平台UI標籤架構欄位，從而方便了此訪問控制。

標籤可以隨時應用，在選擇管理資料的方式上提供了靈活性。 儘管如此，最好在資料被引入平台或資料在平台中可用時立即標籤它。

基於模式的標籤是基於屬性的訪問控制的重要組成部分，用於更好地管理對用戶或用戶組的訪問。 Adobe Experience Platform允許您通過建立和應用標籤來限制對臨時架構的任何欄位的訪問。

本文檔提供一個教程，用於通過將標籤應用於通過查詢服務生成的即席架構的資料欄位來管理對敏感資料的訪問。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [體驗資料模型(XDM)系統](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant):Experience Platform組織客戶體驗資料的標準化框架。
   * [[!DNL Schema Editor]](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=zh-Hant):瞭解如何在平台UI中建立和管理架構和其他資源。
* [[!DNL Data Governance]](../../data-governance/home.md):瞭解如何 [!DNL Data Governance] 允許您管理客戶資料並確保遵守適用於資料使用的法規、限制和策略。
* [基於屬性的訪問控制](../../access-control/abac/overview.md):基於屬性的訪問控制是Adobe Experience Platform的一種功能，它使管理員能夠基於屬性控制對特定對象和/或權能的訪問。 屬性可以是添加到對象的元資料，如添加到即席或常規模式欄位的標籤。 管理員定義包括屬性的訪問策略以管理用戶訪問權限。

## 建立即席架構

執行查詢並生成結果後，將自動生成即席模式並將其添加到模式清單。

要添加資料標籤，請導航至 [!UICONTROL 架構] 通過選擇 [!UICONTROL 架構] 在平台UI的左滑軌中。 將顯示架構清單。

>[!NOTE]
>
>預設情況下，在架構清單中不顯示即席架構。

## 在平台UI的架構清單中發現即席架構 {#discover-ad-hoc-schemas}

要在平台UI中啟用即席架構的顯示，請選擇篩選器表徵圖(![篩選器表徵圖。](../images/data-governance/filter.png))，然後選擇**[!UICONTROL 顯示即席架構] 左欄。

![啟用「顯示即席架構」切換的「架構」儀表板篩選器選項左側的欄。](../images/data-governance/adhoc-schema-toggle.png)

從可用清單中選擇最近建立的臨時架構的名稱。 此時將顯示即席模式結構的可視化。

![ad hoc架構結構圖示例。](../images/data-governance/adhoc-schema-structure-diagram.png)

## 編輯控管標籤

要編輯即席架構的資料標籤，請選擇 [!UICONTROL 標籤] 頁籤。 標籤工作區允許您將標籤應用、建立和編輯到您的即席架構欄位，並通過UI控制訪問權限。 此處表示即席架構中的所有欄位。

## 編輯架構或欄位的標籤

要編輯整個架構的標籤，請選擇鉛筆表徵圖(![鉛筆表徵圖。](../images/data-governance/edit-icon.png))到架構名稱的一側 [!UICONTROL 標籤] 頁籤。

![方案工作區中的標籤視圖，鉛筆表徵圖突出顯示。](../images/data-governance/edit-entire-schema-labels.png)

要將標籤應用於現有欄位，請從清單中選擇一個或多個欄位，後跟 [!UICONTROL 編輯治理標籤] 的下界。

![架構工作區中的標籤視圖，右側提要欄中突出顯示了「編輯治理標籤」選項。](../images/data-governance/edit-governance-labels.png)

## 編輯標籤沿面

的 [!UICONTROL 編輯標籤] 出現「popover（跨距）」。 通過此視圖，可以通過UI建立或編輯現有治理標籤。

![「編輯」(Edit)標籤沿面。](../images/data-governance/edit-labels-popover.png)

請參閱文檔，瞭解有關如何 [建立或編輯所選方案或欄位的標籤](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/labels.html#edit-the-labels-for-the-schema-or-field)。

>[!NOTE]
>
>建立新標籤或編輯現有標籤需要您組織的管理員權限。 如果您沒有管理員權限，請與系統管理員聯繫以安排訪問。

也可以使用權限工作區建立標籤。 查看 [有關在權限工作區中建立標籤的指南](../../access-control/abac/ui/labels.md) 的雙曲餘切值。

一旦應用了相應級別的基於屬性的訪問控制，則當用戶嘗試訪問不可訪問的資料時，以下系統行為將應用於通過查詢服務執行的任何查詢：

1. 如果用戶被拒絕訪問架構中的某個欄位，則用戶將無法讀取或寫入受限欄位。 這適用於以下常見方案：

   * 當用戶嘗試僅使用受限列執行查詢時，系統將引發一個列不存在的錯誤。
   * 當用戶嘗試執行包含限制列的多個列的查詢時，系統將僅返回所有非限制列的輸出。

1. 如果用戶請求訪問計算欄位，則用戶必須有權訪問合成中使用的所有欄位，否則系統將拒絕訪問計算欄位。

如果在即席模式上設定了標識或主標識，則系統將自動執行任何關聯的資料衛生請求並清除那些與標識列關聯的資料集中的資料。

## 後續步驟

閱讀此文檔後，您更瞭解如何將資料使用標籤添加到通過查詢服務CTAS查詢建立的即席架構。 如果尚未執行此操作，則以下文檔對於提高您對查詢服務中資料治理的瞭解非常有用：

* [即席架構標識](./ad-hoc-schema-identities.md)
* [資料治理](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)
