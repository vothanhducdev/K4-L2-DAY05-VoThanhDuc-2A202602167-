# Mẫu tham khảo — đã điền theo bài Day 5

**Cách dùng:** Bản coach chấm là [`REPORT.md`](../REPORT.md) ở gốc fork. File này điền cùng nội dung để đối chiếu khi kiểm GitHub.

- Mã học viên theo lớp: 2A202602167
- Ngày / CVAT local: 17/09/2026, CVAT local
- Công cụ đã dùng: Brush / Polygon; không dùng Intelligent Scissors, gợi ý tự động hay SAM

Mã học viên là mã lớp cấp, không cần ghi họ tên trong bản nộp nếu kênh lớp đã nhận diện bạn. Ở dòng công cụ, giữ lại những công cụ bạn thật sự dùng; không có SAM cũng hoàn toàn bình thường.

## 1. Bài đã nộp

**Bạn cần điền gì?** “File ZIP đúng tên” là tên file bạn đã tải từ CVAT rồi đặt lại, ví dụ `easy_semantic.zip`. “Hoàn thành mấy ảnh” là số ảnh bạn đã vẽ và Save, không phải số ảnh có trong task. Chưa làm hoặc export lỗi thì ghi `chưa có`, đừng ghi tên một ZIP rỗng. Cột điểm là **điểm tối đa của task**, không phải điểm tự chấm.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Không tự điền điểm nếu chưa có phản hồi từ người chấm. Nếu export lỗi, ghi task, trạng thái Save và thông báo đã gửi coach.

Lỗi export đã xử lý: `easy_semantic` lần đầu ZIP ~343 byte, không có PNG trong `SegmentationClass/`; đã Save 3/3 ảnh, export lại **Segmentation mask 1.1**, đặt đúng `submissions/easy_semantic.zip`.

## 2. Một quyết định trước khi dùng gợi ý

**Mục này hỏi cách bạn tự ra quyết định.** Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi mở bất kỳ đề xuất tự động nào cho object đó. “Vị trí” chỉ cần mô tả đủ để tìm lại, chẳng hạn “xe bên trái, nửa dưới ảnh”; nếu nhớ tên file JPG thì ghi luôn. “Quy tắc biên” nghĩa là lý do bạn dừng mask ở đâu, nhất là mép ảnh hoặc vật che. Không cần ảnh chụp riêng nếu lớp không yêu cầu.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: `000000181542.jpg`, xe bus lớn gần camera (phía trước, chiếm phần lớn khung).
- Class và quy tắc tôi dùng để chọn biên: class `bus`. Chỉ vẽ phần thân xe nhìn thấy; dừng ở mép kính/thân; không đoán phần bị che; không gộp `car`/`person` sát cạnh vào cùng mask.
- Nếu dùng gợi ý sau đó: không dùng.
- Nếu không dùng gợi ý: không dùng. Gán `bus` vì đây là xe khách lớn, khác `car`/`truck` cùng cảnh; kính/cửa vẫn nằm trong một instance, không khoét thành lỗ.

## 3. Một lỗi tôi tìm thấy và sửa

**Chọn một lỗi có thật trong bài của bạn**, không cần lỗi lớn nhất. Nếu chưa sửa được do công cụ lỗi, nói rõ đã thử gì và cần coach hỗ trợ gì; đừng ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `easy_semantic` — thiếu mask PNG cho `7ee6d192-89e2408b.jpg`, `817bca71-00000000.jpg`, `81ae7cbb-6bc63a4a.jpg`.
- Lỗi thuộc loại: khác (export thiếu `SegmentationClass/*.png`).
- Bằng chứng tôi nhìn thấy: `inspect_submissions.py` báo không có PNG, thiếu 3 ảnh; ZIP chỉ còn `labelmap.txt` và `ImageSets/`.
- Quy tắc và hành động sửa: Easy phải export **Segmentation mask 1.1**; Save lại trên CVAT, export ZIP mới, tên đúng `easy_semantic.zip`.
- Sau sửa đã Save và export lại chưa? Rồi. Inspect: OK, đủ 3 mask class.

**Nếu đã xem điểm tự đánh giá trên GitHub Actions hoặc chạy scorer:** scorer local với gói mentor, không đưa ground truth lên fork: Easy **17.9/20** (mIoU 0.802; `road`/`sky` ~0.97, `sidewalk` 0.702, `building` 0.680, `vegetation` 0.684). Medium **25.0/32**. Hard **30.0/30**. Tổng ba tier **72.9/82**. Không tự ghi PASS, top 3 hoặc bonus.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

**“Ca” là một vùng cụ thể khiến bạn phải dừng lại và chọn cách hiểu**, không nhất thiết là ba lỗi. Với mỗi dòng, ghi vị trí, hai khả năng bạn đã cân nhắc, dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi quyết định của bạn. Nếu quy tắc chưa đủ rõ, viết một câu hỏi mà coach có thể trả lời. Ba dòng có thể đến từ ba task khác nhau.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| Easy, ranh `road` / `sidewalk` | Tô theo màu nhựa giống mặt đường, hoặc tách theo bó vỉa / lối đi bộ | Mini-sheet: ranh theo chức năng và bó vỉa, không chỉ theo màu; IoU sidewalk còn 0.70 | Đã tách sidewalk theo phần nền nâng/bó vỉa. Xin xác nhận chỗ màu gần giống road. |
| Medium, cả 3 ảnh (92 mask vs 71 GT) | Giữ mọi mảng nhỏ `person`/`car` là instance, hoặc xóa mảnh phụ | Đủ vật, không thừa; một vật một mask; chỉ phần nhìn thấy; R@0.5 = 1.00, FP = 21 | Recall đủ nhưng thừa mask. Coach xem mảnh người/xe rất nhỏ có tính object không. |
| Hard `000000350023.jpg`, `bicycle` bbox ~8×12 và nhóm `person` | Bicycle vs một phần person/motorcycle; tách person bị che thành nhiều object vs một instance | Thing tách instance; vật bị che vẫn một instance; không đoán vùng khuất; PQ person 0.26 | Giữ 1 bicycle vì nhìn thấy khung/bánh. Hỏi ranh person–motorcycle khi chồng lên nhau. |
