# a7y18lte-TrebleDroid

TrebleDroid GSI (bản **vndklite-vanilla**, dùng kernel riêng của máy) + kernel tùy chỉnh cho **Samsung Galaxy A7 (2018) — SM-A750GN / a7y18lte** (các bản SM-A750F/FN/G/N/C cùng một phần cứng).

File lớn được lưu bằng **Git LFS** — cần `git lfs install` trước khi clone/pull.

## Nội dung

| File | Nguồn | Ghi chú |
|---|---|---|
| `rom/system-td-arm64-ab-vndklite-vanilla.img.xz` | [TrebleDroid/treble_experimentations](https://github.com/TrebleDroid/treble_experimentations/releases/tag/ci-20250117) (tag `ci-20250117`, Android 15) | GSI arm64 A/B vndklite vanilla, ~655MB nén `.xz` |
| `kernel/boot.img` | [Hari-Pi/kernel_samsung_a7y18lte](https://github.com/Hari-Pi/kernel_samsung_a7y18lte/releases/tag/8570639315) (release `8570639315`) | Kernel tùy chỉnh, flash vào partition `boot` |

Tài nguyên tham khảo (recovery TWRP/PBRP, disable dm-verity/force-encrypt, stock ROM de-googled, hướng dẫn chi tiết):
👉 https://github.com/Hari-Pi/a7y18lte-Resources

## Cài đặt (tóm tắt theo hướng dẫn của Hari-Pi)

> ⚠️ **Backup toàn bộ dữ liệu trước khi flash.** Các bước này có thể làm mất dữ liệu và có thể làm mất bảo hành.

### Trường hợp 1: Máy đang chạy stock OneUI

1. Cập nhật firmware mới nhất cho máy (xem [samfw.com](https://samfw.com/)).
2. Flash stock ROM de-googled (nếu cần) — xem repo tham khảo ở trên.
3. Vào recovery (nguồn tắt: giữ **Power + Volume Up**; hoặc giữ **Power + Volume Down** rồi đổi sang **Power + Volume Up** khi màn hình tắt).
4. Flash **disable dm-verity/force-encrypt** từ repo tham khảo.
5. Flash GSI + kernel theo các bước chung bên dưới.

### Trường hợp 2: Máy đang chạy LineageOS 18.1 (đã là GSI/Treble) ← máy của bạn

Không cần quay về stock. Chỉ cần:

1. Vào recovery (TWRP): nguồn tắt giữ **Power + Volume Up**.
2. Flash `kernel/boot.img` vào partition **Boot** (recovery → Install → Install Image, hoặc `fastboot flash boot kernel/boot.img`). Kernel mới cần cho GSI Android 15.
3. Flash GSI mới vào **System** (bước 5–6 bên dưới).
4. **Wipe → Factory Reset (Format Data)** — bắt buộc khi nhảy từ Android 11 lên Android 15 để tránh bootloop do khác biệt mã hóa/data.
5. Reboot system.

### Các bước chung (flash GSI)

1. Giải nén ROM: `xz -d rom/system-td-arm64-ab-vndklite-vanilla.img.xz` → được file `system-td-arm64-ab-vndklite-vanilla.img`.
2. Trong recovery, chọn **Install** → chọn file `.img` → chọn partition **System** để flash.
3. (Nếu chưa flash ở trên) Flash `kernel/boot.img` vào partition **Boot**.
4. Reboot system. Lần đầu khởi động có thể lâu.

## Lưu ý

- Bản `vndklite` cần kernel của máy (bước 7) — nếu camera/vân tay không hoạt động thì là do kernel, hãy flash đúng `boot.img` kèm theo.
- Slider độ sáng có thể lỗi ở Android 11+ GSI: vào **Settings → PHH Treble Settings → Misc Features → Backlight** và bật các tùy chọn backlight.
- Magisk mới nhất trên a7y18lte cần nâng cấp qua app (xem chi tiết trong repo tham khảo).

## Giấy phép / trách nhiệm

Sử dụng theo rủi ro của bạn. Xem disclaimer trong repo tham khảo.
