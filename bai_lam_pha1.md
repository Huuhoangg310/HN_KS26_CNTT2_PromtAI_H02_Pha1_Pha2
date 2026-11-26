# BÀI LÀM PHA 1 – HACKATHON 02

- **Mã đề:** 04
- **Họ tên:Nguyễn Hữu Hoàng**
- **Lớp:CNTT2**
- **Link repository Pha1:** https://github.com/Huuhoangg310/HN_KS26_CNTT2_PromtAI_H02_Pha1_Pha2

> Pha 1 (70 phút đầu, KHÔNG dùng AI). Viết xong, kéo thả file này vào repository Pha1 trước mốc giờ giám thị công bố.

## 4.1. Bảo vệ dữ liệu và chống ảo giác

### a) Ghi chú đã ẩn danh hoá

**GHI CHU DA AN DANH**

```text
Khách hàng [tên khách], số điện thoại [SO_DIEN_THOAI], số CCCD [SO_CCCD], email [DIA_CHI_EMAIL], đặt 2 vé người lớn và 1 vé trẻ em 6 tuổi tuyến Sài Gòn – Nha Trang (mã SGNT) ngày 20/12/2026. Khách đã chuyển khoản đặt cọc 500.000 đồng. Khách yêu cầu giường tầng dưới.

```

### b) Hai câu lệnh chống ảo giác

**CAU LENH**

```text
Câu 1: Dựa và file đính kèm đưa ra cho tôi cách hoàn tiền cho vị khách và nếu trong file không có thông tin hãy điền là [ đang cập nhật ], yêu cầu bắt buộc không bịa câu trả lời, không thêm bớt những thông tin không có trong file tuân thủ nghiêm ngặt các quy tắc, điều khoản có trong file
Câu 2: Ghi rõ những thông tin bạn trả lời được lấy ở mục hay điều khoản nào trong file để tôi có thể đối chiếu và kiểm tra độ chính xác.

```

## 4.2. Trích xuất tin nhắn đặt vé xe ra JSON

**PROMPT**

```text
Bạn là một chuyên gia phân tích dữ liệu đặt vé xe.Nhiệm vụ của bạn là phân tích và chuẩn hoá các tin nhắn của khách hàng về dạng JSON.Yêu cầu không thêm lời chào và câu kết ở đầu và ở cuối câu trả lời, không giải thích chỉ trả về kết quả theo yêu cầu, nghiêm cấm bịa thêm thông tin và chỉ dựa vào dữ liệu đã được cấp để trả lời.
Bước 1: chuẩn hoá dữ liệu 
1. ma_tuyen lấy theo bảng mã tuyến xe.
2. ngay_di dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
3. Khách không nhắc trẻ em thì ve_tre_em là 0 và mọi khách là người lớn.
4. loai_cho chỉ nhận "giuong", "ghe" hoặc null.
5. ghi_chu chỉ ghi yêu cầu đặc biệt về sức khoẻ, đi lại, mang thai; không có thì null.
Bước 2: chuyển các tin nhắn và thông tin về dạng JSON
Ví dụ:
Tin nhắn mẫu 1:
Đặt giúp em 2 vé người lớn 1 vé trẻ em đi Nha Trang ngày 18/11/2026, giường nằm nha. Bé hay say xe.
Kết quả đúng:
{"ma_tuyen": "SGNT", "ngay_di": "2026-11-18", "ve_nguoi_lon": 2, "ve_tre_em": 1, "loai_cho": "giuong", "ghi_chu": "bé hay say xe"}

Tin nhắn mẫu 2:
Xe đi Cần Thơ còn ghế ngồi không anh, em đi 1 mình, ngày nào cũng được.
Kết quả đúng:
{"ma_tuyen": "SGCT", "ngay_di": null, "ve_nguoi_lon": 1, "ve_tre_em": 0, "loai_cho": "ghe", "ghi_chu": null}
Đây là giữ liệu tôi cần bạn xử lí :
<TN1: Cho mình đặt xe Sài Gòn đi Đà Lạt ngày 22/12 nha, 2 người lớn với 1 bé 8 tuổi, đi giường nằm.>

<TN2: Đặt 3 vé đi Nha Trang ngày 02/01/2027 ạ. Một người đang mang thai 6 tháng.>

<TN3: Tuyến Cần Thơ dịp Tết còn vé không ạ? Nhà em 4 người lớn, bà nội đi xe lăn, đi ghế ngồi.>

```

## 4.3. Báo giá bằng Chain-of-Thought

### a) Prompt

**PROMPT**

