---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢；查詢編輯器；查詢編輯器；查詢編輯器；
solution: Experience Platform
title: 查詢服務認證指南
description: Adobe Experience Platform查詢服務提供使用者介面，可用於寫入和執行查詢、檢視以前執行的查詢，以及存取組織內使用者儲存的查詢。
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: ba4ff2715d4e3eb71377542ab2361b967cd3ac11
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 1%

---

# 認證指南

Adobe Experience Platform查詢服務可讓您與外部使用者端連線。 您可以使用即將到期的認證或不即將到期的認證來連線到這些外部使用者端。

>[!NOTE]
>
>認證面板不會自動供所有使用者使用。 請聯絡您的Adobe客戶團隊以要求 [!UICONTROL 認證] 索引標籤，以在您需要時包含在查詢服務工作區中。 如有要求，此變更會涵蓋整個組織，並由Adobe的工程團隊執行。 這不是由使用者控制的設定。

## 到期的認證 {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="用戶端的 SSL 模式"
>abstract="必須在連線至查詢服務的用戶端中啟用 SSL。確保 SSL 模式設定為「要求」。"

您可以使用即將到期的認證來快速設定與外部使用者端的連線。

![「查詢儀表板認證」索引標籤中會醒目顯示「即將到期的認證」區段。](../images/ui/credentials/expiring-credentials.png)

此 **[!UICONTROL 即將到期的認證]** 一節提供下列資訊：

- **[!UICONTROL 主機]**：要將使用者端連線至的主機名稱。 這會合併您的組織名稱，如同在Platform UI的頂端功能區中所示。
- **[!UICONTROL 連線埠]**：要連線之主機的連線埠號碼。
- **[!UICONTROL 資料庫]**：要連線使用者端的資料庫名稱。
- **[!UICONTROL 使用者名稱]**：用來連線至查詢服務的使用者名稱。
- **[!UICONTROL 密碼]**：用來連線至查詢服務的密碼。 UI中的密碼已進行雜湊處理，以提高安全性。 選取復製圖示(![復製圖示。](../images/ui/credentials/copy-icon.png))，將您完整的未雜湊認證複製到剪貼簿。
- **[!UICONTROL PSQL命令]**：自動插入所有相關資訊的命令，以供您在命令列上使用PSQL連線至Query Service。
- **[!UICONTROL 過期]**：即將到期的認證的到期日期和時間。 權杖的預設有效期間為24小時，但可在Admin Console的進階設定中變更。

