# Dán label vào CVAT (không cần gõ tay)

Mỗi file `.json` trong thư mục này = **một task**. Đừng dùng nhầm file.

## Cách dán (5 bước)

1. CVAT → **Tasks** → **Create new task**
2. Ô **Name**: gõ đúng tên task, ví dụ `easy_semantic`
3. Ở phần **Labels**, bấm **Raw** (không bấm Constructor)
4. Xóa hết chữ trong ô (nếu có)
5. Mở đúng file json của task → Ctrl+A → Ctrl+C → quay lại CVAT → Ctrl+V
6. Upload ảnh của **đúng task đó** rồi Submit

Nếu CVAT báo lỗi JSON: bạn đang dán nhầm file, hoặc còn sót chữ cũ trong ô Raw. Xóa hết rồi dán lại **cả file**.

## File nào cho task nào

| Task trên CVAT | File copy | Ảnh upload |
| --- | --- | --- |
| easy_semantic | easy_semantic.json | data/tiers/easy_semantic/images |
| medium_instance | medium_instance.json | data/tiers/medium_instance/images |
| hard_panoptic | hard_panoptic.json | data/tiers/hard_panoptic/images |
| cp1_holes | cp1_holes.json | data/checkpoints/cp1_holes/images |
| cp2_slice | cp2_slice.json | data/checkpoints/cp2_slice/images |
| cp5_occlusion | cp5_occlusion.json | data/checkpoints/cp5_occlusion/images |
| cp3_thin | cp3_thin.json | data/checkpoints/cp3_thin/images |
| cp4_curb | cp4_curb.json | data/checkpoints/cp4_curb/images |
| cp6_coverage | cp6_coverage.json | data/checkpoints/cp6_coverage/images |

Sau khi dán, nhìn danh sách label: số lượng và tên phải giống file. `traffic sign` phải có dấu cách.
