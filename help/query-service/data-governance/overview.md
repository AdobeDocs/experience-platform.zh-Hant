---
title: 查詢服務中的資料治理
description: 本概述介紹了Experience Platform查詢服務中資料治理的主要要素。
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: 54a6f508818016df1a4ab2a217bc0765b91df9e9
workflow-type: tm+mt
source-wordcount: '2843'
ht-degree: 1%

---

# 查詢服務中的資料管理

Adobe Experience Platform將來自多個企業系統的資料匯集在一起，允許您根據需要通過查詢服務來清理、塑造、操作和豐富資料。 這使營銷人員能夠更好地識別、理解和吸引客戶。 確保適當的資料治理是處理個人資訊的一個關鍵方面，因為某些資料可能受基於組織策略和法律法規的使用限制的制約。 確保所攝取的資料及其相關操作符合定義的資料使用策略至關重要。

查詢服務中的資料治理允許您管理客戶資料並確保遵守適用於資料使用的法規、限制和策略。 在確保已根據您的企業定義的法規應用使用策略時，此功能將發揮關鍵作用。

建議定期執行資料處理的組織概述、實踐和實施這些指導原則，以便為所有用戶建立一個注重隱私的環境。

在使用查詢服務時，以下類別有助於遵守資料合規性法規：

1. 安全性
1. 審計
1. 資料使用
1. 隱私權
<!-- 1. Data hygiene -->

本文檔將檢查治理的各個不同領域，並演示如何使用查詢服務來促進資料合規性。 查看 [治理、隱私和安全概述](../../landing/governance-privacy-security/overview.md) 瞭解有關Experience Platform如何允許您管理客戶資料並確保法規遵從性的更多資訊。

## 安全性

資料安全是保護資料免受未經授權訪問和確保資料在其整個生命週期中安全訪問的過程。 通過通過諸如基於角色的訪問控制和基於屬性的訪問控制等功能對角色和權限的應用，在Experience Platform中維護安全訪問。 憑據、SSL和資料加密也用於確保跨平台的資料保護。

有關查詢服務的安全性分為以下幾類：

