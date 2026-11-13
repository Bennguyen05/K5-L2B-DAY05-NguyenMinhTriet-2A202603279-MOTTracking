# Báo cáo cá nhân — HoVaTen-MSSV

Đổi tên file theo quy tắc `MSSV_HoTen.md`. Ví dụ: `20241234_NguyenVanAn.md`.

Đoạn video: MOT17-09, 150 frame (frame 1–150), nguồn MOTChallenge, giấy phép CC BY-NC-SA 3.0.

## 0. Thông tin học viên

- Họ tên: Nguyễn Minh Triết
- MSSV: 2A202603279
- Mã đề (A/B/C): B
- Email: trietn0512@gmail.com
- Link repository: https://github.com/Bennguyen05/K5-L2B-DAY05-NguyenMinhTriet-2A202603279-MOTTracking.git
- Giờ bắt đầu: 16h
- Giờ kết thúc: 19h30

## 1. Xem trước đoạn video (CP0)

Ghi **trước khi vẽ**, mỗi người một dòng.

| Mã | Frame xuất hiện | Frame cuối thấy được | Rẽ / dừng / đổi tốc độ ở frame | Bị che ở frame | Ghi chú |
|---|---|---|---|---|---|
| P1 |1 |150 | ban đầu tốc độ chậm nhưng từ frame 50 thì tốc độ tăng dần |1-36, 109-149 |Dáng người to, cao, mang balo |
| P2 |1 |150 |tốc độ đều |không có |phụ nữ lớn tuổi, mang túi to, mặc áo màu xanh lá |
| P3 |1 |112 |di chuyển chậm lại và dừng từ frame 40 |89-149 | phụ nữ, đi cùng với đứa trẻ |
| P4 |1 |129 |dừng lại từ frame 26 |105-139, 142-149 |trẻ em, mặc váy |
| P5 |1 |150 |tóc độ đều |0-64 |người nam lớn tuổi, đội mũ lưỡi trai trắng |

## 2. Keyframe và thời gian (CP1, CP4)

Số keyframe lấy từ kết quả `src/check_submission.py`.

| Mã | Số keyframe | Keyframe ở frame | Số frame có mặt | Keyframe / 100 frame | Thời gian (phút) | Chỗ khó |
|---|---|---|---|---|---|---|
| P1 |134 |0–89, 92–113, 115–119, 122–136, 148–149 |137 |97.8 |25 | Ở các frame cuối người này bị che hoàn toàn rồi lại xuất hiện nên phải đánh giá lúc nào bật occluded hay outside |
| P2 |147 |0–31, 33–39, 41–44, 46–149 |150 |98.0 |25 |không có, người này xuất hiện rõ ở hầu hết mọi frame |
| P3 |45 |0–20, 22–23, 30, 32–34, 39, 45–46, 89–92, 95, 102–103, 105–107, 127–128, 131, 136–137 |120 |37.5 |20 | Người ở xa nên hơi khó quan sát vẽ track |
| P4 |94 |0, 2–24, 27–28, 33–43, 45–46, 49–52, 54–67, 72–74, 77, 80, 82, 85, 88, 90, 94, 97–98, 100–101, 103–110, 129–131, 135–146 |129 |72.9 |20 | Người ở xa nên hơi khó quan sát vẽ track |
| P5 |123 |0–3, 5–21, 23–86, 88–94, 96–119, 143–149 |150 |82.0 |20 | Ở các frame đầu người này ở ngoài khung hình nên phải xem xét mở occluded |
| **Tổng** |543 | | | | | |

Keyframe / 100 frame của cả bài = tổng keyframe ÷ tổng số frame có mặt × 100 = 543 ÷ 686 × 100 = 79.2.

Bạn đặt keyframe nhiều nhất ở người nào? Vì sao (người đó rẽ, dừng, lại gần camera hay bị che)?
Tôi đặt keyframe nhiều nhất ở P2 vì người đó xuất hiện rõ ở hầu hết các frame

## 3. Đoạn bị che (CP2)

Người bị che: `P1`

| Mốc | Frame |
|---|---:|
| Bắt đầu bị che một phần (bật `occluded`) | 109 |
| Mất hẳn (bật `outside`) |120 |
| Hiện lại (tắt `outside`) |122 |
| Thấy rõ trở lại (tắt `occluded`) |không có |

- Thời gian khuất hẳn: 2 frame = 0.6s giây.
- Quyết định: giữ cùng ID .
- Lý do (trả lời 3 câu: khuất bao lâu so với 60 frame, ngoại hình có khớp, chỗ hiện lại có đúng hướng và tốc độ):
Khuất 2 frame so với 60 frame, ngoại hình giống hệt, tốc độ và hướng đúng với các frame đầu

