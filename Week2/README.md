# Content based Recommend system
思考方向:

1.原本預期使用metadata的ranking，作為category分類，但因數量集中在某一類別，因此不使用此方法。

2.使用metadata中title項，去除重複的部分後，進行NLP的資料前處理，包含:去除標點符號、字母小寫化、Lemmatization、去除stopwords。

      需要有次序性的使用，例如先使用remove_punctuation，這樣區分字詞的時候才不會無意義的字母連在一起；
      
      使用Lemmatization而不使用stemming的原因，也是因為爬文看到Lemmatization可以更好的處理黏在一起的字符，且是會考慮前後文及單字意義的轉換形式。
      
3.NLP前處理完，便進行TF-IDF計算

推薦所做的嘗試為:

A. 使用全部的testing data(所有顧客的平均成效)

    0. 僅使用title的TF-IDF結果去進行相似性推薦
         
       > 可能因分母較大而稀釋了效果
    
    1. 僅使用brand分類，由ranking最高者進行分類推薦
    
    2. 使用title的TF-IDF結果去進行相似性推薦，不足10個推薦的項目用Top-10的項目由最熱門開始補充
    
        > 使用title的相似性結果、Top-10合併進行推薦效果變好，與B3.的結果比較，可能因新顧客的Top-10推薦較佳，所以分數接近
    3. 限制training data時間在最新的三個月內，使用title的TF-IDF結果去進行相似性推薦，不足10個推薦的項目用Top-10的項目由最熱門開始補充
    
    4. 限制training data時間在最新的三個月內，使用title的TF-IDF結果去進行相似性推薦，不足10個推薦的項目用Top-15的項目隨機抽取補充
    
        > 3、4可見直接使用Top-10推薦效果較佳
        
![image](https://user-images.githubusercontent.com/49614247/147875800-85c979a5-30c4-4b1a-9f94-5c42482b568a.png)

B. 僅使用有出現在training data中的顧客進行計算，以此計算回頭客的推薦成效

    0. 僅使用title的TF-IDF結果去進行相似性推薦
    
        > 以A、B兩種的1.結果來看，僅使用title的效果在購物超過一次的顧客效果較佳，但效果仍有限
        
    1. 僅使用brand分類，由ranking最高者進行分類推薦
    
        > A、B的結果皆不佳
        
    2. 使用title的TF-IDF結果去進行相似性推薦，不足10個推薦的項目用Top-10的項目由最熱門開始補充
    
        > 使用title的相似性結果、Top-10合併進行推薦效果在舊顧客的反應上變差，需要檢查一下，因A1.有0.11，理論來說加上Top-10應該要持平或是變佳
        
    3. 限制training data時間在最新的三個月內，使用title的TF-IDF結果去進行相似性推薦，不足10個推薦的項目用Top-10的項目由最熱門開始補充
    
        > 使用title的相似性結果、Top-10合併進行推薦效果
        
    4. 限制training data時間在最新的三個月內，使用title的TF-IDF結果去進行相似性推薦，不足10個推薦的項目用Top-15的項目隨機抽取補充
    
![image](https://user-images.githubusercontent.com/49614247/147875807-9e9ba56c-e383-40e5-b0fd-91f971df0e25.png)
    

