---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢編輯器；查詢編輯器；查詢編輯器；查詢編輯器；
solution: Experience Platform
title: 查詢服務憑據指南
topic-legacy: guide
description: Adobe Experience Platform查詢服務提供一個用戶介面，可用於編寫和執行查詢、查看以前執行的查詢以及訪問IMS組織內用戶保存的查詢。
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 1%

---

# 憑據指南

Adobe Experience Platform查詢服務允許您與外部客戶端連接。 您可以使用過期憑據或非過期憑據連接到這些外部客戶端。

## 過期憑據

您可以使用過期憑據快速設定到外部客戶端的連接。

![「查詢」面板「身份證明」頁籤，其中「過期身份證明」部分突出顯示。](../images/ui/credentials/expiring-credentials.png)

的 **[!UICONTROL 過期憑據]** 部分提供了以下資訊：

- **[!UICONTROL 主機]**:要連接的主機的名稱。 要連接到查詢服務，這將包括您當前使用的IMS組織的名稱。
- **[!UICONTROL 埠]**:要連接的主機的埠號。
- **[!UICONTROL 資料庫]**:要連接到的資料庫的名稱。
- **[!UICONTROL 用戶名]**:用於連接到查詢服務的用戶名。
- **[!UICONTROL 密碼]**:用於連接到查詢服務的密碼。
- **[!UICONTROL PSQL命令]**:一個命令，它自動插入了所有相關資訊，以便您使用命令行上的PSQL連接到查詢服務。
- **[!UICONTROL 過期]**:過期憑據的到期日期。 憑據在生成後24小時過期。

## 未過期的憑據 {#non-expiring-credentials}

可以使用非過期憑據設定到外部客戶端的更永久連接。

### 先決條件

在生成未過期的憑據之前，必須在Adobe Admin Console完成以下步驟：

