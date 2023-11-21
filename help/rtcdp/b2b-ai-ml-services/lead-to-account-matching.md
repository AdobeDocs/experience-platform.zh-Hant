---
title: Real-Time CDP B2B中的銷售線索與帳戶相符
type: Documentation
description: 有關Experience PlatformCDP B2B中潛在客戶與帳戶比對功能的概述和詳細資訊。
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 2%

---

# Real-Time CDP B2B中的銷售線索與帳戶相符

## 概觀 {#overview}

帳戶式行銷是B2B行銷日益重要的策略。 以帳戶為基礎的行銷提供下列主要優點，可贏取特定的高價值客戶：

- 清除ROI
- 銷售與行銷協調
- 個人化方法
- 減少浪費的資源
- 較短的銷售週期

帳戶型行銷可將已知人員和匿名網路訪客連結至銷售帳戶。 這可讓行銷團隊在客戶歷程的早期，與目標客戶的潛在客戶互動，以提高其轉換機會。 已知人員記錄通常包括下列部分或全部資訊：

- 個人名稱
- 電子郵件地址
- 聯絡電話
- 公司名稱
- 公司網站
- 職稱
- 位置

銷售機會帳戶比對可讓您將已知人員設定檔聯結到帳戶設定檔。 然後，您可以在B2B內容（例如帳戶、商機等）中細分及鎖定資料。 個人資料可分類為下列三個類別：

- **帳戶個人設定檔：** 此人員設定檔已透過來自資料來源的關係，與至少一個帳戶設定檔建立關聯。 這表示至少有一個連絡人片段。

>[!NOTE]
>
> 執行銷售線索與帳戶比對工作時，帳戶個人設定檔不相符。

- **已知人員設定檔：** 此人員設定檔未關聯至任何帳戶設定檔，且下列人員設定檔屬性中至少有一個具有值：

   - 電子郵件地址
   - 公司名稱
   - 公司網站

- **匿名人員設定檔：** 此人員設定檔未關聯至任何帳戶設定檔，且下列人員設定檔屬性都沒有值：

   - 電子郵件地址
   - 公司名稱
   - 公司網站

>[!NOTE]
>
> 個人設定檔可能與多個帳戶設定檔相關。 但是，銷售線索與帳戶的比對程式只會比對到最佳比對。 如果需要更廣的相符集合，請將銷售機會連結到與相關帳戶功能相符的帳戶。

## 運作方式 {#how-it-works}

每日執行的工作會同時使用確定性和機率因素，來比對已知的潛在客戶設定檔，而不需建立現有的帳戶關聯。 已知潛在客戶設定檔將具有下列其中一個可用屬性：

- b2b.companyName
- b2b.companyWebsite
- 工作電子郵件

>[!NOTE]
>
> b2b.personKey.sourceKey屬性必須存在。

b2b.companyName、b2b.companyWebsite和b2b.personKey.sourceKey屬性可位於B2B人員結構描述的b2b欄位群組中。

![顯示屬性的B2B個人結構描述](/help/rtcdp/accounts/images/b2b-person-schema.png)

workEmail屬性可作為B2B人員結構描述中的頂層欄位群組找到。

![顯示工作電子郵件的B2B個人結構描述](/help/rtcdp/accounts/images/b2b-person-workemail.png)

只有在符合分數超過內部信賴臨界值時，才會最符合設定檔。 結果會儲存在現有帳戶個人關係XDM的新系統資料集中。

當新的人員設定檔快照可供使用時（每24小時執行一次），帳戶比對服務的銷售機會就會執行。 請參閱檔案以瞭解更多關於 [銷售線索與帳戶的比對設定](/help/rtcdp/accounts/account-profile-ui-guide.md).

## 如何檢視銷售線索與帳戶的比對輸出 {#how-to-view}

工作執行後，結果會儲存在現有帳戶個人關係XDM的新資料集中。

若要預覽資料集，請選取 **[!UICONTROL 預覽資料集]** 右上角。

![新資料集](/help/rtcdp/accounts/images/b2b-dataset-output.png)

資料集包含相符的帳戶資訊，以及您所選資料集的相符分數。 此 **[!UICONTROL 關係來源]** 欄位會指出是否來自銷售線索與帳戶的比對程式。

![預覽資料集信賴分數和輸出](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## 監控銷售線索與帳戶比對工作 {#monitoring-jobs}

您可以透過控制面板監控任何銷售線索與帳戶比對工作的工作狀態和相關測量結果。

請參閱檔案以瞭解更多關於 [監控銷售線索與帳戶的比對工作](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