```text
Bạn là một kế toán có nhiều năm kinh nghiệm.Nhiệm vụ của bạn là tính tổng tiền khách hàng phải thanh toán dựa vào bảng giá,quy tắc và yêu cầu báo giá  được cung cấp:
BẢNG GIÁ VÉ (đồng/vé người lớn)
SGDL – Sài Gòn – Đà Lạt: 320.000
SGNT – Sài Gòn – Nha Trang: 380.000
SGCT – Sài Gòn – Cần Thơ: 180.000

QUY TẮC TÍNH GIÁ
1. Trẻ em từ 5 đến 10 tuổi tính 75% giá vé người lớn. Trẻ dưới 5 tuổi ngồi cùng người lớn miễn phí.
2. Đoàn từ 6 người lớn trở lên được giảm 5% trên tiền vé (tiền vé người lớn + tiền vé trẻ em).
3. Phụ thu hành lý cồng kềnh: 100.000 đồng/kiện. Phụ thu không được giảm giá.
4. Tổng tiền = tiền vé sau giảm + phụ thu.

YÊU CẦU BÁO GIÁ
Đoàn đi tuyến SGDL gồm 8 người lớn, 3 trẻ em (6, 7 và 9 tuổi) và 1 bé 2 tuổi. Đoàn có 2 kiện hành lý cồng kềnh.

```

## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

### a) Prompt Trạm 1

**PROMPT**

```text
Bạn là nhân viên chăm sóc khách hàng của Phương Nam Express, nhiệm vụ của bạn là đọc file email_khieu_nai.txt của khách hàng để đưa ra mức bồi thường thoả đáng.Yêu cầu trả về 1 đối tượng JSON gồm đúng 4 trường: loại sự cố, số khách, số chặng bị đổi, tóm tắt( không quá 20 từ)
{"loai_su_co": một trong "tre_chuyen" | "sai_loai_xe" | "tai_xe" | "khac", "so_khach": số nguyên, "so_chang_bi_doi": số nguyên hoặc null, "tom_tat": "không quá 20 từ"}
```

### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1

1. kiểm tra kết quả trả về có đúng 4 trường theo quy định không
2.Tính đúng sai/độ chính xác của kết quả

### c) Câu lệnh viết tiếp

**CAU LENH**

```text
Hãy tiếp tục viết phần nội dung còn thiếu của Trạm 3, bắt đầu chính xác ngay sau từ cuối cùng: “Phương nam Express xin hoàn lại Quý khán giả khoản” Chỉ viết phần nội dung tiếp theo, tuyệt đối không viết lại đoạn đã có.Giữ nguyên văn phong, cách xưng hô và định dạng của phần trước.Đảm bảo nội dung liền mạch, đúng ngữ cảnh và không tự ý thay đổi thông tin đã cung cấp.Không thêm lời dẫn, lời giải thích hoặc nhận xét bên ngoài nội dung cần tiếp tục.
```

## 4.5. Prompt chấm bài theo Rubric

**PROMPT**

```text
Bạn là một chuyên gia phân tích và đánh giá nhiệm vụ của bạn là dựa vào các thông tin tôi cung cấp để đánh giá và nhận xét.
thông tin:
- Giá vé SGNT: 380.000 đồng/vé người lớn.
- Chính sách đổi vé: đổi trước giờ xe chạy từ 24 giờ trở lên miễn phí; từ 6 đến dưới 24 giờ phí 20% giá vé; dưới 6 giờ không được đổi.
* Bài cần chấm
-<Dạ chào chị! Vé đi Nha Trang bên em 350.000đ nha chị, xe xịn lắm luôn. Chị đổi trước 12 tiếng thì đổi free nha chị. Cần gì chị nhắn em liền!>
* Hãy chấm câu nói trên dựa trên thang điểm 10 dựa vào các tiêu trí sau:
- Đúng thông tin (50%): giá và chính sách đổi vé đúng với thông tin chuẩn.
- Đầy đủ (30%): trả lời đủ cả hai câu hỏi của khách và mời khách cung cấp ngày đi, số vé để đặt chỗ.
- Giọng điệu (20%): lịch sự, chuyên nghiệp, không dùng từ ngữ suồng sã.

```

## 4.6. Hoàn thiện System Prompt

> Phần Vai trò và Chuẩn đầu ra đã cho sẵn. Viết tiếp phần Quy tắc ràng buộc và Xử lý ngoại lệ.

```text
[Vai trò]
Bạn là "Trợ lý Phương Nam", nhân viên tư vấn trên website của nhà xe Phương Nam Express, giúp khách chọn và đặt vé một trong 3 tuyến: SGDL (Sài Gòn – Đà Lạt), SGNT (Sài Gòn – Nha Trang), SGCT (Sài Gòn – Cần Thơ).

[Quy tắc ràng buộc]
1. Chỉ tư vấn 3 chuyến xe của công ty
2. Không hứa giảm giá bảng ngoài giá
3. Không hỏi xin số CCCD, số thẻ ngân hàng

[Chuẩn đầu ra]
Trả lời bằng tiếng Việt, lịch sự, tối đa 120 từ. Giá vé trình bày dạng gạch đầu dòng. Kết thúc bằng một câu hỏi về nhu cầu tiếp theo của khách.

[Xử lý ngoại lệ]
- Khách hỏi ngoài phạm vi: (Viết cách trả lời – xoá dòng này)
- Khách cung cấp thiếu thông tin:
```
