---
title: 沙箱工具API指南附錄
description: 本檔案提供與使用沙箱工具API相關的補充資訊。
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# Sandbox API指南附錄

本檔案提供與使用[!DNL Sandbox] API相關的補充資訊。

## 使用查詢引數 {#query}

沙箱工具API支援在列出套件時使用查詢引數來分頁和篩選結果。

>[!NOTE]
>
>`limit`可以個別傳遞和啟動。

| 參數 | 說明 |
| --- | --- |
| `limit` | 回應中可傳回的最大記錄數。 預設限製為20。 |
| `start` | 專案子集清單開始位置的起點。 |
| `targetSandbox` | 代表您要在其中匯入成品的沙箱名稱。 |
| `jobType` | 工作的型別。 此值可以是NEW、RESUME和ROLLBACK。 |
| `jobStatus` | 工作的狀態。 此值可以是PENDING、IN_PROGRESS、SUCCESS、FAILED和CANCELED。 |
| `requestType` | 要求的型別。 此值可以是EXPORT、IMPORT和COPY。 |
| `expiryPeriod ` | 這個使用者指定的時段會定義從發佈套件開始的套件到期日（以天為單位）。 此值不應為負數。 預設值是從呼叫更新或發佈API後的90天。 |
