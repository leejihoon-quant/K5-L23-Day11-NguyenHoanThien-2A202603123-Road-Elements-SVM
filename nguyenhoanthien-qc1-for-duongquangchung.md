# Phiếu QC 1 — Road v1.0

> **Ghi chú:** chưa có lô của bạn được ghép nên phiếu này là **tự kiểm lô của chính tôi** (nguyenhoanthien, revision 1) bằng `road_check lint` và xem lại ảnh. Khi có lô của bạn kia, thay tên file, tên người kiểm và số liệu.

Lô được kiểm (học viên): nguyenhoanthien (tự kiểm)   Người kiểm (học viên): Nguyễn Hoàn Thiện  
Ngày: 2026-11-22                  Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): nguyenhoanthien-front.zip, nguyenhoanthien-fisheye.zip, revision 1  
Số ảnh kiểm: 6 (+ 22 ảnh thêm, ghi riêng: toàn bộ 28 ảnh A01–A16, B01–B12 đã lint)   Số nhãn đã kiểm (shape + tag): 304 shape (front 254, fisheye 50 ở manifest; tag 4/ảnh × 28 ảnh)  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 28 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 28 | 4 (ca chờ lead) | nặng |
| QC1-03 position | sai thuộc tính / thừa | 28 | 0 (B06 đã sửa) | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 28 | chưa đo | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 28 | 1 (A08, ca mơ hồ) | chính |
| QC1-06 style, color, kind | sai thuộc tính | 28 | 0 phát hiện | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 28 | chưa đo | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 28 | chưa đo | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 28 | chưa đo | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 28 | chưa đo | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 12 | 0 (đã thêm điểm theo cung) | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

"Chưa đo": lint không kiểm được (cần GT hoặc người xem ảnh); không có nghĩa là không lỗi.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A05 | lane | nặng | Chưa có L1 và R1; ảnh không thấy vạch sơn (đường nhựa mờ) |
| 2 | QC1-02 | A07 | lane | nặng | Chưa có L1; bên trái là dải bê tông, không có vạch sơn |
| 3 | QC1-02 | A09 | lane | nặng | Chưa có R1; bên phải đường mở rộng, không thấy vạch |
| 4 | QC1-05 | A08 | lane (id 8097, 9003) | chính | 2 polyline cùng L1: vạch liền chuyển sang vạch đứt, khác style nên tách |

Lỗi đã tự sửa trước khi nộp (không tính vào số lỗi): B06 position L1 thay bằng other cho 2 lane (QC1-03); A06 vạch phải other thành R1; A07 xóa điểm lặp ở polygon drivable; B02, B03, B04, B07, B08 thêm điểm theo cung cho lane và road_curb (QC1-11); B03 bật edge_zone cho biển ở rìa.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Không thấy vạch sơn nào; xác nhận miễn QC1-02 cho L1 và R1? |  |
| A07 | Bên trái là dải bê tông không vạch; xác nhận miễn L1 (mép đường dùng road_curb)? |  |
| A09 | Bên phải đường mở rộng không vạch; xác nhận miễn R1? |  |
| A08 | Vạch liền rồi đứt cùng vị trí L1: tách hai polyline có đúng không? |  |
| B11 | Bãi đỗ xe, không vẽ shape nào (vạch ô đỗ không gán lane); có chấp nhận? |  |

## Quyết định
Lỗi nặng: 4 (đều chờ lead)   Lỗi chính: 1 / 304 nhãn = 0,3 %   Lỗi nhẹ: 0   Ca chờ lead: 5  
Quyết định (Release / Hold / Rework): Hold (đề xuất), chờ lead xác nhận 4 ca QC1-02; nếu được miễn thì Release  
Lý do (theo luật của phiếu): còn lỗi mức nặng chưa được lead xác nhận miễn; ngoài 4 ca này lint không còn cảnh báo nặng. Quyết định cuối thuộc về lead, theo [thang mức lỗi](../docs/qc_severity_road_v1.0.md).

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
