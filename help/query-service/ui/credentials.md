---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢編輯器；查詢編輯器；查詢編輯器；
solution: Experience Platform
title: Query Service UI指南
topic-legacy: guide
description: Adobe Experience Platform查詢服務提供可用來撰寫和執行查詢、檢視先前執行的查詢，以及存取由您IMS組織內的使用者儲存的查詢的使用者介面。
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

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

要建立一組未到期的憑據，請選擇&#x200B;**[!UICONTROL 生成憑據]**。

>[!NOTE]
>
>您必須同時擁有&#x200B;**沙箱**&#x200B;和&#x200B;**管理查詢服務整合**&#x200B;權限，才能建立未到期的憑證。 若要了解如何指派這些權限，請參閱[存取控制](../../access-control/home.md)上的檔案。

![](../images/ui/credentials/generate-credentials.png)

出現「Generate credentials modal（生成憑據模式）」。 若要建立非到期憑證，您必須提供下列詳細資料：

- **[!UICONTROL 名稱]**:您正在生成的憑據的名稱。
- **[!UICONTROL 說明]**:（選用）您要產生的憑證說明。
- **[!UICONTROL 指派給]**:將分配給憑據的用戶。此值應為建立憑證之使用者的電子郵件地址。
- **[!UICONTROL 密碼]** （選用）您憑證的選用密碼。如果未設定密碼，Adobe將自動為您生成密碼。

提供所有所需詳細資訊後，請選擇&#x200B;**[!UICONTROL 生成憑據]**&#x200B;以生成憑據。

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>選擇&#x200B;**[!UICONTROL 生成憑據]**&#x200B;按鈕後，配置檔案將包含諸如技術帳戶名、技術帳戶ID和憑據等資訊。 由於Adobe **不**&#x200B;記錄生成的憑據，因此您&#x200B;**必須**&#x200B;安全地儲存下載的檔案並保留憑據的記錄。
>
>此外，如果90天內未使用憑證，則會剪下憑證。

現在您已儲存產生的憑證，請選取&#x200B;**[!UICONTROL Close]**。 您現在可以看到所有未到期憑證的清單。

![](../images/ui/credentials/list-credentials.png)

您可以編輯或刪除未到期的憑證。 要編輯未到期的憑據，請選擇鉛筆表徵圖(![](../images/ui/credentials/edit-icon.png))。 要刪除未到期的憑據，請選擇刪除表徵圖(![](../images/ui/credentials/delete-icon.png))。

編輯未到期的憑證時，會出現強制回應視窗。 您可以提供下列詳細資料以進行更新：

- **[!UICONTROL 名稱]**:您正在生成的憑據的名稱。
- **[!UICONTROL 說明]**:（選用）您要產生的憑證說明。
- **[!UICONTROL 指派給]**:將分配給憑據的用戶。此值應為建立憑證之使用者的電子郵件地址。

![](../images/ui/credentials/update-credentials.png)

提供所有必要的詳細資訊後，請選擇&#x200B;**[!UICONTROL 更新帳戶]**&#x200B;以完成憑據的更新。

## 使用憑據連接到外部客戶端

您可以使用即將到期或未到期的憑據來連接外部客戶端，如Aqua Data Studio、Looker或Power BI。

連線至這些外部用戶端時，您通常需要包含下列資訊：

- **伺服器/主機**:要連接的伺服器/主機的名稱。此值的形式為`server.adobe.io`，可在即將到期的憑證區段的&#x200B;**[!UICONTROL Host]**&#x200B;下找到。
- **埠**:要連接的伺服器/主機的埠。此值可在即將到期的憑證區段的&#x200B;**[!UICONTROL Port]**&#x200B;下找到。 埠的範例值為`80`。
- **使用者名稱**:連接到外部客戶端的用戶的用戶名。此格式為`ID@AdobeOrg`，可在即將到期的憑證區段的&#x200B;**[!UICONTROL 使用者名稱]**&#x200B;下找到。
- **密碼**:連接到外部客戶端的用戶的密碼。如果您使用即將到期的憑證，可在即將到期的憑證區段的&#x200B;**[!UICONTROL Password]**&#x200B;下找到。 如果您使用的是未到期的憑證，此值由技術帳戶ID和憑證組成，格式為：`technicalAccountId:credential`。
- **資料庫**:您要連接的資料庫。此值可在即將到期的憑據區段的&#x200B;**[!UICONTROL Database]**&#x200B;下找到。 資料庫的範例值為`prod:all`。

## 後續步驟

現在您已了解過期和未過期的憑證如何運作，您可以使用這些憑證連線至外部用戶端。 有關外部客戶端的詳細資訊，請參閱[將客戶端連接到查詢服務指南](../clients/overview.md)。