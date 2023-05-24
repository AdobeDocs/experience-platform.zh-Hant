---
keywords: Experience Platform；首頁；熱門主題；標籤標識
title: 在UI中將欄位標籤為標識
description: 包含個人身份資訊(PII)的欄位可以標籤為身份欄位。 標識欄位中提供的值被標識服務解釋為標識。 標識的命名空間被指定為標籤欄位的一部分。
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 在UI中將欄位標籤為標識

包含個人身份資訊(PII)的欄位可以標籤為身份欄位。 在標識欄位中提供的值被解釋為標識 [!DNL Identity Service]。 標識的命名空間被指定為標籤欄位的一部分。

要將欄位標籤為標識，必須滿足以下條件：

* 只能將字串類型欄位用於標識
* 標識僅在記錄和時間序列資料中識別
* 只應將PII欄位標籤為標識。 選擇表示更一般資料的欄位將導致更不精確的關係，並可能導致從身份圖訪問相關身份的錯誤

有關如何在UI中標籤標識欄位的說明，請參見上的指南 [定義UI中的標識欄位](../../xdm/ui/fields/identity.md)。

## 後續步驟

有關 [!DNL Identity Service]，請參見 [[!DNL Identity Service] 概述](../home.md)。
