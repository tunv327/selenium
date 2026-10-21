# Kiểm thử tự động website bằng Selenium

Bài tập thực hành công cụ kiểm thử **Selenium WebDriver** (Python + pytest): xây dựng 05 test case tự động cho website demo [Sauce Demo](https://www.saucedemo.com).

## 1. Giới thiệu

- **Công cụ:** Selenium WebDriver 4, pytest, pytest-html
- **Ngôn ngữ:** Python 3
- **Trình duyệt:** Google Chrome (Selenium tự tải driver phù hợp)
- **Website kiểm thử:** https://www.saucedemo.com
- **Tài khoản demo:** `standard_user` / `secret_sauce`

## 2. Danh sách test case

| Mã | Tên test | Mô tả | Dữ liệu vào | Kết quả mong đợi |
|----|----------|-------|-------------|------------------|
| TC01 | `test_login_success` | Đăng nhập thành công | standard_user / secret_sauce | Chuyển đến trang danh sách sản phẩm (`inventory.html`) |
| TC02 | `test_login_wrong_password` | Đăng nhập sai mật khẩu | standard_user / sai_mat_khau | Hiện thông báo lỗi "Username and password do not match" |
| TC03 | `test_add_to_cart` | Thêm sản phẩm vào giỏ hàng | Sauce Labs Backpack | Biểu tượng giỏ hàng hiện số 1 |
| TC04 | `test_remove_from_cart` | Xóa sản phẩm khỏi giỏ hàng | Sauce Labs Backpack | Giỏ hàng không còn sản phẩm nào |
| TC05 | `test_logout` | Đăng xuất | Menu → Logout | Quay về trang đăng nhập |

## 3. Cấu trúc thư mục

```
Selenium-Testing/
├── test_saucedemo.py    # Mã nguồn 5 test case
├── requirements.txt     # Danh sách thư viện
├── screenshots/         # Ảnh chụp màn hình sau mỗi test (tự sinh khi chạy)
├── report.html          # Báo cáo kết quả (tự sinh khi chạy với --html)
└── README.md
```

## 4. Yêu cầu môi trường

- Python 3.9 trở lên
- Google Chrome đã cài đặt
- Kết nối Internet

## 5. Cài đặt

Mở PowerShell trong thư mục dự án và chạy:

```powershell
python -m pip install selenium pytest pytest-html
```

Hoặc cài từ file `requirements.txt`:

```powershell
python -m pip install -r requirements.txt
```

## 6. Chạy test

Chạy toàn bộ test case:

```powershell
python -m pytest test_saucedemo.py -v
```

Chạy một test case riêng, ví dụ TC03:

```powershell
python -m pytest test_saucedemo.py -v -k test_add_to_cart
```

Chạy và xuất báo cáo HTML:

```powershell
python -m pytest test_saucedemo.py -v --html=report.html --self-contained-html
```

Kết quả mong đợi khi mọi test đều đạt:

```
test_saucedemo.py::test_login_success PASSED
test_saucedemo.py::test_login_wrong_password PASSED
test_saucedemo.py::test_add_to_cart PASSED
test_saucedemo.py::test_remove_from_cart PASSED
test_saucedemo.py::test_logout PASSED
============ 5 passed ============
```

## 7. Kỹ thuật sử dụng

- **Locator:** `By.ID`, `By.CLASS_NAME`, `By.CSS_SELECTOR`
- **Explicit Wait:** `WebDriverWait` kết hợp `visibility_of_element_located`, `element_to_be_clickable`, `invisibility_of_element_located` để tránh lỗi do trang tải chậm
- **Fixture (pytest):** mở trình duyệt trước mỗi test, chụp ảnh và đóng trình duyệt sau mỗi test
- **Assertion:** kiểm tra URL, nội dung thông báo, số lượng sản phẩm trong giỏ
- **Cấu hình Chrome:** tắt popup đổi mật khẩu của Chrome để test chạy ổn định

## 8. Xử lý lỗi thường gặp

| Lỗi | Cách xử lý |
|-----|-----------|
| `pytest` is not recognized | Dùng `python -m pytest ...` thay cho `pytest ...` |
| `No module named 'selenium'` | Chạy lại lệnh cài đặt ở mục 5 |
| `file or directory not found` | Chạy lệnh trong đúng thư mục chứa `test_saucedemo.py` |
| `TimeoutException` | Kiểm tra kết nối mạng và chạy lại |

## 9. Tài liệu tham khảo

- Selenium Documentation: https://www.selenium.dev/documentation/
- pytest Documentation: https://docs.pytest.org/
- Website thực hành: https://www.saucedemo.com
