# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602167
- Ngày / CVAT local: 17/09/2026, CVAT local
- Công cụ đã dùng: Brush / Polygon trên CVAT local; không dùng SAM

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

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

Export Easy lần đầu thiếu PNG (`SegmentationClass/`); đã Save lại, export **Segmentation mask 1.1** và thay `easy_semantic.zip`.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: `000000181542.jpg` — xe bus lớn phía trước/gần camera (object `bus` đầu tiên trên ảnh này).
- Class và quy tắc tôi dùng để chọn biên: class `bus`. Chỉ vẽ phần thân xe còn nhìn thấy; dừng mask ở mép kính/thân, không đoán phần bị che và không gộp xe/người sát cạnh.
- Nếu dùng gợi ý sau đó: không dùng.
- Nếu không dùng gợi ý: không dùng; quyết định gán `bus` vì đây là xe khách lớn, khác `car`/`truck` cùng cảnh, và giữ một instance cho cả xe dù có chi tiết cửa/kính.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `easy_semantic` — lần export đầu (ZIP ~343 byte) không có mask PNG cho `7ee6d192-89e2408b.jpg`, `817bca71-00000000.jpg`, `81ae7cbb-6bc63a4a.jpg`.
- Lỗi thuộc loại: khác (export thiếu file mask / sai hoặc thiếu thư mục `SegmentationClass/`).
- Bằng chứng tôi nhìn thấy: inspect báo không có PNG trong `SegmentationClass/` và thiếu ba ảnh; ZIP chỉ còn `labelmap.txt` và `ImageSets/`.
- Quy tắc và hành động sửa: đúng format Easy là **Segmentation mask 1.1**; Save lại trên CVAT, export lại, đặt đúng tên `easy_semantic.zip`.
- Sau sửa đã Save và export lại chưa? Rồi. Inspect sau sửa: OK, đủ 3 mask.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): sau khi có ZIP Easy đúng, scorer local với `tiers_gt.zip` của mentor: **Easy 17.9/20 (mIoU 0.802)**; `road`/`sky` ~0.97, `sidewalk` 0.702, `building` 0.680, `vegetation` 0.684. Cả ba tier **72.9/82** (Medium 25.0/32, Hard 30.0/30). Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| Easy, ranh `road`/`sidewalk` (IoU sidewalk còn 0.70) | Tô theo màu nhựa giống mặt đường, hoặc tách theo bó vỉa/chức năng đi bộ | Mini-sheet: ranh road–sidewalk theo chức năng và bó vỉa, không chỉ theo màu | Đã tách sidewalk theo phần nền nâng/bó vỉa. Xin xác nhận chỗ màu gần giống road. |
| Medium, 3 ảnh; nộp 92 mask vs GT 71 (FP 21, FN 0) | Giữ mọi mảng nhỏ `person`/`car` là instance, hoặc gộp/xóa mảnh phụ | Instance: đủ vật, không thừa; một vật một mask; chỉ phần nhìn thấy | Recall 1.00 nhưng thừa mask. Sẽ xóa instance nhỏ/nhầm; coach xem giúp mảnh người xa có tính object không. |
| Hard `000000350023.jpg`, một mask `bicycle` rất nhỏ (bbox ~8×12) và nhóm `person` (9 mask, PQ person 0.26) | Xe đạp vs một phần người/xe máy; tách person bị che thành nhiều object vs một instance | Panoptic: thing tách instance; vật bị che vẫn một instance; không đoán vùng khuất | Giữ 1 bicycle nhỏ vì nhìn thấy khung/bánh. Person còn FP/FN — hỏi ranh person–motorcycle khi chồng lên nhau. |
