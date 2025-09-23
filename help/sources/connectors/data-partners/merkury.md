---
title: Merkury Enterprise Identity Resolution Source概觀
description: 瞭解如何使用使用者介面將Merkury企業身分識別解析連線至Adobe Experience Platform。
exl-id: c5eaa561-d620-4c82-bce1-972d0a422c3f
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

Adobe Experience Platform支援從資料合作夥伴應用程式擷取資料。 資料合作夥伴的支援包括[!DNL Merkury Enterprise Identity Resolution]。

您可使用[!DNL Merkury] by [!DNL Merkle]來辨識更多數位訪客（即使未使用Cookie），並提供客戶所需的相關個人化體驗。

您可以將&#x200B;**人員ID**&#x200B;用作[!DNL Merkury]來源的一部分，將貴組織所瞭解的所有個人資訊合併成單一完整設定檔。 這些詳細資料可包括：

- 數位行為
- 購買偏好設定
- 識別資訊，例如，名稱、電子郵件地址、實體地址或裝置ID。

您可以將內嵌的資料格式化為Experience Data Model (XDM) JSON、XDM Parquet或分隔。 流程的每個步驟都整合到來源工作中

![Merkury來源的資料處理工作流程圖例。](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## IP位址允許清單

您必須先將您所在地區的必要IP位址新增至允許清單，才能使用來源聯結器。 如果您未新增這些IP位址，來源聯結器可能會無法正常運作或產生錯誤。 如需詳細指示及允許的IP位址清單，請閱讀[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 檔案和目錄的命名限制

以下是在命名雲端儲存空間檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)結尾。 如果提供，則會自動移除。
- 必須正確逸出下列保留的URL字元： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許下列字元： `" \ / : | < > * ?`。
- 不允許非法URL路徑字元。 類似`\uE000`的程式碼點雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的規則，請參閱[RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 先決條件

您必須符合下列必要條件，才能開始使用[!DNL Merkury]來源：

- 您必須與您的[!DNL Merkury]團隊完成您的[!DNL Merkury]設定。
- 您必須從您的[!DNL Merkury]團隊擷取您的認證（存取金鑰、秘密金鑰和貯體名稱）。 

>[!NOTE]
>
>類似`myBucket/folder/subfolder/subsubfolder/abc.csv`的檔案路徑可能只讓您存取`subsubfolder/abc.csv`。 如果您想要存取子資料夾，您可以將bucket引數指定為myBucket，將folderPath指定為folder/subfolder，以確保檔案探索從子資料夾開始，而不是`subsubfolder/abc.csv`。

## 後續步驟

閱讀本檔案後，您已完成將[!DNL Merkury]帳戶中的資料帶入Experience Platform所需的先決條件設定。 您現在可以使用使用者介面[在 [!DNL Merkury] 連線](../../tutorials/ui/create/data-partners/merkury.md)至Experience Platform時繼續參閱指南。
