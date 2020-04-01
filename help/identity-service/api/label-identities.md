---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 將欄位標示為身分
topic: api guide
translation-type: tm+mt
source-git-commit: 40ce232e39f62f1ee478ef05229dd2fc125ee4c0

---


# 將欄位標示為身分

包含個人識別資訊(PII)的欄位可標示為識別欄位。 身分欄位中提供的值，由Identity Service解譯為身分。 標識的名稱空間指定為標籤欄位的一部分。

欄位必須符合下列標示為身分的條件：

- 僅字串類型欄位可用於識別
- 身份只能在記錄和時間序列資料中識別
- 只有PII欄位應標示為身分。 選擇代表更一般資料的欄位，會導致關係不太精確，而且可能會因從識別圖存取相關身分而出錯

有關如何使用方案註冊表API將欄位標籤為標識的說明，請訪問 [建立描述符](../../xdm/api/descriptors.md)。

## 後續步驟

繼續下一個教程以列出 [群集標識](./list-cluster-identites.md)