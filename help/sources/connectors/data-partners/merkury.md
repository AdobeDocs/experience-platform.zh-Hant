---
title: Merkury Enterprise身分解析來源概觀
description: 瞭解如何使用使用者介面將Merkury企業身分識別解析連線至Adobe Experience Platform。
badge: Beta
source-git-commit: 12f73ac2578b6c5b024cc4ebdd75cd945c7b55c9
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>此 [!DNL Merkury Enterprise Identity Resolution] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

Adobe Experience Platform支援從資料合作夥伴應用程式擷取資料。 對資料合作夥伴的支援包括 [!DNL Merkury Enterprise Identity Resolution].

您可以使用 [!DNL Merkury] 作者： [!DNL Merkle] 辨識更多數位訪客（即使未使用Cookie），並提供客戶所需的相關個人化體驗。

您可以利用 **人員ID** 做為 [!DNL Merkury] 來源，將貴組織所瞭解的個人所有資訊合併為單一全面設定檔。 這些詳細資料可包括：

- 數位行為
- 購買偏好設定
- 識別資訊，例如，名稱、電子郵件地址、實體地址或裝置ID。

您可以將內嵌的資料格式化為Experience Data Model (XDM) JSON、XDM Parquet或分隔。 流程的每個步驟都整合到來源工作中

![Merkury來源的資料處理工作流程圖例。](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 檔案和目錄的命名限制

以下是在命名雲端儲存空間檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元： `" \ / : | < > * ?`.
- 不允許非法URL路徑字元。 程式碼點數如下 `\uE000`雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，也不允許使用某些ASCII或Unicode字元，例如控制字元（0x00到0x1F、\u0081等）。 如需HTTP/1.1中Unicode字串的管理規則，請參閱 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允許下列檔案名稱： LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)和兩個點字元(..)。

## 先決條件

您必須符合下列必要條件，才能開始使用 [!DNL Merkury] 來源：

- 您必須完成您的 [!DNL Merkury] 使用您的設定 [!DNL Merkury] 團隊。
- 您必須從您的資料庫擷取您的認證（存取金鑰、秘密金鑰和貯體名稱） [!DNL Merkury] 團隊。 

>[!NOTE]
>
>檔案路徑，例如 `myBucket/folder/subfolder/subsubfolder/abc.csv` 可能導致您僅存取 `subsubfolder/abc.csv`. 如果您想要存取子資料夾，您可以將bucket引數指定為myBucket，將folderPath指定為folder/subfolder，以確保檔案探索從子資料夾開始，而不是從子資料夾開始 `subsubfolder/abc.csv`.

## 後續步驟

閱讀本檔案後，您已完成從匯入資料所需的先決條件設定 [!DNL Merkury] 要Experience Platform的帳戶。 您現在可以在以下位置繼續參閱指南： [正在連線 [!DNL Merkury] 以使用使用者介面Experience Platform](../../tutorials/ui/create/data-partners/merkury.md).
