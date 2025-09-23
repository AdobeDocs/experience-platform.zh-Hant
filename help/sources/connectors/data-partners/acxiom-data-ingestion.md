---
title: Acxiom 資料內嵌
description: 瞭解如何將 [!DNL Acxiom] 資料擷取至Real-Time Customer Data Platform、豐富第一方設定檔，以及改善對象和跨行銷管道啟用。
exl-id: 3bbbe4e1-5e34-4104-bf39-2c452865b807
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# [!DNL Acxiom Data Ingestion]

使用[!DNL Acxiom Data Ingestion]來源將[!DNL Acxiom]資料擷取至Real-Time Customer Data Platform並擴充第一方設定檔。 接著，您可以使用富[!DNL Acxiom]的第一方設定檔來改善對象，並跨行銷管道啟用。

![acxiom-data-ingestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

請閱讀以下檔案，瞭解如何設定[!DNL Acxiom Data Ingestion]來源帳戶的資訊。

## 先決條件 {#prerequisites}

若要將您的[!DNL Acxiom Data Ingestion]帳戶連線至Experience Platform，您必須提供下列驗證認證的值：

| 認證 | 說明 |
| --- | --- |
| [!DNL Acxiom]驗證金鑰 | 驗證金鑰。 您可以從[!DNL Acxiom]團隊擷取此值。 |
| [!DNL Amazon S3]存取金鑰 | 貯體的存取金鑰ID。 您可以從[!DNL Acxiom]團隊擷取此值。 |
| [!DNL Amazon S3]秘密金鑰 | 貯體的秘密金鑰ID。 您可以從[!DNL Acxiom]團隊擷取此值。 |
| 貯體名稱 | 這是您的貯體，檔案將在此共用。 您可以從[!DNL Acxiom]團隊擷取此值。 |

## IP位址允許清單

您必須先將您所在地區的必要IP位址新增至允許清單，才能使用來源聯結器。 如果您未新增這些IP位址，來源聯結器可能會無法正常運作或產生錯誤。 如需詳細指示及允許的IP位址清單，請閱讀[IP位址允許清單](../../ip-address-allow-list.md)頁面。

### 在Experience Platform上設定許可權

您必須同時為您的帳戶啟用&#x200B;**[!UICONTROL 檢視來源]**&#x200B;和&#x200B;**[!UICONTROL 管理來源]**&#x200B;許可權，才能將您的[!DNL Acxiom Data Ingestion]帳戶連線至Experience Platform。 請聯絡您的產品管理員以取得必要許可權。 如需詳細資訊，請閱讀[存取控制UI指南](../../../access-control/ui/overview.md)。

### 檔案和目錄的命名限制

在命名您的雲端儲存空間檔案或目錄時，必須考慮下列限制：

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)結尾。 如果提供，則會自動移除。
- 必須正確逸出下列保留的URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許下列字元： `" \ / : | < > * ?`。
- 不允許非法URL路徑字元。 類似`\uE000`的程式碼點雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的規則，請參閱[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 後續步驟

閱讀本檔案後，您已完成所需的先決條件設定，以將資料從[!DNL Acxiom]帳戶帶入Experience Platform。 您現在可以使用使用者介面[在 [!DNL Acxiom Data Ingestion] 連線](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md)至Experience Platform時繼續參閱指南。
