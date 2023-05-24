---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy ServiceAPI指南附錄
description: 此文檔包含有關使用Privacy ServiceAPI的其他資訊。
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 5%

---

# Privacy ServiceAPI指南附錄

以下各節包含有關使用Adobe Experience Platform Privacy ServiceAPI的其他資訊。

## 標準標識命名空間 {#standard-namespaces}

發送到的所有標識 [!DNL Privacy Service] 必須在特定標識名稱空間下提供。 標識命名空間是 [Adobe Experience Platform身份服務](../../identity-service/home.md) 指明身份相關的上下文。

下表概述了幾種常用的預定義標識類型，這些類型由 [!DNL Experience Platform]以及他們的關聯 `namespace` 值：

| 標識類型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 電子郵件 | `Email` | `6` |
| 電話 | `Phone` | `7` |
| Adobe Advertising CloudID | `AdCloud` | `411` |
| Adobe Audience ManagerUUID | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| Adobe TargetID | `TNTID` | `9` |
| [!DNL Apple] 廣告商ID | `IDFA` | `20915` |
| [!DNL Google] 廣告 ID | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>每個標識類型還 `namespaceId` 整數值，可用來代替 `namespace` 設定標識時的字串 `type` 屬性。 請參閱 [命名空間限定符](#namespace-qualifiers) 的子菜單。

您可以通過向以下站點發出GET請求來檢索組織正在使用的標識命名空間清單 `idnamespace/identities` 端點 [!DNL Identity Service] API。 查看 [Identity Service開發人員指南](../../identity-service/api/getting-started.md) 的子菜單。

## 命名空間限定符

指定 `namespace` 值 [!DNL Privacy Service] API, a **命名空間限定符** 必須包含在相應 `type` 的下界。 下表概述了不同的接受的命名空間限定符。

| 限定符 | 定義 |
| --------- | ---------- |
| `standard` | 一個標準命名空間是全局定義的，不與單個組織資料集（例如，電子郵件、電話號碼等）相關。 提供了命名空間ID。 |
| `custom` | 在組織上下文中建立的、未在 [!DNL Experience Cloud]。 值表示要搜索的友好名稱（「名稱」欄位）。 提供了命名空間ID。 |
| `integrationCode` | 整合代碼 — 類似於「自定義」，但具體定義為要搜索的資料源的整合代碼。 提供了命名空間ID。 |
| `namespaceId` | 指示值是通過命名空間服務建立或映射的命名空間的實際ID。 |
| `unregistered` | 未在命名空間服務中定義且採用「原樣」的自由形式字串。 處理這些類型命名空間的任何應用程式都會針對它們進行檢查，並在適合公司上下文和資料集時進行處理。 未提供命名空間ID。 |
| `analytics` | 內部映射的自定義命名空間 [!DNL Analytics]，不在命名空間服務中。 此命令直接按照原始請求指定的方式傳入，但沒有命名空間ID |
| `target` | 內部理解的自定義命名空間 [!DNL Target]，不在命名空間服務中。 此命令直接按照原始請求指定的方式傳入，但沒有命名空間ID |

{style="table-layout:auto"}

## 接受的產品值

下表概述了在中指定Adobe產品的接受值 `include` 作業建立請求的屬性。

| 產品 | 用於 `include` 屬性 |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform（資料湖） | `aepDataLake` |
| Adobe Experience Platform（即時客戶概要資訊） | `profileService` |
| Adobe Primetime驗證 | `primetimeAuthentication` |
| Adobe Target | `target` |
| 客戶屬性(CRS) | `CRS` |
| 身份識別服務 | `identity` |
| Marketo Engage | `marketo` |

{style="table-layout:auto"}
