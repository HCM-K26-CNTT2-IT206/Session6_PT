# Báo cáo: So sánh trade-off các giải pháp ra lệnh cho ứng dụng AI trong học tập và nghiên cứu

## 1. Mục tiêu và phạm vi

Báo cáo so sánh hai cách viết prompt cho một ứng dụng AI hỗ trợ học tập và nghiên cứu, tập trung vào hai chức năng:

1. **Gia sư Feynman:** giúp người học tự diễn giải kiến thức bằng lời của mình, phát hiện chỗ hiểu chưa chắc và học qua câu hỏi gợi mở.
2. **Chấm bài theo rubric:** đánh giá bài làm theo tiêu chí công khai, có dẫn chứng, nêu điểm mạnh và gợi ý cải thiện.

Giải pháp 1 ưu tiên sự ngắn gọn và dễ dùng. Giải pháp 2 bổ sung quy trình, giới hạn và cách xử lý trường hợp thiếu dữ liệu để đầu ra ổn định hơn.

## 2. Bước 1 — Hai prompt mẫu

### Giải pháp 1: Prompt đơn giản

> Bạn là gia sư AI. Hãy giúp tôi học chủ đề **[chủ đề]** bằng phương pháp Feynman: yêu cầu tôi giải thích bằng lời đơn giản, chỉ ra chỗ chưa rõ hoặc sai, rồi đặt câu hỏi gợi mở và giúp tôi diễn đạt lại. Nếu tôi gửi bài làm và rubric, hãy chấm từng tiêu chí theo rubric, nêu lý do ngắn gọn, tổng điểm và một gợi ý cải thiện. Không bịa thông tin; nếu thiếu dữ liệu thì hãy hỏi lại.

**Đặc điểm:** ngắn, dễ nhớ, có thể dùng nhanh cho nhiều môn. Tuy nhiên, “lý do ngắn gọn” và quy trình chấm chưa được định nghĩa cụ thể nên kết quả có thể thay đổi giữa các lần hỏi.

### Giải pháp 2: Prompt chi tiết, có ràng buộc

> **Vai trò:** Bạn là gia sư AI hỗ trợ học tập và nghiên cứu. Mục tiêu là giúp người học hiểu và tự cải thiện, không làm thay toàn bộ bài tập.
>
> **Đầu vào người học cung cấp:**
> - Chủ đề/câu hỏi: **[chủ đề]**
> - Trình độ hoặc lớp học: **[trình độ]**
> - Phần giải thích/bài làm của người học: **[nội dung]**
> - Rubric và thang điểm (nếu cần chấm): **[rubric]**
> - Nguồn/tài liệu được phép dùng (nếu có): **[nguồn]**
>
> **Quy trình Feynman**
> 1. Đọc phần giải thích và xác định tối đa 3 ý người học đã hiểu đúng.
> 2. Nêu tối đa 3 chỗ còn thiếu, mơ hồ hoặc có khả năng sai. Trích cụm từ liên quan từ bài làm; phân biệt rõ lỗi kiến thức với cách diễn đạt chưa rõ.
> 3. Không đoán ý người học và không tự thêm dữ kiện không có căn cứ. Nếu đầu vào quá ít để đánh giá, hỏi tối đa 2 câu làm rõ trước khi kết luận.
> 4. Đặt một câu hỏi gợi mở tại một thời điểm; chờ người học trả lời trước khi đưa lời giải hoàn chỉnh.
> 5. Sau khi người học trả lời, giải thích phần cần sửa bằng ngôn ngữ phù hợp trình độ, đưa một ví dụ ngắn nếu hữu ích, rồi mời người học diễn đạt lại bằng lời của mình.
>
> **Quy trình chấm rubric (chỉ thực hiện khi có rubric và bài làm)**
> 1. Chấm riêng từng tiêu chí theo đúng mức điểm và mô tả trong rubric; không tự thêm tiêu chí hoặc thay đổi trọng số.
> 2. Với mỗi tiêu chí, trình bày: điểm đạt/tối đa, dẫn chứng cụ thể trong bài làm, lý do khớp hoặc chưa khớp rubric.
> 3. Cộng điểm và tính tỷ lệ phần trăm nếu thang điểm cho phép. Kiểm tra phép cộng trước khi trả lời.
> 4. Nếu rubric thiếu thang điểm, tiêu chí mâu thuẫn hoặc không đủ thông tin để chấm, nêu rõ điểm chưa xác định và hỏi lại; không tự đặt quy tắc.
> 5. Kết thúc bằng hai điểm mạnh và tối đa ba hành động cải thiện, sắp theo mức ưu tiên.
>
> **Định dạng đầu ra**
> - Khi chỉ học: “Điểm đã hiểu”, “Điểm cần kiểm tra”, “Câu hỏi tiếp theo”.
> - Khi chấm: bảng gồm “Tiêu chí | Điểm | Dẫn chứng và nhận xét”, sau đó là “Tổng điểm”, “Điểm mạnh”, “Ưu tiên cải thiện”.
> - Giữ giọng điệu tôn trọng, rõ ràng; không khẳng định chắc chắn khi bằng chứng chưa đủ.
> - Bảo vệ quyền riêng tư: không yêu cầu thông tin cá nhân không cần thiết. Nếu người học yêu cầu nguồn học thuật nhưng chưa cung cấp nguồn và không thể xác minh, hãy nói rõ giới hạn thay vì bịa trích dẫn.

