# Tự đánh giá — Nguyễn Thành Phong · G07

## 1. Tự rà soát bốn ảnh

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S02_ir | person / child_seat | ok | Kiểm lại ánh xạ ghế: trái ảnh là `rear_right`, người bên phải ảnh là `rear_left`; không thêm face khi chỉ thấy sau đầu | có, đã rà |
| S03_rgb | infant_seat / object | ok | Nôi xách và túi là hai đối tượng khác nhau; giữ box riêng | có, đã rà |
| D03 | face13 | flag | Tay và chai che phần dưới mặt; kiểm tra cờ điểm thay vì suy vị trí | có |
| D06 | face / face13 | flag | Kiểm tra trạng thái mắt phải nhất quán với `occluded/outside` của bốn điểm mắt | có |

## 2. Lỗi lặp lại nhiều nhất

Lỗi: trạng thái `open/closed/unknown` của mắt đôi lúc chưa nhất quán với cờ `occluded/outside` của các điểm `face13`.

Vì sao mắc: ban đầu tập trung vào vị trí keypoint nhưng chưa kiểm tra lại thuộc tính của face sau khi đổi cờ điểm.

Lần sau tránh bằng cách: sau mỗi skeleton, kiểm lần lượt từng mắt theo cặp “thuộc tính eye → bốn điểm eye”; nếu không thấy mí thì dùng `unknown`, nếu điểm bị che thì bật cờ phù hợp.

## 3. Ghi chú về disagreement_log

Một bất đồng hữu ích là trạng thái mắt và cờ `face13` trên D02. Bài học là hai phần này phải mô tả cùng một mức độ nhìn thấy; `cabin_check` chỉ kiểm tính nhất quán cơ bản, còn quyết định hình ảnh vẫn phải dựa vào guideline và review chéo.
