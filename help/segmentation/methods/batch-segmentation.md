---
title: 批次分段指南
description: 瞭解批次細分，包括內容、如何建立使用批次細分評估的對象，以及如何檢視使用批次細分建立的對象。
exl-id: b6fba2fb-8eec-4429-92fd-ece5c79d379d
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---

# 批次分段指南

批次細分是一種細分評估方法，可讓您一次移動所有設定檔資料，以建立對應的對象。

透過批次分段，您可以建立詳細而豐富的對象，並執行分段工作以決定何時將此資料傳播到下游服務。

## 合格的查詢型別 {#query-types}

所有查詢都符合批次細分的資格。

## 建立客群 {#create-audience}

您可以使用Segmentation Service API或透過UI中的對象入口網站，建立使用批次細分來評估的對象。

>[!BEGINTABS]

>[!TAB 分段服務API]

**API格式**

```http
POST /segment/definitions
```

**要求**

+++ 建立已啟用批次細分之區段定義的範例請求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People in the USA",
        "description: "An audience that looks for people who live in the USA",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "homeAddress.country = \"US\""
        },
        "evaluationInfo": {
            "batch": {
                "enabled": true
            },
            "continuous": {
                "enabled": false
            },
            "synchronous": {
                "enabled": false
            }
        },
        "schema": {
            "name": "_xdm.context.profile"
        }
     }'
```

+++

**回應**

成功的回應會傳回HTTP狀態200以及您新建立區段定義的詳細資料。

+++建立區段定義時的範例回應。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People in the USA",
    "description": "An audience that looks for people who live in the USA",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "homeAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

+++

在[區段定義端點指南](../api/segment-definitions.md)中找到有關使用此端點的詳細資訊。

>[!TAB Audience Portal]

在對象入口網站中，選取&#x200B;**[!UICONTROL 建立對象]**。

![對象入口網站中會醒目顯示[建立對象]按鈕。](../images/methods/batch/select-create-audience.png)

彈出視窗隨即顯示。 選取&#x200B;**[!UICONTROL 建置規則]**&#x200B;以輸入區段產生器。

![「建立對象」彈出視窗中會醒目顯示「建置規則」按鈕。](../images/methods/batch/select-build-rules.png)

建立區段定義後，選取&#x200B;**[!UICONTROL 批次]**&#x200B;作為&#x200B;**[!UICONTROL 評估方法]**。

![會顯示區段定義。 評估型別已反白顯示，顯示可以使用串流區段來評估區段定義。](../images/methods/batch/batch-evaluation-method.png)

若要深入瞭解如何建立區段定義，請參閱[區段產生器指南](../ui/segment-builder.md)

>[!ENDTABS]

## 擷取對象 {#retrieve-audiences}

您可以使用Segmentation Service API或透過UI中的對象入口網站，擷取使用批次細分評估的所有對象。

>[!BEGINTABS]

>[!TAB 分段服務API]

向`/segment/definitions`端點發出GET請求，以擷取使用組織內批次細分評估的所有區段定義清單。

**API格式**

您必須在請求路徑中包含查詢引數`evaluationInfo.batch.enabled=true`，以擷取使用批次分段評估的區段定義。

```http
GET /segment/definitions?evaluationInfo.batch.enabled=true
```

**要求**

+++ 列出所有已啟用批次之區段定義的範例請求

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.batch.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含貴組織中使用批次分段評估的一系列區段定義。

+++此範例回應包含貴組織中所有批次細分評估區段定義的清單

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

在[區段定義端點指南](../api/segment-definitions.md)中找到有關傳回的區段定義的詳細資訊。

+++

>[!TAB Audience Portal]

您可以使用Audience Portal中的篩選條件，擷取貴組織內針對批次細分啟用的所有對象。 選取![篩選器圖示](../../images/icons/filter.png)圖示以顯示篩選器清單。

![對象入口網站中會醒目顯示篩選圖示。](../images/methods/filter-audiences.png)

在可用的篩選器內，移至&#x200B;**[!UICONTROL 更新頻率]**&#x200B;並選取[!UICONTROL 批次]。 使用此篩選器會顯示貴組織中使用批次細分評估的所有對象。

![已選取批次更新頻率，顯示組織中使用批次細分評估的所有對象。](../images/methods/batch/filter-batch.png)

若要進一步瞭解如何在Experience Platform中檢視對象，請參閱[對象入口網站指南](../ui/audience-portal.md)。

>[!ENDTABS]

## 後續步驟

本指南說明如何建立可使用Adobe Experience Platform上的批次細分進行評估的區段定義。

若要進一步瞭解如何使用Experience Platform使用者介面，請參閱[分段使用手冊](../ui/overview.md)。

如需批次劃分的相關常見問題，請參閱常見問題[&#128279;](../faq.md#batch-segmentation)的批次劃分割槽段。
