---
title: Ad Hoc結構的屬性型存取控制支援
description: 限制存取透過Adobe Experience Platform查詢服務產生之隨選結構之資料欄位的指南。
exl-id: d675e3de-ab62-4beb-9360-1f6090397a17
source-git-commit: 91f318596bf268aa93e8b2df9c13774aab76d13a
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 1%

---

# 臨機結構的基於屬性的訪問控制支援

匯入Adobe Experience Platform的任何資料都會以Experience Data Model(XDM)結構封裝，且可能受到貴組織所定義或法律規範的使用限制所限制。

當未指定架構時，通過查詢服務執行CTAS查詢，自動生成臨機架構。 通常需要限制臨機結構的特定欄位或資料集的使用，以控制對敏感個人資料和個人識別資訊的存取。 Adobe Experience Platform可讓您使用屬性型存取控制功能，透過Platform UI標示架構欄位，以方便進行存取控制。

標籤可隨時套用，提供您選擇控管資料的彈性。 不過，最佳實務是在資料內嵌至Platform時立即加上標籤，或是當資料可供Platform使用時立即加上標籤。

基於方案的標籤是基於屬性的訪問控制的重要組成部分，以更好地管理分配給用戶或用戶組的訪問。 Adobe Experience Platform可讓您建立和套用標籤，以限制對臨機結構的任何欄位的存取。

本檔案提供教學課程，透過將標籤套用至透過Query Service產生的臨機結構的資料欄位，以管理對敏感資料的存取。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [Experience Data Model(XDM)系統](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant):Experience Platform組織客戶體驗資料的標準化架構。
   * [[!DNL Schema Editor]](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html):了解如何在Platform UI中建立和管理結構和其他資源。
* [[!DNL Data Governance]](../../data-governance/home.md):了解如何 [!DNL Data Governance] 可讓您管理客戶資料，並確保符合適用於資料使用的法規、限制和政策。
* [基於屬性的訪問控制](../../access-control/abac/overview.md):基於屬性的存取控制是Adobe Experience Platform的一項功能，可讓管理員根據屬性控制對特定物件和/或功能的存取。 屬性可以是新增至物件的中繼資料，例如新增至臨機或一般結構欄位的標籤。 管理員定義了包括屬性的訪問策略以管理用戶訪問權限。

## 建立隨選結構

執行查詢並產生結果後，就會自動產生隨選結構並新增至結構清單。

若要新增資料標籤，請導覽至 [!UICONTROL 結構] 選擇 [!UICONTROL 結構] 在Platform UI的左側邊欄中。 系統會顯示結構清單。

>[!NOTE]
>
>預設情況下，臨機結構不會顯示在結構清單中。

## 在Platform UI的結構清單中探索隨選結構 {#discover-ad-hoc-schemas}

若要在Platform UI中啟用臨機結構的顯示，請選取篩選圖示(![篩選圖示。](../images/data-governance/filter.png))，然後選取**[!UICONTROL 顯示隨選結構] 在左側邊欄中。

![「結構控制面板」篩選選項在左側邊欄中切換為啟用「顯示隨選結構」。](../images/data-governance/adhoc-schema-toggle.png)

從可用清單中選取最近建立的臨機架構的名稱。 隨即顯示臨機結構的視覺效果。

![臨機架構結構圖範例。](../images/data-governance/adhoc-schema-structure-diagram.png)

## 編輯控管標籤

若要編輯臨機結構的資料標籤，請選取 [!UICONTROL 標籤] 標籤。 標籤工作區可讓您將標籤套用、建立和編輯至您的臨機結構欄位，並透過UI控制存取權限。 此處顯示臨機架構內的所有欄位。

## 編輯架構或欄位的標籤

若要編輯整個架構的標籤，請選取鉛筆圖示(![鉛筆圖示。](../images/data-governance/edit-icon.png))，並排到 [!UICONTROL 標籤] 標籤。

![標籤檢視在結構工作區中，會以鉛筆圖示醒目顯示。](../images/data-governance/edit-entire-schema-labels.png)

要將標籤應用於現有欄位，請從清單中選擇一個或多個欄位，後跟 [!UICONTROL 編輯控管標籤] 在右邊欄。

![標籤在結構工作區中的檢視，右側邊欄中強調顯示「編輯控管標籤」選項。](../images/data-governance/edit-governance-labels.png)

## 編輯標籤彈出窗口

此 [!UICONTROL 編輯標籤] 彈出視窗隨即出現。 從此檢視，您可以透過UI建立或編輯現有的控管標籤。

![「編輯標籤」彈出視窗。](../images/data-governance/edit-labels-popover.png)

如需如何進行的指引，請參閱本檔案 [為所選架構或欄位建立或編輯標籤](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/labels.html#edit-the-labels-for-the-schema-or-field).

>[!NOTE]
>
>建立新標籤或編輯現有標籤需要貴組織的管理員權限。 如果您沒有管理員權限，請與系統管理員聯繫以安排訪問。

您也可以使用權限工作區來建立標籤。 請參閱 [在權限工作區中建立標籤的指南](../../access-control/abac/ui/labels.md) 的說明。

在應用了適當的基於屬性的訪問控制級別後，當用戶嘗試訪問不可訪問的資料時，以下系統行為將應用於通過查詢服務執行的任何查詢：

1. 如果用戶被拒絕訪問架構內的其中一個欄位，則用戶將無法在受限欄位上讀取或寫入。 這適用於下列常見案例：

   * 當用戶嘗試只執行受限列的查詢時，系統將引發該列不存在的錯誤。
   * 當用戶嘗試執行包含多個列（包括受限列）的查詢時，系統將僅返回所有非受限列的輸出。

1. 如果用戶請求訪問計算欄位，則用戶必須擁有對合成中使用的所有欄位的訪問權限，否則系統將拒絕對計算欄位的訪問。

如果在臨機結構上設定了身分或主要身分，系統會自動執行任何相關的資料衛生請求，並清除與身分欄系結的資料集中的資料。

## 後續步驟

閱讀本檔案後，您更了解如何將資料使用量標籤新增至透過Query Service CTAS查詢建立的臨機結構。 如果您尚未這麼做，下列檔案有助於您進一步了解Query Service中的資料控管：

* [臨機結構識別](./ad-hoc-schema-identities.md)
* [資料控管](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)
