---
keywords: Experience Platform；身分；身分服務；疑難排解；護欄；指引；限制；
title: Identity Service的護欄
description: 本檔案提供Identity Service資料的使用與速率限制相關資訊，協助您最佳化身分圖表的使用方式。
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: 2f226ae1356733b89b10e73ef1a371c42da05295
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 1%

---

# 護欄 [!DNL Identity Service] 資料

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
| （目前行為）圖表中的身分數量 | 150 | 此限制會套用至沙箱層級。 當身分數量達到150個或更多時，不會新增任何身分，且不會更新身分圖表。 由於連結了一或多個具有少於150個身分的圖表，圖表可能會顯示大於150個身分。 **注意**：身分圖表中的身分數量上限 **適用於個別合併的設定檔** 為50。 根據具有超過50個身分的身分圖表合併的設定檔會從即時客戶設定檔中排除。 如需詳細資訊，請閱讀以下指南： [設定檔資料的護欄](../profile/guardrails.md). |
| （近期行為）圖表中的身分數量 [!BADGE 測試版]{type=Informative} | 50 | 更新具有50個連結身分的圖形時，Identity Service將套用「先進先出」機制，並刪除最舊的身分，為最新的身分騰出空間。 刪除是根據身分型別和時間戳記。 此限制會套用至沙箱層級。 閱讀 [附錄](#appendix) 如需詳細資訊，瞭解在達到上限後Identity服務如何刪除身分。 |
| XDM記錄中的身分數量 | 20 | 需要的XDM記錄數量下限為2。 |
| 自訂名稱空間數量 | None | 您可以建立的自訂名稱空間數量沒有限制。 |
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

>[!IMPORTANT]
>
>以下刪除邏輯是Identity Service即將推出的行為。 如果您的生產沙箱包含：
>
> * 將人員識別碼（例如CRM ID）設定為Cookie/裝置身分型別的自訂名稱空間。
> * 將Cookie/裝置識別碼設定為跨裝置識別型別的自訂名稱空間。


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

>[!BEGINSHADEBOX]

**刪除邏輯的視覺化表示法**

![刪除最舊身分以容納最新身分的範例](./images/graph-limits-v3.png)

*圖表附註：*

* `t` = 時間戳記.
* 時間戳記的值對應至指定身分的造訪間隔。 例如， `t1` 代表第一個連結的身分（最舊）和 `t51` 將代表最新的連結身分。

在此範例中，Identity Service會先刪除具有最舊時間戳記的現有身分，之後才能使用新身分更新左側的圖形。 但是，由於最舊的身分識別是裝置ID，Identity Service會略過該身分識別，直到它到達刪除優先順序清單中型別較高的名稱空間(在此例中為 `ecid-3`. 一旦移除具有更高刪除優先順序型別的最舊身分識別，圖表就會更新為新連結。 `ecid-51`.

* 在極少數情況下，會有兩個具有相同時間戳記和身分型別的身分，Identity Service會根據此ID排序 [XID](./api/list-native-id.md) 並執行刪除。

>[!ENDSHADEBOX]