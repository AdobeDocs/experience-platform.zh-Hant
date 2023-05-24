---
keywords: Experience Platform；首頁；熱門主題；標籤標識
solution: Experience Platform
title: 將欄位標籤為標識
description: 包含個人身份資訊(PII)的欄位可以標籤為身份欄位。 標識欄位中提供的值被標識服務解釋為標識。 標識的命名空間被指定為標籤欄位的一部分。
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# 將欄位標籤為標識

包含個人身份資訊(PII)的欄位可以標籤為身份欄位。 在標識欄位中提供的值被解釋為標識 [!DNL Identity Service]。 標識的命名空間被指定為標籤欄位的一部分。

要將欄位標籤為標識，必須滿足以下條件：

- 只能將字串類型欄位用於標識
- 標識僅在記錄和時間序列資料中識別
- 只應將PII欄位標籤為標識。 選擇表示更一般資料的欄位將導致更不精確的關係，並可能導致從身份圖訪問相關身份的錯誤

有關如何使用架構註冊表API將欄位標籤為標識的說明，請訪問 [描述符端點指南](../../xdm/api/descriptors.md#create)。

## 後續步驟

繼續下一教程， [清單群集標識](./list-cluster-identites.md)
