# Thu nhập đầu người 2010–2014

[**Notebook phân tích**](bao_cao_vhlss/thu_nhap_2010_2014.ipynb) · [**Câu hỏi, phương pháp và kết quả**](bao_cao_vhlss/README_thu_nhap.md)

Ba câu hỏi: thu nhập thực bình quân có tăng trên toàn mẫu, trong từng Q1–Q4 và trong từng khu vực thành thị/nông thôn không? Mức tăng được báo kèm CI 95%.

Một notebook chạy hai bản: **giữ toàn mẫu** và **bỏ top 0,1% từng năm**, dùng CPI để quy về giá 2010. Biểu đồ Q4 được trình bày trước khi lọc và kiểm định. Các kết quả đã được chạy và lưu trong notebook.

| Đường dẫn | Nội dung |
|---|---|
| [Notebook](bao_cao_vhlss/thu_nhap_2010_2014.ipynb) | Dữ liệu, biểu đồ, giả thuyết, công thức lớp, code và kết luận |
| [Kết quả](bao_cao_vhlss/thu_nhap_ket_qua.csv) | Mean, mức tăng, SE, t, df, p và CI 95% |
| [Dữ liệu](dataset/VHLSS_2014.xls) | Excel gốc, dùng hai sheet 2010/2014 |
| [CPI và nguồn](bao_cao_vhlss/CPI_nguon_va_cach_quy_doi.md) | CPI bình quân năm, cùng gốc 2010 = 100 |

Cài thư viện bằng `python -m pip install -r bao_cao_vhlss/requirements_thu_nhap.txt`, mở notebook và Run All. Giữ nguyên các thư mục khi tải repo.

Nguồn dữ liệu: Khảo sát Mức sống Hộ gia đình Việt Nam (VHLSS).
