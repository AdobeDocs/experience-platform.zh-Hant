---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢編輯器；查詢編輯器；查詢編輯器；
solution: Experience Platform
title: Query Service UI指南
topic-legacy: guide
description: Adobe Experience Platform查詢服務提供可用來撰寫和執行查詢、檢視先前執行的查詢，以及存取由您IMS組織內的使用者儲存的查詢的使用者介面。
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 696db8081ab8225d79cd468b7435770d407d3e3d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 1%

---

# 認證指南

Adobe Experience Platform查詢服務可讓您與外部用戶端連線。 您可以使用到期憑證或非到期憑證來連線至這些外部用戶端。

## 即將到期的憑據

您可以使用到期憑證來快速設定與外部用戶端的連線。

![](../images/ui/credentials/expiring-credentials.png)

**[!UICONTROL 即將到期的憑據]**&#x200B;部分提供以下資訊：

- **[!UICONTROL 主機]**:您要連接的主機的名稱。若要連線至查詢服務，這會包含您目前使用的IMS組織名稱。
- **[!UICONTROL 埠]**:要連接的主機的埠號。
- **[!UICONTROL 資料庫]**:要連接的資料庫的名稱。
- **[!UICONTROL 使用者名稱]**:用於連接到查詢服務的用戶名。
- **[!UICONTROL 密碼]**:用於連接到Query Service的密碼。
- **[!UICONTROL PSQL命令]**:一個命令，它自動插入了所有相關資訊，以便您使用命令行上的PSQL連接到查詢服務。
- **[!UICONTROL 過期]**:即將到期的憑證的到期日。憑證產生後24小時過期。

## 未到期的憑據

您可以使用非到期憑證來設定與外部用戶端的更永久連線。

### 先決條件

您必須先在Adobe Admin Console中完成下列步驟，才能產生非到期憑證：