**Đặc điểm:** chỉ dẫn cụ thể về thứ tự, bằng chứng, xử lý thiếu dữ liệu và định dạng. Đổi lại, prompt dài hơn, tốn token hơn và có thể làm tương tác kém linh hoạt nếu mọi tác vụ đều phải đi theo khuôn.

## 3. Bước 2 — Bảng so sánh trade-off

| Tiêu chí | Giải pháp 1 (đơn giản) | Giải pháp 2 (chi tiết) |
|---|---|---|
| Độ dễ hiểu | **Cao** — ít chỉ dẫn, dễ đọc và sửa | **Trung bình** — nhiều bước và điều kiện |
| Tốn token | **Ít** | **Nhiều hơn** |
| Tốc độ soạn và bắt đầu dùng | Nhanh | Chậm hơn do cần điền đủ đầu vào |
| Độ nhất quán giữa các lần chạy | Trung bình — cách hiểu “chấm ngắn gọn” có thể khác nhau | Cao hơn — quy trình và định dạng được quy định |
| Chặn lỗi biên | **Trung bình** — có nhắc hỏi lại nhưng chưa mô tả các trường hợp | **Cao** — xử lý thiếu rubric, thiếu dữ liệu, mâu thuẫn và giới hạn bằng chứng |
| Hữu ích cho phản tư Feynman | Khá — có yêu cầu người học diễn giải và nhận phản hồi | Cao — giới hạn số ý, dùng câu hỏi từng bước, yêu cầu người học diễn đạt lại |
| Minh bạch khi chấm | Thấp đến trung bình — yêu cầu lý do nhưng không bắt buộc dẫn chứng | Cao — điểm gắn với tiêu chí và dẫn chứng cụ thể |
| Khả năng tùy biến | Cao — dễ đổi mục tiêu bằng một câu | Trung bình — cần sửa cấu trúc nếu đổi quy trình |
| Rủi ro chính | Phản hồi/chấm điểm không đồng đều, bỏ sót trường hợp thiếu dữ liệu | Prompt dài, có thể cứng nhắc hoặc tạo cảm giác quá nhiều thủ tục |
| Phù hợp nhất | Hỏi nhanh, học thử, nhiệm vụ rủi ro thấp | Chấm bài cần giải trình, học theo quy trình và đầu vào phức tạp |

*Nhận xét:* “Cao” hay “thấp” là đánh giá định tính trong phạm vi bài tập, không phải kết quả đo thực nghiệm. Prompt tốt vẫn cần được thử với nhiều môn học và nhiều dạng bài trước khi triển khai rộng.

## 4. Bước 3 — Lựa chọn và chạy thử

### Lựa chọn

Chọn **Giải pháp 2** cho bài toán này. Yêu cầu bao gồm cả gia sư Feynman lẫn chấm bài tự động, vì vậy tính nhất quán, căn cứ điểm số và khả năng nhận ra dữ liệu thiếu quan trọng hơn việc tiết kiệm một ít token. Giải pháp 2 cũng định hướng AI hỗ trợ người học tự sửa thay vì làm thay.

Đánh đổi cần chấp nhận: prompt dài hơn và trải nghiệm có thể nặng nề nếu áp dụng nguyên vẹn cho mọi câu hỏi ngắn. Trong ứng dụng thực tế, có thể chọn chế độ “gia sư” hoặc “chấm rubric” để chỉ áp dụng phần hướng dẫn tương ứng.

### Prompt được chọn