Ảnh chụp màn hình:

<img width="217" height="318" alt="che_1_truoc" src="https://github.com/user-attachments/assets/c2fdb314-d094-4833-bca6-4c7e39e90811" />

<img width="179" height="322" alt="che_2_giua" src="https://github.com/user-attachments/assets/66165ac6-9abe-4e72-be5f-3f2c8a8a8a3f" />

<img width="168" height="338" alt="che_3_sau" src="https://github.com/user-attachments/assets/8afbcf56-3283-499d-8d48-279fbdbee36b" />

## 4. Tự review ID (CP3)

Lượt 1 theo người (đi ngược từ frame 149 về 0 trên CVAT), lượt 2 theo cảnh (nhảy 10 frame). Ít nhất 3 dòng; không có lỗi thì ghi một dòng "đã kiểm hai lượt, không lỗi".

Loại lỗi dùng đúng một trong 7 mã: `id_switch`, `fragmentation`, `lost`, `merge`, `false_track`, `drift`, `flag`.

| Frame | Mã người | Loại lỗi | Mô tả một câu | Phát hiện ở lượt | Đã sửa? |
|---:|---|---|---|---|---|
| | | | | | |
| | | | | | |
| | | | | | |


Tổng hợp số lỗi theo loại:

| `id_switch` | `fragmentation` | `lost` | `merge` | `false_track` | `drift` | `flag` |
|---:|---:|---:|---:|---:|---:|---:|
| | | | | | | |

Lỗi nào chỉ lượt 2 (theo cảnh) mới thấy, lượt 1 (theo người) không thấy? Vì sao?

Đã kiểm hai lượt, không lỗi

## 5. File xuất và kết quả tự kiểm (CP4)

| Kiểm tra | Kết quả |
|---|---|
| Tên file MOT 1.1 |NguyenMinhTriet_mot.zip |
| Tên file CVAT for video 1.1 |NguyenMinhTriet_cvat_video.zip |
| Số track ID khác nhau trong `gt/gt.txt` (phải là 5) |5|
| Frame `outside` không có dòng trong `gt.txt` (đúng / sai) |đúng |
| Job đã completed trên CVAT máy cá nhân |rồi |

Dán phần tóm tắt in ra từ `src/check_submission.py`:

=== File MOT 1.1: NguyenMinhTriet_mot.zip ===
  Số track ID: 5   |   Tổng số box: 686
  [OK]        Đúng 5 track ID.

  Track | Frame có mặt | Số frame | Đoạn vắng (outside)
      1 |   0–149      |      137 | 120–121, 137–147
      2 |   0–149      |      150 | -
      3 |   0–138      |      120 | 108–126
      4 |   0–146      |      129 | 111–128
      5 |   0–149      |      150 | -

  [CẢNH BÁO]  Track 1: chiều cao box đổi > 30% trong 1 frame ở frame [119, 125, 149]. Kiểm tra box co giật (co box theo phần nhìn thấy?).
  [CẢNH BÁO]  Track 3: chiều cao box đổi > 30% trong 1 frame ở frame [131, 132, 133, 134, 137]. Kiểm tra box co giật (co box theo phần nhìn thấy?).
  [CẢNH BÁO]  Track 4: chiều cao box đổi > 30% trong 1 frame ở frame [110, 135, 137]. Kiểm tra box co giật (co box theo phần nhìn thấy?).

