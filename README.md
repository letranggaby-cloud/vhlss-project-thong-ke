# VHLSS: xử lý dữ liệu và phân tích

[Mở trên Colab](https://colab.research.google.com/github/letranggaby-cloud/vhlss-project-thong-ke/blob/main/vhlss_preprocess_va_thu_nhap.ipynb) · [Notebook](vhlss_preprocess_va_thu_nhap.ipynb) · [Dữ liệu processed](processed/vhlss_processed.csv)

Chọn **Runtime → Run all**. Các thư viện cần dùng: NumPy, pandas, SciPy (từ 1.11) và Matplotlib. Dữ liệu tự tải từ GitHub; cần Internet cho bước đọc nguồn.

Notebook gồm:

1. Làm sạch toàn bộ 2010/2012/2014, tạo biến và lưu một CSV gồm 28.196 dòng, 95 cột.
2. Định nghĩa hàm kiểm định t/Z, paired t, phương sai, tỷ lệ, ANOVA, χ², tương quan và Jarque–Bera; ghi công thức và điều kiện dùng.
3. **A. Thu Nhập:** 2010–2014, toàn mẫu và bỏ top 0,1%, theo Quart và khu vực.
4. **B. Chi Tiêu** và **C. Thu - Chi:** đã đặt khung, chưa triển khai phân tích.
5. **D. Tài Sản:** tổng 9 tài sản bền, thành thị–nông thôn, giá trị thiết bị theo Q, tỷ lệ sở hữu và số nhóm thiết bị mỗi hộ.

**CPI bình quân năm, gốc 2010 = 100:** 2010: 100,00; 2012: 129,50; 2014: 143,69. [Nguồn: Niên giám thống kê 2014, bảng 250, trang 551](https://www.nso.gov.vn/wp-content/uploads/2019/10/Nien-giam-2014-pdf.pdf). Dùng CI 95% hai phía và α = 5%; kiểm định thu nhập phía phải theo Chap 7 §7.2.4.

Giữ thiếu là thiếu và giữ Quart gốc. Tổng chi 13 khoản chỉ tính khi đủ dữ liệu; tổng 12 không fuel dùng đối chiếu. Biến `*_pc_real` có đơn vị triệu đồng/người/năm, giá 2010. Từ điển biến nằm trong notebook.

Hai mẫu năm được coi là độc lập, mỗi hộ có trọng số bằng nhau. Không ghép hộ theo thứ tự dòng. ANOVA mặc định chỉ phân rã SS; chỉ tính p khi đủ điều kiện. Hàm hai nhân tố dùng thiết kế cân bằng trong slide.

Nguồn đầu vào: [vhlss_merged.csv tại commit 4a2c3c0](https://raw.githubusercontent.com/letranggaby-cloud/vhlss-project-thong-ke/4a2c3c06ba191010f536b811deb9e65de6424d46/processed/vhlss_merged.csv), có kiểm hash. Nếu đã tải nguồn về máy, đặt đường dẫn ở `SOURCE_PATH`. Nếu chỉ cần phân tích tiếp, đọc `processed/vhlss_processed.csv`.

Đã chạy notebook từ thư mục trống và đối chiếu 14 kết quả thu nhập cùng CI với SciPy. Phần tài sản đối chiếu tổng, Welch t/CI và 20 phép Z với χ². Các hàm kiểm định được kiểm tra bằng dữ liệu ví dụ và bảng ANOVA trong Chap 8. Môi trường kiểm tra: Python 3.12, NumPy 2.5.3, pandas 3.0.5, SciPy 1.18.1, Matplotlib 3.11.1; chưa chạy trực tiếp trong phiên Colab.

Các bản cũ còn trong [lịch sử Git](https://github.com/letranggaby-cloud/vhlss-project-thong-ke/tree/4a2c3c06ba191010f536b811deb9e65de6424d46).

Phần tài sản được ghép từ [notebook Colab được cung cấp](https://colab.research.google.com/drive/1mtAVFZxFl1JkVguy4Sq_5tLt_FAegXmE), dùng cùng dữ liệu processed, CPI và CI 95%. Tổng 9 tài sản cần đủ 9 khoản; tỷ lệ sở hữu dùng số hộ biết trạng thái từng thiết bị. Không dùng p ANOVA hai nhân tố của bản nguồn vì bốn thiết bị cùng hộ tạo các quan sát phụ thuộc. CI skewness dùng bootstrap 1.000 lần theo bản nguồn; p Bonferroni được ghi riêng, CI vẫn 95% từng phép.
