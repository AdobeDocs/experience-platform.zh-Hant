---
title: Adobe Content Analytics擴充功能發行說明
description: Adobe Experience Platform中Content Analytics標籤擴充功能的最新發行說明。
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 9fad0b092263c08a2744023b08f5f353f2c85422
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---

# Adobe Content Analytics擴充功能發行說明

以下為Content Analytics標籤擴充功能的發行說明清單。

| 版本 | 日期 | 修正 |
|---|---|---|
| 1.0.47 | 2025年7月23日 | <ul><li>修正未啟用體驗時所發生的錯誤，此錯誤會導致體驗的規則運算式檢查失敗。 此問題會導致無法收集Content Analytics資料。</li><li>解決預設語言設定無法向某些未在Experience Cloud中設定主要預設語言的使用者顯示標籤UI的問題。</li></ul> |
| 1.0.46 | 2025年6月18日 | <ul><li>已新增在嘗試儲存擴充功能設定時（如果生產資料流不存在）的toast通知。</li><li>暫時修正Content Analytics裝載的可見度問題，方法是將字串化的裝載內容改為置於主控台。</li><li>新增擴充功能UI的本地化支援。</li><li>部分修正CSS問題，此問題導致擴充功能UI內容周圍出現額外邊框間距。</li></ul> |
| 1.0.45 | 2025年4月14日 | <ul><li>已解決在等待頁面檢視事件時與保留Content Analytics事件相關的組態設定中的幾個錯誤。 Content Analytics現在預設會等到第一個頁面檢視事件發生後再引發事件。</li></ul> |
| 1.0.44 | 2025年3月31日 | <ul><li>AppMeasurement整合的第一個反複專案。</li><li>此版本尚不支援篩選特定請求（例如頁面檢視），但此功能可在未來的更新中新增。 其目前使用在頁面上找到的第一個AppMeasurement執行個體。</li></ul> |
| 1.0.43 | 2025年3月10日 | <ul><li>初始擴充功能發行。</li></ul> |
