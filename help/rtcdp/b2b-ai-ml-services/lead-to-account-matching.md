---
title: Real-Time CDP B2B中的銷售線索與帳戶相符
type: Documentation
description: 有關Experience PlatformCDP B2B中潛在客戶與帳戶比對功能的概述和詳細資訊。
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/tw/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 4ba609e777716b1b38f5b143587e5476d851e344
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---

# Real-Time CDP B2B中的銷售線索與帳戶相符

## 概觀 {#overview}

帳戶式行銷是B2B行銷日益重要的策略。 以帳戶為基礎的行銷提供下列主要優點，可贏取特定的高價值客戶：

- 清除ROI
- 銷售與行銷協調
- 個人化方法
- 減少浪費的資源
- 較短的銷售週期

帳戶型行銷提供將已知客戶連結至銷售帳戶的功能。 這可讓行銷團隊在客戶歷程的早期，與目標客戶的潛在客戶互動，以提高其轉換機會。 已知人員記錄通常包括下列部分或全部資訊：

- 個人名稱
- 電子郵件地址
- 聯絡電話
- 公司名稱
- 公司網站
- 職稱
- 位置

## 運作方式 {#how-it-works}

每日執行的工作會同時使用確定性和機率因素，來比對已知的潛在客戶設定檔，而不需建立現有的帳戶關聯。 已知潛在客戶設定檔將具有下列其中一個可用屬性：

- b2b.companyName
- b2b.companyWebsite
- 工作電子郵件

>[!NOTE]
>
> b2b.personKey.sourceKey屬性必須存在。

b2b.companyName、b2b.companyWebsite和b2b.personKey.sourceKey屬性可位於B2B人員結構描述的b2b欄位群組中。

![B2B人員結構描述顯示屬性](/help/rtcdp/accounts/images/b2b-person-schema.png)

workEmail屬性可作為B2B人員結構描述中的頂層欄位群組找到。

顯示workEmail![&#128279;](/help/rtcdp/accounts/images/b2b-person-workemail.png)的B2B人員結構描述

只有在符合分數超過內部信賴臨界值時，才會最符合設定檔。 結果會儲存在現有帳戶個人關係XDM的新系統資料集中。

當新的人員設定檔快照可供使用時（每24小時執行一次），帳戶比對服務的銷售機會就會執行。 請參閱檔案，以取得有關潛在客戶的[設定與帳戶相符](/help/rtcdp/accounts/account-profile-ui-guide.md)的詳細資訊。

## 如何檢視銷售線索與帳戶的比對輸出 {#how-to-view}

工作執行後，結果會儲存在現有帳戶個人關係XDM的新資料集中。

若要預覽資料集，請選取右上角的&#x200B;**[!UICONTROL 預覽資料集]**。

![新資料集](/help/rtcdp/accounts/images/b2b-dataset-output.png)

資料集包含相符的帳戶資訊，以及您所選資料集的相符分數。 **[!UICONTROL 關聯性Source]**&#x200B;欄位指出它是否來自銷售機會與帳戶比對程式。

![預覽資料集信賴分數和輸出](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## 監控銷售線索與帳戶比對工作 {#monitoring-jobs}

您可以透過控制面板監控任何銷售線索與帳戶比對工作的工作狀態和相關測量結果。

請參閱檔案以取得有關潛在客戶與帳戶相符[&#128279;](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)的監視工作的詳細資訊。
