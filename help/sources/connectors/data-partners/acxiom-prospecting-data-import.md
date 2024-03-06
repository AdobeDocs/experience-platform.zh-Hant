---
title: Acxiom潛在客戶資料匯入
description: 瞭解如何使用UI將Acxiom潛在資料連線到Adobe Experience Platform和Adobe Real-time Customer Data Platform。
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# [!DNL Acxiom Prospecting Data Import]

>[!NOTE]
>
>此 [!DNL Acxiom Prospecting Data Import] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

Adobe Experience Platform支援從資料合作夥伴應用程式擷取資料。 對資料和身分合作夥伴的支援包括 [!DNL Acxiom Prospecting Data Import].

[!DNL Acxiom]的Adobe Real-time Customer Data Platform潛在客戶資料匯入是儘可能提供最高生產力的潛在客戶對象的程式。 [!DNL Acxiom] 透過安全匯出擷取Real-Time CDP第一方資料，並透過獲獎的衛生和身分解析系統執行資料。 產生可用作隱藏清單的資料檔案。 然後，此資料檔案會與 [!DNL Acxiom Global] 資料庫，可讓您自訂潛在客戶清單以進行匯入。

您可以使用 [!DNL Acxiom] 來源以擷取和對應回應 [!DNL Acxiom] 潛在客戶服務使用 [!DNL Amazon S3] 作為放置點。

## 先決條件

若要在Experience Platform上存取貯體，您必須提供下列憑證的有效值：

| 認證 | 說明 |
| --- | --- |
| [!DNL Acxiom] 驗證金鑰 | 驗證金鑰。 此值可取自 [!DNL Acxiom] 團隊。 |
| [!DNL Amazon S3] 存取金鑰 | 貯體的存取金鑰ID。 此值可取自 [!DNL Acxiom] 團隊。 |
| [!DNL Amazon S3] 秘密金鑰 | 貯體的秘密金鑰ID。 此值可取自 [!DNL Acxiom] 團隊。 |
| 貯體名稱 | 這是您的貯體，檔案將在此共用。 此值可取自 [!DNL Acxiom] 團隊。 |

### 權限

您必須同時擁有兩者 **[!UICONTROL 檢視來源]** 和 **[!UICONTROL 管理來源]** 為您的帳戶啟用的許可權以連線您的 [!DNL Acxiom Prospecting Data Import] 要Experience Platform的帳戶。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀 [存取控制UI指南](../../../access-control/abac/ui/permissions.md).

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 檔案和目錄的命名限制

在命名您的雲端儲存空間檔案或目錄時，必須考慮下列限制：

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元： `" \ / : | < > * ?`.
- 不允許非法URL路徑字元。 程式碼點數如下 `\uE000`雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的管理規則，請參閱 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 後續步驟

閱讀本檔案後，您已完成從匯入資料所需的先決條件設定 [!DNL Acxiom] 要Experience Platform的帳戶。 您現在可以在以下位置繼續參閱指南： [正在連線 [!DNL Acxiom Prospecting Data Import] 以使用使用者介面Experience Platform](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md).