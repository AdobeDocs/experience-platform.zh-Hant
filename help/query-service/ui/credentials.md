---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢編輯器；查詢編輯器；查詢編輯器；
solution: Experience Platform
title: 查詢服務憑證指南
topic-legacy: guide
description: Adobe Experience Platform查詢服務提供可用來撰寫和執行查詢、檢視先前執行的查詢，以及存取由您IMS組織內的使用者儲存的查詢的使用者介面。
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 344602a0e828d140ea386daf30a25b8f595f8d04
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 1%

---

# 認證指南

Adobe Experience Platform查詢服務可讓您與外部用戶端連線。 您可以使用到期憑證或非到期憑證來連線至這些外部用戶端。

## 即將到期的憑據 {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="用戶端的SSL模式"
>abstract="必須在連接至查詢服務的用戶端中啟用SSL。 確認SSL模式設為「必要」。"

您可以使用到期憑證來快速設定與外部用戶端的連線。

![「查詢」儀表板「憑據」頁簽，其中「即將到期的憑據」部分突出顯示。](../images/ui/credentials/expiring-credentials.png)

此 **[!UICONTROL 即將到期的憑據]** 一節提供下列資訊：

- **[!UICONTROL 主機]**:您要連接的主機的名稱。 若要連線至查詢服務，這會包含您目前使用的IMS組織名稱。
- **[!UICONTROL 埠]**:要連接的主機的埠號。
- **[!UICONTROL 資料庫]**:要連接的資料庫的名稱。
- **[!UICONTROL 使用者名稱]**:用於連接到查詢服務的用戶名。
- **[!UICONTROL 密碼]**:用於連接到Query Service的密碼。
- **[!UICONTROL PSQL命令]**:一個命令，它自動插入了所有相關資訊，以便您使用命令行上的PSQL連接到查詢服務。
- **[!UICONTROL 過期]**:即將到期的憑證的到期日。 憑證產生後24小時過期。

## 未到期的憑據 {#non-expiring-credentials}

您可以使用非到期憑證來設定與外部用戶端的更永久連線。

### 先決條件

您必須先在Adobe Admin Console中完成下列步驟，才能產生非到期憑證：

