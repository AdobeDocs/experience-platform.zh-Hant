---
title: 在Reactor API中共用私人擴充功能套件
description: 瞭解如何授權其他企業在Reactor API中共用私人擴充功能套件。
source-git-commit: ea9a2bb00d3ce59e28ea4cda0d30945e77aa95cb
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 2%

---


# 共用私人擴充功能套件

>[!NOTE]
>
>在擴充功能套件擁有者組織中具有`develop_extensions`許可權的使用者可以建立、列出和刪除該擴充功能套件的擴充功能套件使用授權。 在已授權組織中，擁有`manage_properties`許可權的使用者僅可列出其組織的擴充功能套件使用授權，並且如果他們想要使用該擴充功能套件，則將其狀態更新為`accepted`，如果不想使用它，則更新為`rejected`。

擴充功能套件的擁有者可透過Reactor API授予其他公司利用其私人版本的許可權。 一個擴充功能套件的使用授權會授與給每個已核准的企業，此授權適用於該套件的所有目前和未來私人版本。

本指南提供如何設定擴充功能套件使用授權的高層級概觀。 如需有關如何在Reactor API中管理授權的詳細指引，包括授權結構的範例JSON，請參閱[擴充功能套件使用授權端點指南](../endpoints/extension-package-usage-authorizations.md)。

## 建立授權 {#create-authorization}

若要建立新的授權，您必須擁有`develop_extensions`許可權。 下列範例示範如何使用您要授權的公司`authorized_org_id`，為擴充套件建立擴充套件使用授權。

**API格式**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| 參數 | 說明 |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | 您要為其建立授權的延伸套件`ID`。 |

{style="table-layout:auto"}

**要求**

以下請求會為指定的公司建立新的擴充功能套件授權。

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| 屬性 | 說明 |
| --- | --- |
| `attributes.authorized_org_id` | 您要授權的組織`ID`。 |

{style="table-layout:auto"}

授權的初始狀態處於`pending_approval`階段。 使用擴充功能套件前，公司必須核准授權。 當授權正在等候核準時，公司的使用者可以瀏覽私人擴充功能套件，但他們無法安裝該套件，且無法在擴充功能目錄中找到。

## 核准授權 {#approve-authorization}

若要核准授權，您必須擁有`manage_properties`許可權。 身為授權公司，您需要傳送PATCH要求給擴充套件使用授權，包括授權的`ID`，並將狀態設定為`approved`。

**API格式**

```http
PATCH //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | 您要核准的授權之`ID`。 |

{style="table-layout:auto"}

**要求**

下列PATCH要求會將授權的`state`設定為`approved`。

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
	          "state": "approved"
	        },
	        "id": ":extension_package_usage_authorization_id",
	        "type": "extension_package_usage_authorizations"
        }
      }
```

在核准授權後，身為獲授權的公司，您現在可以在您的屬性上安裝擴充功能套件。

>[!NOTE]
>
>如果授權遭拒，獲授權的公司將無法使用擴充功能套件。

## 刪除授權 {#delete-authorization}

身為擴充功能套件擁有者，您可以隨時刪除擴充功能套件使用授權以撤銷授權。 這樣可防止授權公司檢視目錄中擴充功能套件的私人版本，以及在其屬性上安裝該套件。 不過，已安裝的私人版本在刪除後仍可繼續如預期運作。

**API格式**

```http
DELETE //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | 您要刪除的授權`ID`。 |

{style="table-layout:auto"}

**要求**

以下DELETE請求會移除公司的授權許可權。

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
```
