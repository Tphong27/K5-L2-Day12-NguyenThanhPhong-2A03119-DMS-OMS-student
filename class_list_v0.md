# Danh sách lớp v0 — Nguyễn Thành Phong · G07

## DMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `eye_left`, `eye_right` | open / closed / unknown | Theo dõi nhắm mắt kéo dài và nguy cơ buồn ngủ | Có, nhưng kính và phản xạ có thể làm `unknown` |
| 2 | `gaze_zone` | road / mirrors / cluster / center / lap / other | Phát hiện tài xế rời mắt khỏi vùng đường | Có, nếu mắt và hướng đầu đủ rõ |
| 3 | `glasses` | none / clear / sun / unknown | Đánh giá độ tin cậy của quan sát mắt và xử lý phản xạ kính | Có, nhưng loại kính có thể khó phân biệt trên NIR |
| 4 | `face13` | 13 keypoint + occluded/outside | Ước lượng hướng đầu, hình học mắt và miệng | Có, trừ điểm bị che hoặc mặt quá nhỏ |
| 5 | `hand.on_wheel` | yes / no / unknown | Xác định tay có đang kiểm soát vô lăng | Có, nếu tay và vô lăng cùng nhìn rõ |
| 6 | `phone.state` | held / mounted / lap | Phát hiện hành vi sử dụng điện thoại gây mất tập trung | Có, dựa chủ yếu vào hình dạng và vị trí |
| 7 | `person.seatbelt` | worn_correct / worn_incorrect / not_worn / unknown | Cảnh báo sử dụng dây an toàn sai hoặc không sử dụng | Có, nhưng vùng dây tối hoặc bị che phải ghi `unknown` |

## OMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person.seat` | rear_left / rear_middle / rear_right | Xác định ghế nào đang có người để hỗ trợ cảnh báo và túi khí | Có |
| 2 | `child_seat` | seat + occupied no/unknown | Phát hiện ghế trẻ em và trạng thái quan sát được | Có theo hình dạng |
| 3 | `infant_seat` | seat + facing rear/front | Nhận biết nôi xách và hướng lắp ghế em bé | Có theo hình dạng và tay cầm |
| 4 | `object.type` | bag / box / cup / other | Phân biệt đồ vật với người trên từng ghế | Có theo hình dạng; không dựa vào màu |
| 5 | `face` | rectangle | Xác nhận vị trí đầu/mặt của người ngồi | Có nếu mặt không quay đi hoặc bị che gần hết |
| 6 | `frame_meta.modality` | rgb / ir | Tách luồng xử lý ảnh màu và ảnh hồng ngoại | Có từ nguồn ảnh và tên frame |
| 7 | `frame_meta.camera_blocked` | yes / no | Phát hiện camera bị che để không tin kết quả OMS | Có |

## Hai câu hỏi leo thang

1. Câu hỏi: Khi một người rất nhỏ đang ngồi trong ghế trẻ em thì cần gán cả `person` và `child_seat`, hay chỉ gán `person`?
   Khung ví dụ: `S08_rgb.png`, `S08_ir.png`.
   Tạm gán: giữ các box riêng và đánh dấu ca `ambiguous`, vì guideline mô tả `child_seat` chủ yếu cho ghế trống nhưng hình ảnh có người nhỏ đang ngồi.
2. Câu hỏi: Khi đường viền kính rất mờ trên NIR thì ưu tiên `clear` hay `unknown`?
   Khung ví dụ: `D04.png`.
   Tạm gán: `unknown` nếu không nhìn chắc kính đang được đeo; không suy từ vật giống kính gần tay.
