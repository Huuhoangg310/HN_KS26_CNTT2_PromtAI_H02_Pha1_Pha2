# BÀI LÀM PHA 2 – HACKATHON 02

- **Mã đề:** 04
- **Họ tên:Nguyễn Hữu Hoàng**
- **Lớp:CNTT2**
- **Link repository Pha2:**
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):Chat GPT**

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đặt vé xe ra JSON

**KET QUA AI**

```text
[
  {
    "ma_tuyen": null,
    "ngay_di": "2026-12-22",
    "ve_nguoi_lon": 2,
    "ve_tre_em": 1,
    "loai_cho": "giuong",
    "ghi_chu": null
  },
  {
    "ma_tuyen": "SGNT",
    "ngay_di": "2027-01-02",
    "ve_nguoi_lon": 3,
    "ve_tre_em": 0,
    "loai_cho": null,
    "ghi_chu": "một người đang mang thai 6 tháng"
  },
  {
    "ma_tuyen": "SGCT",
    "ngay_di": null,
    "ve_nguoi_lon": 4,
    "ve_tre_em": 0,
    "loai_cho": "ghe",
    "ghi_chu": "bà nội đi xe lăn"
  }
]
```

**Link trò chuyện:** https://chatgpt.com/share/6b079ddb-efb0-83ec-89ae-6e2510437908

## 4.3. Báo giá bằng Chain-of-Thought

**KET QUA AI**

```text
BẢNG BÁO GIÁ VÉ XE
Tuyến SGDL: Sài Gòn – Đà Lạt
Nội dung	Số lượng	Đơn giá (đồng)	Thành tiền (đồng)
Vé người lớn	8	320.000	2.560.000
Vé trẻ em (6, 7 và 9 tuổi)	3	240.000	720.000
Trẻ em 2 tuổi	1	0	0
Tổng tiền vé			3.280.000
Giảm giá đoàn 5%			-164.000
Tiền vé sau giảm giá			3.116.000
Phụ thu hành lý	2	100.000	200.000
Tổng tiền thanh toán			3.316.000

Số tiền khách hàng phải thanh toán: 3.316.000 đồng.

Bằng chữ: Ba triệu ba trăm mười sáu nghìn đồng.

Đoàn đủ điều kiện giảm giá 5% do có 8 người lớn. Phụ thu hành lý không áp dụng giảm giá.
```

**Link trò chuyện:** https://chatgpt.com/share/6b079e30-2ba4-83ec-ae96-664bb7ab8b4d

### b) Kiểm tra kết quả AI

Đúng

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
{
  "loai_su_co": "sai_loai_xe",
  "so_khach": 3,
  "so_chang_bi_doi": 2,
  "tom_tat": "Ba khách đặt xe giường nằm nhưng bị đổi sang xe ghế ngồi cả hai chặng."
}
```

**Link trò chuyện:** https://chatgpt.com/share/6b079f28-b800-83ec-95bc-731664a1fe17

## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI**

```text
1. Kết quả chấm điểm
Tiêu chí	Điểm tối đa	Điểm đạt	Nhận xét
Đúng thông tin (50%)	5	0	Sai giá vé và chính sách đổi vé.
Đầy đủ (30%)	3	2	Đề cập cả giá vé và chính sách đổi vé nhưng chưa mời khách cung cấp ngày đi và số lượng vé.
Giọng điệu (20%)	2	1	Có lời chào lịch sự nhưng sử dụng từ ngữ suồng sã, thiếu chuyên nghiệp.
Tổng điểm	10	3	Không đạt yêu cầu.

2. Phân tích lỗi cụ thể
- Sai giá vé: Giá vé đúng là 380.000 đồng, không phải 350.000 đồng.
- Sai chính sách đổi vé: Đổi vé trước 12 giờ phải chịu phí 20% giá vé, không được miễn phí.
- Thiếu thông tin: Chưa trình bày đầy đủ các mốc thời gian và điều kiện đổi vé.
- Thiếu bước hỗ trợ đặt chỗ: Chưa hỏi khách về ngày đi và số lượng vé.
- Giọng điệu thiếu chuyên nghiệp: Sử dụng các cụm từ như “xe xịn lắm luôn”, “đổi free”, “nhắn em liền”.
3. Câu trả lời đề xuất
Dạ, em chào chị! Giá vé tuyến Sài Gòn – Nha Trang là 380.000 đồng/vé người lớn.

Chính sách đổi vé như sau:
- Trước giờ xe chạy từ 24 giờ trở lên: miễn phí đổi vé.
- Trước giờ xe chạy từ 6 đến dưới 24 giờ: phí đổi vé bằng 20% giá vé.
- Trước giờ xe chạy dưới 6 giờ: không được đổi vé.
Chị vui lòng cung cấp ngày đi và số lượng vé để em hỗ trợ đặt chỗ ạ!




4. Nhận xét chung: Câu trả lời ban đầu có thái độ thân thiện nhưng mắc lỗi nghiêm trọng về tính chính xác của thông tin, có thể gây hiểu nhầm và phát sinh khiếu nại từ khách hàng. Cần ưu tiên kiểm tra thông tin trước khi tư vấn, đồng thời sử dụng ngôn ngữ lịch sự, chuyên nghiệp.

Điểm thành phần được phân bổ theo mức độ đáp ứng từng tiêu chí do đề bài chưa quy định thang điểm chi tiết cho từng lỗi.
```

**Link trò chuyện:** https://chatgpt.com/share/6b079f82-361c-83ec-b3e7-037086708b98https://chatgpt.com/share/6b079f82-361c-83ec-b3e7-037086708b98
