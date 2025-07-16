---
title: 建立對象API端點
description: 瞭解如何使用API為外部對象建立中繼資料。
hide: true
hidefromtoc: true
source-git-commit: 74fa66e78ac36c8007eb89e8c271d989845c96f0
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 6%

---


# 建立對象端點

POST `/audiences`端點可用於建立外部對象的中繼資料。 如果受眾擷取是在另一個服務中進行管理（例如批次擷取），您應使用此端點。

## 快速入門

>[!IMPORTANT]
>
>本指南中的端點會加上前置詞`/core/ais`，而不是`/core/ups`。

若要使用Experience Platform API，您必須已完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程，提供Experience Platform API呼叫中每個必要標題的值，如下所示：

- 授權： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的所有請求都需要一個標頭，以指定將執行操作的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需在[!DNL Experience Platform]中使用沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

**API格式**

>[!IMPORTANT]
>
>您&#x200B;**必須**&#x200B;在要求中包含`createAudienceMetaOnly=true`查詢引數。

```http
POST /audiences?createAudienceMetaOnly=true
```

**要求**

>[!IMPORTANT]
>
>您&#x200B;**必須**&#x200B;在API要求中加入`Accept: application/vnd.adobe.external.audiences+json; version=2`標頭。

```shell
curl -X POST https://platform.adobe.io/core/ais/audiences?createAudienceMetaOnly=true \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'\
 -H 'Accept: application/vnd.adobe.external.audiences+json; version=2'
 -d '{
    "name": "Sample audience name",
    "description" "A sample description for the audience.",
    "namespace": "agora",
    "originName": "Agora_Collaboration"
 }'
```

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| `name` | 字串 | 對象的名稱。 |
| `description` | 字串 | 適用於對象的說明（選用）。 |
| `namespace` | 字串 | 對象的名稱空間。 |
| `originName` | 字串 | 對象來源的名稱。 |

**回應**

成功的回應會傳回HTTP狀態200以及有關新建立對象的資訊。

```json
{
    "name": "Sample audience name",
    "audienceId": "4a815904-f2f9-4237-82fb-55605bcc2ad7"
}
```

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| `name` | 字串 | 您建立的對象名稱。 |
| `audienceId` | 字串 | 您建立的對象ID。 |
