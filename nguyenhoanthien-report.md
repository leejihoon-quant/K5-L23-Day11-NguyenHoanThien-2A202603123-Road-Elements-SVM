# Báo cáo cá nhân — Ngày 11
Họ tên: Nguyễn Hoàn Thiện   Mã học viên: 2A202603123  
Phiên bản CVAT (Help → About): 2.83.1 (CVAT local; hướng dẫn của lab viết cho 2.82.0)  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-22 (khoảng 08:52 giờ máy; manifest ghi 01:52 UTC)    Số lần nộp lại sau Rework: 0  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | lane/road_curb là polyline, crosswalk/drivable là polygon, traffic_light/traffic_sign là rectangle |
| Thuộc tính và giá trị | Đúng | lane: position, style, color, kind; drivable: area_type; traffic_sign: group, facing, edge_zone |
| 4 tag ảnh | Đúng | camera, timeofday, weather, source; lint báo cả 28 ảnh đủ bốn tag |
Cách kết thúc polyline trên bản CVAT này: (bạn điền theo thao tác thực tế trên CVAT của bạn)  
Cách đặt tag ảnh trên bản CVAT này: (bạn điền)  

## 2. Số lượng đã gán
Hai file zip đã gộp task chính và task extra, nên số liệu dưới đây là tổng của từng zip (theo manifest).

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front + front-extra (A01–A16, làm đủ 4/4 ảnh extra) | 16 | 42 | 12 | 6 | 42 | 58 | 94 |
| fisheye + fisheye-extra (B01–B12, làm đủ 4/4 ảnh extra) | 12 | 7 | 13 | 12 | 10 | 3 | 5 |

B11 (camera sau, bãi đỗ xe) không có shape nào, chỉ có tag, vì không có vạch dọc và vạch ô đỗ không gán lane.

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | lane | Vẽ L1/R1 hay không vẽ | Không vẽ | Đường nhựa mờ, không thấy vạch sơn; guideline: không vẽ cái không có. Chờ coach xác nhận |
| A07 | lane | Vẽ L1 hay dùng road_curb | Không vẽ L1 | Bên trái là dải bê tông, không có vạch sơn; mép đường dùng road_curb |
| A09 | lane | Vẽ R1 hay không vẽ | Không vẽ | Bên phải đường mở rộng, không thấy vạch. Chờ coach xác nhận |
| A08 | lane | Một hay hai polyline L1 | Hai polyline | Vạch liền chuyển sang vạch đứt, khác style nên tách |
| A06 | lane | R1 hay other | R1 | Vạch trắng bên phải là vạch gần nhất bên phải xe |
| B06 | lane | position L1 hay other | other | Camera bên trái, guideline bắt buộc position = other; style dashed |
| B03 | traffic_sign | edge_zone | bật | Tâm box nằm ngoài 80% bán kính ảnh fisheye |
| B11 | lane / drivable | Vạch ô đỗ có phải lane? | Không vẽ gì | Vạch ô đỗ không gán lane (guideline mục fisheye); ô đỗ nằm ngoài phạm vi v1.0 |
| Ảnh có vạch vàng sát vỉa | lane | lane hay sơn lề (cấm đỗ) | Xem lại từng ảnh | Vạch vàng sát bó vỉa nhiều khả năng là sơn lề, không phải vạch chia làn |
| Ảnh có dải giữa hai vạch vàng | drivable | dải phân cách hay làn cùng chiều | Không gán drivable cho dải phân cách | `alternative` chỉ dành cho làn cùng chiều |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: (bạn điền)  Quyết định nhận được: (bạn điền)  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| (bạn điền khi nhận phiếu) |  |  |  |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| nguyenhoanthien-front.zip | Có (`road_check lint` đọc được, 16 ảnh, không kèm ảnh) | (bạn điền) | (bạn điền) | Có (16/16 ảnh đủ 4 tag) |
| nguyenhoanthien-fisheye.zip | Có (12 ảnh, không kèm ảnh) | (bạn điền) | (bạn điền) | Có (12/12 ảnh đủ 4 tag) |

Lint lần cuối: 0 cảnh báo nhẹ, 1 cảnh báo chính (A08), 4 cảnh báo nặng QC1-02 (A05 thiếu L1 và R1, A07 thiếu L1, A09 thiếu R1). Cả 4 là ảnh tôi không thấy vạch; đã ghi để coach xác nhận.

## 6. Ảnh chụp màn hình
(bạn tự chụp và chèn 4 ảnh theo yêu cầu: tab Labels, một ảnh camera trước đã gán đủ, một ảnh fisheye phóng to polyline cong, một đoạn XML có `<polyline label="lane">`)

## 7. Tự đánh giá
**Khó khăn gặp phải trong quá trình làm bài**

1. **Dùng AI hỗ trợ set up bài tập, hướng dẫn chạy lệnh
2. **Không có ground truth để học theo.** Tôi cố tìm nhãn gốc của BDD100K (lane, curb, crosswalk) nhưng trang chính thức báo lỗi chứng chỉ và DNS không truy cập được; bản BDD cục bộ chỉ có box, vùng lái, thời tiết, không có lane/curb/crosswalk. WoodScape thì cần đăng ký với Valeo. Vì vậy lane, curb và crosswalk phần lớn do vẽ tay ước lượng, độ chính xác không bảo đảm trong 5 px.
3. **Ảnh fisheye khó:** vạch và mép đường cong theo cung, cần đặt nhiều điểm; camera sau bị lật trái/phải; camera bên trái/phải luôn phải dùng position = other. Lỗi này tôi mắc ở B06 và lint phát hiện.
4. **Không phân biệt chắc chắn vạch sơn lề và vạch chia làn,** hay dải phân cách và làn cùng chiều (guideline và nhãn BDD định nghĩa `alternative` khác nhau).
5. **Ảnh thật sự không có vạch (A05, A07, A09):** lint báo QC1-02 nhưng vẽ thêm là sai, nên giữ nguyên và chờ coach xác nhận.
6. **Kỹ thuật:** CVAT local 2.83.1 khác bản hướng dẫn; export phải gộp hai task thành một zip; xử lý CORS và mã hóa tiếng Việt trên Windows.

Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20: QC1-03 (position sai ở camera bên) và QC1-11 (fisheye ít điểm). Ngày 20 tôi sẽ đọc luật theo loại camera trước khi gán, rồi chạy lint sau mỗi ảnh fisheye thay vì chờ cuối buổi.  
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào: Lỗi B06: nếu để L1 trên camera trái, model row-anchor sẽ học vạch bên là vạch sát xe của làn đang đi, làm hệ thống giữ làn (LKA) đánh giá sai vị trí xe trong làn. Dải phân cách gán nhầm `drivable` thì model coi vùng cấm là đi được.  
