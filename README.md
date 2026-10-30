# HCM-KS26-CNTT1_NhapMonCNTT_Session15_BTVN9
# BÀI 9: TỰ THIẾT KẾ HỆ THỐNG LƯU TRỮ VÀ PHÂN QUYỀN CHO DỰ ÁN CAMPUSPAY

**Họ và tên:** Phạm Thành Đạo  
**Lớp:** HCM-KS26-CNTT1  
**Môn học:** Nhập môn Công nghệ thông tin  
**Chủ đề:** Thiết kế hệ thống lưu trữ và phân quyền Google Drive  
**Dự án:** CampusPay

---

# PHẦN 1: PHÂN TÍCH BÀI TOÁN (I/O)

## 1.1. Xác định đầu vào (Input)

Đầu vào của hệ thống bao gồm các nhóm dữ liệu và đối tượng sử dụng sau:

**A. Các cấp độ tài liệu cần quản lý**

- Tài liệu kỹ thuật: Mã nguồn, tài liệu API, API Keys và thông tin kết nối hệ thống.
- Tài liệu thiết kế: UI/UX, hình ảnh, biểu tượng và tài sản đồ họa.
- Tài liệu kinh doanh: Business Plan, chiến lược kinh doanh và thông tin đối tác.
- Tài liệu thuyết trình: Slide Pitch và Business Summary.
- Tài liệu nhạy cảm: API Keys, thông tin khách hàng và dữ liệu nội bộ.

**B. Các vai trò người dùng**

- Ban Kỹ thuật: 3 thành viên, phụ trách viết code, kiểm thử API và quản lý mã nguồn.
- Ban Thiết kế: 2 thành viên, phụ trách thiết kế giao diện và tài sản đồ họa.
- Ban Kinh doanh: 2 thành viên, phụ trách Business Plan và liên hệ đối tác.
- Nhà đầu tư: 1 người bên ngoài, chỉ cần xem Business Plan và Slide Pitch.

## 1.2. Xác định đầu ra (Output)

Hệ thống cần tạo ra các kết quả:

- Một cấu trúc thư mục Google Drive gồm 2 cấp: cấp dự án và cấp ban nhóm.
- Một bảng phân quyền hoàn chỉnh cho 4 vai trò và 5 loại tài liệu.
- Quy định truy cập theo nguyên tắc Least Privilege.
- Cơ chế bảo vệ tài liệu nhạy cảm bằng Restricted.
- Cơ chế quản lý lịch sử phiên bản tối thiểu 30 ngày.
- Cơ chế giới hạn thời gian truy cập của nhà đầu tư trong 14 ngày.
- Quy trình thu hồi quyền truy cập khi thành viên nghỉ việc.

## 1.3. Đề xuất giải pháp

Em đề xuất sử dụng Google Drive làm nền tảng lưu trữ tập trung cho dự án CampusPay.

Hệ thống được thiết kế theo mô hình phân cấp 2 cấp:

- Cấp 1: Thư mục dự án CampusPay.
- Cấp 2: Các thư mục riêng theo từng ban và thư mục cộng tác chung.

Nguyên tắc thiết kế:

1. Mỗi ban có thư mục riêng để lưu trữ tài liệu chuyên môn.
2. Chỉ cấp quyền cho những thành viên thực sự cần truy cập.
3. Tài liệu cần chia sẻ chéo được đặt trong thư mục Shared Workspace.
4. Tài liệu nhạy cảm phải sử dụng Restricted.
5. Không cấp quyền Editor cho người chỉ cần xem hoặc góp ý.
6. Nhà đầu tư chỉ được truy cập các tài liệu được phê duyệt và quyền truy cập hết hạn sau 14 ngày.

---

# PHẦN 2: THIẾT KẾ CẤU TRÚC THƯ MỤC GOOGLE DRIVE

## 2.1. Cấu trúc thư mục đề xuất

```text
CAMPUSPAY/
│
├── 01_TECHNICAL/
│   ├── Source_Code/
│   ├── API_Documentation/
│   ├── Testing/
│   └── Technical_Reports/
│
├── 02_DESIGN/
│   ├── UI_UX/
│   ├── Graphic_Assets/
│   ├── Prototypes/
│   └── Design_Guidelines/
│
├── 03_BUSINESS/
│   ├── Business_Plan/
│   ├── Partner_Information/
│   ├── Market_Research/
│   └── Financial_Information/
│
├── 04_SHARED_WORKSPACE/
│   ├── Business_Summary/
│   ├── Slide_Pitch/
│   └── Meeting_Notes/
│
└── 05_CONFIDENTIAL/
    ├── API_Keys/
    ├── Customer_Data/
    └── Internal_Credentials/
```

