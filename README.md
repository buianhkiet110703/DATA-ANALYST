# I. Background (Bối Cảnh)
You are a Data Analyst working for an e-commerce company called X. You are given the standard task of giving a presentation to present an overview of the business and operations of the computer company. Up to the present time at for Sales Manager and Operations Manager. The presentation should at a minimum, include the following information: business overview, customer satisfaction, and 2 to 3 suggestions (area) where the company can improve.

(Bạn là một Data Analyst làm việc cho một công ty thương mại điện tử tên là X. Bạn được giao nhiệm vụ chuẩn bị một bài thuyết trình để trình bày tổng quan tình hình kinh doanh và vận hành của công ty tính đến thời điểm hiện tại cho Giám đốc bán hàng và Giám đốc vận hành. Bài thuyết trình tối thiểu phải bao gồm các thông tin sau: tổng quan tình hình kinh doanh, mức độ hài lòng của khách hàng, và đề xuất 2 đến 3 lĩnh vực (areas) mà công ty có thể cải thiện.)

# II. Analysis (Phân tích)

### Business situation of the company (Tình hình kinh doanh của công ty)
### 1. Business situation by year and month of the company (Tình hình kinh doanh theo năm và tháng của công ty)

```php
turnover= pd.pivot_table(df,index='month', columns='year', values='payment_value', aggfunc=np.sum, fill_value=0).reset_index(drop= False)
```
![image](https://user-images.githubusercontent.com/110837675/201594426-160a3d10-b32b-42d6-b80b-3ec0b2d62997.png)

#### A. Business situation by year (Tình hình kinh doanh theo năm)
```php
turnover_year= df.groupby('year')['payment_value'].sum().reset_index()
xs,ys= turnover_year['year'], turnover_year['payment_value']
plt.figure(figsize=(15,10))
plt.bar(xs,ys, color= sns.color_palette('Paired'));
plt.xlabel('year')
plt.ylabel('payment_value')
for x,y in zip(xs,ys):
    
        label = "{:.2f}".format(y)

        plt.annotate(label, # this is the text
                    (x,y), # these are the coordinates to position the label
                    textcoords="offset points", # how to position the text
                    xytext=(0,10), # distance from text to points (x,y)
                    ha='center') # horizontal alignment can be left, right or center

plt.show()
```
output:

![image](https://user-images.githubusercontent.com/110837675/201594590-3739c064-2fa8-4adf-aa47-af60ed97f01b.png)

 The company's business situation over the years has grown stronger, the revenue source has increased rapidly over the years, in 2016 the revenue was only 6,470 USD, in 2017 the revenue increased to 8,696,300 USD (revenue). In 2017 grew by 134% compared to 2016), and by September 2018 the revenue was $11,819,953 (September 2018 revenue grew by 36% compared to 2017, and had a growth of 182% compared to 2016). ). Therefore, the company has grown very strong, the number of sales orders in recent years has increased a lot, bringing a lot of revenue to the company.
 
 (Tình hình kinh doanh của công ty qua các năm có sự tăng trưởng mạnh mẽ, nguồn doanh thu tăng nhanh qua các năm, năm 2016 doanh thu chỉ vỏn vẹn là 6.470$, năm 2017 doanh thu tăng lên 8.696.300$ (doanh thu năm 2017 tăng trưởng 134% so với năm 2016), và đến 9/2018 doanh thu là 11.819.953$( doanh thu 9/2018 tăng trưởng 36% so với năm 2017, và có mức tăng trưởng 182% so với năm 2016), doanh thu trong 3 năm qua đã đã có sự tăng trưởng đột biến, mặc dù chỉ tới quý III năm 2018 doanh thu đã tăng 182%, rất nhiều so với với 2 năm trước. Vì vậy thấy được công ty đã phát triển rất là mạnh mẽ, số dơn hàng bán được trong các năm qua đã tăng rất nhiều mang lại rất nhiều doanh thu cho công ty.)
 
=> The company's high revenue shows that the company's business situation has improved and developed strongly over the years.

(Doanh thu của công ty tăng cao có thể thấy được tình hình kinh doanh của công ty có cải thiện tốt và phát triển mạnh qua các năm.)

#### B. Business situation by month (Tình hình kinh doanh theo tháng)

```php
turnover_month= df.groupby('month')['payment_value'].sum().reset_index()
x,y= turnover_month['month'], turnover_month['payment_value']
plt.figure(figsize=(15,10))
plt.plot(x,y)
plt.xlabel('month')
plt.ylabel('payment_value')
for a,b in zip(x,y):
    
        label = "{:.2f}".format(b)

        plt.annotate(label, # this is the text
                    (a,b), # these are the coordinates to position the label
                    textcoords="offset points", # how to position the text
                    xytext=(0,10), # distance from text to points (x,y)
                    ha='center') # horizontal alignment can be left, right or center

plt.show()
```
output:

![image](https://user-images.githubusercontent.com/110837675/201618347-d13af184-dde8-4c39-8fa2-d708d47f97cc.png)

- Revenue from January to August generally has a uniform growth, and August revenue has a marked increase compared to the previous months, but this is only September 2018 not enough data to evaluate. Prices in the months after September 2018, but it can be seen that the increase in monthly revenue shows that the company has a good development.

(Doanh thu từ tháng 1 cho tới tháng 8 nhìn chung có sự tăng trưởng đồng đều, và doanh thu tháng 8 có sự tăng cao rõ rệt so với những tháng trước đó, tuy nhiên đây mới là 9/2018 chưa đủ dữ liệu để đánh giá các tháng sau tháng 9/2018,nhưng có thể thấy là doanh thu các tháng có sự tăng đều chứng tỏ công ty có sự phát triển tốt.)

### 2. Top product groups (product_category_name) bring the most revenue for the company (Top nhóm sản phẩm (product_category_name) mang lại doanh thu nhiều nhất cho công ty)

```php
df.groupby('product_category_name')['payment_value'].sum().nlargest(10).reset_index()
```
Output:

![image](https://user-images.githubusercontent.com/110837675/201618412-00feb514-8a89-425f-978a-56f8facc8ad2.png)

The product groups above the table are the best-selling and highest-recall product groups for the company. Those are the strong products of the company store because the company's revenue is mainly due to those product groups falling behind. Therefore, we need to focus more resources to develop our company's strong products. The following ideas can be developed:
 
(Những nhóm sản phẩm ở trên bảng, đó là nhóm sản phẩm bán chạy nhất và đem lại doanh thu cao nhất cho công ty. Đó là những sản phẩm thế mạnh của cửa hàng công ty vì doanh thu của công ty chủ yếu là do những nhóm sản phẩm đó đem lại. Vì vậy chúng ta cần phải tập trung nhiều nguồn lực để mà phát triển những sản phẩm thế mạnh của công ty mình lên nữa. Có thể phát triển bằng những ý sau đây:)

- After knowing the company's strong selling product groups, you can: (Sau khi đã biết những nhom sản phẩm thế mạnh bán chạy của công ty thì có thể)
  
  -Product ecosystem development. More specifically, focus on building, supporting products, auxiliary products or accessories for these top products.
  
  (phát triển hệ sinh thái của sản phẩm. Cụ thể hơn, tập trung xây dựng các sản phẩm hỗ trợ, sản phẩm phụ trợ hoặc phụ kiện cho các sản phẩm top này.)
  
  -Provide vouchers for ancillary products (ecosystem) when buying top products, to stimulate demand they can buy additional accessories.
  
  (Cung cấp voucher cho các sản phẩm phụ trợ (hệ sinh thái) khi mua các sản phẩm top, để kích cầu họ có thể mua thêm các sản phẩm phụ kiện đi theo.)

### 3. Number of orders delivered successfully and canceled (Số đơn hàng giao thành công và bị hủy)

![image](https://user-images.githubusercontent.com/110837675/201618598-da610c8c-9357-4db5-b988-72871bd1520b.png)

-Looking at the data table, the number of canceled orders is 750 orders, accounting for 0.7% of the total number of successfully delivered orders, we need to find out the reason why the orders are canceled for any reason and from there we need to fix it. To minimize the number of canceled orders. These are the customer ids who cancel the most orders:

(Nhìn vào bảng số liệu, số đơn hàng bị hủy là 750 đơn chiếm 0.7% trong tổng số các đơn hàng giao thành công,chúng ta cần phải tìm ra nguyên nhân số đơn hàng bị hủy vì lý do gì và từ đó cần phải khắc phục để cho số đơn hàng bị hủy càng ít lại. Đây là những id khách hàng hủy đơn hàng nhiều nhất:)

![image](https://user-images.githubusercontent.com/110837675/201618700-5d16a9a3-01a7-4dc4-98a7-da06e5a424a7.png)

   -These are the customer ids with the most order cancellations, need to find out the reason for canceling orders from them, and we should also warn them to help them reduce the cancellation rate by is that the promotional vouchers for these people will be limited and they are unlikely to receive much discount vouchers, or the shipping time will be longer than expected, and the order account will be limited. In some articles, which have been cancelled a lot...

(Đây là những id khách hàng có số lần hủy đơn hàng nhiều nhất cần tìm hiểu nguyên nhân hủy đơn hàng từ họ vì lý do gì, và chúng ta cũng nên cảnh cáo họ đẻ cho họ giảm tỉ lệ hủy đơn hàng xuống bằng cách là những voucher khuyến mãi đối với những người này sẽ bị hạn chế và họ khó có thể nhận được những voucher giảm giá nhiều, hoặc là  thời gian vận chuyển của sẽ bị lâu hơn dự kiến, và  tài khoản đặt hàng sẽ bị hạn chế ở một số mặt hàng mà bị hủy nhiều...)

### 4. Payments (Hình thức thanh toán)

```php
plt.figure(figsize=(12,6))
sns.countplot(data=df, x='payment_type');
```
Output:

![image](https://user-images.githubusercontent.com/110837675/201619137-c9f1a7b4-728a-4f8c-8146-44751c6b1693.png)

-Based on the chart, the form of payment that customers use the most to pay is credit_card, because people often have the habit of shopping online with credit cards.

(Dựa vào biểu đò thì hình thức thanh toán mà khách hàng dùng để thanh toán nhiều nhất là credit_card, Vì mọi người thường có thói quen mua sắm online bằng thẻ tín dụng.)

=>The goal is to minimize cash transactions. Prioritize payment via credit card/debit card to minimize the rate of customers not receiving the goods.
(Mục tiêu là hạn chế tối đa các giao dịch bằng tiền mặt. Ưu tiên thanh toán qua thẻ credit card/debit card để giảm thiểu tỉ lệ khách không nhận hàng.)

=> Create promotions that apply to credit/debit card payments. (Tạo các chương trình ưu đãi áp dụng cho hình thức thanh toán bằng thẻ tín dụng/ghi nợ.)


### 5. Customer review title (Tiêu đề đánh giá của khách hàng)

```php
df.groupby('review_comment_title')['customer_id'].count().sort_values(ascending= False).nlargest(5).to_frame()
```
Output:

![image](https://user-images.githubusercontent.com/110837675/201619329-70623489-bde8-4e7f-be0a-da68e2db3179.png)

Translate the meanings of the words in the table (Dịch nghĩa các từ trong bảng:)

-Recomendo: khuyên, đề nghị

-Bom: Tốt

-super recomendo: rất khuyên bạn nên

-Excelente : Tuyệt

-Muito bom : rất tốt

- Looking at the data table, recomendo and super recomendo are rated by customers quite a lot, which shows that seller_id's products are not really good.
 advised and suggested by customers to correct, the sales people should approach and take care of them to find out the cause of the bad products, then absorb and improve the product to match the needs. from buyers, thereby increasing sales revenue.

(Nhìn vào bảng số liệu thì recomendo và super recomendo được khách hàng đánh giá khá là nhiều, điều đó cho thấy sản phẩm của seller_id(id người bán) chưa thật sự tốt
được khách hàng khuyên và đề nghị sửa đối, những người bán hàng nên tiếp cận và chăm sóc họ tìm ra được nguyên nhân của những sản phẩm không tốt ở đâu từ dó tiếp thu và cải thiện lại sản phẩm để cho đúng với nhu cầu của người mua, từ đó mới có thể tăng doanh thu bán hàng lên cao được.)

- For products that are well-reviewed by customers, it is advisable to continue to maintain the quality of that product and continue to develop higher quality to earn more revenue. 

(Đối với những sản phẩm được khách hàng đánh giá tốt thì nên tiếp tục giữ vững chất lượng sản phẩm đó và tiếp tục phát triển chất lượng cao hơn nữa để kiếm được doanh thu nhiều hơn nữa)

### 6.Customer Satisfaction Level. (Mức Độ Hài Lòng của khách hàng.)

```php
star= df.groupby('review_score')['customer_id'].count().reset_index(name='count')
ax= star['review_score']
bx= star['count']
plt.figure(figsize=(15,6))
plt.pie(bx, labels=ax ,autopct='%1.1f%%');
```
Output:

![image](https://user-images.githubusercontent.com/110837675/201619753-3ff64aaa-10d5-4824-af45-201175d646f9.png)

-For product groups that are rated 1 and 2 points, we need to reconsider, need to find out the reason, and consider which product group 1,2 reviews come from / seller id, thereby improving product quality to meet the needs of customers.

(Đối với những nhóm sản phẩm bị đánh giá 1 và 2 điểm thì chúng ta cần phải xem xét lại , cần tìm hiểu nguyên nhân, và xem xét xem các đánh giá 1,2 đến từ nhóm sản phẩm nào/id người bán nào, từ đó cải thiện lại chất lượng sản phẩm cho đúng nhu cầu khách hàng.)

### 7. List of product groups rated 1 and 2 points (Danh sách những nhóm sản phẩm bị đánh giá 1 và 2 điểm)

```php
star12= df.loc[(df['review_score']== 1)|(df['review_score']==2)]
pd.crosstab(star12.product_category_name, star12.review_score).sort_values(by=1, ascending=False)
```
Output:

![image](https://user-images.githubusercontent.com/110837675/201619855-91f640ed-1779-4d9b-a161-48d14e32d8fd.png)


These are lists of product groups that are rated 1 and 2 points. (Đây là những danh sách nhóm sản phẩm bị đánh giá 1 và 2 điểm.)

Step 1: We have to find out the reason from the seller id (seller_id) why customers rate 1 and 2 points.
(Bước 1: Chúng ta phải tìm hiểu nguyên nhân từ những id của người bán hàng(seller_id) tại sao khách hàng lại đánh giá 1 và 2 điểm.)

Step 2: We need to collect customer feedback, find out the reason. 
(Bước 2: Chúng ta cần phải thu tập những phản hồi của khách hàng, tìm hiểu nguyên nhân.)

Step 3: Categorize the cause. Is a bad review due to a bad product or bad service? If it is due to the product, consider improving the quality of the product, or removing the product from the sales list. If it is due to poor service quality, it is necessary to find out and work with the supplier.
(Bước 3: Phân loại nguyên nhân. Điểm đánh giá tệ là do sản phẩm tệ hay chất lượng dịch vụ tệ? Nếu là do sản phẩm, thì cần cân nhắc nâng cao chất lượng sản phẩm, hoặc loại sản phẩm khỏi danh mục bán hàng. Nếu là do chất lượng dịch vụ tệ, cần tìm hiểu và làm việc với nhà cung cấp.)

Step 4: If the reason for evaluating 1 2 points is legitimate, it is necessary to take measures to compensate the customer. It is possible to compensate with an email voucher to apologize, promising to improve service/product quality.
(Bước 4: Nếu lí do đánh giá 1 2 điểm là chính đáng, cần có biện pháp đền bù cho khách hàng. Có thể đền bù bằng voucher qua email xin lỗi, hứa hẹn sẽ cải thiện chất lượng dịch vụ/sản phẩm.)


### 8. List of seller ids with 1 and 2 star reviews. (Danh sách id người bán có lượt đánh giá 1 và 2 sao.)

```php
star12.groupby('seller_id')['review_score'].count().sort_values(ascending=False).nlargest(10).reset_index()
```
Output:

![image](https://user-images.githubusercontent.com/110837675/201619931-7d93d822-d47e-47da-bf76-c8355427cee8.png)

These are the seller id lists with the highest ratings of 1 and 2. In this case, the company needs 
(Đây là những danh sách id người bán có bán lượt rating 1 và 2 điểm cao nhất. Đối với trường hợp này thì công ty cần)

Step 1: Classify the causes from rating 1 and 2 points. 
(Bước 1: Phân loại các nguyên nhân từ rating 1 và 2 điểm.)

Step 2: Ask the seller to explain about the rating of 1 or 2 points. Seller needs to present the way to remedy the consequences, improve the product/service and commit to doing so.
(Bước 2: Đề nghị seller giải trình về việc bị rating 1, 2 điểm. Seller cần trình bày hướng khắc phục hậu quả, cải thiện sản phẩm/dịch vụ và cam kết thực hiện.)

Step 3: Compensate customers with bad experiences. (voucher, refund, product exchange, ...)
(Bước 3: Đền bù cho các khách hàng có trải nghiệm không tốt. (voucher, hoàn tiền, đổi trả sản phẩm,…))

Step 4: Evaluate the seller's ability. If the rating of 1 or 2 points is too much, the seller does not improve the product or service => ban id seller.
(Bước 4: Đánh giá năng lực của seller. Nếu lượt rating  1, 2 điểm quá nhiều, seller không cải thiện sản phẩm, dịch vụ => cấm id seller.)

 
And should warn seller id, when being rated 1 and 2 stars, that low score will be pushed up and will bring trouble to other customers when they see such low score, they will lose faith in the product. Doubts about quality and do not make a purchase decision will make sales go down, orders will not be sold much anymore, and especially they have to improve their own products.

(Và nên cảnh báo id seller, khi bị đánh giá 1 và 2 sao thì số điểm thấp đó bị đẩy lên và sẽ làm hang mang cho những khách khác khi thấy lượt điểm thấp như vậy, họ sẽ mất niềm tin vào sản phẩm,có sự nghi ngờ về chất lượng và không đưa ra quyết định mua hàng sẽ làm cho doanh số đi xuống đơn hàng sẽ không còn được bán nhiều nữa, và đặc biệt là họ phải tự cải thiện sản phẩm của mình.)

### 9. Customers with the most orders. (Những khách hàng có số lần đặt hàng nhiều nhất.)

```php
df.groupby('customer_id')['order_id'].count().sort_values(ascending=False).head(10).to_frame()
```
Output:

![image](https://user-images.githubusercontent.com/110837675/201620781-3073b600-f58e-46fb-86f1-c2287abe3013.png)

- This is a list of customers with the highest number of orders at the company, they are the ones who believe in the company's products, so it is necessary to pay attention to taking care of them regularly so that they do not leave buying products from the company. own company.

(Đây là danh sách những khách có số lần đặt hàng nhiều nhất ở công ty, họ là những người tin tưởng những sản phẩm ở công ty nên cần phải chú trọng chăm sóc họ thường xuyên để họ không rời bỏ việc mua sản phẩm bên công ty mình.)

Usually, consumers tend to choose to buy in bulk. Therefore, when a business satisfies the existing group of customers, these people will act as intermediaries to introduce products / services to their acquaintances. Unwittingly, loyal customers have become salespeople for the products of the businesses they trust. This will be vital to business enterprises in the 4.0 era, where the power of word-of-mouth marketing is being blown along with the development of the internet. Almost just need to take good care of existing customers, will have more new customers.
Treatments may include:

(Thông thường, người tiêu dùng đều có xu hướng lựa chọn mua hàng theo số đông. Vì vậy, khi một doanh nghiệp làm hài lòng nhóm khách hàng hiện tại, những người này sẽ đóng vai trò làm trung gian giới thiệu sản phẩm/ dịch vụ với những người quen biết của mình. Một cách vô tình, những khách hàng trung thành đã trở thành những nhân viên bán hàng cho sản phẩm của doanh nghiệp họ tin tưởng. Điều này sẽ mang ý nghĩa sống còn với các doanh nghiệp kinh doanh thời đại 4.0, nơi sức mạnh của phương pháp marketing truyền miệng đang được thổi bùng cùng với sự phát triển của internet. Gần như chỉ cần chăm sóc tốt khách hàng hiện tại, sẽ lại có thêm khách hàng mới.
Các phương pháp chăm sóc có thể như:)

-	Give vouchers to customers when reaching spending levels according to each milestone. (Tặng voucher cho các khách hàng khi đạt mức chi tiêu theo từng mốc.)

-	Email inquires when customers do not buy goods for a long time. (Email hỏi thăm khi không thấy khách mua hàng trong thời gian dài.)


### 10. List of customers who bring the highest revenue for the company. (Danh sách những khách hàng đem lại doanh thu cao nhất cho công ty.)

```php
df.groupby('customer_city')['payment_value'].sum().sort_values(ascending=False).to_frame().head(10)
```

![image](https://user-images.githubusercontent.com/110837675/201620909-5e4baae9-41e7-49f5-9995-14a2645ea644.png)

-These are the top 10 customers that bring the main revenue to the company, we need to pay special attention and care to these customers so that they do not leave our services, and need to create promotional vouchers. Best forever to encourage them to buy their products, because they are the main source of income for the company, if not well taken care of, they will leave then the company's revenue will go down. Although customers order from the company a lot, but based on the Pareto chart, it can be seen that only 20% of those customers bring in 80% of the company's profits, so it is necessary to take special care of these customers.

(Đây là top 10 khách hàng đem lại chủ yếu doanh thu cho công ty, chúng ta cần chú ý và chăm sóc đặc biệt những khách hàng này nhiều hơn để họ không rời bỏ dịch vụ của mình, và cần tạo ra những cái voucher khuyến mãi tối ửu để có khuyến khích họ mua hàng của mình, vì họ là nguồn thu nhập chính của công ty nếu không chăm sóc tốt họ sẽ rời bỏ khi đó doanh thu công ty sẽ đi xuống. Tuy khách đặt hàng ở công ty nhiều nhưng dựa vào biểu đồ pareto thì thấy đucợ chỉ có 20% khách hàng đó đem lại chủ yêu 80% lợi nhuận của công ty nên vì thế cần phải chăm sóc đặt biệt những vị khách hàng này.)

### 11. Percentage of customers paying in a lump sum and one-time payment. (Phần trăm khách hàng trả hóp và thanh toán một lần.)

![image](https://user-images.githubusercontent.com/110837675/201646035-819ac2db-5a6b-43c5-b3a1-394a18067ea6.png)

-The number of one-time payments and installment payments are almost the same, but for installment customers, we need to pay attention and remind them to learn to pay debt and interest on time, to avoid annoying cases. both of us have to call and text them and hpj will both be bothered by my messages and their interest will increase if not paid on time.

(Số lần thanh toán một lần và thanh toán trả góp gần như tương đương nhau, nhưng đối với khách hàng trả góp chúng ta cần phải chú ý và cần nhắc nhở họ để học trả nợ và lãi đúng hạn, để tránh trường hợp làm phiền cả đôi bên mình phải gị điện và nhắn tin với họ và hpj sẽ cụng bị phiền bởi bởi những tin nhắn của mình và lãi của họ sẽ bị gia tăng theem nếu không trả đúng hạn.)

### 12. Cities that bring in the highest revenue for the company (Những thành phố đem lại doanh thu cao nhất cho công ty)

```php
df.groupby('customer_city')['payment_value'].sum().sort_values(ascending=False).to_frame().head(10)
```
Output:

![image](https://user-images.githubusercontent.com/110837675/201646151-532014b0-4896-4977-922f-49a77649dbe7.png)

- The company's revenue is mainly concentrated in these cities, proving that customers are mainly concentrated in these cities for optimization, it is advisable to place warehouses so that transshipment can be saved. Save more and customers when ordering can receive their goods faster and they also save on their shipping costs.

(Doanh thu của công ty chủ yếu tập trung ở những thành phố này, chứng tỏ khách hàng chủ yếu tập trung ở những thành phố này để mà tối ưu hóa thì chứng ta nên đặt những kho hàng để mà việc trung chuyển có thể được tiết kiệm nhiều hơn và khách hàng khi dặt hàng có thể nhận hàng nhanh chóng hơn và họ cũng đỡ việc phí hip nhận hàng của mình.) 

### Provide solutions for the company (Đưa ra giải pháp cho công ty)
# III. Conclusion (Kết luận)

- The company's business situation in the past 3 years has developed strongly when the revenue has increased a lot each year, the number of sales orders has also increased significantly, but the monthly revenue has changed. not crowded when the first months of the year sold a lot of orders, but conversely, the months at the end of the year, the revenue decreased more than we need to review to improve this. For product groups that bring high revenue to the company, it is necessary to focus resources to develop more strongly because it is their strength, and for installment customers, employees need to pay attention and reminding them to pay their debts and interest on time, in addition, taking care of customers who bring high revenue to the company is also very important because they are the lifeblood of the company, so it is necessary to have a customer care team. special for these people.

(Tình hình kinh doanh của công ty trong 3 năm trở lại đây có bước phát triển mãnh mẽ khi mà doanh thu tăng lên rất nhiều qua mỗi năm, số đơn hàng bán được cũng tăng lên đáng kể, nhưng doanh thu theo mỗi tháng có sự không đông đều khi mà những tháng đầu năm thì bán được rất là nhiều đơn hàng nhưng ngược lại những tháng ở cuối năm thì doanh thu lại bị giảm hơn chúng ta cần xem xét lại để cải thiện điều này. Đối với những nhóm sản phẩm đem lại doanh thu cao cho công ty thì cần tập trung nguồn lực để phát triển mạnh mẽ hơn nữa vì nó là thế mạnh của mình, còn với những khách hàng trả góp thì các nhân viên cần chú ý và nhắc nhở họ đóng nợ và tiền lãi đúng hạn, ngoài ra việc chăm sóc những khách hàng đem lại doanh thu cao cho công ty cũng rất quan trọng vì họ là nguồn sống của công ty nên vì thế cần phải có đội ngũ chăm sóc khách hàng dặc biệt đối với những người này.)

Areas where the company can improve: (Các lĩnh vực mà công ty có thể cải thiện)

  - The first is that the product and seller id have low ratings, this is the first important thing the company needs to improve, the company needs to remind about the seller id has to improve for the items that are damaged. low rating, because customers often have the phenomenon of following the crowd when the product rating is so low, it will make the customers behind them feel afraid about making a purchase decision, maybe they will give up the product service. products to choose a service to buy from another company. In order to improve this, it is necessary to collect and listen to all customer opinions about the product, thereby improving the product to suit the market needs and customers' needs.
  
  (Thứ nhất là về việc các sản phẩm và id người bán có lượt rating thấp thì đây là việc quan trọng đầu tiên công ty cần cải thiện, công ty cần nhắc nhở về việc id các người bán phải cải thiện đối với những món hàng bị rating thấp, vì khách hàng hay có hiện tượng theo số đông khi sản phẩm rating thấp như vậy thì sẽ làm cho những khách hàng phía sau thấy sẽ e ngại về việc đưa ra quyết định mua hàng, có thể họ sẽ bỏ dịch vụ sản phẩm bên mình để mà chọn một dịch vụ mua hàng bên công ty khác. Để mà cải thiện đucợ việc này thì cần phải thu thập và lắng tất cả ý kiến khách hàng về sản phẩm từ đó sẽ cải thiện lại sản phẩm cho nó phù hợp với nhu cầu thị trường và nhà ngu cầu của khách hàng.)
  
    -The second is about taking care of customers that bring high profits to the company, because they are a living part of the company, contributing very high revenue to the company, in order to retain them, it is necessary to have a caring team. Special customer care for these customers, need to regularly email or call to ask them about our products, in addition we can create special vouchers based on customers This is to retain them and stimulate them to buy their products, as mentioned above, customers often follow the phenomenon of the majority. Therefore, when a business satisfies the existing group of customers, these people. will act as an intermediary to introduce products/services to his acquaintances. Unwittingly, loyal customers have become salespeople for the products of the businesses they trust.
    
    (Thứ hai là về việc chăm sóc khách hàng đem lại lợi nhuận cao cho công ty, vì họ là một phần sống cảu công ty đóng góp doanh thu cho công ty rất là cao để mà giữ chân được họ thì cần phải có đội ngũ chăm sóc khách hàng dặc biệt đối những vị khách này, cần phải thường xuyên gửi mail hoặc gọi điện thăm dò ý kiến của họ về sản phẩm của mình, ngoài ra chúng ta có thể tạo ra những cái voucher đặc biệt dựa trên những khách hàng này để mà giữ chân họ và kích cầu họ mua sản phẩm bên mình, như đã nói ở trên khách hàng thường hay theo hiện tượng số đông .Vì vậy, khi một doanh nghiệp làm hài lòng nhóm khách hàng hiện tại, những người này sẽ đóng vai trò làm trung gian giới thiệu sản phẩm/ dịch vụ với những người quen biết của mình. Một cách vô tình, những khách hàng trung thành đã trở thành những nhân viên bán hàng cho sản phẩm của doanh nghiệp họ tin tưởng.) 
    
  -Thirdly, about the installment customers, the company needs to pay attention to this group of installment customers. It needs to notify the customer care department to regularly pay attention and see if they have paid their debt and interest on time. or not, remind them, to overcome this situation, we can create promotions for customers who pay once to stimulate them to buy and pay once.
  
  (Thứ ba là về việc những khách hàng trả góp, công ty cần chú ý đối với nhóm khách hàng trả góp này cần thông báo bên bộ phận chăm sóc khách hàng để thường xuyên chú ý và xem họ đã đóng nợ và tiền lãi đúng hạn hay chưa từ đó mà nhắc nhở họ, để khắc phục tình trạng này thì chúng ta có thể tạo ra những cái khuyến mãi đối với những khách hàng thanh toán một lần để có thể kích cầu họ mua hàng và trả một lần luôn.)
  
  
[Click the link to view the dashboard](https://app.powerbi.com/groups/7ddb72d0-2e02-4a0e-b5c4-8d1493524633/reports/9cd9c119-a222-4fe1-93c3-58cc08bf4a82/ReportSection)
   
   




