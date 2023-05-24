---
description: 瞭解如何使用目標測試API為流目標生成示例配置檔案，您可以在目標測試中使用這些配置檔案。
title: 基於源架構生成示例配置檔案
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 1%

---


# 基於源架構生成示例配置檔案 {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API終結點**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

此頁列出並說明了可以使用 `/authoring/sample-profiles` API終結點。

## 為不同的API生成不同的配置檔案類型 {#different-profiles-different-apis}

>[!IMPORTANT]
>
>使用此API終結點為兩個單獨的使用案例生成示例配置檔案。 您可以：
>* 生成配置檔案時使用 [編寫和測試消息轉換模板](create-template.md)  — 使用 *目標ID* 作為查詢參數。
>* 生成調用時使用的配置檔案 [test目標配置正確](streaming-destination-testing-overview.md)  — 使用 *目標實例ID* 作為查詢參數。


您可以根據AdobeXDM源架構（在測試目標時使用）或目標架構（在製作模板時使用）生成示例配置檔案。 要瞭解AdobeXDM源架構和目標架構之間的差異，請閱讀 [消息格式](../../functionality/destination-server/message-format.md) 文章。

請注意，可以使用示例配置檔案的目的不可互換。 基於 *目標ID* 只能用於根據生成的消息轉換模板和配置檔案 *目標實例ID* 只能用於test目標終結點。

## 示例配置檔案生成API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](../../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 根據測試目標時要使用的源架構生成示例配置檔案 {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>將此處生成的示例配置檔案添加到HTTP調用 [測試目標](streaming-destination-testing-overview.md)。

通過向Web站點發出GET請求，可以根據源架構生成示例配置檔案 `authoring/sample-profiles/` 終結點，並提供您根據要test的目標配置建立的目標實例的ID。

要獲取目標實例的ID，必須先在Experience PlatformUI中建立到目標的連接，然後才能嘗試test目標。 閱讀 [激活目標教程](../../../ui/activation-overview.md) 有關如何獲取要用於此API的目標實例ID的提示，請參閱下面的提示。

>[!IMPORTANT]
>
>* 要使用此API，必須在Experience PlatformUI中與目標建立現有連接。 閱讀 [連接到目標](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 和 [激活配置檔案和段到目標](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) 的子菜單。
> * 在建立到目標的連接後，獲取在API調用到此終結點時應使用的目標實例ID [瀏覽與目標的連接](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en)。
   >![UI映像如何獲取目標實例ID](../../assets/testing-api/get-destination-instance-id.png)


**API格式**

```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 生成示例配置檔案時所基於的目標實例的ID。 |
| `{COUNT}` | *可選*. 您正在生成的示例配置檔案數。 參數可以取值 `1 - 1000`。 <br> 如果未指定count參數，則由 `maxUsersPerRequest` 值 [目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)。 如果未定義此屬性，則Adobe將生成一個示例配置檔案。 |

{style="table-layout:auto"}


**要求**

以下請求生成示例配置檔案，由 `{DESTINATION_INSTANCE_ID}` 和 `{COUNT}` 查詢參數。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的響應返回HTTP狀態200，其中包含指定數量的示例配置檔案，以及與源XDM架構對應的段成員資格、標識和配置檔案屬性。

>[!TIP]
>
> 響應僅返回目標實例中使用的段成員身份、標識和配置檔案屬性。 即使源架構有其他欄位，也會忽略這些欄位。

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| 屬性 | 說明 |
| -------- | ----------- |
| `segmentMembership` | 描述個人段成員身份的映射對象。 有關 `segmentMembership`，閱讀 [段成員身份詳細資訊](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html)。 |
| `lastQualificationTime` | 此配置檔案上次限定段的時間的時間戳。 |
| `xdm:status` | 一個字串欄位，指示是否已將段成員資格作為當前請求的一部分實現。 接受以下值： <ul><li>`realized`:輪廓是段的一部分。</li><li>`exited`:配置檔案作為當前請求的一部分退出段。</li></ul> |
| `identityMap` | 映射類型欄位，它描述個人的各種標識值及其關聯的命名空間。 有關 `identityMap`，閱讀 [架構組合的基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap)。 |

{style="table-layout:auto"}

## 生成基於目標模式的示例配置檔案，以便在生成消息轉換模板時使用 {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>使用在建立模板時在此處生成的示例配置檔案， [呈現模板步驟](render-template-api.md#multiple-profiles-with-body)。

您可以根據目標方案生成示例配置檔案，向 `authoring/sample-profiles/` 端點，並根據建立模板的目標配置提供目標ID。

>[!TIP]
>
>* 在此應使用的目標ID是 `instanceId` 與目標配置對應，使用 `/destinations` 端點。 請參閱 [檢索目標配置](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 的子菜單。


**API格式**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 生成示例配置檔案時所基於的目標配置的ID。 |
| `{COUNT}` | *可選*. 您正在生成的示例配置檔案數。 參數可以取值 `1 - 1000`。 <br> 如果未指定count參數，則由 `maxUsersPerRequest` 值 [目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)。 如果未定義此屬性，則Adobe將生成一個示例配置檔案。 |

{style="table-layout:auto"}

**要求**

以下請求生成示例配置檔案，由 `{DESTINATION_ID}` 和 `{COUNT}` 查詢參數。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的響應返回HTTP狀態200，其中包含指定數量的示例配置檔案，以及與目標XDM架構對應的段成員資格、標識和配置檔案屬性。

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀此文檔後，您現在知道如何生成示例配置檔案，以便在 [測試消息轉換模板](create-template.md) 或 [測試目標配置是否正確](streaming-destination-testing-overview.md)。