## 2.2. Chức năng từng thư mục

| Thư mục | Nội dung lưu trữ | Đối tượng sử dụng |
|---|---|---|
| 01_TECHNICAL | Code, API, kiểm thử và báo cáo kỹ thuật | Ban Kỹ thuật |
| 02_DESIGN | UI/UX, hình ảnh, prototype và tài sản đồ họa | Ban Thiết kế |
| 03_BUSINESS | Business Plan, nghiên cứu thị trường và thông tin đối tác | Ban Kinh doanh |
| 04_SHARED_WORKSPACE | Business Summary, Slide Pitch và biên bản họp | Các ban được chỉ định |
| 05_CONFIDENTIAL | API Keys, thông tin khách hàng và thông tin đăng nhập | Người được ủy quyền đặc biệt |

**Lưu ý về bảo mật:** Thư mục `05_CONFIDENTIAL` không được chia sẻ mặc định cho toàn bộ thành viên. Chỉ những người có trách nhiệm trực tiếp với dữ liệu mới được cấp quyền.

Đối với mã nguồn, nhóm nên sử dụng GitHub Repository riêng để quản lý phiên bản code. Google Drive chủ yếu lưu tài liệu kỹ thuật, tài liệu hướng dẫn và các dữ liệu cộng tác cần thiết.

---

# PHẦN 3: CÁC BƯỚC THIẾT LẬP HỆ THỐNG

## 3.1. Bước 1 – Tạo thư mục dự án

- Đăng nhập tài khoản Google Drive quản lý dự án.
- Chọn New → New folder.
- Tạo thư mục chính tên `CAMPUSPAY`.
- Tạo 5 thư mục cấp 2 theo cấu trúc đã thiết kế.
- Đặt tên rõ ràng, thống nhất và tránh sử dụng tên thư mục gây nhầm lẫn.

## 3.2. Bước 2 – Sắp xếp tài liệu

- Đưa mã nguồn và tài liệu API vào `01_TECHNICAL`.
- Đưa tài sản đồ họa và thiết kế UI/UX vào `02_DESIGN`.
- Đưa Business Plan và tài liệu đối tác vào `03_BUSINESS`.
- Đưa tài liệu cần cộng tác vào `04_SHARED_WORKSPACE`.
- Đưa dữ liệu nhạy cảm vào `05_CONFIDENTIAL`.

## 3.3. Bước 3 – Cấp quyền truy cập

- Xác định email của từng thành viên.
- Chia thành các nhóm theo vai trò: Ban Kỹ thuật, Ban Thiết kế, Ban Kinh doanh.
- Cấp quyền phù hợp cho từng thư mục hoặc tài liệu.
- Sử dụng Viewer khi chỉ cần xem.
- Sử dụng Commenter khi cần góp ý.
- Chỉ sử dụng Editor khi cần trực tiếp chỉnh sửa.

Đối với nhà đầu tư:

- Chỉ chia sẻ Business Plan và Slide Pitch.
- Đặt quyền Viewer.
- Đặt phạm vi chia sẻ Restricted.
- Thiết lập Expiration Date là 14 ngày nếu tài khoản và loại tài nguyên hỗ trợ tính năng này.

## 3.4. Bước 4 – Kiểm tra quyền truy cập

Sau khi thiết lập, trưởng nhóm cần kiểm tra:

- Ban Kỹ thuật có truy cập được tài liệu kỹ thuật hay không.
- Ban Thiết kế có chỉnh sửa được tài liệu thiết kế hay không.
- Ban Kinh doanh có quản lý được Business Plan hay không.
- Nhà đầu tư có xem được đúng hai tài liệu được phép hay không.
- Không có người ngoài truy cập được dữ liệu nhạy cảm.
- Không có liên kết Anyone with the link đối với tài liệu mật.

Nên kiểm tra bằng cách sử dụng tài khoản thử nghiệm thuộc từng vai trò để xác nhận quyền thực tế.

## 3.5. Bước 5 – Quản lý phiên bản và thu hồi quyền

**Quản lý phiên bản:**

- Lưu tài liệu quan trọng trên Google Drive.
- Sử dụng Version History để theo dõi thay đổi.
- Đặt tên phiên bản rõ ràng, ví dụ: `Business_Plan_v1`, `Business_Plan_v2`.
- Kiểm tra khả năng khôi phục phiên bản cũ.
- Với file quan trọng, tạo thêm bản sao lưu độc lập.

