# Báo cáo cá nhân — HoVaTen-MSSV

Đổi tên file theo quy tắc `MSSV_HoTen.md`. Ví dụ: `20241234_NguyenVanAn.md`.

Dữ liệu: 12 ảnh người COCO val2017 (Lin et al., 2014) và 8 ảnh chân dung Wikimedia Commons, chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên: Nguyễn Trường Nam
- MSSV: 2A202604067
- Email: truongnam0304@gmail.com
- Link repository: https://github.com/ntnguyen03/K5-L2B-NguyenTruongNam-2A202604067-KeypointPose-Student.git
- Phiên bản CVAT (Help → About):2.74.1
- Máy: hệ điều hành `Window` · RAM `16` GB · chạy CVAT lite
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có
- Giờ bắt đầu: 16h00
- Giờ kết thúc: 23h59

## 1. Kiểm tra label (CP0)

 Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` | Skeleton | 17 | Có | Có | 19 |
| `face` | Skeleton | 13 | Có | Có | 13 |

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)? Có / Không

Cách đổi cờ `occluded` / `outside` cho **một điểm** trên phiên bản CVAT này (một câu):

Rê chuột vào đúng điểm rồi nhấn `Q` để bật/tắt `occluded` hoặc `O` để bật/tắt `outside`.

...

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 | 5 | 2 | 0 | 45 |
| `occluded` | 3 | 6 | 0 | 1 | 30 |
| `back` | 2 | 4 | Ít nhất 3 | 0 | 15 |
| `small` | 1 | 2 | 2 | 0 | 10 |
| `crowd` | 1 | 3 | 0 | 0 | 10 |
| `faces` | 8 | 8 | — | — | 50 |

Tổng cộng 20 skeleton người trên 12 ảnh và 8 skeleton mặt trên 8 ảnh. Tổng được xác nhận trong CVAT. Số lượng theo nhóm được đối chiếu từ tóm tắt export theo từng ảnh và `src/lab/pool.json`.

Số người bỏ qua được đếm trên ảnh ở kích thước gốc. Hai người dưới 60 px ở nhóm `easy` đứng xa trong ảnh công viên `000000241837.jpg`. Hai người nhỏ ở nhóm `small` nằm sát hai mép ảnh `000000100510.jpg`. Ảnh `000000307757.jpg` có ít nhất ba người nhỏ nhận ra được ở xa bên trái đường. Một số bóng ở xa quá mờ để xác nhận, nên con số nhóm `back` là số tối thiểu. Nhóm `occluded` có một chân dung đóng khung trên tủ trong ảnh `000000056651.jpg`. Các số 0 nghĩa là không thấy trường hợp rõ ràng khi rà ảnh.

- Số ảnh người đã xong ở mốc phút 105: Chưa ghi nhận / 10.
- Thời gian thực tế (phút): CP1, CP2 và CP3 chưa có số phút riêng trong ghi chép được cung cấp.
- Ảnh tốn thời gian nhất: `000000542160.jpg`

...

## 3. Bảng ca khó (CP1, CP2)

Mỗi điểm bạn phân vân một dòng, nhất là phân vân giữa `v = 1` và `v = 0`, hoặc không chắc hướng người.

| Ảnh | Người / mặt | Điểm | Cờ đã chọn | Phân vân giữa | Lý do chọn |
|---|---|---|---:|---|---|
| `000000043500.jpg` | Người ở bậc toa tàu | Gối hoặc cổ chân sau bậc | [Kiểm tra] | `v = 1` / `v = 0` | Chọn `v = 1` nếu các đoạn chân nhìn thấy đủ để suy ra vị trí. Ghi lý do thực tế sau khi phóng to. |
| `000000311497.jpg` | Người #2 theo checker | `knee`, `ankle` | [Kiểm tra] | Chi bị che / chân đổi phía trong ảnh | Lần từ hông qua gối đến cổ chân để xác nhận cùng một bên cơ thể. |
| `face_294580.jpg` | Mặt #1 | Khóe hoặc mí mắt bị che | [Kiểm tra] | `v = 1` / `v = 0` | Ghi dấu hiệu trên ảnh đủ để ước lượng vị trí hoặc lý do chưa đủ căn cứ. |

## 4. Bảng tự review (CP3)

Đi từ ảnh cuối về ảnh đầu. 5 ảnh người (ít nhất 2 ảnh `back` hoặc `crowd`) và 3 ảnh mặt. Ít nhất 8 dòng, kể cả dòng `ok`. Ghi lỗi trước, sửa sau.

Mã lỗi dùng đúng một trong: `lr_swap`, `vis_flag`, `position`, `missing`, `extra`, `ok`.

| Ảnh | Người / mặt | Điểm | Kết quả | Ghi chú | Sửa trong CVAT |
|---|---|---|---|---|---|
| `000000542160.jpg` (`crowd`) | Người #1 theo checker | `ankle` | Cảnh báo `lr_swap` | Checker báo cặp cổ chân lệch phía. Cần lần theo chân của từng người trong cụm. | Chưa xác nhận |
| `000000311497.jpg` (`occluded`) | Người #2 theo checker | `knee`, `ankle` | Cảnh báo `lr_swap` | Checker báo cặp gối và cổ chân lệch phía. Tư thế chồng chi có thể tạo cảnh báo tương tự. | Chưa xác nhận |
| `000000307757.jpg` (`back`) | Hai người quay lưng | `nose`, `left_eye`, `right_eye` | `ok` ở các cờ đã kiểm | Cả hai skeleton có `v = 0` ở mũi và hai mắt, phù hợp với hướng nhìn từ phía sau. | Không cần ở các điểm đã kiểm |
| `000000043968.jpg` (`easy`) | Người #1 theo checker | `ankle` | Cảnh báo `lr_swap` | Hai chân ở sát nhau trên ván. Cần lần từ gối xuống từng giày để xác nhận phía. | Chưa xác nhận |
| `000000043500.jpg` (`back`) | Người #1 | Hai cổ chân | `ok` ở các cờ đã kiểm | Hai cổ chân xuất `v = 0`, phù hợp với việc không định vị chắc sau bậc toa. | Không cần ở các điểm đã kiểm |
| `face_483667.jpg` | Mặt #1 | Khóe ngoài và mí trên mắt trái | Đã kiểm cờ trong JSON | Cả hai điểm xuất `v = 1`. Cần đối chiếu lại vị trí trên ảnh. | Chưa xác nhận |
| `face_449454.jpg` | Mặt #1 | 13 điểm mặt | Đã kiểm cấu trúc | Có 39 số, cả 13 điểm là `v = 2`. Kết quả này xác nhận cấu trúc và cờ đã lưu. | Chưa xác nhận |
| `face_147624.jpg` | Mặt #1 | 13 điểm mặt | Đã kiểm cấu trúc | Có 39 số, cả 13 điểm là `v = 2` và `num_keypoints = 13`. | Chưa xác nhận |

Tổng hợp số lỗi theo mã:

| `lr_swap` | `vis_flag` | `position` | `missing` | `extra` | `ok` |
|---:|---:|---:|---:|---:|---:|
| | | | | | |
(Chưa có lỗi)

Điểm còn phân vân giữa `v = 1` và `v = 0` (ghi cả hai lựa chọn và lý do chọn):
Cờ `v = 1` phù hợp khi có đủ mốc nhìn thấy để đặt điểm gần tâm khớp. Với hai cổ chân sau bậc toa trong `000000043500.jpg`, bản xuất dùng `v = 0`.

...

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Tự kiểm tay trong file JSON:

| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`? | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `NguyenTruongNam_persons.zip` | `000000043500.jpg`, người #1 | 51 theo tóm tắt | [Đối chiếu từng cờ] | [Đếm số bộ có `v > 0`] |
| `NguyenTruongNam_persons.zip` | `000000311497.jpg`, người #2 | 51 theo tóm tắt | [Đối chiếu từng cờ] | [Đếm số bộ có `v > 0`] |
| `NguyenTruongNam_faces.zip` | `face_147624.jpg`, mặt #1 | 39 theo tóm tắt | [Đối chiếu từng cờ] | [Đếm số bộ có `v > 0`] |

