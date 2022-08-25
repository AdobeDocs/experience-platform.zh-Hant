---
keywords: Experience Platform；入門；屬性；熱門主題
feature: Attribution AI
title: 入門Attribution AI
topic-legacy: Getting started
description: 以下指南要求瞭解Adobe Experience Platform與使用Attribution AI有關的各種服務。 在開始教程之前，請查看以下文檔。
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: 9ce5a383bed24c4bfe9245521149443a57764da5
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Attribution AI入門

以下指南要求瞭解 [!DNL Adobe Experience Platform] 與使用Attribution AI相關的服務。 在開始教程之前，請查看以下文檔：

- [體驗資料模型(XDM)系統概述](../../xdm/home.md):XDM是一個基礎框架，它允許 [!DNL Adobe Experience Cloud]在Experience Platform的支援下，在正確的時刻，在正確的頻道向正確的人傳遞正確的資訊。 構建Experience Platform的方法體系XDM系統可操作經驗資料模型模式供平台服務使用。
- [架構組合的基礎](../../xdm/schema/composition.md):本文檔介紹了經驗資料模型(XDM)架構，以及組合要用於的架構的構造塊、原則和最佳做法 [!DNL Adobe Experience Platform]。
- [生成架構](../../xdm/tutorials/create-schema-ui.md):本教程介紹了在Experience Platform中使用架構編輯器建立架構的步驟。

Attribution AI需要資料集以符合消費者體驗事件(CEE)架構，該架構是 [體驗資料模型(XDM)](../../xdm/home.md) 架構欄位組。 請通過attributionai-support@adobe.com與Adobe支援部門聯繫，以實施或更改此資料。 如果存在介質支出資料，您可以進一步分析，如增量收入和ROI。 如果客戶配置檔案資料可用，您可以進一步將貸項屬性至客戶配置檔案層。

## 術語

- **轉換事件：** 客戶為指示目標（如會議註冊）的里程碑而做的任何數字事件或數字交互。 其他示例包括付費轉換、免費帳戶註冊或特徵合格。

- **觸點：** 客戶在實現目標的過程中所做的任何數字事件或數字交互。 示例包括與購買前相關的營銷工作、顯示已查看的廣告印象以及付費搜索點擊。

## 下載Attribution AI分數

>[!NOTE]
>
>如果不需要下載原始分數，可跳過此步驟並繼續 [後續步驟](#next-steps)。

通過API調用的組合來下載Attribution AI分數。 要調用平台API，必須先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成Experience Platform教程將提供所有驗證API調用中每個必需標頭的值，如下所示：

- 授權：持 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的所有資源都與特定的虛擬沙箱隔離。 所有對平台API的請求都需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關平台中沙箱的詳細資訊，請參閱 [沙盒概述文檔](../../sandboxes/home.md)。

### 讀取示例API調用

本指南提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md) Experience Platform疑難解答指南。

## ## GDPR和加密 {#gdpr-and-encryption}

使用基於角色的訪問控制時， **查看Attribution AI** 和 **管理Attribution AI** 權限授予對不同功能的Attribution AI訪問權限。 的 **管理Attribution AI** 讓 **建立**。 **克隆**。 **編輯**。 **刪除**。 **啟用**&#x200B;或 **禁用** 在 **查看Attribution AI** 讓 **讀** 或 **視圖** 它。 的 **建立**。 **編輯** 和 **刪除** 操作由審核日誌記錄。

請參閱要瞭解的文檔 [分配訪問控制權限](../../../help/access-control/home.md) 或如何 [使用審核日誌來監視訪問和活動](../../../help/landing/governance-privacy-security/audit-logs/overview.md)。

## 後續步驟 {#next-steps}

準備好並準備好所有憑據和架構後，請按照 [Attribution AI用戶介面指南](./user-guide.md)。 本指南指導您建立實例並提交它以進行培訓和評分。
