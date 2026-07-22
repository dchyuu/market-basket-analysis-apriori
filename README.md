# Market Basket Analysis with Apriori

> Mini project thực hành Apriori và Association Rules để phát hiện các nhóm hàng thường được mua cùng nhau.

[**Mở notebook**](./market_basket_analysis_apriori.ipynb)

## Project overview

Một beauty retailer muốn thiết kế combo khuyến mãi và sắp xếp gian hàng dựa trên hành vi mua kèm. Project chuyển dữ liệu giao dịch thành basket matrix, khai phá frequent itemsets ở cấp Subcategory và đánh giá luật kết hợp bằng support, confidence và lift.

Project được xây dựng như một **mini project học tập**, tập trung chứng minh khả năng áp dụng kỹ thuật phân tích vào một business question cụ thể.

## Business questions

1. Những subcategory nào thường xuất hiện cùng nhau trong một đơn hàng?
2. Luật nào có mức liên kết mạnh nhất theo lift?
3. Luật nào đủ support và confidence để có tính ứng dụng kinh doanh?
4. Các nhóm hàng nào đóng vai trò trung tâm trong combo?

## Dataset

| File | Vai trò / trường dữ liệu chính |
| --- | --- |
| EcomSales.csv | `OrderID`, `ProductCode`, `Quantity`, `OrderDate` |
| Product.csv | `ProductCode`, `Category`, `Subcategory` |


### Download data

Do kích thước dữ liệu lớn, các file dữ liệu đầy đủ không được lưu trực tiếp trong repository.

[**Mở thư mục dữ liệu dùng chung trên Google Drive**](https://drive.google.com/drive/folders/1NrvyT_tMArcoZvI_sEgPLclD4Vw0iCBq?usp=sharing)

Chỉ cần tải các file được liệt kê trong bảng phía trên; các file còn lại trong thư mục Drive được sử dụng cho những mini project khác. Giữ nguyên tên file để notebook đọc dữ liệu chính xác.

> Quyền chia sẻ đề xuất: **Anyone with the link → Viewer**. Hãy kiểm tra link bằng cửa sổ ẩn danh trước khi public repository.

## Techniques practiced

- Merge transaction và product master data
- One-hot encoding để tạo basket matrix
- Frequent itemset mining bằng Apriori
- Association rules với support, confidence và lift
- Chọn `min_support` và lọc luật theo business relevance
- Tạo `potential_score` để cân bằng độ mạnh và quy mô

## Main KPIs

| KPI | Ý nghĩa |
| --- | --- |
| Support | Tỷ lệ đơn hàng chứa itemset hoặc rule |
| Confidence | Xác suất mua consequent khi đã mua antecedent |
| Lift | Mức liên kết so với hành vi mua độc lập |
| Order Count | Số đơn hàng ước tính chứa combo |
| Potential Score | Điểm ưu tiên kết hợp nhiều tiêu chí |


## Analysis workflow

1. Làm sạch giao dịch và product master.
2. Merge theo `ProductCode` và chọn cấp phân tích Subcategory.
3. Tạo basket matrix theo `OrderID`.
4. Chạy Apriori với `min_support = 0.001`.
5. Sinh association rules và chuyển frozenset thành text.
6. So sánh luật mạnh nhất với luật có tính ứng dụng kinh doanh.

## Key findings

- Luật có lift cao nhất là `fragrances → Nail care products + body moisturizers`, nhưng chỉ xuất hiện khoảng **32 đơn** và confidence khoảng **5.3%**.
- Combo thực tế hơn là `Accessories + brushes and applicators → Nail care products`, với khoảng **75 đơn**, confidence **33.5%** và lift **1.68**.
- `Nail care products` xuất hiện nổi bật trong nhiều combo tiềm năng.

## Recommendations

- Thử bundle nhỏ hoặc cross-sell Nail care products khi khách mua phụ kiện và dụng cụ làm đẹp.
- Dùng luật lift cao nhưng volume thấp cho thử nghiệm hẹp thay vì khuyến mãi đại trà.
- A/B test combo và theo dõi incremental conversion, margin và cannibalization.

## Limitations

- Association rule thể hiện đồng xuất hiện, không chứng minh quan hệ nhân quả.
- Kết quả nhạy với `min_support`, cấp độ phân nhóm và thời gian dữ liệu.
- Chưa kết hợp giá bán, margin, tồn kho hoặc chi phí khuyến mãi.

## Repository structure

```text
market-basket-analysis-apriori/
├── README.md
├── market_basket_analysis_apriori.ipynb
├── requirements.txt
└── .gitignore
```

## How to run

### Google Colab

1. Mở notebook từ repository bằng Google Colab.
2. Truy cập [thư mục dữ liệu trên Google Drive](https://drive.google.com/drive/folders/1NrvyT_tMArcoZvI_sEgPLclD4Vw0iCBq?usp=sharing).
3. Tải đúng các file được liệt kê trong phần **Dataset** và upload chúng vào thư mục `/content/` của Colab.
4. Giữ nguyên tên file, sau đó chọn **Runtime → Restart session and run all**.

### Local Jupyter

1. Tải đúng các file được liệt kê trong phần **Dataset** từ [Google Drive](https://drive.google.com/drive/folders/1NrvyT_tMArcoZvI_sEgPLclD4Vw0iCBq?usp=sharing).
2. Đặt các file cạnh notebook hoặc cập nhật đường dẫn đọc dữ liệu trong notebook cho phù hợp.
3. Cài thư viện và mở Jupyter:

```bash
pip install -r requirements.txt
jupyter notebook
```

Notebook hiện được thiết kế chủ yếu cho Google Colab và có thể sử dụng đường dẫn `/content/...`; khi chạy local, cần thay đường dẫn này bằng vị trí dữ liệu trên máy.

## Tools

- Python
- Jupyter Notebook / Google Colab
- pandas, numpy, matplotlib, mlxtend
