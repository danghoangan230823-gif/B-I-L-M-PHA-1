# BÀI LÀM PHA 1 

- **Họ tên:** Trần Hoàng Ân
- **Lớp:** CNTT1
- **Link repository Pha1:**

> Pha 1 (70 phút đầu, KHÔNG dùng AI). Viết xong, kéo thả file này vào repository Pha1 trước mốc giờ giám thị công bố.

## 4.1. Bảo vệ dữ liệu và chống ảo giác

### a) Ghi chú đã ẩn danh hoá

**GHI CHU DA AN DANH**

```text
- khán giảng: [khách hàng 1]
- Số điện thoại: [Số điện thoại]
- CCCD: [Số CCCD]
- Email: [email cá nhân]
- đặt 3 vé gói SVT trận bán kết Cúp Sao Vàng ngày 18/12/2026 cho 2 người lớn và 1 trẻ em 9 tuổi. 
- Khán giả đã chuyển khoản đặt cọc 1.500.000 đồng. Khán giả yêu cầu 3 ghế ngồi cạnh nhau gần lối đi.
```

### b) Hai câu lệnh chống ảo giác

**CAU LENH**

```text
- Chỉ sử dụng duy nhất ở thông tinh ghi chú ẩn danh trên để trả lời.Tuyệt đối không sử dụng kiến thức bên ngoài, không tự suy diễn thêm các chi tiết không quan trọng
- 
```

## 4.2. Trích xuất tin nhắn đặt vé ra JSON

**PROMPT**

```text
Context
- Bạn là một hệ thống tự động đặt vé chuyên nghiệp trong các sự kiện thể thao.Nhiệm vụ của bạn là đọc tinh nhắn đặt vé của khách hàng 
Request
- Hãy đọc các tin nhắn đặt vé trong phần dữ liệu đầu vào và trích xuất thông tin thành một mảng JSON (JSON Array) hợp lệ gồm các đối tượng tương ứng với từng tin nhắn.
Explanation
Áp dụng bảng mã gói và 5 quy tắc chuẩn hóa sau để ánh xạ dữ liệu:
1.Bảng mã gói (`ma_goi`):
   - `SVT`: Sân Vận Động (vé trận đấu)
   - `FZ`: Fan Zone (khu cổ vũ)
   - `VIP`: Khán đài VIP
2.QUY TẮC CHUẨN HOÁ (5 quy tắc)
+ ma_goi lấy theo bảng mã gói.
+ ngay_su_kien dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
+ Khách không nhắc trẻ em thì tre_em là 0 và mọi khách là người lớn.
+ loai_ve chỉ nhận "thuong", "vip" hoặc null.
+ ghi_chu chỉ ghi yêu cầu đặc biệt về chỗ ngồi, hỗ trợ di chuyển hoặc ăn uống; không có thì null.
Action.
- Đọc từng tin nhắn, đối chiếu quy tắc, gán `null` nếu thiếu thông tin (không suy diễn) và xuất ra mảng JSON gồm 3 đối tượng.
Tone
- Chính xác, chỉ xuất duy nhất mã JSON, không kèm lời giải thích.
Extras
Tin nhắn mẫu 1:
Đặt giúp mình 2 vé VIP trận chung kết ngày 15/11/2026, 2 người lớn và 1 bé. Cần chỗ ngồi cạnh lối đi.
Kết quả đúng:
{"ma_goi": "VIP", "ngay_su_kien": "2026-11-15", "nguoi_lon": 2, "tre_em": 1, "loai_ve": "vip", "ghi_chu": "chỗ ngồi cạnh lối đi"}

Tin nhắn mẫu 2:
Cho mình một vé Fan Zone, ngày nào cũng được, mình đi một mình.
Kết quả đúng:
{"ma_goi": "FZ", "ngay_su_kien": null, "nguoi_lon": 1, "tre_em": 0, "loai_ve": "thuong", "ghi_chu": null}

```

## 4.3. Báo giá vé bằng Chain-of-Thought

### a) Prompt

**PROMPT**

```text
Bạn là nhân viên tư vấn báo giá vé sự kiện thể thao chuyên nghiệp. Dựa vào bảng giá và quy tắc dưới đây, hãy tính tổng tiền cho yêu cầu báo giá.
BẢNG GIÁ VÉ (đồng/người lớn)
SVT – Sân Vận Động: 1.200.000
FZ – Fan Zone: 800.000
VIP – Khán đài VIP: 2.500.000
QUY TẮC TÍNH GIÁ
1. Trẻ em từ 5 đến 11 tuổi tính 70% giá người lớn. Trẻ dưới 5 tuổi miễn phí.
2. Nhóm từ 5 người lớn trở lên được giảm 5% trên tiền vé (tiền người lớn + tiền trẻ em).
3. Phụ thu khu ghế ưu tiên: 300.000 đồng/người. Phụ thu không được giảm giá.
4. Tổng tiền = tiền vé sau giảm + phụ thu.
YÊU CẦU BÁO GIÁ
Nhóm cổ động viên đi xem trận bán kết, mua gói SVT, gồm 5 người lớn, 2 trẻ em (8 tuổi và 10 tuổi) và 1 bé 3 tuổi. Có 1 người lớn chọn khu ghế ưu tiên.
YÊU CẦU TRÌNH BÀY CHAIN-OF-THOUGHT


```

## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

### a) Prompt Trạm 1

**PROMPT**

```text
(Viết prompt vào đây – xoá dòng này)
```

### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1

1. (Viết câu trả lời vào đây – xoá dòng này)

2.

### c) Câu lệnh viết tiếp

**CAU LENH**

```text
(Viết câu lệnh vào đây – xoá dòng này)
```

## 4.5. Prompt chấm bài theo Rubric

**PROMPT**

```text
(Viết prompt vào đây – xoá dòng này)
```

## 4.6. Hoàn thiện System Prompt

> Phần Vai trò và Chuẩn đầu ra đã cho sẵn. Viết tiếp phần Quy tắc ràng buộc và Xử lý ngoại lệ.

```text
[Vai trò]
Bạn là "Trợ lý Cúp Sao Vàng", nhân viên tư vấn vé và dịch vụ trên website của giải bóng đá Cúp Sao Vàng, giúp khán giả chọn và đặt một trong 3 gói: SVT (Sân Vận Động – vé trận đấu), FZ (Fan Zone – khu cổ vũ), VIP (Khán đài VIP).

[Quy tắc ràng buộc]
1. (Viết quy tắc 1 – xoá dòng này)
2.
3.

[Chuẩn đầu ra]
Trả lời bằng tiếng Việt, lịch sự, tối đa 120 từ. Giá vé trình bày dạng gạch đầu dòng. Kết thúc bằng một câu hỏi về nhu cầu tiếp theo của khách.

[Xử lý ngoại lệ]
- Khách hỏi ngoài phạm vi: (Viết cách trả lời – xoá dòng này)
- Khách cung cấp thiếu thông tin:
```
