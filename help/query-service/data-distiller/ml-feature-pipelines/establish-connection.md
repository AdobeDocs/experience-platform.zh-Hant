---
title: 從Jupyter筆記本連線至Data Distiller
description: 瞭解如何從Jupyter Notebook連線至Data Distiller。
source-git-commit: 12926f36514d289449cf0d141b5828df3fac37c2
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 1%

---

# 從Jupyter筆記型電腦連線到DD

若要使用高價值客戶體驗資料讓您的機器學習管道更為豐富，您必須先從Jupyter Notebooks連線至Data Distiller。 本檔案說明在機器學習環境中，從Python筆記本連線至Data Distiller的步驟。

## 快速入門

本指南假設您熟悉互動式Python筆記型電腦，且可存取筆記型電腦環境。 筆記本可在雲端型機器學習環境中託管，或在本機使用 [Jupyter Notebook](https://jupyter.org/).

### 取得連線認證

若要連線至Data Distiller和其他Adobe Experience Platform服務，您需要Experience Platform API認證。 API認證可在以下位置建立：  [Adobe Developer Console](https://developer.adobe.com/console/home) 由擁有該Experience Platform開發人員存取許可權的人員所執行。 建議您建立專門用於資料科學工作流程的Oauth2 API認證，並請貴組織的Adobe系統管理員將該認證指派給具有適當許可權的角色。

另請參閱 [驗證及存取Experience PlatformAPI](../../../landing/api-authentication.md) 以取得建立API認證和取得必要許可權的詳細指示。

資料科學的建議許可權包括：

- 用於資料科學的沙箱（通常是prod）
- 資料模式：管理結構
- 資料管理：管理資料集
- 資料擷取：檢視來源
- 目的地：管理和啟用資料集目的地
- 查詢服務：管理查詢

依預設，角色（以及指派給該角色的API認證）會遭到封鎖，無法存取任何標示的資料。 根據組織的資料控管原則，系統管理員可授予角色存取某些被視為適合資料科學使用的已標籤資料的許可權。 Platform客戶有責任適當地管理標籤存取和政策，以遵守相關法規和組織政策。

### 將認證儲存在單獨的設定檔案中

為了確保您的認證安全，建議您避免將認證資訊直接寫入程式碼。 請改為將認證資訊儲存在個別設定檔案中，並讀取連線至Experience Platform和資料Distiller所需的值。

例如，您可以建立名為 `config.ini` 並包含下列資訊（連同任何其他有助於在工作階段之間儲存的資訊，例如資料集ID）：

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

在筆記型電腦中，您就可以使用 `configParser` 來自標準Python程式庫的套件：

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)
```

接著，您可以在程式碼中參考認證值，如下所示：

```python
org_id = config.get('Credential', 'ims_org_id')
```

## 此 `aepp` Python資料庫

[aepp](https://github.com/adobe/aepp/tree/main) 是Adobe管理的開放原始碼Python程式庫，提供連線至Data Distiller和提交查詢，以及對其他Experience Platform服務提出要求的功能。 此 `aepp` 程式庫又依賴PostgreSQL資料庫配接器套件  `psycopg2` 互動式資料Distiller查詢專用。 您可以使用連線至Data Distiller並查詢Experience Platform資料集 `psycopg2` 單獨使用，但 `aepp` 為向所有Experience Platform API服務提出請求提供更大的便利性和附加功能。

若要安裝或升級 `aepp` 和 `psycopg2` 在您的環境中，您可以使用 `%pip` 您的筆記型電腦中的magic指令：

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

然後，您可以設定 `aepp` 使用下列程式碼以您的認證建立程式庫：

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)

# Configure aepp with your credentials
import aepp

aepp.configure(
  org_id=config.get('Credential', 'ims_org_id'),
  sandbox=config.get('Credential', 'sandbox_name'),
  client_id=config.get('Credential', 'client_id'), 
  secret=config.get('Credential', 'client_secret'),
  scopes=config.get('Credential', 'scopes'),
  tech_id=config.get('Credential', 'tech_acct_id')
)
```

## 建立與Data Distiller的連線

一次 `aepp` 已使用您的憑證設定，您可以使用下列程式碼建立與Data Distiller的連線，並啟動互動式工作階段，如下所示：

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

然後，您可以查詢Experience Platform沙箱中的資料集。 根據您要查詢的資料集ID，您可以從目錄服務擷取對應的表格名稱，然後在表格上執行查詢：

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### 連線至單一資料集以加快查詢效能

依預設，資料Distiller連線會連線至沙箱中的所有資料集。 為加快查詢速度並減少資源使用量，您可以改為連線至感興趣的特定資料集。 您可以透過變更 `dbname` 在Distiller資料連線物件至 `{sandbox}:{table_name}`：

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## 後續步驟

閱讀本檔案後，您已瞭解如何在機器學習環境中，從Python筆記本連線至Data Distiller。 在機器學習環境中，從Experience Platform建立功能管道以饋送自訂模型的 [探索和分析您的資料集](./exploratory-analysis.md).
