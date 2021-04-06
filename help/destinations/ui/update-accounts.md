---
keywords: 更新目標帳戶；目標帳戶；如何更新帳戶
title: 更新目標帳戶
type: 教學課程
description: 本教學課程列出在Adobe Experience PlatformUI中更新目標帳戶的步驟
translation-type: tm+mt
source-git-commit: 6fd980b486c4a330f9188065bac55c624af584a1
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 1%

---


# 更新目標帳戶

## 概述 {#overview}

**[!UICONTROL Accounts]**&#x200B;頁籤顯示您與各種目標建立的連接的詳細資訊。 請參閱下表，以取得有關每個目標的所有資訊：

![「帳戶」頁籤](../assets/ui/update-accounts/destination-accounts.png)

| 元素 | 說明 |
---------|----------
| [!UICONTROL Platform] | 您已設定連接的目標。 |
| [!UICONTROL Connection Type] | 表示與儲存桶或目標的連接類型。 <ul><li>對於電子郵件行銷目標：可以是S3或FTP。</li><li>針對即時廣告目的地：伺服器對伺服器</li><li>針對AmazonS3雲端儲存空間目標：存取金鑰 </li><li>對於SFTP雲端儲存空間目標：SFTP的基本驗證</li></ul> |
| [!UICONTROL Username] | 在[連接目標嚮導](../catalog/email-marketing/overview.md#connect-destination)中選擇的用戶名。 |
| [!UICONTROL Destinations] | 表示與為目標建立的基本資訊連接的唯一成功目標流的數量。 |
| [!UICONTROL Authorized] | 授權此目的地的連線的日期。 |

## 更新帳戶{#update}

請遵循下列步驟，將連接詳細資訊更新到現有目標。

1. 登入[Experience PlatformUI](https://platform.adobe.com/)並從左導覽列選擇&#x200B;**[!UICONTROL Destinations]**。 從頂部標題中選擇&#x200B;**[!UICONTROL Accounts]**&#x200B;以查看現有帳戶。

   ![「帳戶」頁籤](../assets/ui/update-accounts/accounts-tab.png)

2. 選擇左上角的篩選器表徵圖![Filter-icon](../assets/ui/update-accounts/filter.png)以啟動排序面板。 排序面板提供您所有目的地的清單。 您可以從清單中選取多個目標，以查看與所選目標相關聯的帳戶篩選選擇。

   ![篩選目標](../assets/ui/update-accounts/filter-accounts.png)

3. 選擇&#x200B;**[!UICONTROL Platform]**&#x200B;欄中的![編輯帳戶按鈕](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Edit]**&#x200B;按鈕以編輯帳戶的資訊。

   ![「帳戶」頁籤](../assets/ui/update-accounts/accounts-edit.png)

4. 輸入您更新的帳戶憑證。

   * 對於使用`OAuth2`連接類型的帳戶，請選擇&#x200B;**[!UICONTROL Reconnect OAuth]**&#x200B;以續約您的帳戶憑證。

      ![編輯詳細資訊OAuth](../assets/ui/update-accounts/edit-details-oauth.png)


   * 對於使用`Access Key`或`ConnectionString`連線類型的帳戶，您可以編輯帳戶驗證資訊，包括存取ID、機密金鑰或連線字串等資訊。

      ![編輯詳細資訊訪問密鑰](../assets/ui/update-accounts/edit-details-key.png)

5. 選擇&#x200B;**[!UICONTROL Save]**&#x200B;以完成憑據更新。
