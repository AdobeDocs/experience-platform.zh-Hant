---
title: Adobe Content Analytics擴充功能發行說明
description: Adobe Experience Platform中Content Analytics標籤擴充功能的最新發行說明。
source-git-commit: 24ff17af89bc882f08ec0f331ebae53b61f35d78
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# Adobe Content Analytics擴充功能發行說明

以下為Content Analytics標籤擴充功能的發行說明清單。

| 版本 | 日期 | 修正 |
|---|---|---|
| <p>1.0.47</p> | <p>2025年7月23日</p> | <ul><li>修正客戶體驗未啟用且體驗的規則運算式檢查失敗時遇到的錯誤。 這會導致系統無法收集Content Analytics資料。</li><li>修正某些使用者在Experience Cloud中未設定主要預設語言時，無法顯示標籤UI的預設語言錯誤。</li></ul> |
| <p>1.0.46</p> | <p>2025年6月18日</p> | <ul><li>嘗試儲存擴充功能設定時，如果生產資料流不存在，請新增Toast通知。</li><li>暫時修正可見的Content Analytics裝載，但將簡化的Content Analytics裝載內容放入主控台。</li><li>新增擴充功能UI的當地語系化。</li><li>部分修正擴充功能UI內容周圍額外邊框間距的CSS問題。</li></ul> |
| <p>1.0.45</p> | <p>2025年4月14日</p> | <ul><li>解決在等待頁面檢視事件時保留Content Analytics事件時的一些組態設定錯誤。 現在，Content Analytics預設會等待以引發事件，直到「第一個頁面檢視」事件發生為止。</li></ul> |
| <p>1.0.44</p> | <p>2025年3月31日</p> | <ul><li>AppMeasurement整合的第一個反複專案。</li><li>此版本不支援篩選特定請求（例如頁面檢視），但日後可能會新增。  這也會使用在頁面上找到的第一個AppMeasurement執行個體。</li></ul> |
| <p>1.0.43</p> | <p>2025年3月10日</p> | <ul><li>初始擴充功能發行。</li></ul> |

