---
title: Acxiom資料擷取
description: 瞭解如何內嵌 [!DNL Acxiom] 將資料放入Real-time Customer Data Platform、豐富第一方設定檔，並改善對象和跨行銷管道啟用。
badge: Beta
source-git-commit: 9419da451616ca7f087ecea7aa66a6c10a474fb3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# [!DNL Acxiom Data Ingestion]

>[!NOTE]
>
>此 [!DNL Acxiom Prospecting Data Import] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

使用 [!DNL Acxiom Data Ingestion] 要擷取的來源 [!DNL Acxiom] 將資料匯入Real-time Customer Data Platform並豐富第一方設定檔。 然後，您可以使用您的 [!DNL Acxiom] — 擴充第一方設定檔，以改善對象並跨行銷管道啟用。

![acxiom-data-ingestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

請閱讀以下檔案，瞭解如何設定 [!DNL Acxiom Data Ingestion] 來源帳戶。

## 先決條件 {#prerequisites}

為了連線您的 [!DNL Acxiom Data Ingestion] 要Experience Platform的帳戶，您必須提供下列驗證認證的值：

| 認證 | 說明 |
| --- | --- |
| [!DNL Acxiom] 驗證金鑰 | 驗證金鑰。 此值可取自 [!DNL Acxiom] 團隊。 |
| [!DNL Amazon S3] 存取金鑰 | 貯體的存取金鑰ID。 此值可取自 [!DNL Acxiom] 團隊。 |
| [!DNL Amazon S3] 秘密金鑰 | 貯體的秘密金鑰ID。 此值可取自 [!DNL Acxiom] 團隊。 |
| 貯體名稱 | 這是您的貯體，檔案將在此共用。 此值可取自 [!DNL Acxiom] 團隊。 |

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

### 設定Experience Platform的許可權

您必須同時擁有兩者 **[!UICONTROL 檢視來源]** 和 **[!UICONTROL 管理來源]** 為您的帳戶啟用的許可權以連線您的 [!DNL Acxiom Data Ingestion] 要Experience Platform的帳戶。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀 [存取控制UI指南](../../../access-control/ui/overview.md).

### 檔案和目錄的命名限制

在命名您的雲端儲存空間檔案或目錄時，必須考慮下列限制：

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元： `" \ / : | < > * ?`.
- 不允許非法URL路徑字元。 程式碼點數如下 `\uE000`雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的管理規則，請參閱 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 後續步驟

閱讀本檔案後，您已完成從匯入資料所需的先決條件設定 [!DNL Acxiom] 要Experience Platform的帳戶。 您現在可以在以下位置繼續參閱指南： [正在連線 [!DNL Acxiom Data Ingestion] 以使用使用者介面Experience Platform](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md).
