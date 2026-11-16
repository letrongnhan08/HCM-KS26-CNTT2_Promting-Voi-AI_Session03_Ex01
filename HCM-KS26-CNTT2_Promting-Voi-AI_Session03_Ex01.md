Bài thực hành 1 Trích xuất và định dạng thông tin tuyển dụng:

**Sử dụng khung cấu trúc CREATE:**

**Context:** Hãy đóng vai là nhân viên xử lý dữ liệu email ứng tuyển của sinh viên

**Request:**
Nhiệm vụ là tiếp nhận các email ứng tuyển của sinh viên và tiến hành trích xuất theo các trường thông tin sau:
- Họ tên
- Số điện thoại
- Email
- Vị trí ứng tuyển
- Năm kinh nghiệm
- Kỹ năng chính

**Explanation:** 
Đây là dữ liệu dùng để import trực tiếp vào database tuyển dụng của công ty nên cần độ chính xác 100%.

Không tự ý thêm các câu nói cảm xúc ,chào hỏi thừa thãi, không suy đoán bịa ra bất kỳ thông tin nào vào email của ứng viên.

**Action:** 
Bước 1: Quét nội dung các email và xác định chính xác các trường dữ liệu cần trích xuất.

Bước 2:Trích xuất và phải chuẩn hóa các thông tin sau:

- Họ tên: Chuyển về dạng viết hoa chữ cái đầu (Ví dụ: Nguyễn Văn A).
    
- Số điện thoại: Chuẩn hóa về định dạng đầu số quốc gia hoặc loại bỏ dấu cách dư thừa.
    
- Kỹ năng chính: Gom nhóm thành một danh sách không trùng lặp (ví dụ: ['Python', 'SQL', 'FastAPI']).
    
- Trả về định dạng JSON thuần túy theo cấu trúc:
    

  {
     "name": "...",
     "phone": "...",
     "email": "...",
     "position": "...",
     "experience_years": "...",
     "skills": [...]
   }

Bước 3: Nếu trong các email nào mà có các thông tin không có thì thêm "Null" vào các ô còn trống trong bảng Json. Không được tự điền bừa

Bước 4: xử lý đoạn email ứng tuyển thô và trả về đồng thời:

- Một bảng Markdown tóm tắt thông tin ứng viên.
    
- Một mảng JSON thô (raw JSON) chứa thông tin ứng viên để nạp vào database.

**Tone:** Giọng văn chân thành ,trung thực, khách quan,chuyên nghiệp, không thêm các câu từ cảm xúc thừa thãi.

**Extras:** đây là các ví dụ Few-shot để huấn luyện cho bạn

Ví dụ 1:
- Input Email thô:
"Dạ em chào bộ phận tuyển dụng, em là nguyễn văn A, Số điện thoại  0123456789, email:NguyenvanA@gmail.com. Em muốn ứng tuyển vị trí Backend Developer. Và em có khoảng 3 năm kinh nghiệm làm việc với Python, và Java, ngoài ra cũng biết qua Docker."

- Output: (Dạng Markdown)
| Trường thông tin | Giá trị chuẩn hóa |
| :--- | :--- |
| **Họ tên** | Nguyễn Văn A |
| **Số điện thoại** | 0123456789 |
| **Email** | NguyenvanA@gmail.com |
| **Vị trí ứng tuyển** | Backend Developer |
| **Năm kinh nghiệm** | 3 |
| **Kỹ năng chính** | Python, Java, Docker |

```json
{
  "name": "Nguyễn Văn A",
  "phone": "0123456789",
  "email": "NguyenvanA@gmail.com",
  "position": "Backend Developer",
  "experience_years": 3,
  "skills": ["Python", "Java", "Docker"]
}
```

Ví dụ 2:

Input Email thô:
"Gửi bộ phận tuyển dụng, hồ sơ ứng tuyển vị trí Fullstack Developer từ Thị Linh B. Liên hệ qua email Linh@gmail.com. Các kỹ năng chính của tôi gồm SQL, Java và C++."

Output: (Dạng Markdown)
| Trường thông tin | Giá trị chuẩn hóa |
| :--- | :--- |
| Họ tên | Thị Linh B |
| Số điện thoại | null |
| Email | Linh@gmail.com |
| Vị trí ứng tuyển | Fullstack Developer |
| Năm kinh nghiệm | null |
| Kỹ năng chính | SQL, Java, C++ |

```
```JSON
{
  "name": "Thị Linh B",
  "phone": null,
  "email": "Linh@gmail.com",
  "position": "Fullstack Developer",
  "experience_years": null,
  "skills": ["SQL", "Java", "C++"]
}
```

