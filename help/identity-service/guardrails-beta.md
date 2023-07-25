---
title: Identity Service的護欄（含刪除邏輯）
description: 瞭解Identity Service的護欄。
hide: true
hidefromtoc: true
source-git-commit: db8edbbc3ea5d8fcec3de95b9a37387bea493693
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 2%

---

# 護欄 [!DNL Identity Service] 資料（含刪除邏輯）

本檔案提供以下專案的使用與速率限制相關資訊： [!DNL Identity Service] 資料可協助您最佳化身分圖表的使用方式。 檢閱下列護欄時，系統假設您已正確地模型化資料。 如果您有任何關於如何模型化資料的問題，請聯絡您的客戶服務代表。

## 快速入門

下列Experience Platform服務與模型化身分資料有關：

* [身分](home.md)：橋接擷取到Platform中的不同資料來源身分。
* [[!DNL Real-Time Customer Profile]](../profile/home.md)：使用來自多個來源的資料建立統一的消費者設定檔。

## 資料模型限制

下表提供有關靜態限制的護欄指南，以及要考慮用於身分名稱空間的驗證規則。

### 靜態限制

下表概述套用至身分資料的靜態限制。

| 護欄 | 限制 | 附註 |
| --- | --- | --- |
| 圖表中的身分數量 [!BADGE 測試版]{type=Informative} | 50 | 更新具有50個連結身分的圖形時，Identity Service將套用「先進先出」機制，並刪除最舊的身分，為最新的身分騰出空間。 刪除是根據身分型別和時間戳記。 此限制會套用至沙箱層級。 閱讀 [附錄](#appendix) 如需詳細資訊，瞭解在達到上限後Identity服務如何刪除身分。 |
| XDM記錄中的身分數量 | 20 | 需要的XDM記錄數量下限為2。 |
| 自訂名稱空間數量 | None | 您可以建立的自訂名稱空間數量沒有限制。 |
| 圖表數量 | None | 您可以建立的身分圖表數量沒有限制。 |
| 名稱空間顯示名稱或身分符號的字元數 | None | 名稱空間顯示名稱或身分符號的字元數沒有限制。 |

### 身分值驗證

下表概述您必須遵循的現有規則，以確保身分值成功驗證。

| 命名空間 | 驗證規則 | 違反規則時的系統行為 |
| --- | --- | --- |
| ECID | <ul><li>ECID的身分值必須剛好38個字元。</li><li>ECID的身分值必須僅由數字組成。</li></ul> | <ul><li>如果ECID的身分值不完全是38個字元，則會略過記錄。</li><li>如果ECID的身分值包含非數字字元，則會略過記錄。</li></ul> |
| 非ECID | 身分值不可超過1024個字元。 | 如果身分值超過1024個字元，則會略過記錄。 |

### 身分名稱空間擷取

自2023年3月31日起，Identity Service將封鎖新客戶的Adobe Analytics ID (AAID)擷取。 此身分通常透過 [Adobe Analytics來源](../sources/connectors/adobe-applications/analytics.md) 和 [Adobe Audience Manager來源](../sources//connectors/adobe-applications/audience-manager.md) 和是多餘的，因為ECID代表相同的網頁瀏覽器。 如果您想要變更此預設設定，請聯絡您的Adobe客戶團隊。

## 後續步驟

請參閱以下檔案以瞭解更多有關 [!DNL Identity Service]：

* [[!DNL Identity Service] 概覽](home.md)
* [身分圖表檢視器](ui/identity-graph-viewer.md)

## 附錄 {#appendix}

下節包含有關Identity Service護欄的其他資訊。

### [!BADGE 測試版]{type=Informational}瞭解當容量中的身分圖表更新時的刪除邏輯 {#deletion-logic}

更新完整的身分圖表時，Identity Service會先刪除圖表中最舊的身分，然後再新增最新的身分。 這是為了維持身分資料的正確性和關聯性。 此刪除程式會遵循兩個主要規則：

#### 刪除規則#1會根據名稱空間的身分型別來排定優先順序

刪除優先順序如下：

1. Cookie ID
2. 裝置ID
3. 跨裝置ID、電子郵件和電話

#### 刪除規則#2根據儲存在身分上的時間戳記

圖表中所連結的每個身分都有各自的對應時間戳記。 更新完整圖表時，Identity Service會刪除具有最舊時間戳記的身分。

當完整圖表更新為新身分時，這兩個規則會協同工作，指定將刪除哪個舊身分。 Identity Service會先刪除最舊的Cookie ID，接著刪除最舊的裝置ID，最後刪除最舊的跨裝置ID/電子郵件/電話。

>[!NOTE]
>
>如果要刪除的身分已連結到圖表中的多個其他身分，則連線該身分的連結也會被刪除。

在下列範例中，在以新身分更新左側的圖形之前，Identity Service必須先刪除具有最舊時間戳記的現有身分。 但是，由於最舊的身分識別是裝置ID，Identity Service會略過該身分識別，直到它到達刪除優先順序清單中型別較高的名稱空間(在此例中為 `ecid-3`. 一旦移除具有更高刪除優先順序型別的最舊身分識別，圖表就會更新為新連結。 `ecid-51`.

>[!NOTE]
>
>在極少數兩個身分具有相同時間戳記和身分型別的情況下，Identity Service會根據XID排序ID並進行刪除。

![刪除最舊身分以容納最新身分的範例](./images/graph-limits-v3.png)