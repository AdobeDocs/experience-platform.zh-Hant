---
title: 使用Python和SQLAlchemy管理平台資料
description: 瞭解如何使用SQLAlchemy來使用Python而不是SQL管理平台資料。
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: 8644b78c947fd015f6a169c9440b8d1df71e5e17
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 使用 [!DNL Python] 和 [!DNL SQLAlchemy]

瞭解如何使用SQLAlchemy來更靈活地管理您的Adobe Experience Platform資料。 對於不熟悉SQL的用戶，SQLAlchemy在使用關係資料庫時可以大大縮短開發時間。 本文檔提供了連接的說明和示例 [!DNL SQLAlchemy] 查詢服務並開始使用Python與資料庫交互。

[!DNL SQLAlchemy] 是對象關係映射器(ORM)和 [!DNL Python] 可將儲存在SQL資料庫中的資料傳輸到 [!DNL Python] 對象。 然後，可以使用 [!DNL Python] 代碼。 這樣就不再需要僅使用PSQL管理資料。

## 快速入門

獲取連接所需的憑據 [!DNL SQLAlchemy] 要Experience Platform，您必須有權訪問平台UI中的「查詢」工作區。 如果您當前沒有訪問「查詢」工作區的權限，請與組織管理員聯繫。

## [!DNL Query Service] 憑據 {#credentials}

要查找憑據，請登錄到平台UI並選擇 **[!UICONTROL 查詢]** 從左導航，然後 **[!UICONTROL 憑據]**。 有關如何查找登錄憑據的完整說明，請閱讀 [憑據指南](../ui/credentials.md)。

![突出顯示了Query Service的憑據過期的憑據頁籤。](../images/use-cases/credentials.png)

雖然埠80是與查詢服務連接的推薦埠，但您也可以使用埠5432。

>[!IMPORTANT]
>
>如果您使用過期憑據（如上圖所示）連接到查詢服務，則連接的會話壽命將在組織設定中定義的設定時間段後過期。 預設情況下，此期間為24小時。 請參閱文檔以瞭解如何 [連接具有非過期憑據的客戶端](../ui/credentials.md#non-expiring-credentials)，或如何 [更改過期憑據的會話壽命](../ui/credentials.md#expiring-credentials)。

一旦您有權訪問QS憑據，請開啟 [!DNL Python] 編輯。

### 將憑據儲存在 [!DNL Python] {#store-credentials}

在 [!DNL Python] 編輯器，導入 `urllib.parse.quote` 將每個憑據變數保存為參數。 的 `urllib.parse` 模組提供了將URL字串拆分為元件的標準介面。 引號函式將替換URL字串中的特殊字元，以使資料安全地用作URL元件。 下面是所需代碼的示例：

>[!TIP]
>
>使用 [!DNL Python]&#39;s的三引號以輸入多行密碼字串。

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
>您為連接提供的密碼 [!DNL SQLAlchemy] 到Experience Platform將在您使用過期憑據時過期。 查看 [憑據部分](#credentials) 的子菜單。

### 建立引擎實例 [#create引擎]

建立變數後，導入 `create_engine` 函式，並建立一個字串以編譯和格式化SQLAlchemy中的查詢服務憑據。 的 `create_engine` 然後使用函式來構造引擎實例。

>[!NOTE]
>
>`create_engine`返回引擎的實例。 但是，在調用需要連接的查詢之前，它不會開啟到查詢服務的連接。

使用第三方客戶端訪問平台時必須啟用SSL。 作為引擎的一部分，使用 `connect_args` 輸入其他關鍵字參數。 建議您將SSL模式設定為 `require`。 查看 [SSL模式文檔](../clients/ssl-modes.md) 的子菜單。

下面的示例顯示 [!DNL Python] 初始化引擎和連接字串所需的代碼。

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
>您為連接提供的密碼 [!DNL SQLAlchemy] 到Experience Platform將在您使用過期憑據時過期。 查看 [憑據部分](#credentials) 的子菜單。

您現在可以使用 [!DNL Python]。 下面所示的示例返回Query Service表名的陣列。

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
