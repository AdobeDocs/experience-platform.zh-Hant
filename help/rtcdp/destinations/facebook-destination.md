---
title: Facebook目標
seo-title: Facebook目標
description: 根據雜湊的電子郵件，啟用您Facebook宣傳的個人檔案，以鎖定受眾、個人化和抑制受眾。
seo-description: 根據雜湊的電子郵件，啟用您Facebook宣傳的個人檔案，以鎖定受眾、個人化和抑制受眾。
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# （測試版）Facebook目標

>[!IMPORTANT]
>
>Adobe Real-time CDP中的Facebook目標目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

## 概述

根據雜湊的電子郵件，啟用您Facebook宣傳的個人檔案，以鎖定受眾、個人化和抑制受眾。

## 目標規格

### 啟動類型

區段匯出——您正匯出區段（對象）的所有成員，以及其識別碼（名稱、電話號碼等）用於Facebook目的地

## 必要條件

在將受眾細分傳送至之前，請 [!DNL Facebook]確定您符合下列需求：

1. 您 [!DNL Facebook] 的使用者帳戶必須為您 **** 計畫使用的廣告帳戶啟用「管理促銷活動」權限。
2. 將 **Adobe Experience Cloud商業帳戶新增為廣告合作夥伴**[!DNL Facebook Ad Account]。 使用 `business ID=206617933627973`。 如需詳 [細資訊，請參閱將合作夥伴新增至您的業務經理](https://www.facebook.com/business/help/1717412048538897) 。
   >[!IMPORTANT]
   > 設定Adobe Experience Cloud的權限時，您必須啟用「管理促銷 **活動** 」權限。 這是整合的必 [!DNL Adobe Real-time CDP] 要項。
3. 閱讀並簽署 [!DNL Facebook Custom Audiences] 服務條款。 若要這麼做，請前 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`往您的 `accountID` 位置 [!DNL Facebook Ad Account ID]。


## 連接目標

若要連線Facebook目標，請參閱 [Social網路目標驗證工作流程](/help/rtcdp/destinations/social-network-destinations-workflow.md)。


## 啟用區段至Facebook

如需如何啟用區段至Facebook的指示，請參閱啟 [用資料至目標](/help/rtcdp/destinations/activate-destinations.md)。