1. 登入[Adobe Admin Console](https://adminconsole.adobe.com/)並從頂端導覽列選取相關組織。
2. [選取產品設定檔。](../../access-control/ui/browse.md)
3. [為產品設定 **** 檔設定 **沙箱和管** ](../../access-control/ui/permissions.md) 理查詢服務整合權限。
4. [將新使用者新增至產品設](../../access-control/ui/users.md) 定檔，這些使用者即會獲得其設定的權限。
5. [將使用者新增為產品設定檔管](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) 理員，以允許為任何作用中的產品設定檔建立帳戶。
6. [將使用者新增為產品設定檔開](https://helpx.adobe.com/tw/enterprise/using/manage-developers.html) 發人員，以建立整合。

若要進一步了解如何指派權限，請參閱[存取控制](../../access-control/home.md)上的檔案。

所有必要權限現在都已在「Adobe開發人員控制台」中設定，供使用者使用即將到期的憑證功能。

### 生成憑據

若要建立一組非到期憑證，請返回Platform UI，並從左側導覽中選取&#x200B;**[!UICONTROL Queries]**&#x200B;以存取[!UICONTROL Queries]工作區。 接下來，選擇&#x200B;**[!UICONTROL Credentials]**&#x200B;頁簽，後跟&#x200B;**[!UICONTROL Generate credentials]**。

![](../images/ui/credentials/generate-credentials.png)

此時將顯示一個對話框，允許您生成憑據。 若要建立未到期的憑證，您必須提供下列詳細資料：

- **[!UICONTROL 名稱]**:您正在生成的憑據的名稱。
- **[!UICONTROL 說明]**:（選用）您要產生的憑證說明。
- **[!UICONTROL 指派給]**:將為其分配憑據的用戶。此值應為建立憑證之使用者的電子郵件地址。
- **[!UICONTROL 密碼]** （選用）您憑證的選用密碼。如果未設定密碼，Adobe將自動為您生成密碼。

提供所有所需詳細資訊後，請選擇&#x200B;**[!UICONTROL 生成憑據]**&#x200B;以生成憑據。

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>選擇&#x200B;**[!UICONTROL 生成憑據]**&#x200B;按鈕後，配置JSON檔案將下載到本地電腦。 由於Adobe **不**&#x200B;記錄生成的憑據，因此您必須安全地儲存下載的檔案並保留憑據的記錄。
>
>此外，如果90天內未使用憑證，則會清除憑證。

設定JSON檔案包含技術帳戶名稱、技術帳戶ID和憑證等資訊。 以下列格式提供。

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

保存生成的憑據後，選擇&#x200B;**[!UICONTROL Close]**。 您現在可以看到所有未到期憑證的清單。

![](../images/ui/credentials/list-credentials.png)

您可以編輯或刪除未到期的憑證。 要編輯未到期的憑據，請選擇鉛筆表徵圖(![](../images/ui/credentials/edit-icon.png))。 要刪除未到期的憑據，請選擇刪除表徵圖(![](../images/ui/credentials/delete-icon.png))。

編輯未到期的憑證時，會出現強制回應視窗。 您可以提供下列詳細資料以進行更新：

- **[!UICONTROL 名稱]**:您正在生成的憑據的名稱。
- **[!UICONTROL 說明]**:（選用）您要產生的憑證說明。
- **[!UICONTROL 指派給]**:將為其分配憑據的用戶。此值應為建立憑證之使用者的電子郵件地址。

![](../images/ui/credentials/update-credentials.png)

提供所有必要的詳細資訊後，請選擇&#x200B;**[!UICONTROL 更新帳戶]**&#x200B;以完成憑據的更新。

## 使用憑據連接到外部客戶端

您可以使用即將到期或未到期的憑據來連接外部客戶端，如Aqua Data Studio、Looker或Power BI。 這些憑證的輸入方法會因外部用戶端而異。 請參閱外部客戶端的文檔，以了解有關使用這些憑據的具體說明。

影像會指出UI中找到之每個參數的位置，但非即將到期憑證的密碼除外。 雖然非到期憑證是由其JSON組態檔提供，您可以在UI的&#x200B;**Credentials**&#x200B;標籤下檢視未到期憑證。

![](../images/ui/credentials/expiring-credentials.png)

下表概述了連接到外部客戶端通常所需的參數。

>[!NOTE]
>
>使用非到期憑據連接到主機時，仍需使用[!UICONTROL 即將到期憑據]部分中列出的所有參數，但密碼和用戶名除外。

| 參數 | 說明 |
|---|---|
| 伺服器/主機 | 要連接的伺服器/主機的名稱。 <ul><li>此值用於即將到期的憑證和非即將到期的憑證，其形式為`server.adobe.io`。 該值位於[!UICONTROL EXPINING CREDENTIALS]部分的&#x200B;**[!UICONTROL Host]**&#x200B;下。</ul></li> |
| 埠 | 要連接的伺服器/主機的埠。 <ul><li>此值用於即將到期的憑據和非即將到期的憑據，可在[!UICONTROL EXPINING CREDENTIALS]部分的&#x200B;**[!UICONTROL Port]**&#x200B;下找到。 埠的範例值為`80`。</ul></li> |
| 資料庫 | 您要連接的資料庫。 <ul><li>此值用於到期憑據和非到期憑證，可在[!UICONTROL 到期憑據]區段的&#x200B;**[!UICONTROL Database]**&#x200B;下找到。 資料庫的範例值為`prod:all`。</ul></li> |
| 使用者名稱 | 連接到外部客戶端的用戶的用戶名。 <ul><li>如果您使用即將到期的憑證，其形式會是`@AdobeOrg`之前的英數字串。 此值位於&#x200B;**[!UICONTROL Username]**&#x200B;下。</li><li>如果您使用的是非到期憑證，這是您選擇的字串，但它&#x200B;**不能**&#x200B;與設定JSON檔案中找到的`technicalAccountID`值相同。</li></ul> |
| 密碼 | 連接到外部客戶端的用戶的密碼。 <ul><li>如果您使用即將到期的憑證，可在[!UICONTROL 即將到期的憑證]區段的&#x200B;**[!UICONTROL 密碼]**&#x200B;下找到。</li><li>如果您使用的是未到期的憑證，此值是來自technicalAccountID的串連引數，以及來自設定JSON檔案的憑證。 密碼值採用以下形式：`{technicalAccountId}:{credential}`。</li></ul> |

## 後續步驟

現在您已了解過期和未過期的憑證如何運作，您可以使用這些憑證連線至外部用戶端。 有關外部客戶端的詳細資訊，請參閱[將客戶端連接到查詢服務指南](../clients/overview.md)。