Sau khi xuất, CVAT ghi `occluded` thành `v = ___` và `outside` thành `v = ___`. Tọa độ của điểm `outside` trong file là `0, 0` hay tọa độ cũ? ___

Hai job đã chuyển sang completed trên CVAT? Có / Không

Dán phần **TÓM TẮT** in ra từ `src/check_submission.py`:

```text
- File person: NguyenTruongNam_persons.zip
  Số ảnh: 12 · số skeleton `person`: 20 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000043500=2, 000000043968=1, 000000056651=2, 000000100510=2, 000000179201=2, 000000196283=1, 000000205650=1, 000000241837=1, 000000307757=2, 000000311497=2, 000000542160=3, 000000558066=1
  Cờ v: v=2 256 (75%) · v=1 31 (9%) · v=0 53 (16%)
  num_keypoints trung bình: 14.3
- File face: NguyenTruongNam_faces.zip
  Số ảnh: 8 · số skeleton `face`: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_147624=1, face_204787=1, face_294580=1, face_345145=1, face_359139=1, face_416730=1, face_449454=1, face_483667=1
  Cờ v: v=2 94 (90%) · v=1 2 (2%) · v=0 8 (8%)
  num_keypoints trung bình: 12.0
- Ghi chú: 55 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 3
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)
```