1. 登入 [Adobe Admin Console](https://adminconsole.adobe.com/) 並從頂端導覽列選取相關組織。
2. [選取產品設定檔。](../../access-control/ui/browse.md)
3. [設定 **沙箱** 和 **管理查詢服務整合** 權限](../../access-control/ui/permissions.md) 針對產品設定檔。
4. [將新使用者新增至產品設定檔](../../access-control/ui/users.md) 因此，系統會授予這些使用者已設定的權限。
5. [將使用者新增為產品設定檔管理員](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) 允許為任何作用中的產品設定檔建立帳戶。
6. [將使用者新增為產品設定檔開發人員](https://helpx.adobe.com/enterprise/using/manage-developers.html) 以建立整合。

若要進一步了解如何指派權限，請參閱 [存取控制](../../access-control/home.md).

使用者現在可在Adobe Developer Console中設定所有必要權限，以使用即將到期的憑證功能。

### 生成憑據

若要建立一組未到期的憑證，請返回Platform UI並選取 **[!UICONTROL 查詢]** 從左側導覽器存取 [!UICONTROL 查詢] 工作區。 下一步，選取 **[!UICONTROL 憑證]** 標籤後面 **[!UICONTROL 生成憑據]**.

![突出顯示「Credentials（憑據）」頁簽和「Generate（生成）」憑據的「Querys（查詢）」儀表板。](../images/ui/credentials/generate-credentials.png)

此時將顯示一個對話框，允許您生成憑據。 若要建立未到期的憑證，您必須提供下列詳細資料：

- **[!UICONTROL 名稱]**:您正在生成的憑據的名稱。
- **[!UICONTROL 說明]**:（選用）您要產生的憑證說明。
- **[!UICONTROL 指派給]**:將為其分配憑據的用戶。 此值應為建立憑證之使用者的電子郵件地址。
- **[!UICONTROL 密碼]** （可選）您的憑證的選用密碼。 如果未設定密碼，Adobe將自動為您生成密碼。

提供所有必要的詳細資訊後，請選取 **[!UICONTROL 生成憑據]** 來產生您的憑證。

![將突出顯示「生成憑據」對話框。](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>當 **[!UICONTROL 生成憑據]** 選取後，配置JSON檔案會下載到您的本地電腦。 因為Adobe有 **not** 記錄生成的憑據，您必須安全地儲存下載的檔案並保留憑據的記錄。
>
>此外，如果90天內未使用憑證，則會清除憑證。

設定JSON檔案包含技術帳戶名稱、技術帳戶ID和憑證等資訊。 以下列格式提供。

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

儲存產生的憑證後，請選取 **[!UICONTROL 關閉]**. 您現在可以看到所有未到期憑證的清單。

![突出顯示了「查詢儀表板憑據」頁簽的「非到期憑據」部分。](../images/ui/credentials/list-credentials.png)

您可以編輯或刪除未到期的憑證。 要編輯未到期的憑據，請選擇鉛筆表徵圖(![鉛筆圖示。](../images/ui/credentials/edit-icon.png))。要刪除未到期的憑據，請選擇刪除表徵圖(![垃圾桶圖示。](../images/ui/credentials/delete-icon.png))。

編輯未到期的憑證時，會出現強制回應視窗。 您可以提供下列詳細資料以進行更新：

- **[!UICONTROL 名稱]**:您正在生成的憑據的名稱。
- **[!UICONTROL 說明]**:（選用）您要產生的憑證說明。
- **[!UICONTROL 指派給]**:將為其分配憑據的用戶。 此值應為建立憑證之使用者的電子郵件地址。

![「更新帳戶」對話框。](../images/ui/credentials/update-credentials.png)

提供所有必要的詳細資訊後，請選取 **[!UICONTROL 更新帳戶]** 完成憑據的更新。

## 使用憑據連接到外部客戶端 {#use-credential-to-connect}

您可以使用即將到期或未到期的憑據來連接外部客戶端，如Aqua Data Studio、Looker或Power BI。 這些憑證的輸入方法會因外部用戶端而異。 請參閱外部客戶端的文檔，以了解有關使用這些憑據的具體說明。

影像會指出UI中找到之每個參數的位置，但非即將到期憑證的密碼除外。 雖然其JSON設定檔案提供了非到期憑證，但您可以在 **憑證** 標籤。

![「查詢工作區憑據」頁簽，其中「即將到期的憑據」部分突出顯示。](../images/ui/credentials/expiring-credentials.png)

下表概述了連接到外部客戶端通常所需的參數。

>[!NOTE]
>
>使用非到期憑證連線至主機時，仍需使用 [!UICONTROL 即將到期的憑據] 區段，但密碼和使用者名稱除外。
>輸入用戶名和密碼的格式使用冒號分隔值，如本示例所示 `username:{your_username}` 和 `password:{password_string}`.

| 參數 | 說明 |
|---|---|
| **伺服器/主機** | 要連接的伺服器/主機的名稱。 <ul><li>此值用於即將到期的憑據和未到期的憑據，其形式為 `server.adobe.io`. 值位於 **[!UICONTROL 主機]** 在 [!UICONTROL 即將到期的憑據] 區段。</ul></li> |
| **埠** | 要連接的伺服器/主機的埠。 <ul><li>此值用於即將到期的憑據和非即將到期的憑據，可在以下找到 **[!UICONTROL 埠]** 在 [!UICONTROL 即將到期的憑據] 區段。 埠的範例值為 `80`.</ul></li> |
| **資料庫** | 您要連接的資料庫。 <ul><li>此值用於即將到期的憑證和非即將到期的憑證，可在 **[!UICONTROL 資料庫]** 在 [!UICONTROL 即將到期的憑據] 區段。 資料庫的範例值為 `prod:all`.</ul></li> |
| **使用者名稱** | 連接到外部客戶端的用戶的用戶名。 <ul><li>此值用於即將到期的憑據和非即將到期的憑據。 其格式為字母數字字串 `@AdobeOrg`. 此值位於 **[!UICONTROL 使用者名稱]**.</li></ul> |
| **密碼** | 連接到外部客戶端的用戶的密碼。 <ul><li>如果您使用即將到期的憑證，可在 **[!UICONTROL 密碼]** 在 [!UICONTROL 即將到期的憑據] 區段。</li><li>如果您使用的是未到期的憑證，此值是來自technicalAccountID的串連引數，以及來自設定JSON檔案的憑證。 密碼值採用以下形式： `{technicalAccountId}:{credential}`.</li></ul> |

## 後續步驟

現在您已了解過期和未過期的憑證如何運作，您可以使用這些憑證連線至外部用戶端。 有關外部客戶端的詳細資訊，請閱讀 [將客戶端連接到查詢服務指南](../clients/overview.md).
