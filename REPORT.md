# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `...` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: lehainam8114
- Ngày / CVAT local: 17/09/2026 / localhost:8080
- Công cụ đã dùng: CVAT Polygon Tool, Semi-Auto (Intelligent Scissors)

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

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; "quy tắc biên" là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh `000000181542.jpg` — object **person** ở vị trí trung tâm ảnh, đứng trên vỉa hè, nhìn thấy toàn thân từ đầu đến chân.
- Class và quy tắc tôi dùng để chọn biên: Class **person**. Quy tắc biên: vẽ sát theo đường viền cơ thể thực tế nhìn thấy; phần chân tiếp đất dừng tại mép tiếp xúc với mặt đường, không kéo xuống dưới; phần tay nếu sát người khác thì dừng tại điểm chia tách rõ ràng nhất.
- Nếu dùng gợi ý sau đó: Dùng Intelligent Scissors để trace nhanh viền lưng và vai — vùng gợi ý khá khớp, chỉ cần sửa phần chân bị bám vào vỉa hè, kéo điểm cuối lên đúng mép chân.
- Nếu không dùng gợi ý: —

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi "đã sửa" khi chưa sửa.

- Task/ảnh/vùng: `cp2_slice` — ảnh `000000017627.jpg`, hai xe ô tô đứng sát nhau ở giữa ảnh.
- Lỗi thuộc loại: **gộp-tách** — ban đầu vẽ một mask chung cho cả hai xe vì chúng tiếp giáp và có màu tương tự nhau.
- Bằng chứng tôi nhìn thấy: Nhìn kỹ ở zoom lớn thấy đường viền thân xe bên trái và bên phải có khe chia tách nhỏ khoảng 5–8px, hai màu sơn xe cũng khác nhau.
- Quy tắc và hành động sửa: Mỗi xe là một instance riêng biệt dù đứng sát nhau. Xóa mask gộp, vẽ lại hai polygon riêng — xe trái dừng tại đường viền ngoài cùng bên phải thân xe trái; xe phải bắt đầu từ đường viền ngoài cùng bên trái thân xe phải.
- Sau sửa đã Save và export lại chưa? **Đã Save và export lại** — file `cp2_slice.zip` là bản đã sửa với 12 annotation (9 car + 3 person) cho 1 ảnh, các xe đã được tách đúng instance.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `hard_panoptic` / `000000460147.jpg` — vùng road ở trung tâm ảnh, xe ô tô đỗ một phần trên đường | (A) road chạy xuyên gầm xe vì chức năng vẫn là đường; (B) dừng mask road tại đáy xe vì không nhìn thấy mặt đường dưới gầm | hard_panoptic yêu cầu stuff (road) và things (car) cùng đúng; phần gầm xe không nhìn thấy được | Quyết định: dừng road tại mép xe, không phủ xuyên gầm. Hỏi coach: với stuff có nên ước lượng vùng bị che hay chỉ annotate phần nhìn thấy? |
| `medium_instance` / `000000458325.jpg` — bicycle nằm dựa vào tường, frame xe gần như trùng màu tường | (A) bicycle là một instance riêng dù khó thấy rõ viền; (B) bỏ qua vì quá nhỏ và lẫn nền | Zoom 200% vẫn thấy bánh xe và tay lái phân biệt được; task yêu cầu đủ vật, tổng 53 annotation cho 3 ảnh | Quyết định: vẽ mask bicycle theo phần nhìn thấy (bánh + khung), chấp nhận biên có thể lệch ±5px. |
| `cp1_holes` / `000000144300.jpg` — kính xe (windshield) có phản chiếu bầu trời | (A) kính là hole cần khoét bỏ khỏi mask car vì có thể nhìn xuyên; (B) kính vẫn là bề mặt xe, không khoét | CP1 yêu cầu xử lý holes: kính/khe nằm trong mask vật theo quy tắc task; kính là vật liệu cứng không phải lỗ thực sự | Quyết định: giữ kính trong mask car, không khoét. Hỏi coach nếu quy tắc lớp yêu cầu khoét kính xe. |
