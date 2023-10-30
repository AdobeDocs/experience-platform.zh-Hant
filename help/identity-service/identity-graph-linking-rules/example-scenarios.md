---
title: 設定身分設定的範例情境
description: 瞭解設定身分設定的範例情境。
hide: true
hidefromtoc: true
badge: Alpha
exl-id: bccd5b7a-3836-47d8-b976-51747b9c1803
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 1%

---

# 設定身分圖表連結規則的範例案例

>[!IMPORTANT]
>
>身分圖表連結規則目前Alpha。 功能和檔案可能會有所變更。

本檔案概述設定身分圖表連結規則時可考慮的範例情境。

## 共用裝置

在單一裝置上可能發生多次登入的例項：

| 共用裝置 | 說明 |
| --- | --- |
| 家用電腦和平板電腦 | 丈夫和妻子都登入各自的銀行帳戶。 |
| 公用資訊站 | 在機場登入的旅行者，會使用他們的忠誠度身份證來登記行李和列印登機牌。 |
| 客服中心 | 客服中心人員代表客戶致電客戶支援以解決問題，登入單一裝置。 |

![共用裝置](../images/identity-settings/shared-devices.png)

在這些情況下，從圖表觀點來看，未啟用任何限制，單一ECID會連結至多個CRM ID。

使用身分圖表連結規則，您可以：

* 設定用於登入的ID作為唯一識別碼。 例如，您可以將圖表限製為只儲存一個具有CRM ID名稱空間的身分識別，藉此將該CRM ID定義為共用裝置的唯一識別碼。
   * 這麼做可確保ECID不會合併CRM ID。

## 無效的電子郵件/電話案例

註冊時也會有使用者提供虛假值做為電話號碼和/或電子郵件地址的例項。 在這些情況下，如果未啟用限制，則電話/電子郵件相關的身分最終將會連結至多個不同的CRM ID。

![invalid-email-phone](../images/identity-settings/invalid-email-phone.png)

使用身分圖表連結規則，您可以：

* 將CRM ID、電話號碼或電子郵件地址設定為唯一識別碼，因此將一個人限製為只能有一個與其帳戶相關聯的CRM ID、電話號碼和/或電子郵件地址。

## 錯誤或錯誤的身分值

在某些情況下，無論名稱空間為何，都會在系統中擷取非唯一、錯誤的身分值。 例如：

* 身分值為「user_null」的IDFA名稱空間。
   * IDFA身分值應該有36個字元： 32個英數字元和4個連字型大小。
* 身分值為「未指定」的電話號碼名稱空間。
   * 電話號碼不應有任何字母字元。

這些身分可能會導致以下圖表，其中多個CRM ID與「不良」身分合併在一起：

![bad-data](../images/identity-settings/bad-data.png)

透過身分圖表連結規則，您可以將CRM ID設定為唯一識別碼，以防止由於此類資料而造成不想要的設定檔收合。

## 後續步驟

如需身分圖表連結規則的詳細資訊，請參閱下列檔案：

* [身分圖表連結規則概觀](./overview.md)
* [Identity Service和即時客戶個人檔案](identity-and-profile.md)
* [身分連結邏輯](./identity-linking-logic.md)
