# Bài 1 : Hệ thống Quản lý Tài liệu Dự án Doanh nghiệp

## Phần 1 (Phân tích) :

```text
[ Designer thao tác Ctrl + S ]
              │
              ▼
    [ ATOMIC SAVE / SAFE WRITE ]
              │
              ├── [ Sập nguồn / Lỗi ghi ] ────► Giữ nguyên file gốc trước đó
              ▼

    (Hệ điều hành gửi tín hiệu File Modified tới Sync Client)
              │
              ▼
    [ CLOUD SYNC ENGINE ]
    (Chia nhỏ file -> Tính toán Checksum)
              │
              ├── [ Mất kết nối Internet ] ───► [ LOCAL SYNC QUEUE ] ──> Lưu hàng đợi, tự Retry khi có mạng
              │
              └── [ Kết nối mạng khả dụng ] ──► Kiểm tra mã Hash với phiên bản trên Cloud
                                                          │
                                ┌─────────────────────────┴─────────────────────────┐
                                ▼                                                   ▼
                    [ Trùng khớp bản gốc ]                               [ Xuất hiện xung đột (Conflict) ]
                                │                                                   │
                                ▼                                                   ▼
                    [ Upload Delta Blocks ]                              [ ÁP DỤNG QUY TẮC BẢO TOÀN ]
                                │                                        - Giữ nguyên file trên Cloud
                                ▼                                        - Đổi tên bản mới đẩy lên
                    [ Tạo Version History mới ]                          - Kích hoạt phân nhánh dữ liệu
```


## Phần 2 : 3 bước thiết lập phần mềm đồng bộ

- Bước 1 : Lập trình viên cần tải (google drive / onedrive)
- Bước 2 : Thiết lập tự động hóa , tự động lưu bài
- Bước 3 : Thiết lập chuẩn hóa tên và  version history để lấy lại file cũ mội khi cần