Dùng **Giải pháp 2** ở trên. Trong lần chạy thử dưới đây, chỉ phần Feynman và phần chấm rubric được kích hoạt vì đầu vào có cả lời giải thích lẫn rubric.

### Dữ liệu chạy thử

- **Chủ đề:** Quang hợp
- **Trình độ:** Lớp 8
- **Giải thích của người học:** “Cây lấy thức ăn từ đất bằng rễ. Lá dùng ánh sáng để biến nước thành oxy. Cây thải oxy ra ngoài.”
- **Rubric (10 điểm):**
  - Nêu đúng nguyên liệu nước và carbon dioxide: 0–3 điểm
  - Nêu vai trò ánh sáng và diệp lục: 0–2 điểm
  - Nêu sản phẩm glucose và oxygen: 0–3 điểm
  - Diễn đạt quan hệ giữa nguyên liệu và sản phẩm rõ ràng: 0–2 điểm

### Kết quả chạy thử

#### Điểm đã hiểu

- Người học nhận ra ánh sáng có liên quan đến hoạt động của lá.
- Người học biết cây tạo và thải oxygen.

#### Điểm cần kiểm tra

- Câu “Cây lấy thức ăn từ đất bằng rễ” chưa chính xác: rễ hút nước và muối khoáng; cây tạo glucose chủ yếu trong lá nhờ quang hợp.
- Bài chưa nhắc đến carbon dioxide đi vào lá.
- Bài chưa nêu glucose là sản phẩm được tạo ra; nước không chỉ đơn giản “biến thành oxy”.

#### Chấm theo rubric

| Tiêu chí | Điểm | Dẫn chứng và nhận xét |
|---|---:|---|
| Nêu đúng nguyên liệu nước và carbon dioxide | 1/3 | Có nhắc “nước”, nhưng gán việc lấy thức ăn cho rễ và chưa nêu carbon dioxide. |
| Nêu vai trò ánh sáng và diệp lục | 1/2 | Có câu “Lá dùng ánh sáng”; chưa nêu diệp lục. |
| Nêu sản phẩm glucose và oxygen | 1/3 | Có nêu oxygen; chưa nêu glucose. |
| Diễn đạt quan hệ giữa nguyên liệu và sản phẩm | 1/2 | Có ý ánh sáng biến đổi nước, nhưng chưa mô tả đủ nguyên liệu và sản phẩm. |
| **Tổng điểm** | **4/10 (40%)** | Tổng các tiêu chí: 1 + 1 + 1 + 1 = 4. |

#### Điểm mạnh

1. Đã liên hệ ánh sáng với hoạt động của lá.
2. Đã nhớ oxygen là một sản phẩm được cây thải ra.

#### Ưu tiên cải thiện

1. Bổ sung carbon dioxide là nguyên liệu cây lấy từ không khí.
2. Phân biệt vai trò của rễ (hút nước và muối khoáng) với lá (nơi quang hợp diễn ra chủ yếu).
3. Bổ sung glucose là sản phẩm cây tạo ra; diệp lục giúp lá hấp thụ năng lượng ánh sáng.

#### Câu hỏi Feynman tiếp theo

**Nếu lá cần nước và carbon dioxide để tạo ra glucose, carbon dioxide đi vào lá từ đâu, và ánh sáng giúp quá trình này như thế nào?** Hãy giải thích bằng lời của em; sau đó mình sẽ phản hồi phần em hiểu đúng và chỗ cần sửa.

### Đánh giá lần chạy thử

Prompt chi tiết tạo được kết quả chấm có thể kiểm tra: mỗi điểm số đi kèm dẫn chứng, tổng điểm được cộng rõ, và phần gia sư kết thúc bằng một câu hỏi để người học tự suy nghĩ. Ví dụ cũng cho thấy giới hạn của chấm tự động: điểm vẫn phụ thuộc vào cách diễn giải rubric và cần giáo viên xem lại khi dùng để quyết định có ảnh hưởng lớn.

## 5. Kết luận

Giải pháp 1 phù hợp với câu hỏi nhanh và tình huống cần prompt ngắn. Giải pháp 2 phù hợp hơn với quy trình học và chấm bài có cấu trúc vì minh bạch, nhất quán và xử lý đầu vào thiếu tốt hơn. Với yêu cầu của bài tập, chọn Giải pháp 2; kết quả thử nghiệm cho thấy prompt vừa phản hồi theo phương pháp Feynman, vừa chấm theo rubric có dẫn chứng và nêu rõ bước học tiếp theo.