Google Docs, Sheets và Slides có lịch sử phiên bản riêng. Với các file tải lên như PDF hoặc tài liệu Office, cần kiểm tra lịch sử phiên bản và chính sách lưu giữ của Drive; không nên mặc định mọi loại file đều có cùng thời gian lưu lịch sử.

**Thu hồi quyền:**

- Kiểm tra danh sách thành viên đang có quyền truy cập.
- Xóa quyền của người không còn tham gia dự án.
- Kiểm tra quyền được kế thừa từ thư mục cha hoặc nhóm.
- Kiểm tra các liên kết chia sẻ bên ngoài.
- Chuyển quyền sở hữu tài liệu cần thiết trước khi xóa hoặc vô hiệu hóa tài khoản.

---

# PHẦN 4: BẢNG PHÂN QUYỀN HOÀN CHỈNH

## 4.1. Nguyên tắc phân quyền

Hệ thống sử dụng ba cấp quyền chính:

- **Viewer:** Chỉ được xem tài liệu.
- **Commenter:** Được xem và thêm nhận xét, không được chỉnh sửa nội dung chính.
- **Editor:** Được xem và chỉnh sửa nội dung tài liệu.

Ngoài ra, phạm vi chia sẻ được đặt là **Restricted** để chỉ những tài khoản được chỉ định mới có thể truy cập.

## 4.2. Bảng phân quyền 4 vai trò × 5 loại tài liệu

| Loại tài liệu | Ban KT | Ban TK | Ban KD | Nhà đầu tư | Ghi chú bảo mật |
|---|---|---|---|---|---|
| Mã nguồn và tài liệu API | Editor | Không truy cập | Không truy cập | Không truy cập | Restricted; không chứa API Key thật. |
| Tài liệu thiết kế UI/UX | Viewer | Editor | Không truy cập | Không truy cập | Chỉ thành viên thiết kế được chỉnh sửa. |
| Business Plan | Viewer | Không truy cập | Editor | Viewer | Tài liệu mật; Restricted. |
| Slide Pitch | Viewer | Commenter | Editor | Viewer | Nhà đầu tư chỉ nhận bản PDF để tải về. |
| Business Summary | Viewer | Commenter | Editor | Viewer | Chia sẻ chéo có kiểm soát. |

**Giải thích bảng phân quyền:**

**1. Mã nguồn và tài liệu API**

- Ban Kỹ thuật được Editor để phát triển và kiểm thử.
- Các ban khác không cần truy cập mã nguồn.
- Không đưa API Keys hoặc mật khẩu vào tài liệu chia sẻ.

**2. Tài liệu thiết kế UI/UX**

- Ban Thiết kế được Editor để trực tiếp tạo và chỉnh sửa giao diện.
- Ban Kỹ thuật được Viewer để tham khảo thiết kế khi triển khai.
- Ban Kinh doanh và nhà đầu tư không cần truy cập tài liệu thiết kế nội bộ.

**3. Business Plan**

- Ban Kinh doanh được Editor để quản lý và cập nhật kế hoạch.
- Ban Kỹ thuật được Viewer để hiểu mục tiêu kinh doanh và định hướng sản phẩm.
- Nhà đầu tư được Viewer để xem kế hoạch.
- Ban Thiết kế không được cấp quyền vì không cần sử dụng tài liệu này trong phạm vi công việc.

**4. Slide Pitch**

- Ban Kinh doanh được Editor để quản lý nội dung thuyết trình.
- Ban Thiết kế được Commenter để góp ý về bố cục, màu sắc và hình ảnh.
- Ban Kỹ thuật được Viewer để hiểu nội dung sản phẩm.
- Nhà đầu tư được Viewer đối với bản PDF đã xuất.

**5. Business Summary**

- Ban Kinh doanh được Editor để cập nhật thông tin.
- Ban Kỹ thuật được Viewer để nắm bắt mục tiêu và yêu cầu nghiệp vụ.
- Ban Thiết kế được Commenter để góp ý cách trình bày.
- Nhà đầu tư được Viewer để theo dõi tổng quan dự án.

**Lưu ý:** Quyền truy cập phải được cấp trực tiếp theo từng tài liệu hoặc nhóm phù hợp. Không nên cấp quyền Editor cho toàn bộ thư mục dự án chỉ để giải quyết nhu cầu cộng tác của một vài thành viên.

---

# PHẦN 5: GIẢI QUYẾT 3 BẪY DỮ LIỆU

## 5.1. Bẫy 1 – Ban Kinh doanh chia sẻ Business Plan cho Ban Kỹ thuật

