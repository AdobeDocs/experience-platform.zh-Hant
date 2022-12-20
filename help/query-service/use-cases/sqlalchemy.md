---
title: 使用Python和SQLAlchemy管理平台資料
description: 了解如何使用SQLAlchemy來使用Python（而非SQL）管理您的平台資料。
source-git-commit: 6b7de4236982181eaac2aa37d525604cba31198e
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 使用管理平台資料 [!DNL Python] 和 [!DNL SQLAlchemy]

了解如何使用SQLAlchemy，以在管理Adobe Experience Platform資料方面獲得更大的靈活性。 對於不熟悉SQL的用戶，SQLAlchemy可以大大改進使用關係資料庫時的開發時間。 本檔案提供連線的指示和範例 [!DNL SQLAlchemy] 查詢服務，並開始使用Python與資料庫交互。

[!DNL SQLAlchemy] 是對象關係映射器(ORM)和 [!DNL Python] 可將儲存在SQL資料庫中的資料傳輸到 [!DNL Python] 對象。 然後，您就可以使用 [!DNL Python] 程式碼。 這樣就無需僅使用PSQL管理資料。

## 快速入門

獲取連接所需的憑據 [!DNL SQLAlchemy] 若要Experience Platform，您必須擁有平台UI中查詢工作區的存取權。 如果您目前沒有查詢工作區的存取權，請聯絡您的組織管理員。

## [!DNL Query Service] 憑據 {#credentials}

若要尋找憑證，請登入Platform UI並選取 **[!UICONTROL 查詢]** 從左側導覽，後跟 **[!UICONTROL 憑證]**. 有關如何查找登錄憑據的完整說明，請閱讀 [認證指南](../ui/credentials.md).

![已突出顯示查詢服務的憑據頁簽，其憑據即將到期。](../images/use-cases/credentials.png)

雖然埠80是連接查詢服務的建議埠，但您也可以使用埠5432。

>[!IMPORTANT]
>
>如果您使用即將到期的憑證（如上圖所示）來連線至Query Service，則連線的工作階段期限將在貴組織設定中定義的設定時段後過期。 預設情況下，此期間為24小時。 請參閱檔案以了解如何 [連接具有未到期憑據的客戶端](../ui/credentials.md#non-expiring-credentials)，或如何 [更改即將到期的憑據的會話期限](../ui/credentials.md#expiring-credentials).

訪問QS憑據後，請開啟 [!DNL Python] 選擇的編輯。

### 將憑證儲存在 [!DNL Python] {#store-credentials}

在 [!DNL Python] 編輯器，匯入 `urllib.parse.quote` 程式庫，並將每個憑據變數儲存為參數。 此 `urllib.parse` 模組提供標準介面，將URL字串分割為元件。 引號函式會取代URL字串中的特殊字元，以確保資料安全地作為URL元件使用。 以下是必要程式碼的範例：

>[!TIP]
>
>使用 [!DNL Python]輸入多行密碼字串的三引號。

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>您為連接提供的密碼 [!DNL SQLAlchemy] 若您使用即將到期的憑證，Experience Platform將會過期。 請參閱 [憑據部分](#credentials) 以取得更多資訊。

### 建立引擎例項 [#create-engine]

建立變數後，請匯入 `create_engine` 函式和建立字串，以在SQLAlchemy中編譯和格式化查詢服務憑據。 此 `create_engine` 函式被用來構造引擎實例。

>[!NOTE]
>
>`create_engine`傳回引擎的例項。 但是，在調用需要連接的查詢之前，它不會開啟到查詢服務的連接。

使用協力廠商用戶端存取Platform時，必須啟用SSL。 在引擎中，請使用 `connect_args` 輸入其他關鍵字參數。 建議您將SSL模式設為 `require`. 請參閱 [SSL模式檔案](../clients/ssl-modes.md) 以取得接受值的詳細資訊。

以下範例顯示 [!DNL Python] 初始化引擎和連線字串所需的程式碼。

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>您為連接提供的密碼 [!DNL SQLAlchemy] 若您使用即將到期的憑證，Experience Platform將會過期。 請參閱 [憑據部分](#credentials) 以取得更多資訊。

您現在可以使用 [!DNL Python]. 以下示例返回Query Service表名的陣列。

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