1. 登錄 [Adobe Admin Console](https://adminconsole.adobe.com/) 並從頂部導航欄中選擇相關組織。
2. [選擇產品配置檔案。](../../access-control/ui/browse.md)
3. [配置 **沙箱** 和 **管理查詢服務整合** 權限](../../access-control/ui/permissions.md) 的下界。
4. [將新用戶添加到產品配置檔案](../../access-control/ui/users.md) 因此它們被授予其配置的權限。
5. [將用戶添加為產品配置檔案管理員](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) 允許為任何活動產品配置檔案建立帳戶。
6. [將用戶添加為產品配置檔案開發人員](https://helpx.adobe.com/tw/enterprise/using/manage-developers.html) 以建立整合。

要瞭解有關如何分配權限的詳細資訊，請閱讀上的文檔 [訪問控制](../../access-control/home.md)。

所有所需權限現在都在Adobe Developer控制台中配置，以便用戶使用過期的憑據功能。

### 生成憑據

要建立一組未過期的憑據，請返回平台UI並選擇 **[!UICONTROL 查詢]** 從左側導航 [!UICONTROL 查詢] 工作區。 接下來，選擇 **[!UICONTROL 憑據]** 後跟 **[!UICONTROL 生成憑據]**。

![「查詢」面板中的「身份證明」頁籤和「生成身份證明」突出顯示。](../images/ui/credentials/generate-credentials.png)

將顯示一個對話框，允許您生成憑據。 要建立未過期的憑據，必須提供以下詳細資訊：

- **[!UICONTROL 名稱]**:您正在生成的憑據的名稱。
- **[!UICONTROL 說明]**:（可選）您正在生成的憑據的說明。
- **[!UICONTROL 分配給]**:將為其分配憑據的用戶。 此值應為建立憑據的用戶的電子郵件地址。
- **[!UICONTROL 密碼]** （可選）憑據的可選密碼。 如果未設定密碼，Adobe將自動為您生成密碼。

提供所有必需的詳細資訊後，選擇 **[!UICONTROL 生成憑據]** 生成憑據。

![「生成憑據」對話框突出顯示。](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>當 **[!UICONTROL 生成憑據]** 選中後，配置JSON檔案將下載到您的本地電腦。 因為Adobe **不** 記錄生成的憑據，必須安全地儲存下載的檔案並保留憑據的記錄。
>
>此外，如果憑據在90天內未使用，則會刪除憑據。

配置JSON檔案包含技術帳戶名、技術帳戶ID和憑據等資訊。 它以下列格式提供。

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

保存生成的憑據後，選擇 **[!UICONTROL 關閉]**。 您現在可以看到所有未過期的憑據的清單。

![「查詢」面板「身份證明」頁籤，「未過期身份證明」部分已展開。](../images/ui/credentials/list-credentials.png)

您可以編輯或刪除未過期的憑據。 要編輯未過期的憑據，請選擇鉛筆表徵圖(![](../images/ui/credentials/edit-icon.png))。 要刪除未過期的憑據，請選擇刪除表徵圖(![](../images/ui/credentials/delete-icon.png))。

編輯未過期的憑據時，將顯示模式。 您可以提供以下詳細資訊以進行更新：

- **[!UICONTROL 名稱]**:您正在生成的憑據的名稱。
- **[!UICONTROL 說明]**:（可選）您正在生成的憑據的說明。
- **[!UICONTROL 分配給]**:將為其分配憑據的用戶。 此值應為建立憑據的用戶的電子郵件地址。

![「更新帳戶」對話框。](../images/ui/credentials/update-credentials.png)

提供所有必需的詳細資訊後，選擇 **[!UICONTROL 更新帳戶]** 完成對憑據的更新。

## 使用憑據連接到外部客戶端

您可以使用過期或未過期的憑據與外部客戶端(如Aqua Data Studio、Looker或Power BI)連接。 這些憑據的輸入方法會因外部客戶端而異。 有關使用這些憑據的具體說明，請參閱外部客戶的文檔。

該影像指示在UI中找到的每個參數的位置，但不包括未過期憑據的密碼。 當非過期憑據由其JSON配置檔案提供時，您可以在 **憑據** 頁籤

![](../images/ui/credentials/expiring-credentials.png)

下表概述了通常連接到外部客戶端所需的參數。

>[!NOTE]
>
>使用未過期的憑據連接到主機時，仍需要使用中列出的所有參數 [!UICONTROL 過期憑據] 除密碼和用戶名外。

| 參數 | 說明 |
|---|---|
| **伺服器/主機** | 要連接的伺服器/主機的名稱。 <ul><li>此值用於過期的憑據和非過期的憑據，其形式為 `server.adobe.io`。 值位於 **[!UICONTROL 主機]** 的 [!UICONTROL 過期憑據] 的子菜單。</ul></li> |
| **埠** | 要連接的伺服器/主機的埠。 <ul><li>此值用於過期憑據和非過期憑據，可在 **[!UICONTROL 埠]** 的 [!UICONTROL 過期憑據] 的子菜單。 埠的示例值為 `80`。</ul></li> |
| **資料庫** | 要連接的資料庫。 <ul><li>此值用於過期憑據和非過期憑據，在 **[!UICONTROL 資料庫]** 的 [!UICONTROL 過期憑據] 的子菜單。 資料庫的示例值為 `prod:all`。</ul></li> |
| **用戶名** | 連接到外部客戶端的用戶的用戶名。 <ul><li>此值用於過期憑據和非過期憑據。 它採用字母數字字串的形式 `@AdobeOrg`。 此值位於 **[!UICONTROL 用戶名]**。</li></ul> |
| **密碼** | 連接到外部客戶端的用戶的密碼。 <ul><li>如果您正在使用過期憑據，則可以在 **[!UICONTROL 密碼]** 在 [!UICONTROL 過期憑據] 的子菜單。</li><li>如果您使用的是非過期憑據，則此值是technicalAccountID的級連參數和從配置JSON檔案獲取的憑據。 密碼值採用以下形式： `{technicalAccountId}:{credential}`。</li></ul> |

## 後續步驟

現在，您已經瞭解過期和未過期的憑據的工作原理，可以使用這些憑據連接到外部客戶端。 有關外部客戶端的詳細資訊，請閱讀 [將客戶端連接到查詢服務指南](../clients/overview.md)。