**Tình huống:**

Ban Kinh doanh muốn Ban Kỹ thuật đọc Business Plan để hiểu bối cảnh kinh doanh và định hướng phát triển CampusPay. Tuy nhiên, Ban Kinh doanh không muốn Ban Kỹ thuật chỉnh sửa nội dung.

**Quyền phù hợp: Viewer.**

**Giải thích:**

- Viewer cho phép Ban Kỹ thuật đọc và tham khảo nội dung Business Plan.
- Không thể chỉnh sửa trực tiếp tài liệu.
- Giúp bảo vệ nội dung do Ban Kinh doanh chịu trách nhiệm.
- Đảm bảo nguyên tắc Least Privilege vì Ban Kỹ thuật chỉ cần xem, không cần chỉnh sửa.

**Cách thiết lập:**

1. Mở file Business Plan trên Google Drive.
2. Chọn Share.
3. Nhập email các thành viên Ban Kỹ thuật.
4. Chọn quyền Viewer.
5. Đặt General Access là Restricted.
6. Kiểm tra lại danh sách người có quyền truy cập.

**Kết luận:** Không cần cấp Commenter hoặc Editor vì nhu cầu chỉ là đọc và hiểu thông tin. Viewer là quyền phù hợp nhất.

## 5.2. Bẫy 2 – Nhà đầu tư muốn tải Slide Pitch về máy để thuyết trình offline

**Tình huống:**

Nhà đầu tư muốn tải Slide Pitch về máy tính để sử dụng khi không có Internet. Trưởng nhóm không muốn nhà đầu tư chỉnh sửa bản trình chiếu gốc.

**Quyền phù hợp: Viewer đối với file PDF đã xuất.**

**Giải thích:**

- Ban Kinh doanh giữ quyền Editor đối với bản trình chiếu gốc.
- Xuất Slide Pitch thành file PDF.
- Chia sẻ bản PDF cho nhà đầu tư với quyền Viewer.
- Nhà đầu tư có thể tải bản PDF để sử dụng offline nếu tính năng tải xuống được cho phép.
- Nhà đầu tư không có quyền chỉnh sửa bản trình chiếu gốc.

**Có cần tắt tính năng "Viewers can download" không?**

**Không nên tắt nếu nhà đầu tư cần tải PDF về máy.**

Nếu tắt quyền tải xuống, nhà đầu tư có thể không tải được tài liệu để thuyết trình offline.

Cách xử lý phù hợp:

1. Giữ bản Google Slides gốc trong khu vực nội bộ.
2. Xuất một bản PDF riêng.
3. Chia sẻ PDF với quyền Viewer.
4. Cho phép tải xuống đối với file PDF.
5. Đặt phạm vi chia sẻ Restricted.
6. Thiết lập thời hạn truy cập 14 ngày.

**Kết luận:** Viewer không đồng nghĩa với việc không thể tải tài liệu. Việc tải PDF không cấp quyền chỉnh sửa bản Google Slides gốc. Tuy nhiên, PDF vẫn có thể bị sao chép hoặc chỉnh sửa bằng công cụ bên ngoài, nên không nên xem đây là biện pháp chống sao chép tuyệt đối.

## 5.3. Bẫy 3 – Một thành viên nghỉ việc

**Tình huống:**

Một thành viên trong nhóm nghỉ việc và trưởng nhóm cần đảm bảo người đó không còn truy cập bất kỳ tài liệu nào của CampusPay.

**Thao tác cần thực hiện: Thu hồi toàn bộ quyền truy cập của thành viên.**

**Các bước thực hiện:**

**Bước 1: Xác định tài khoản**

- Xác định email Google của thành viên nghỉ việc.
- Kiểm tra các thư mục và tài liệu người đó đang được cấp quyền.

**Bước 2: Xóa quyền truy cập**

- Truy cập Google Drive.
- Kiểm tra danh sách người được chia sẻ trong các thư mục và file.
- Xóa email của thành viên khỏi danh sách chia sẻ.
- Xóa thành viên khỏi các nhóm Google có quyền truy cập dự án.

**Bước 3: Kiểm tra quyền kế thừa**

- Kiểm tra quyền được kế thừa từ thư mục cha.
- Kiểm tra quyền truy cập thông qua Shared Drive nếu dự án sử dụng.
- Kiểm tra các liên kết chia sẻ và quyền truy cập trực tiếp.
- Đảm bảo thành viên không còn quyền truy cập thông qua nhóm khác.

**Bước 4: Xử lý tài khoản doanh nghiệp**

