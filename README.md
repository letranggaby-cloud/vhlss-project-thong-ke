# VHLSS · Notebook dùng chung

[**Mở trên Google Colab**](https://colab.research.google.com/github/letranggaby-cloud/vhlss-project-thong-ke/blob/main/vhlss_preprocess_va_thu_nhap.ipynb) · [Xem notebook trên GitHub](vhlss_preprocess_va_thu_nhap.ipynb)

Chọn **Runtime → Run all**. Notebook tự đọc nguồn merged cố định từ GitHub, preprocess toàn bộ 2010/2012/2014, định nghĩa các hàm kiểm định, rồi phân tích thu nhập 2010–2014. Không cần Google Drive, Excel hoặc đường dẫn máy cá nhân. Kết quả đã chạy được lưu ngay trong notebook.

Repo chỉ giữ một notebook và [một CSV processed](processed/vhlss_processed.csv), cùng hướng dẫn và cấu hình Git. CSV gồm **28.196 dòng, 95 cột**; notebook tạo lại file này mỗi lần chạy. Các bảng kết quả và biểu đồ hiển thị trong notebook, không xuất thêm file mặc định.

## Quy ước chung

- **CPI bình quân năm, gốc 2010 = 100:** 2010: **100,00**; 2012: **129,50**; 2014: **143,69**. [Nguồn: Niên giám thống kê 2014, bảng 250, trang in 551](https://www.nso.gov.vn/wp-content/uploads/2019/10/Nien-giam-2014-pdf.pdf).
- **Confidence level 95%; α = 5%.** CI luôn hai phía. Kiểm định thu nhập dùng H₀: μ2014 − μ2010 = 0; H₁: μ2014 − μ2010 > 0, t hai mẫu độc lập không giả sử phương sai bằng nhau — Chap 7 §7.2.4.
- Thu/chi nguồn: **nghìn đồng/hộ/năm**. Biến `*_pc_real`: **triệu đồng/người/năm, giá 2010**. Giá trị tài sản là stock tại khảo sát, không cộng vào chi tiêu.
- Giữ thiếu là thiếu, không điền fuel/giá trị tài sản thiếu bằng 0. Tổng 13 khoản chỉ tính khi đủ thành phần; tổng 12 không gồm fuel dùng đối chiếu. Giữ Quart nguồn và mọi dòng; không tự xóa ngoại lệ hay dòng giống nhau.
- Các năm coi là **mẫu độc lập**. Bộ hàm có paired t-test để dùng cho dữ liệu có cặp thật; không áp dụng để ghép hộ VHLSS theo thứ tự dòng.

## Nội dung notebook

1. Thiết lập CPI, CI và nguồn dữ liệu.
2. Chuẩn tên, kiểm tra kiểu dữ liệu, giá trị không hợp lệ, tạo biến thực/đầu người, tổng chi, sở hữu và bảng thiếu theo nhóm; lưu CSV processed.
3. Hàm t/Z cho mean, paired t, χ²/F cho phương sai, Z tỷ lệ, ANOVA một/hai nhân tố, χ² goodness of fit/độc lập, Pearson/Spearman và Jarque–Bera. Có điều kiện dùng, công thức và hướng dẫn gọi hàm. ANOVA mặc định chỉ phân rã SS; hai nhân tố chỉ dùng thiết kế cân bằng theo slide.
4. Thu nhập 2010–2014: toàn mẫu và bỏ top 0,1% mỗi năm, biểu đồ Q4 trước lọc, chẩn đoán đúng từng mẫu, ba câu hỏi toàn mẫu/Quart/khu vực, p và CI 95%.

Nếu chỉ cần dữ liệu sạch: `pd.read_csv("processed/vhlss_processed.csv")`. Từ điển biến nằm trong notebook. Trạng thái sở hữu thiếu phải giữ là thiếu khi đọc CSV. Mean thu nhập là trung bình đầu người của các hộ với trọng số hộ bằng nhau; p/CI chưa xét thiết kế khảo sát, giá vùng, so sánh đồng thời hoặc đầy đủ bất định chọn ngưỡng top.

## Nguồn cố định và kiểm tra

Nguồn preprocess là [vhlss_merged.csv tại commit 4a2c3c0](https://raw.githubusercontent.com/letranggaby-cloud/vhlss-project-thong-ke/4a2c3c06ba191010f536b811deb9e65de6424d46/processed/vhlss_merged.csv). Notebook kiểm SHA-256 trước khi dùng. Muốn chạy ngoại tuyến, tải đúng file đó và đặt `SOURCE_PATH` trong notebook. Cần Internet cho lần tải nguồn hoặc cài thư viện còn thiếu.

Đã chạy toàn bộ notebook từ nguồn GitHub; đối chiếu 14 Welch t-test và CI với SciPy, giữ kết quả thu nhập trước đây. Bộ hàm được kiểm tra thêm bằng ví dụ ANOVA trong Chap 8, các phía kiểm định, CI, thiếu theo cặp và đầu vào không hợp lệ. Môi trường kiểm tra: Python 3.12, NumPy 2.5.3, pandas 3.0.5, SciPy 1.18.1, Matplotlib 3.11.1; cấu trúc chạy tương thích Colab, chưa thực thi trực tiếp trong phiên Colab.

Notebook và báo cáo/bảng cũ đã bỏ khỏi bản hiện tại; vẫn khôi phục được từ [lịch sử Git trước khi gom](https://github.com/letranggaby-cloud/vhlss-project-thong-ke/tree/4a2c3c06ba191010f536b811deb9e65de6424d46).
