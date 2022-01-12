#Week3 3 kinds collaborative filtering testing
- User-based collaborative filtering
- Item-based collaborative filtering
- 套件 surprise 實作 collaborative filtering

Test1: 僅使用User-based或Item-based進行推薦，沒有補滿10個推薦的效果: user:0.001695、item:0.001695

Test2: 想知道歷史紀錄中，具有多少數量會影響多少推薦效果，目前假設擁有較多歷史紀錄筆數的人(>1)，較可能得到更正確的推薦，但因為筆數刪除後與原筆數差異很大，因此此結果有可能是樣本數較不足或是僅有一次消費的結果也影響大，目前傾向是因為樣本數不足，因為單使用collaborative filtering的效果極小: user:0、item:0

Test3: 比較Test1，為surprise中KNNBasic算法的推薦，沒有補滿10個推薦的效果(含有全筆部筆數，因RAM不足問題，使用2016.8.1-2018.9.30、去除僅一筆交易紀錄的ID): full_data:0、remove: 0

Test4: Test1加上content-based用title進行相似度推薦，最後以rule-based推薦list補足不足10項推薦的部分: user: 0.133898、 item: 0.133898

Test5: Test4 僅留下具有較多歷史紀錄的ID(>1): user: 0.133898、 item: 0.133898

Test6: 比較Test4，為surprise中KNNBasic算法的推薦，加上content-based用title進行相似度推薦，最後以rule-based推薦list補足不足10項推薦的部分(使用2016.8.1-2018.9.30):  full_data:0.128814、remove: 0.132203

此專案有達到專案的目的效果，但效果微小。
