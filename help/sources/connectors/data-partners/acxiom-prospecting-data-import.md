---
title: Acxiom 潛在客戶資料匯入
description: 了解如何使用 UI 將 Acxiom 潛在客戶資料連接到 Adobe Experience Platform 和 Adobe Real-Time Customer Data Platform。
badge: Beta
exl-id: 6df674d9-c14b-42ea-a287-5377484e567d
source-git-commit: 9419da451616ca7f087ecea7aa66a6c10a474fb3
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 5%

---

# [!DNL Acxiom Prospecting Data Import]

>[!NOTE]
>
>[!DNL Acxiom Prospecting Data Import]來源是測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

Adobe Experience Platform支援從資料合作夥伴應用程式擷取資料。 資料與身分識別合作夥伴的支援包括[!DNL Acxiom Prospecting Data Import]。

[!DNL Acxiom]針對Adobe Real-time Customer Data Platform的潛在客戶資料匯入是提供儘可能有效率潛在客戶對象的程式。 [!DNL Acxiom]透過安全匯出取得Real-Time CDP第一方資料，並透過獲獎的衛生和身分解析系統執行該資料。 產生可用作隱藏清單的資料檔案。 然後，此資料檔案會與[!DNL Acxiom Global]資料庫進行比對，如此即可自訂潛在客戶清單以進行匯入。

您可以使用[!DNL Acxiom]來源，以[!DNL Amazon S3]做為拖放點，從[!DNL Acxiom]潛在客戶服務擷取及對應回應。

![acxiom-propositing-workflow](../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/acxiom-prospecting.png)

請閱讀以下檔案，瞭解如何設定[!DNL Acxiom Prospecting Data Import]來源帳戶的資訊。

## 先決條件

若要在Experience Platform上存取貯體，您必須提供下列憑證的有效值：

| 認證 | 說明 |
| --- | --- |
| [!DNL Acxiom]驗證金鑰 | 驗證金鑰。 您可以從[!DNL Acxiom]團隊擷取此值。 |
| [!DNL Amazon S3]存取金鑰 | 貯體的存取金鑰ID。 您可以從[!DNL Acxiom]團隊擷取此值。 |
| [!DNL Amazon S3]秘密金鑰 | 貯體的秘密金鑰ID。 您可以從[!DNL Acxiom]團隊擷取此值。 |
| 貯體名稱 | 這是您的貯體，檔案將在此共用。 您可以從[!DNL Acxiom]團隊擷取此值。 |

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

### 設定Experience Platform的許可權

您必須同時為您的帳戶啟用&#x200B;**[!UICONTROL 檢視來源]**&#x200B;和&#x200B;**[!UICONTROL 管理來源]**&#x200B;許可權，才能將您的[!DNL Acxiom Prospecting Data Import]帳戶連線至Experience Platform。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀[存取控制UI指南](../../../access-control/abac/ui/permissions.md)。

## 檔案和目錄的命名限制

在命名您的雲端儲存空間檔案或目錄時，必須考慮下列限制：

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)結尾。 如果提供，則會自動移除。
- 必須正確逸出下列保留的URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許下列字元： `" \ / : | < > * ?`。
- 不允許非法URL路徑字元。 類似`\uE000`的程式碼點雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的規則，請參閱[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 後續步驟

閱讀本檔案後，您已完成將[!DNL Acxiom]帳戶中的資料帶入Experience Platform所需的先決條件設定。 您現在可以在[使用使用者介面](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md)連線 [!DNL Acxiom Prospecting Data Import] 以Experience Platform時繼續參閱指南。
