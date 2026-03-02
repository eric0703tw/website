Hi YB:
DKQA與DEQA順序的邏輯性問題
我們發現TDM流程，DKQA 排在DEQA的後面，如果工作流程是這樣，會有幾個邏輯性的問題

1.2025年DEQA 抓到這些PDK的問題，DKQA的目的是改善PDK的正確性，如果工作流程還是排在DEQA的後面，那麼PDK錯誤的比例不會有明顯的改善。

2. 如果DEQA抓到PDK fail了，經過修正後再來做DKQA,一開始的一致性就錯了，DKQA如何能證明PDK的正確性，也就是這個DKQA的正確性是不可信的，除非它一開始就能通過一致性的錯誤。

3.DEQA 從v0.90才開始做，所以v0.90之前是不做DKQA? 這樣能有效改善PDK的正確性?

4.Spice model 是model team QA過才上傳TDM 給我們檢查一致性，Design kit 應該也是要先做QA後才給我們做一致性的檢查


所以我建議DKQA應該在DEQA之前，這樣才能有效改善PDK的正確性與一致性。



