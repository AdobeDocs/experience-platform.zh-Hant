---
title: 在Real-Time CDP B2B中導致帳戶比對
type: Documentation
description: Experience PlatformCDP B2B中帳戶比對功能的概述和詳細資訊。
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 2%

---

# 在Real-Time CDP B2B中導致帳戶比對

## 總覽 {#overview}

帳戶型行銷是B2B行銷的一項日益重要的策略。 以帳戶為基礎的行銷為贏取特定高價值客戶提供下列主要優勢：

- 清除ROI
- 銷售與行銷協調
- 個人化方法
- 減少浪費的資源
- 更短的銷售週期

帳戶型行銷提供將已知人員和匿名網站訪客連結至銷售帳戶的功能。 這可讓行銷團隊在客戶歷程早期與目標帳戶的潛在銷售機會互動，以增加其轉換機會。 已知人員記錄通常包括以下部分或全部資訊：

- 人員名稱
- 電子郵件地址
- 聯繫電話
- 公司名稱
- 公司網站
- 職務
- 位置

帳戶比對的潛在客戶可讓您將已知的人員設定檔加入帳戶設定檔。 然後，您就可以在B2B內容（如帳戶、機會等）中劃分和定位資料。 人員設定檔可分為下列三個類別：

- **帳戶人員配置檔案：** 人員配置檔案已通過來自資料源的關係與至少一個帳戶配置檔案相關聯。 這表示至少存在一個聯繫片段。

>[!NOTE]
>
> 當運行銷售機會導致帳戶匹配作業時，帳戶人員配置檔案不匹配。

- **已知人員配置檔案：** 人員配置檔案「不」與任何帳戶配置檔案相關聯，並且以下人員配置檔案屬性中的至少一個具有值：

   - 電子郵件地址
   - 公司名稱
   - 公司網站

- **匿名人員配置檔案：** 人員配置檔案「不」與任何帳戶配置檔案相關聯，並且以下人員配置檔案屬性中沒有任何一個具有值：

   - 電子郵件地址
   - 公司名稱
   - 公司網站

>[!NOTE]
>
> 人員配置檔案可能與多個帳戶配置檔案相關。 但是，帳戶匹配流程只會符合最佳匹配。 如果需要更廣泛的符合集，請將銷售機會與相關帳戶功能配對。

## 運作方式 {#how-it-works}

每日執行的工作會同時使用決定性和可能性因素，來比對已知的潛在客戶設定檔，而不會與現有帳戶產生關聯。 已知的銷售機會設定檔將具有下列其中一個可用屬性：

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> b2b.personKey.sourceKey屬性必須存在。

b2b.companyName、b2b.companyWebsite和b2b.personKey.sourceKey屬性可位於B2B人員結構的b2b欄位群組中。

![顯示屬性的B2B人員結構](/help/rtcdp/accounts/images/b2b-person-schema.png)

在B2B人員架構中，可以將workEmail屬性作為頂層欄位組找到。

![顯示workEmail的B2B人員結構](/help/rtcdp/accounts/images/b2b-person-workemail.png)

只有在符合分數超過內部信賴臨界值時，設定檔才會獲得最佳比對。 結果會儲存在現有帳戶人員關係XDM的新系統資料集中。

當新的人員配置檔案快照可用時（每24小時一次），將運行帳戶匹配服務。 如需 [銷售機會到帳戶匹配的配置](/help/rtcdp/accounts/account-profile-ui-guide.md).

## 如何檢視銷售機會以取得帳戶比對輸出 {#how-to-view}

作業執行後，結果會儲存在現有帳戶人員關係XDM的新資料集中。

若要預覽資料集，請選取 **[!UICONTROL 預覽資料集]** 在右上角。

![新資料集](/help/rtcdp/accounts/images/b2b-dataset-output.png)

資料集包含相符的帳戶資訊，以及所選資料集的相符分數。 此 **[!UICONTROL 關係源]** 欄位會指出其是否來自銷售機會帳戶比對程式。

![預覽資料集可信度分數和輸出](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## 監控銷售機會導致帳戶匹配作業 {#monitoring-jobs}

您可以透過控制面板，監控任何銷售機會的作業狀態和相關量度，以找出帳戶相符作業。

如需 [監控銷售機會帳戶比對的作業](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
