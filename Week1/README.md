# data-course-sample

split data
train data: ~ 2018-09-01
test data: 2018-09-01 ~ 2018-09-30

工具
pandas, numpy, gzip, json

使用兩種方法進行推薦
1. 直接使用最多被購買的Top 10商品做為推薦
2. 使用個別user在2018-09-01以前購買過的類別，推薦此類別依比例的前幾項，如果沒有類別或是不曾購買，就使用方法推薦分數平均最高作為推薦依據，若有同分者則依購買次數最高作為推薦商品
3. 使用個別user在2018-09-01以前購買過的類別，推薦此類別依比例的前幾項，如果沒有類別或是不曾購買，就使用使用最多被購買的Top 10商品做為推薦商品(與方法一合併)
4. 使用個別user在2018-06-30~2018-09-01之間購買過的類別，推薦此類別依比例的前幾項，如果沒有類別或是不曾購買，就使用使用此區間最多被購買的Top 10商品做為推薦商品

方法1. Recal: 0.083051
方法2. Rcall: 0 ->可能因類別稀疏所以較少推薦的項目，所以最後大半都著重在後半的平均數最高的規則上，可能兩項規則都不佳(方法3.會進行測試)
方法3. Rcall: 0.083051  ->可以佐證方法2.的後半規則應該也叫不適用
方法4. Rcall: 0.135593  ->代表可能因越靠近的時間區間，越接近此商店購買商品的熱門趨勢