Nếu sử dụng tài khoản Google Workspace do doanh nghiệp quản lý, quản trị viên cần vô hiệu hóa hoặc đình chỉ tài khoản khi phù hợp, thu hồi các phiên đăng nhập và xử lý quyền truy cập liên quan.

**Bước 5: Bàn giao dữ liệu**

- Chuyển quyền sở hữu tài liệu cần thiết cho người phụ trách mới.
- Kiểm tra các file do thành viên nghỉ việc tạo ra.
- Đảm bảo công việc không bị gián đoạn.
- Kiểm tra lại quyền truy cập sau khi thu hồi.

**Kết luận:** Chỉ xóa email khỏi một thư mục là chưa đủ. Cần rà soát cả quyền trực tiếp, quyền kế thừa và quyền thông qua nhóm để đảm bảo thành viên không còn truy cập được tài liệu dự án.

---

# PHẦN 6: KIỂM SOÁT VÀ DUY TRÌ AN TOÀN DỮ LIỆU

## 6.1. Quản lý lịch sử phiên bản

Đối với tài liệu quan trọng như Business Plan, Slide Pitch và tài liệu kỹ thuật, nhóm cần:

- Lưu trữ trên Google Drive.
- Bật và sử dụng lịch sử phiên bản của các ứng dụng Google Workspace.
- Kiểm tra lịch sử chỉnh sửa định kỳ.
- Đặt tên phiên bản rõ ràng.
- Lưu bản sao lưu độc lập cho tài liệu quan trọng.

Mục tiêu là duy trì khả năng truy xuất và khôi phục phiên bản trong tối thiểu 30 ngày theo yêu cầu của dự án.

## 6.2. Quản lý thời hạn truy cập của nhà đầu tư

- Chỉ chia sẻ Business Plan và Slide Pitch.
- Cấp quyền Viewer.
- Thiết lập Expiration Date là 14 ngày.
- Không cấp quyền truy cập vào thư mục gốc CAMPUSPAY.
- Kiểm tra quyền sau khi hết thời hạn.

**Lưu ý:** Tính năng đặt ngày hết hạn phụ thuộc loại tài khoản, quyền quản trị và loại tài nguyên Google Drive. Nếu không hỗ trợ đặt thời hạn trực tiếp cho tài nguyên, quản trị viên cần lập lịch thu hồi quyền thủ công hoặc sử dụng giải pháp quản trị được tổ chức hỗ trợ.

## 6.3. Nguyên tắc bảo mật chung

1. Không sử dụng Anyone with the link cho dữ liệu nhạy cảm.
2. Không chia sẻ API Keys và thông tin khách hàng cho người không có trách nhiệm.
3. Không cấp Editor khi người dùng chỉ cần xem hoặc góp ý.
4. Không chia sẻ thư mục gốc cho nhà đầu tư.
5. Kiểm tra quyền truy cập định kỳ.
6. Thu hồi quyền ngay khi thành viên nghỉ việc hoặc đối tác kết thúc hợp tác.
7. Sao lưu dữ liệu và kiểm tra khả năng khôi phục.

---

# PHẦN 7: KẾT LUẬN

Qua bài tập thiết kế hệ thống lưu trữ và phân quyền cho dự án CampusPay, em đã xây dựng được một mô hình quản lý dữ liệu tập trung trên Google Drive với cấu trúc thư mục rõ ràng và quyền truy cập phù hợp cho từng nhóm thành viên.

Các kiến thức được áp dụng:

- **Cloud Storage:** Tổ chức và lưu trữ tài liệu trên Google Drive.
- **Least Privilege:** Chỉ cấp quyền cần thiết theo vai trò.
- **Permissions:** Phân biệt Viewer, Commenter và Editor.
- **Restricted Sharing:** Giới hạn người có thể truy cập tài liệu.
- **Version History:** Theo dõi và khôi phục phiên bản tài liệu.
- **Expiration Date:** Giới hạn thời gian truy cập của nhà đầu tư.
- **Access Revocation:** Thu hồi quyền khi thành viên nghỉ việc.

**Kết luận chung:** Một hệ thống lưu trữ doanh nghiệp hiệu quả không chỉ cần sắp xếp tài liệu khoa học mà còn phải kiểm soát chặt chẽ quyền truy cập, bảo vệ dữ liệu nhạy cảm và có khả năng thu hồi quyền kịp thời. Việc áp dụng nguyên tắc Least Privilege giúp CampusPay giảm nguy cơ rò rỉ thông tin, tăng hiệu quả cộng tác và đảm bảo an toàn dữ liệu trong suốt quá trình phát triển dự án.