* [訪問控制](#access-control):通過角色和權限（包括資料集和列級權限）控制訪問。
* 通過 [連接](#connectivity):通過實現具有過期憑據或非過期憑據的有限連接，通過平台和外部客戶端保護資料。
* 通過 [加密和系統級密鑰](#encryption):在資料處於靜止狀態時通過加密來確保資料安全。

<!-- * Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest. -->

### 存取控制 {#access-control}

Adobe Experience Platform的訪問控制允許您使用 [Adobe Admin Console](https://adminconsole.adobe.com/) 使用基於角色的權限管理對查詢服務功能的訪問。 同樣，您可以通過對方案和資料欄位的標籤管理來控制對特定資料屬性的訪問。

本節概述了用戶必須擁有的必需訪問控制權限才能充分利用查詢服務功能。 查看上的文檔 [管理權限](../../access-control/ui/permissions.md) 和 [管理用戶](../../access-control/ui/users.md) 有關為產品配置檔案分配訪問權限的詳細說明。

#### 相關權限

相關訪問控制權限根據其範圍級別在下表中定義。

**查詢執行權限**

要在查詢服務中運行查詢，必須為用戶分配具有以下權限的角色：

| 權限 | 說明 |
|---|---|
| [!UICONTROL 管理查詢] | 此權限允許用戶執行資料探查和批處理查詢，這些查詢可以讀取現有資料集或在資料集上寫入資料。 這包括 `CREATE TABLE AS SELECT` (`CTAS`) `INSERT INTO AS SELECT` (`ITAS`)查詢。 |

**資料集權限**

本節用於指導在通過查詢服務查詢資料時訪問資料集所需的基於資源的訪問。

通過「權限」介面，您可以定義具有以下權限的資料集和架構的基於資源的訪問控制：

| 權限 | 說明 |
|---|---|
| [!UICONTROL 管理資料集] | 此權限為架構提供只讀訪問，並允許訪問用於查詢服務的讀取、建立、編輯和刪除資料集。 |
| [!UICONTROL 檢視資料集] | 此權限允許對資料集和架構進行只讀訪問，以便與查詢服務一起使用。 |

#### 列/欄位的訪問控制

基於屬性的訪問控制功能使查詢服務用戶能夠限制對關鍵用戶資料的訪問。 可以根據分配給角色的權限授予或限制訪問權限。 用戶對單個列的訪問由相關資料使用標籤和應用到分配給用戶的角色的權限集控制。

使用資料使用標籤標籤架構欄位組和類將資料使用限制應用於具有相同欄位組和類的所有架構。 請參閱 [基於屬性的訪問控制](../../access-control/abac/overview.md) 獲取有關此功能的全面資訊。

此功能使您能夠將機密列的訪問權限授予您選擇的用戶組。 對列的訪問控制可以限制特定類型用戶的讀和寫功能。

對列的訪問控制可以在標準和即席方案的方案級別應用。 將資料使用標籤應用於XDM架構，以限制對一個或多個列的訪問。 資料標籤始終如一地應用，即使對於通過查詢服務建立的資料集也是如此，該資料集使用作為CTAS操作一部分生成的預定義模式或即席模式。

使用標籤和角色應用適當的訪問級別後，當用戶嘗試訪問不可訪問的資料時，將出現以下系統行為：

1. 如果用戶被拒絕訪問模式內的列之一，則用戶也被拒絕對受限列進行讀或寫。 這適用於以下常見方案：

   * **案例1**:當用戶嘗試執行僅影響受限列的查詢時，系統會拋出一個不存在該列的錯誤。
   * **案例2**:當用戶嘗試執行具有多個列（包括受限列）的查詢時，系統僅返回所有非受限列的輸出。

1. 如果用戶嘗試訪問計算欄位，則要求用戶有權訪問合成中使用的所有欄位，或者系統也拒絕訪問計算欄位。

#### 視圖的訪問控制

查詢服務提供了使用標準ANSI SQL的功能 [`CREATE VIEW`](../sql/syntax.md#create-view) 的下界。 對於高度敏感的資料工作流，在建立視圖時必須強制實施相應的控制。

的 `CREATE VIEW` 關鍵字定義查詢的視圖，但視圖未物理實現。 相反，每次在查詢中引用視圖時都會運行查詢。 當用戶從資料集建立視圖時，父資料集的基於角色和屬性的訪問控制規則 **不** 分層應用。 因此，在建立視圖時，必須顯式設定每個列的權限。

#### 在加速的資料集上建立基於欄位的訪問限制 {#create-field-based-access-restrictions-on-accelerated-datasets}

使用 [基於屬性的訪問控制能力](../../access-control/abac/overview.md) 您可以在事實資料集和維資料集上定義組織或資料使用作用域 [加速儲存](../data-distiller/query-accelerated-store/send-accelerated-queries.md)。 這允許管理員管理對特定網段的訪問，並更好地管理授予用戶或用戶組的訪問權限。

要在加速的資料集上建立基於欄位的訪問限制，可以使用Query Service CTAS查詢建立加速的資料集，並基於現有的XDM架構或ad hoc架構構建這些資料集。 然後，管理員可以 [添加和編輯架構的資料使用標籤](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) 或 [ad hoc模式](./ad-hoc-schema-labels.md#edit-governance-labels)。 您可以將標籤應用、建立和編輯到方案中 [!UICONTROL 標籤] 工作區 [!UICONTROL 架構] UI。

資料使用標籤也可以是 [直接應用或編輯到資料集](../../data-governance/labels/user-guide.md#add-labels) 通過資料集UI，或通過訪問控制建立 [!UICONTROL 標籤] 工作區。 請參閱有關如何 [建立新標籤](../../access-control/abac/ui/labels.md) 的子菜單。

然後，用戶對各個列的訪問可以通過附加的資料使用標籤和應用到分配給用戶的角色的權限集來控制。

### 連接 {#connectivity}

可通過平台UI或與外部相容客戶端建立連接來訪問查詢服務。 所有可用前線的訪問由一組證書控制。

#### 通過外部客戶端進行連接

使用第三方客戶端訪問查詢服務需要憑據才能進行授權。 這些憑據是訪問任何相容外部客戶端的查詢服務所必需的。 可以使用 [過期憑據](#expiring-credentials) 或 [非過期憑據](#non-expiring-credentials)。

#### 通過過期憑據的有限連接時間 {#expiring-credentials}

[過期憑據](../ui/credentials.md) 允許用戶與外部客戶端形成臨時連接。 此憑據集僅有效24小時。 這些類型的憑據的到期情況以及「查詢服務」面板中的「憑據」頁籤都可以看到。

![突出顯示了過期憑據的查詢服務工作區中的憑據頁籤。](../images/data-governance/overview/expiring-credentials.png)

#### 未過期的憑據 {#non-expiring-credentials}

[未過期的憑據](../ui/credentials.md#non-expiring-credentials) 允許您與外部客戶端建立永久連接，從而更輕鬆地連接到查詢服務，而無需手動密碼。

要啟用生成非過期憑據的選項，必須遵循概述的 [必備工作流](../ui/credentials.md#prerequisites)。 在此過程中，組織管理員需要配置產品配置檔案的權限，從而讓管理員能夠控制哪些帳戶有權使用未過期的憑據。

可以為具有未過期憑據的技術用戶帳戶分配角色，以通過根據其職責和需要定義其讀寫訪問範圍來確保適當的資料治理。 請參閱上面的 [通過訪問控制使用基於角色的權限](#access-control) 以管理對查詢服務的訪問。

先決工作流完成後，授權用戶現在可以 [生成所需的連接憑據](../ui/credentials.md#generate-credentials)。

#### SSL資料加密

為了提高安全性，Query Service為加密客戶端/伺服器通信的SSL連接提供本機支援。 平台支援各種SSL選項，以滿足您的資料安全需求，並平衡加密和密鑰交換的處理開銷。

請參閱可用的指南 [SSL選項，用於第三方客戶端連接到查詢服務](../clients/ssl-modes.md) 有關詳細資訊，包括如何使用 `verify-full` SSL參數值。

### 加密 {#encryption}

<!-- Commented out lines to be included when customer-managed keys is released. Link out to the new document. -->

<!-- ### Encryption and customer-managed keys (CMK) {#encryption-and-customer-managed-keys} -->

加密是指使用算法過程將資料轉換為編碼和不可讀的文本，以確保在沒有解密密鑰的情況下資訊得到保護和不可訪問。

Query Service資料符合性確保資料始終被加密。 傳輸中的資料始終符合HTTPS，靜態資料在Azure Data Lake儲存中使用系統級密鑰進行加密。 請參閱 [資料如何加密在Adobe Experience Platform](../../landing/governance-privacy-security/encryption.md) 的子菜單。 有關在Azure資料湖儲存中如何加密靜態資料的詳細資訊，請參閱 [正式Azure文檔](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)。

<!-- Data-in-transit is always HTTPS compliant and similarly when the data is at rest in the data lake, the encryption is done with Customer Management Key (CMK), which is already supported by Data Lake Management. The currently supported version is TLS1.2. -->

## 審計 {#audit}

查詢服務記錄用戶活動並將該活動分類為不同的日誌類型。 日誌提供有關 **誰** 執行 **什麼** 操作和 **何時**。 稽核記錄中所記錄的每個動作都包含中繼資料，其指出動作類型、日期和時間、執行動作之使用者的電子郵件 ID，以及與動作類型相關的其他屬性。

平台用戶可以根據需要請求任何日誌類別。 本節提供了有關為Query Service捕獲的資訊類型以及可以在何處訪問此資訊的詳細資訊。

### 查詢日誌 {#query-logs}

查詢日誌UI允許您監視和查看通過查詢編輯器或查詢服務API運行的所有查詢的執行詳細資訊。 這為查詢服務活動帶來了透明度，允許您檢查元資料 **全部** 已在查詢服務中執行的查詢。 它包括所有類型的查詢，無論它是試探性查詢、批處理查詢還是計畫查詢。

查詢日誌可以通過中的平台UI訪問 [!UICONTROL 日誌] 頁籤 [!UICONTROL 查詢] 工作區。

![「查詢」日誌頁籤，其中「詳細資訊」面板突出顯示。](../images/data-governance/overview/queries-log.png)

### 稽核記錄 {#audit-logs}

審核日誌包含比查詢日誌更詳細的資訊，並使您能夠根據用戶、日期、查詢類型等屬性篩選日誌。 除查詢日誌UI中提供的詳細資訊外，「審核日誌」還儲存有關單個用戶的詳細資訊以及其會話資料或與第三方客戶端的連接。

通過提供用戶操作的準確記錄，審核跟蹤可幫助您解決問題，並幫助您的企業有效地遵守公司資料管理策略和法規要求。 審核日誌提供所有平台活動的記錄。 使用審計日誌，您可以審計與查詢執行、模板和計畫查詢相關的用戶操作，以提高查詢服務中用戶執行操作的透明度和可見性。

下表指明了由審計日誌捕獲的查詢類別及其記錄的操作類型：

| 類別 | 操作類型 |
|---|---|
| 查詢 | 執行 |
| 查詢模板 | 建立、刪除、更新 |
| 計畫查詢 | 建立、刪除、更新 |

下面是三個擴展伺服器日誌的清單，這些日誌包含的詳細資訊多於查詢日誌中的日誌。 在審計日誌查詢類別中找到擴展日誌：

1. **元查詢日誌**:當執行查詢時，執行各種關聯的後端子查詢（如分析）。 這些類型的查詢稱為「元資料」查詢。 相關詳細資訊可在審核日誌中找到。
1. **會話日誌**:無論用戶是否執行查詢，系統都會在用戶登錄到查詢服務時為其建立會話條目日誌。
1. **第三方客戶端連接日誌**:當用戶成功將查詢服務連接到第三方客戶端時，將生成連接審核日誌。

查看 [審核日誌概述](../../landing/governance-privacy-security/audit-logs/overview.md) 有關審核日誌如何幫助您的組織實現資料合規性的詳細資訊。

## 資料使用 {#data-usage}

平台中的資料治理框架提供了一種統一的方法，可負責地跨所有Adobe解決方案、服務和平台使用資料。 它協調了在整個Adobe Experience Cloud捕獲、通信和使用元資料的系統性方法。 這反過來又有助於資料控制器根據所需的市場營銷操作以及這些預期市場營銷操作對資料的限制來標籤資料。 請參閱 [資料使用標籤](../../data-governance/labels/overview.md) 有關Data Governance如何允許將資料使用情況標籤應用於資料集和欄位的詳細資訊。

在資料發展過程中的每個階段都努力實現資料法規遵從性是最佳做法。 為此，應將使用臨時架構的派生資料集適當地標籤為資料治理框架的一部分。 由Query Service形成的派生資料集有兩種類型：使用標準架構的資料集和使用臨時架構的資料集。

>[!NOTE]
>
>使用Query Service建立的資料集稱為「派生資料集」。

由於專用模式由單個用戶為特定目的建立，因此XDM模式欄位為該特定資料集命名空間，並且不打算跨不同資料集使用。 因此，預設情況下，Experience PlatformUI中不可見即席架構。 雖然標準架構和即席架構之間資料使用標籤的應用沒有差別，但是必須首先在平台UI中使查詢服務為標籤而建立的即席架構可見。 請參閱上的指南 [在平台UI中發現ad hoc架構](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) 的子菜單。

訪問架構後，您可以 [將標籤應用於單個欄位](../../xdm/tutorials/labels.md)。 一旦標籤了某個架構，從該架構派生的所有資料集都將繼承這些標籤。 在此處，您可以設定資料使用策略，該策略可以限制具有特定標籤的資料被激活到特定目標。 有關詳細資訊，請參閱 [資料使用策略](../../data-governance/policies/overview.md)。

## 隱私權 {#privacy}

[Privacy Service](../../privacy-service/home.md) 幫助您管理客戶請求以根據法律隱私法規訪問和刪除其資料。 它通過搜索資料以查找預先存在的標識符來做到這一點，並根據請求的隱私作業訪問或刪除該資料。 必須正確標籤資料，才能使服務確定在隱私作業期間訪問或刪除哪些欄位。 受隱私請求約束的資料必須包含客戶身份資訊，以便將不同的資料片段與隱私請求所應用的個人聯繫起來。 查詢服務可以使用唯一標識符來豐富其使用的資料，以滿足隱私作業的需要。

隱私請求可以發送到資料湖或配置檔案資料儲存。 從資料湖中刪除的記錄不會導致從這些記錄中刪除配置檔案。 此外，從資料湖中刪除個人資訊的隱私作業不會刪除其配置檔案，因此在完成隱私作業後所攝取的任何資訊（包含該配置檔案ID）都會正常更新該配置檔案。 這重申需要正確識別在特設方案中使用的資料。

有關Privacy Service的詳細資訊，請參閱 [隱私請求的標識資料](../../privacy-service/identity-data.md) 以及如何配置資料操作並利用Adobe技術來有效檢索客戶隱私請求的適當身份資訊。

針對資料治理的查詢服務功能簡化和簡化了資料分類過程，並遵守了資料使用法規。 一旦識別了資料，Query Service就允許您在所有輸出資料集上分配主標識。 你 **必須** 在資料集中添加標識，以便於資料隱私請求並努力實現資料合規性。

通過平台UI和查詢服務，可以將架構資料欄位設定為標識欄位 [使用SQL命令「ALTER TABLE」標籤主標識](../sql/syntax.md#alter-table)。 使用 `ALTER TABLE` 命令在使用SQL而不是通過平台UI直接從架構建立資料集時特別有用。 有關如何 [在UI中定義標識欄位](../../xdm/ui/fields/identity.md) 使用標準架構時。

<!-- COMMENTING OUT DATA HYGEINE SECTION TEMPORARILY UNTIL IT IS GA. currently it is in Beta only.

## Data hygiene 

"Data hygiene" refers to the process of repairing or removing data that may be outdated, inaccurate, incorrectly formatted, duplicated, or incomplete. It is important to ensure adequate data hygiene along every step of the data's journey and even from the initial data storage location. In Query Service, this is either the data lake or the data warehouse.

It is necessary to assign an identity to a derived dataset to allow their management by the [!DNL Data Hygiene] service. Conversely, when you create aggregated data on an accelerated data store, the aggregated data cannot be used to derive the original data. As a result of this data aggregation, the need to raise data hygiene requests is eliminated. == THIS APPEARS TO BE A PRIVACY USE CASE NAD NOT DATA HYGEINE ++  this is confusing.

An exception to this scenario is the case of deletion. If a data hygiene deletion is requested on a dataset and before the deletion is completed, another derived dataset query is executed, then the derived dataset will capture information from the original dataset. In this case, you must be mindful that if a request to delete a dataset has been sent, you must not execute any new derived dataset queries using the same dataset source. 

See the [data hygiene overview](../../hygiene/home.md) for more information on data hygiene in Adobe Experience Platform. -->