>[!TIP]
>
>若要變更您與「查詢服務」之到期認證連線的工作階段期限，請瀏覽至 [Admin Console](https://adminconsole.adobe.com/) 並選取下列熒幕選項： **設定** > **隱私權與安全性** > **驗證設定** > **進階設定** > **最長工作階段期限**.
>
>![Admin Console設定索引標籤中會醒目提示隱私權與安全性、驗證設定和最長工作階段期限。](../images/ui/credentials/max-session-life.png)
>
>請參閱Adobe說明檔案，以瞭解有關 [進階設定](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) 由Admin Console提供。

### 連線至查詢工作階段中的Customer Journey Analytics資料 {#connect-to-customer-journey-analytics}

搭配使用Customer Journey AnalyticsBI擴充功能與Power BI或Tableau來存取您的Customer Journey Analytics [資料檢視](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views) 使用SQL。 藉由整合Query Service與BI擴充功能，您可以直接在Query Service工作階段中存取資料檢視。 此整合簡化了使用查詢服務作為其PostgreSQL介面的BI工具功能。 此功能消除了在BI工具中重複資料檢視的需求，確保跨平台的一致報告，並簡化了Customer Journey Analytics資料與BI平台中其他來源的整合。

請參閱檔案以瞭解如何 [將Query Service連線到各種案頭使用者端應用程式](../clients/overview.md) 例如 [Power BI](../clients/power-bi.md) 或 [Tableau](../clients/tableau.md)

>[!IMPORTANT]
>
>需要Customer Journey Analytics工作區專案和資料檢視才能使用此功能。

若要以Power BI或Tableau存取您的Customer Journey Analytics資料，請選取 [!UICONTROL 資料庫] 下拉式功能表，然後選取 `prod:cja` 可用選項中的。 接下來，複製您的 [!DNL Postgres] 用於您的Power BI或Tableau組態中的證明資料引數（主機、連線埠、資料庫、使用者名稱等）。

![反白顯示資料庫下拉式清單的[查詢服務認證]索引標籤。](../images/ui/credentials/database-dropdown.png)

>[!NOTE]
>
>當您連線Power BI或Tableau以Customer Journey Analytics時，會使用查詢服務「並行工作階段」權益。 如果需要其他工作階段和查詢，可購買額外的臨時查詢使用者套件附加元件，以取得五個額外的並行工作階段和一個額外的並行查詢。

您也可以直接從Query Editor或Postgres CLI存取您的Customer Journey Analytics資料。 若要這麼做，請參考 `cja` 資料庫寫入您的查詢。 請參閱查詢編輯器 [查詢撰寫指南](./user-guide.md#query-authoring) 有關如何寫入、執行和儲存查詢的詳細資訊。

請參閱 [BI擴充功能指南](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/bi-extension) 以取得使用SQL存取Customer Journey Analytics資料檢視的完整指示。

## 不會到期的認證 {#non-expiring-credentials}

您可以使用不會到期的認證來設定與外部使用者端之間更永久的連線。

>[!NOTE]
>
>不會到期的認證有下列限制：<br><ul><li>使用者必須以包含下列專案之使用者名稱和密碼登入： `{technicalAccountId}:{credential}`. 如需詳細資訊，請參閱 [產生認證](#generate-credentials) 區段。</li><li>建立到期的認證後，會建立具有一組基本許可權的新角色，讓使用者檢視結構描述和資料集。 「管理查詢」許可權也會指派給此角色，以搭配查詢服務使用。</li><li>列出查詢物件時，協力廠商使用者端可能會以與預期不同的方式執行。 例如，某些協力廠商使用者端，例如 [!DNL DB Visualizer] 不會在左側面板中顯示檢視名稱。 不過，若在SELECT查詢中呼叫，則可存取檢視名稱。 同樣地， [!DNL PowerUI] 可能不會列出透過SQL建立的、要選取用來建立儀表板的暫存檢視。</li></ul>

### 先決條件

您必須先在Adobe Admin Console中完成下列步驟，才能產生不會到期的認證：

1. 登入 [Adobe Admin Console](https://adminconsole.adobe.com/) 並從上方導覽列中選取相關組織。
2. [選取產品設定檔。](../../access-control/ui/browse.md)
3. [設定兩者 **沙箱** 和 **管理查詢服務整合** 許可權](../../access-control/ui/permissions.md) 用於產品設定檔。
4. [將新使用者新增至產品設定檔](../../access-control/ui/users.md) 因此它們會被授予其設定的許可權。
5. [將使用者新增為產品設定檔管理員](https://helpx.adobe.com/tw/enterprise/using/manage-product-profiles.html) 允許為任何使用中產品設定檔建立帳戶。
6. [將使用者新增為產品設定檔開發人員](https://helpx.adobe.com/jp/enterprise/using/manage-developers.html) 以便建立整合。

若要深入瞭解如何指派許可權，請閱讀以下檔案： [存取控制](../../access-control/home.md).

現在，所有必要的許可權已在Adobe Developer Console中設定，讓使用者能使用即將到期的認證功能。

### 產生認證 {#generate-credentials}

若要建立一組不會到期的認證，請返回平台UI並選取 **[!UICONTROL 查詢]** 從左側導覽存取 [!UICONTROL 查詢] 工作區。 接下來，選取 **[!UICONTROL 認證]** 索引標籤後接 **[!UICONTROL 產生認證]**.

![「查詢」控制面板的「認證」標籤和「產生認證」都反白顯示。](../images/ui/credentials/generate-credentials.png)

會出現一個對話方塊，讓您產生認證。 若要建立不會到期的認證，您必須提供下列詳細資料：

- **[!UICONTROL 名稱]**：您產生的認證名稱。
- **[!UICONTROL 說明]**：（選用）您產生的認證說明。
- **[!UICONTROL 指派給]**：將接受認證指派的使用者。 此值應為建立認證之使用者的電子郵件地址。
- **[!UICONTROL 密碼]** （選用）憑證的選用密碼。 如果未設定密碼，Adobe會自動為您產生密碼。

提供所有必要的詳細資料後，請選取 **[!UICONTROL 產生認證]** 以產生您的認證。

![「產生認證」對話方塊會反白顯示。](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>時間 **[!UICONTROL 產生認證]** ，則會將設定JSON檔案下載至您的本機電腦。 因為Adobe會 **非** 記錄產生的認證，您必須安全地儲存下載的檔案，並保留認證的記錄。
>
>此外，如果認證在90天內未使用，認證將會被清除。

設定JSON檔案包含技術帳戶名稱、技術帳戶ID和認證等資訊。 提供下列格式。

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

儲存您產生的認證後，請選取「 」 **[!UICONTROL 關閉]**. 您現在可以看到所有不會到期的認證清單。

![「查詢儀表板認證」索引標籤中反白了「不會到期的認證」區段。](../images/ui/credentials/list-credentials.png)

您可以編輯或刪除不會到期的認證。 若要編輯不會到期的認證，請選取鉛筆圖示(![鉛筆圖示。](../images/ui/credentials/edit-icon.png))。若要刪除不會到期的認證，請選取刪除圖示(![垃圾桶圖示。](../images/ui/credentials/delete-icon.png))。

編輯不會到期的認證時，強制回應視窗會出現。 您可以提供下列詳細資料以進行更新：

- **[!UICONTROL 名稱]**：您產生的認證名稱。
- **[!UICONTROL 說明]**：（選用）您產生的認證說明。
- **[!UICONTROL 指派給]**：將接受認證指派的使用者。 此值應為建立認證之使用者的電子郵件地址。

![更新帳戶對話方塊。](../images/ui/credentials/update-credentials.png)

提供所有必要的詳細資料後，請選取 **[!UICONTROL 更新帳戶]** 以完成認證的更新。

## 使用認證來連線到外部使用者端 {#use-credential-to-connect}

您可以使用到期或不到期的認證來連線至外部使用者端，例如Aqua Data Studio、Looker或Power BI。 這些憑證的輸入方法會因外部使用者端而異。 請參閱外部使用者端檔案，取得使用這些憑證的特定指示。

此影像會指出在UI中找到的每個引數的位置，但不包括不會到期的認證的密碼。 雖然不會到期的認證是由其JSON設定檔案所提供，但您可以在下方檢視即將到期的認證 **認證** UI中的Tab鍵。

![「查詢」工作區的「認證」索引標籤中，「到期的認證」區段會反白顯示。](../images/ui/credentials/expiring-credentials.png)

下表概述連線至外部使用者端時通常所需的引數。

>[!NOTE]
>
>使用不會到期的證明資料連線到主機時，仍需使用 [!UICONTROL 即將到期的認證] 區段，但密碼和使用者名稱除外。
>輸入使用者名稱和密碼的格式使用冒號分隔值，如本範例所示 `username:{your_username}` 和 `password:{password_string}`.

| 參數 | 說明 | 範例 |
|---|---|---|
| **伺服器/主機** | 您連線的伺服器/主機名稱。 <ul><li>此值會用於即將到期的認證和不即將到期的認證，其形式為 `server.adobe.io`. 值位於 **[!UICONTROL 主機]** 在 [!UICONTROL 即將到期的認證] 區段。</ul></li> | `acme.platform.adobe.io` |
| **連線埠** | 您連線的伺服器/主機連線埠。 <ul><li>此值會用於即將到期的認證和不即將到期的認證，並可在下列位置找到： **[!UICONTROL 連線埠]** 在 [!UICONTROL 即將到期的認證] 區段。</ul></li> | `80` |
| **資料庫** | 您正在連線的資料庫。 <ul><li>此值會用於即將到期的認證和不即將到期的認證，並會發現於 **[!UICONTROL 資料庫]** 在 [!UICONTROL 即將到期的認證] 區段。 </ul></li> | `prod:all` |
| **使用者名稱** | 連線到外部使用者端的使用者使用者名稱。 <ul><li>此值會用於即將到期的認證和不即將到期的認證。 它以前採用英數字串的形式 `@AdobeOrg`. 此值位於 **[!UICONTROL 使用者名稱]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **密碼** | 連線到外部使用者端的使用者密碼。 <ul><li>如果您使用即將到期的認證，您可在下列位置找到： **[!UICONTROL 密碼]** 在 [!UICONTROL 即將到期的認證] 區段。</li><li>如果您使用不會到期的認證，此值是來自technicalAccountID的串連引數，以及從設定JSON檔案取得的認證。 密碼值採用以下形式： `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>即將到期的認證密碼超過一千個字元的英數字串。 將不會提供範例。</li><li>不會到期的認證密碼如下：<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## 後續步驟

現在您已瞭解即將到期和未到期的認證的運作方式，您可以使用這些認證來連線至外部使用者端。 如需有關外部使用者端的詳細資訊，請參閱 [將使用者端連線至查詢服務指南](../clients/overview.md).