=== File CVAT for video 1.1: NguyenMinhTriet_cvat_video.zip ===

  Track | Nhãn   | Frame thấy | Keyframe | KF/100 frame | Frame occluded | Lần bật outside
      0 | person |        137 |      134 |         97.8 |             37 |               2
              Track 0: keyframe ở frame [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 92, 93, 94, 95, 96, 97, 98, 99, 100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110, 111, 112, 113, 115, 116, 117, 118, 119, 122, 123, 124, 125, 126, 127, 128, 129, 130, 131, 132, 133, 134, 135, 136, 148, 149]
  [CẢNH BÁO]  Track 0: 98 keyframe / 100 frame > 50. Quá dày, dồn keyframe vào chỗ rẽ / dừng / bị che.
      1 | person |        150 |      147 |         98.0 |              0 |               0
              Track 1: keyframe ở frame [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 33, 34, 35, 36, 37, 38, 39, 41, 42, 43, 44, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110, 111, 112, 113, 114, 115, 116, 117, 118, 119, 120, 121, 122, 123, 124, 125, 126, 127, 128, 129, 130, 131, 132, 133, 134, 135, 136, 137, 138, 139, 140, 141, 142, 143, 144, 145, 146, 147, 148, 149]
  [CẢNH BÁO]  Track 1: 98 keyframe / 100 frame > 50. Quá dày, dồn keyframe vào chỗ rẽ / dừng / bị che.
      2 | person |        120 |       45 |         37.5 |             30 |               2
              Track 2: keyframe ở frame [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 22, 23, 30, 32, 33, 34, 39, 45, 46, 89, 90, 91, 92, 95, 102, 103, 105, 106, 107, 127, 128, 131, 136, 137]
      3 | person |        129 |       94 |         72.9 |             22 |               2
              Track 3: keyframe ở frame [0, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 27, 28, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 45, 46, 49, 50, 51, 52, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 72, 73, 74, 77, 80, 82, 85, 88, 90, 94, 97, 98, 100, 101, 103, 104, 105, 106, 107, 108, 109, 110, 129, 130, 131, 135, 136, 137, 138, 139, 140, 141, 142, 143, 144, 145, 146]
  [CẢNH BÁO]  Track 3: 73 keyframe / 100 frame > 50. Quá dày, dồn keyframe vào chỗ rẽ / dừng / bị che.
      4 | person |        150 |      123 |         82.0 |             65 |               0
              Track 4: keyframe ở frame [0, 1, 2, 3, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 88, 89, 90, 91, 92, 93, 94, 96, 97, 98, 99, 100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110, 111, 112, 113, 114, 115, 116, 117, 118, 119, 143, 144, 145, 146, 147, 148, 149]
  [CẢNH BÁO]  Track 4: 82 keyframe / 100 frame > 50. Quá dày, dồn keyframe vào chỗ rẽ / dừng / bị che.

  Tổng: 543 keyframe / 686 frame có mặt = 79.2 keyframe / 100 frame
  [OK]        Đọc được 5 track từ annotations.xml.

=== Tóm tắt ===
  Lỗi: 0   |   Cảnh báo: 7
  Không có lỗi định dạng. Mở CVAT xem lại từng [CẢNH BÁO]; cảnh báo đúng ý bạn thì ghi lý do vào báo cáo.

## 6. Ba câu kết

1. Nếu được gán lại, bạn sẽ đặt keyframe khác ở đâu? Vì sao?

   Ở các trường hợp như người bị che khuất chỉ còn hiện một phần cơ thể sẽ khiến cho keyframe bị thu nhỏ đột ngột, khiến hệ thống cảnh báo. Tôi sẽ đặt keyframe ngay tại đỉnh của tư thế giúp box ôm sát cơ thể thay vì bị thừa khoảng trống quá nhiều.

2. Có chỗ nào bạn không chắc "cùng ID hay ID mới"? Bạn đã quyết định và ghi chú thế nào?

   Không có

3. Một lỗi ID trong job của bạn (nếu không còn sót, chọn lỗi đã sửa) có thể làm xe tự lái dự đoán sai chuyển động của người đó như thế nào? Lỗi đó ảnh hưởng MOTA hay IDF1 nhiều hơn?

Một lỗi như id_switch ở frame [137] giữa [P1] và [P3] khiến hệ thống theo dõi gộp hai quỹ đạo thành một. Xe tự lái sẽ thấy người đi bộ đó đột ngột đổi hướng hoặc nhảy vị trí, nên dự đoán chuyển động sai, có thể phanh gấp không cần thiết hoặc không tránh người thật sự đang băng qua. Lỗi này ảnh hưởng IDF1 nhiều hơn MOTA. MOTA chỉ đếm mỗi lần đổi ID như một lỗi nhỏ cộng với FN và FP, nên một lần switch gần như không làm điểm giảm. IDF1 đo mức độ giữ đúng một ID cho một người suốt quỹ đạo, nên một lần đổi ID cắt track thành hai đoạn và làm giảm số khớp đúng của cả hai.

## Bonus (nếu làm)

### B1 — Hai người đi sát

...

### B2 — So cách đặt keyframe

| Cách đặt | Số keyframe | Frame trôi nhất | Ghi chú |
|---|---:|---:|---|
| Đều mỗi 30 frame | | | |
| Theo chỗ đổi hướng | | | |

...

### B3 — So với tracker có sẵn

| Frame | Mã người | Tracker làm gì | Nhãn của bạn | Giải thích (đoán rồi sửa / ghép IoU / box score thấp / ngoại hình) |
|---:|---|---|---|---|
| | | | | |
| | | | | |

## 7. Tài liệu tham khảo và công cụ AI đã dùng

claude để hỗ trợ các chức năng cvat 
