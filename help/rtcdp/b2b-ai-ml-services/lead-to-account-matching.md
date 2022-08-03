---
title: 在即時CDP B2B中導致帳戶匹配
type: Documentation
description: Experience PlatformCDP B2B中有關線索到帳戶匹配功能的概述和詳細資訊。
source-git-commit: 827bd1b930478c3c0b553a9485f98545771a9062
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 在即時CDP B2B中導致帳戶匹配

## 總覽 {#overview}

基於客戶的營銷是B2B營銷中越來越重要的策略。 基於客戶的營銷為收購特定的高價值客戶提供了以下主要好處：

- 清除ROI
- 銷售和市場營銷協調
- 個性化方法
- 減少浪費的資源
- 更短的銷售週期

基於帳戶的營銷提供了將已知人員和匿名Web訪問者連結到銷售帳戶的功能。 這使營銷團隊能夠在客戶旅程的早期與目標客戶的潛在銷售線索接洽，以增加他們轉換的機會。 已知人員記錄通常包括以下部分或全部資訊：

- 人員姓名
- 電子郵件地址
- 聯繫人號碼
- 公司名稱
- 公司網站
- 職務
- 位置

「線索至帳戶」匹配使您能夠將已知人員配置檔案加入帳戶配置檔案。 然後，您可以在B2B上下文中對資料進行分段和目標資料，如帳戶、機會等。 人員配置檔案可分為以下三類：

- **帳戶人員配置檔案：** 通過來自資料源的關係，人員簡檔已經與至少一個帳戶簡檔相關聯。 這意味著至少存在一個接觸碎片。

>[!NOTE]
>
> 在運行與帳戶匹配作業的銷售線索時，帳戶人員配置檔案不匹配。

- **已知人員配置檔案：** 人員配置檔案未與任何帳戶配置檔案關聯，並且以下人員配置檔案屬性中至少有一個具有值：

   - 電子郵件地址
   - 公司名稱
   - 公司網站

- **匿名個人資料：** 人員配置檔案未與任何帳戶配置檔案關聯，並且以下人員配置檔案屬性中沒有一個值：

   - 電子郵件地址
   - 公司名稱
   - 公司網站

>[!NOTE]
>
> 個人簡檔可以與多個帳戶簡檔相關。 但是，從銷售線索到帳戶的匹配過程將僅與最佳匹配匹配匹配。 如果需要更廣的匹配項集，請將銷售線索與相關帳戶功能相匹配。

## 運作方式 {#how-it-works}

日常運行的作業使用確定性因素和概率因素來匹配已知的銷售線索配置檔案，而不存在現有帳戶關聯。 已知銷售線索配置檔案將具有以下屬性之一：

- b2b.companyName
- b2b.companyWebsite
- 工作電子郵件

>[!NOTE]
>
> b2b.personKey.sourceKey屬性必須存在。

b2b.companyName、b2b.companyWeb站點和b2b.personKey.sourceKey屬性可以位於B2B人員架構的b2b欄位組中。

![顯示屬性的B2B人員架構](/help/rtcdp/accounts/images/b2b-person-schema.png)

在B2B人員架構中，可以將workEmail屬性作為頂級欄位組找到。

![顯示workEmail的B2B人員架構](/help/rtcdp/accounts/images/b2b-person-workemail.png)

僅當匹配分數超過內部置信度閾值時，配置檔案才會最佳匹配。 結果被保存在現有帳戶人關係XDM的新系統資料集中。

當新人員配置檔案快照可用時（每24小時一次），將運行線索至帳戶匹配服務。 有關 [銷售線索到帳戶匹配的配置](/help/rtcdp/accounts/account-profile-ui-guide.md)。

## 如何查看與帳戶匹配的輸出 {#how-to-view}

作業運行後，結果被保存在現有帳戶人關係XDM的新資料集中。

要預覽資料集，請選擇 **[!UICONTROL 預覽資料集]** 右上角。

![新資料集](/help/rtcdp/accounts/images/b2b-dataset-output.png)

資料集包括匹配的帳戶資訊以及所選資料集的匹配分數。 的 **[!UICONTROL 關係源]** 欄位指示它是否來自銷售線索到帳戶匹配流程。

![預覽資料集置信度分數和輸出](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## 監視潛在客戶到帳戶匹配作業 {#monitoring-jobs}

您可以通過控制面板監視任何與帳戶匹配的作業的線索的作業狀態和關聯度量。

有關 [監視潛在顧客的作業以及帳戶匹配](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)。
