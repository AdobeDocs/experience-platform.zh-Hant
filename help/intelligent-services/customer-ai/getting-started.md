---
keywords: Experience Platform；入門；客戶ai；熱門主題
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 客戶AI入門
topic-legacy: Getting started
description: 本指南提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: b3c331821e2df17380edbc673066f6b10a06d65f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 客戶AI入門

客戶AI指南要求對使用客戶AI所涉及的各種平台服務有良好的理解。 開始之前，請查看以下文檔：

- [體驗資料模型(XDM)系統概述](../../xdm/home.md):XDM是一個基礎框架，它允許 [!DNL Adobe Experience Cloud]在Experience Platform的支援下，在正確的時刻，在正確的頻道向正確的人傳遞正確的資訊。 構建Experience Platform的方法體系XDM系統可操作經驗資料模型模式供平台服務使用。
- [架構組合的基礎](../../xdm/schema/composition.md):本文檔介紹了經驗資料模型(XDM)架構，以及組合要用於的架構的構造塊、原則和最佳做法 [!DNL Adobe Experience Platform]。
- [生成架構](../../xdm/tutorials/create-schema-ui.md):本教程介紹了在Experience Platform中使用架構編輯器建立架構的步驟。
- [即時客戶概要資訊概述](../../rtcdp/overview.md):基於 [!DNL Adobe Experience Platform],Real-time Customer Data Platform（即時CDP）幫助公司將已知和未知資料匯集起來，通過在整個客戶過程中的智慧決策來激活客戶配置檔案。 即時CDP將多個企業資料源組合在一起，以即時建立統一的配置檔案，這些配置檔案可用於跨所有渠道和設備提供一對一的個性化客戶體驗。
- [分段服務概述](../../segmentation/home.md):細分是定義配置檔案子集與配置檔案儲存共用的特定屬性或行為的過程，以區分可銷售的人員組與客戶群。 例如，在一封名為「你忘記買運動鞋了嗎？」的電子郵件中，你可能希望看到過去30天內搜索跑鞋但沒有完成購買的所有用戶的觀眾。 使用不同的細分市場，您可以專注於不同的受眾，提供更為定製的營銷體驗。
- [段生成器使用手冊](../../segmentation/tutorials/create-a-segment.md):平台允許您輕鬆建立和訪問段，並使用不同的構建塊進一步表徵段。

## 下載客戶AI分數

>[!NOTE]
>
>如果不需要下載原始分數，可跳過此步驟並繼續 [配置指南](./user-guide/configure.md)。

通過API調用的組合來下載客戶AI分數。 要調用平台API，必須先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成Experience Platform教程將提供所有驗證API調用中每個必需標頭的值，如下所示：

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

## 權限

使用訪問控制時， **查看客戶AI** 和 **管理客戶AI** 權限授予對客戶AI的不同功能的訪問權限。 的 **管理客戶AI** 權限允許 **建立**。**更新**。 **刪除**。 **啟用**&#x200B;或 **禁用** 在 **查看客戶AI** 讓您閱讀或查看。 的 **建立**。 **更新** 和 **刪除** 操作由審核日誌記錄。

請參閱要瞭解的文檔 [分配訪問控制權限](../../../help/access-control/home.md) 或如何 [使用審核日誌來監視訪問和活動](../../../help/landing/governance-privacy-security/audit-logs/overview.md)。

## 後續步驟

完成上面文檔中概述的步驟後，請訪問 [輸入和輸出](./input-output.md) 文檔。 本文檔簡要概述了在客戶AI中使用和生成的資料類型。
