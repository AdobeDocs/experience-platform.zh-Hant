---
title: Azure Synapse Analytics Source Connector概觀
description: 瞭解如何使用API或使用者介面將Azure Synapse Analytics連結至Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 3%

---

# [!DNL Azure Synapse Analytics]

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

[!DNL Azure Synapse Analytics]是雲端型分析服務，可整合巨量資料與資料倉儲。 您可以使用SQL、[!DNL Spark]或即時工具來內嵌、探索、準備及分析資料，完全不需要行動資料。

您可以使用[!DNL Azure Synapse Analytics]來源來連線您的帳戶，並將您的資料帶到Adobe Experience Platform。

## 先決條件 {#prerequisites}

請先閱讀下列章節，完成先決條件設定，然後再將[!DNL Azure Synapse Analytics]帳戶連線至Experience Platform。

### IP位址允許清單

將來源連線至Experience Platform之前，您必須先將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址以連線至Experience Platform](../../ip-address-allow-list.md)的指南以瞭解詳細資訊。

### 設定許可權

若要將來源帳戶連線至Experience Platform，您的帳戶必須已啟用下列兩項許可權：

* **檢視來源**
* **管理來源**

如果您沒有這些許可權，請聯絡您的產品管理員以請求存取權。 如需詳細資訊，請閱讀[存取控制UI指南](../../../access-control/ui/overview.md)。

### 向Experience Platform進行驗證

您可以使用帳戶金鑰驗證或服務主體金鑰驗證，將您的[!DNL Azure Synapse Analytics]連線至Experience Platform。

>[!BEGINTABS]

>[!TAB 帳戶金鑰驗證]

提供下列認證的值，以使用帳戶金鑰驗證將您的[!DNL Azure Synapse Analytics]資料庫連線至Experience Platform。

| 認證 | 說明 |
| --- | --- |
| 連接字串 | 這是用來驗證[!DNL Azure Synapse Analytics]的&#x200B;**連線字串**。 標準格式為： `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`。 您必須以實際的連線詳細資料取代預留位置。 |
| 連線規格ID | **連線規格**&#x200B;提供資料來源的聯結器屬性。 這包含驗證規格等詳細資訊，以及建立&#x200B;**基底**&#x200B;和&#x200B;**來源**&#x200B;連線的需求。 針對[!DNL Azure Synapse Analytics]，連線規格ID為： `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`。 **注意：**&#x200B;只有在透過API連線時才需要此認證。 |

>[!TAB 服務主要金鑰驗證]

若要擷取服務主要金鑰驗證的認證，請瀏覽至[[!DNL Microsfot Entra admin center]](https://entra.microsoft.com/#home)並擷取下列專案的值：

* 應用程式 ID
* 顯示名稱
* Secret
* 租用戶 ID

接下來，導覽至您的[[!DNL Azure Synapse Analytics] 執行個體](https://azure.microsoft.com/en-ca/products/synapse-analytics)，然後選取從外部提供者建立使用者的選項。 從這裡，為結構描述上的服務主體提供適當的許可權。 **注意：**：您必須包含「SELECT」，因為它與結構描述預覽所需的「COPY」類似。 例如，範例指令可以是：

```SQL
GRANT SELECT ON SCHEMA::dbo TO {APP_ID};
```

提供下列認證的值，以使用服務主體金鑰驗證將您的[!DNL Azure Synapse Analytics]資料庫連線到Experience Platform。

| 認證 | 說明 |
| --- | --- |
| 伺服器 | [!DNL Azure Synapse Analytics] SQL端點的完整網域名稱。 |
| 資料庫 | [!DNL Azure Synapse Analytics]工作區中特定資料庫的名稱。 |
| 租用戶 | 與您的[!DNL Azure]訂閱相關聯的[!DNL Azure Active Directory]租使用者識別碼。 |
| 服務主體 ID | [!DNL Azure Active Directory]應用程式的使用者端識別碼。 |
| 服務主體金鑰 | 與服務主體關聯的使用者端密碼或密碼。 |
| 連線規格ID | **連線規格**&#x200B;提供資料來源的聯結器屬性。 這包含驗證規格等詳細資訊，以及建立&#x200B;**基底**&#x200B;和&#x200B;**來源**&#x200B;連線的需求。 針對[!DNL Azure Synapse Analytics]，連線規格ID為： `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`。 **注意：**&#x200B;只有在透過API連線時才需要此認證。 |

如需詳細資訊，請閱讀有關管理 [!DNL Azure Synapse Analytics]](https://learn.microsoft.com/en-us/azure/synapse-analytics/synapse-service-identity)的身分的[[!DNL Azure] 檔案。

>[!ENDTABS]

## 使用API連線[!DNL Azure Synapse Analytics]至Experience Platform

* [使用流量服務API連線 [!DNL Azure Synapse Analytics] 至Experience Platform](../../tutorials/api/create/databases/synapse-analytics.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

## 使用UI連線[!DNL Azure Synapse Analytics]至Experience Platform

* [在UI中連線 [!DNL Azure Synapse Analytics] 至Experience Platform](../../tutorials/ui/create/databases/synapse-analytics.md)
* [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)

