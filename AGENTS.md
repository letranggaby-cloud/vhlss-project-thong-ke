# Quy ước làm việc của dự án

## Đồng bộ GitHub — yêu cầu ngày 10/11/2026

- Sau mỗi đợt thay đổi trong phạm vi công việc người dùng yêu cầu, kiểm tra các file liên quan rồi tự commit và push lên nhánh `main` của `letranggaby-cloud/vhlss-project-thong-ke`.
- Áp dụng cho notebook, README, code và bảng kết quả đi kèm; không cần hỏi lại quyền push đã được người dùng cấp.
- Giữ nguyên thay đổi khác của người dùng trên GitHub; không force-push. Nếu workspace không có Git checkout, có thể dùng GitHub API để đồng bộ đúng các file đã sửa.
- Khi hoàn tất, báo ngắn gọn nội dung thay đổi và gửi link GitHub. Chỉ báo đã push sau khi kiểm tra thành công; nếu chưa đồng bộ được, nói rõ trạng thái thực tế.

## Trình bày giả thuyết theo slide — yêu cầu ngày 10/11/2026

- Với bài thu nhập đang làm, viết H₀ bằng dấu “=” theo cách trình bày trong slide Chap 7. Giữ hướng tăng/giảm ở H₁ và chọn đúng phía kiểm định.
- Sửa đồng nhất trong README và notebook. Việc đổi cách viết H₀ không tự thay số liệu hay các phép tính vốn đã dùng chênh lệch giả thuyết bằng 0.


## Notebook chung và dọn repo — yêu cầu 12/11/2026

- Bản làm việc duy nhất: `vhlss_preprocess_va_thu_nhap.ipynb` ở gốc repo. Thứ tự: cấu hình → preprocess toàn bộ merged → hàm kiểm định dùng chung → phân tích thu nhập.
- Process đủ 2010/2012/2014; thu nhập so sánh 2010/2014. Đầu vào merged khóa theo commit và hash trong notebook; file đầu ra duy nhất là `processed/vhlss_processed.csv`.
- CPI bình quân năm: 2010=100; 2012=129,50; 2014=143,69. Confidence level 95%, CI hai phía; kiểm định thu nhập phía phải.
- Không điền thiếu thành 0, không bỏ dòng giống nhau nếu chưa có mã hộ; giữ Quart gốc. Tài sản âm/thiếu là chưa rõ sở hữu. Chi 13 khoản cần đủ dữ liệu, tổng 12 không fuel chỉ đối chiếu.
- Hai mẫu năm độc lập. Paired t-test chỉ là hàm dùng lại cho dữ liệu có cặp thật. ANOVA mặc định chỉ phân rã SS, không gán p khi chưa đánh giá điều kiện; công thức hai nhân tố chỉ cho thiết kế cân bằng.
- Thu nhập giữ toàn mẫu và bản bỏ top 0,1% từng năm, chẩn đoán theo đúng nhóm. Trình bày ngắn, tên rõ, cell thoáng; kết quả/biểu đồ nằm trong notebook, không tạo bảng rời mặc định.
- Không khôi phục các thư mục báo cáo/bảng cũ vào main; dùng lịch sử Git nếu cần đối chiếu. Run All và kiểm tra dữ liệu trước commit/push.