Các `[CẢNH BÁO]` còn giữ nguyên và lý do:
  [CẢNH BÁO] 000000043968.jpg #1: cặp ankle nằm ngược phía so với các cặp còn lại. Có thể đổi trái/phải một cặp (`lr_swap`), hoặc tay / chân bắt chéo thật: kiểm lại.
  [CẢNH BÁO] 000000311497.jpg #2: cặp knee, ankle nằm ngược phía so với các cặp còn lại. Có thể đổi trái/phải một cặp (`lr_swap`), hoặc tay / chân bắt chéo thật: kiểm lại.
  [CẢNH BÁO] 000000542160.jpg #1: cặp ankle nằm ngược phía so với các cặp còn lại. Có thể đổi trái/phải một cặp (`lr_swap`), hoặc tay / chân bắt chéo thật: kiểm lại.


...

## 6. Ảnh chụp màn hình

1. Label `person` trong label constructor (đủ 17 điểm có tên):

   ![Label person](images/1_label_person.png)

2. Một người quay lưng đã gán, cờ đã đặt:

   ![Người quay lưng](images/2_nguoi_quay_lung.png)

3. Một khuôn mặt đã gán 13 điểm, phóng to vùng mắt:

   ![Khuôn mặt phóng to](images/3_mat_phong_to.png)

4. Một đoạn JSON xuất của một người:

   ![JSON export](images/4_json_export.png)

Nguồn ảnh: COCO val2017 / Wikimedia Commons.

## 7. Tự đánh giá

1. Lỗi bạn mắc nhiều nhất hôm nay, và cách bạn sẽ tránh ở dự án thật:
   Chưa có lỗi gì đáng kể, ảnh vẫn còn dễ chưa gặp nhiều khó khăn
   ...

2. Một quy tắc bạn đề xuất thêm vào guideline (kèm ảnh ví dụ nếu có):
   Mắt người đeo kính mát, nếu có thể ước lượng được thì gắn cờ v=1

   ...

3. Nhãn của bạn đi vào model ở đâu? Chọn một lỗi bạn đã sửa và nói nó sẽ làm model học sai thế nào (heatmap, trọng số trong loss, hay bước lật ảnh):
   Nếu đảo nhãn hai cổ chân, mô hình nhận tọa độ mục tiêu của chân trái ở kênh heatmap chân phải và ngược lại. Nếu cờ `v = 1` được gán cho một điểm không thể định vị, mô hình vẫn học theo tọa độ ước lượng đó. Bảng review ghi riêng các cảnh báo chưa xác nhận để phân biệt với những trường hợp đã đối chiếu được.
   ...

## 8. Khó khăn và lỗi kỹ thuật

JSON xuất từ CVAT nằm trên một dòng dài nên khó chụp phần keypoint. Có thể định dạng một bản sao trong VS Code bằng `Shift + Alt + F` và chụp phần `image_id`, `num_keypoints` và `keypoints`. Xác định cờ cho người đeo kính mát
...

## Bonus (nếu làm)

### B1 — 3 ảnh người khó thêm

| Ảnh | Số skeleton | Số người dưới 60 px | Ca khó nhất |
|---|---:|---:|---|
| | | | |
| | | | |
| | | | |

Kết quả `src/check_submission.py` cho `HoVaTen_bonus_persons.zip`:

```text
(dán ở đây)
```

### B2 — 5 ảnh khuôn mặt đen trắng / hồng ngoại

Ảnh không màu khó hơn ở điểm nào? Kính râm trên ảnh hồng ngoại có còn là `v = 1` không?

...

### B3 — Model so với nhãn của tôi (không tính điểm)

- Demo đã dùng:
- Ảnh đã thử:

1. Model có trả điểm cho khớp bị che, hay khớp ngoài ảnh không? Confidence ở các điểm đó thế nào?

   ...

2. Với người quay lưng, model có đổi trái/phải không?

   ...

3. Bộ điểm của model có giống 17 điểm COCO không?

   ...

## 9. Tài liệu tham khảo và công cụ AI đã dùng

- `docs/GUIDELINE.md`, `docs/CVAT_CHEATSHEET.md`, `src/keypoint_schema.json` và `src/lab/pool.json` của repo lab.
- CVAT local để lưu và xem skeleton. `src/check_submission.py` để kiểm file COCO Keypoints theo kết quả đã cung cấp.
- Model Yolov26m Pose, bản nháp khuôn mặt dùng MediaPipe Face Landmarker. Hai model chạy cục bộ.
...
