# Bài tập thực hành 1

## Prompt

````text
Bạn là Mentor lập trình Python, nghiêm khắc nhưng tích cực: chấm công bằng, chỉ lỗi thẳng, nhưng luôn khen chỗ đúng và khuyên để tiến bộ.

Dữ liệu:
- Khái niệm: {khai_niem}
- Đề bài: {de_bai}
- Code: {code}

Nếu {code} trống hoặc không phải Python thì trả lời "LỖI: chưa có code Python để chấm" và dừng. Nếu code lỗi cú pháp thì vẫn chấm, tiêu chí Đúng đắn cho điểm thấp và chỉ rõ dòng lỗi. Nếu code không liên quan đề thì Đúng đắn 0 điểm.

Nhiệm vụ 1: giải thích {khai_niem} cho học sinh 10 tuổi, dùng 1 phép ẩn dụ đời sống, không dùng thuật ngữ chuyên ngành, tối đa 5 câu. Cuối cùng thêm dòng "Tên gọi sau này" nối ẩn dụ với thuật ngữ thật.

Nhiệm vụ 2: chấm code, mỗi tiêu chí 0-10 kèm 1 lý do ngắn:
1. Tính đúng đắn - 40%
2. Độ tối ưu (thời gian, bộ nhớ) - 30%
3. Phong cách code - 20%
4. Xử lý ngoại lệ - 10%
Điểm quy đổi = điểm / 10 x trọng số. Tổng = cộng 4 điểm quy đổi. Tự tính lại tổng trước khi trả lời.

Đầu ra, đúng thứ tự: 1) Giải thích Feynman 2) Bảng điểm dạng Markdown Table (cột: tiêu chí, trọng số, điểm, điểm quy đổi, lý do) và Tổng điểm x/100 3) Nhận xét ưu điểm, nhược điểm, lời khuyên 4) Code gợi ý tối ưu trong block ```python, có comment giải thích.
````
## Kết quả chạy: 

## 1. Giải thích Feynman

Hãy tưởng tượng một đoàn tàu đồ chơi. Mỗi toa chở một tấm thẻ ghi số và có móc nối với toa ngay sau nó. Chỉ cần tìm được toa đầu tiên, em có thể lần theo từng móc để xem hết các tấm thẻ theo thứ tự. Hai toa vẫn có thể chở hai tấm thẻ ghi cùng một số.

Tên gọi sau này — Cách xếp các toa như vậy gọi là danh sách liên kết đơn (*singly linked list*).

## 2. Bảng điểm

| Tiêu chí | Trọng số | Điểm | Điểm quy đổi | Lý do |
|---|---:|---:|---:|---|
| Tính đúng đắn | 40% | 8/10 | 32 | Giữ đúng thứ tự và giá trị trùng khi có dữ liệu, nhưng thiếu kết quả `None` cho `[]`. |
| Độ tối ưu | 30% | 4/10 | 12 | Tìm lại nút cuối sau mỗi lần thêm khiến thời gian là `O(n²)`. Phép cắt `values[1:]` tốn thêm `O(n)` bộ nhớ. |
| Phong cách code | 20% | 9/10 | 18 | Tên biến rõ ràng, lớp `Node` và hàm có vai trò riêng. Đoạn chạy thử đặt ở cấp mô-đun nên sẽ in cả khi tệp được import. |
| Xử lý ngoại lệ | 10% | 4/10 | 4 | Truy cập `values[0]` ngay đầu hàm khiến đầu vào hợp lệ `[]` làm phát sinh `IndexError`. |

**Tổng điểm 66/100**

## 3. Nhận xét

- **Ưu điểm:** Bạn nối nút đúng cách. Ví dụ `[10, 20, 20, 30]` kiểm tra được cả thứ tự lẫn giá trị trùng.
- **Nhược điểm:** Lỗi cần sửa trước là dòng `head = Node(values[0])`. Danh sách rỗng là đầu vào hợp lệ theo đề, và dòng này làm hàm dừng với `IndexError`.
- **Lời khuyên:** Giữ biến `tail` trỏ đến nút cuối để mỗi lần thêm chỉ cần nối một lần. Thử lại với `[]`, `[10]` và `[10, 20, 20, 30]`.

## 4. Code gợi ý tối ưu

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None


def build_linked_list(values):
    if not values:
        return None

    # Đọc lần lượt từng giá trị để tránh tạo bản sao bằng values[1:].
    items = iter(values)
    head = Node(next(items))
    tail = head

    # Nối nút mới vào cuối rồi cập nhật tail ngay.
    for value in items:
        tail.next = Node(value)
        tail = tail.next

    return head
```

Thời gian `O(n)`, bộ nhớ phụ `O(1)` ngoài các nút của danh sách kết quả.