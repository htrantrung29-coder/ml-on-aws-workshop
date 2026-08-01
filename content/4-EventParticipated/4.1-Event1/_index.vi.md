---
title: "Event 1: Agentic AI Build Week & Solution Architecture Showcase"
date: 2026-07-31
weight: 1
chapter: false
pre: "<b>4.1 </b>"
---

# Báo cáo sự kiện

## Tổng quan sự kiện

Sự kiện là buổi tổng kết và trình diễn các dự án trong khuôn khổ **Agentic AI Build Week** – một chương trình hackathon kéo dài 1 tuần, nơi các nhóm tham gia xây dựng các giải pháp AI ứng dụng trên nền tảng AWS. Các nhóm đã trình bày sản phẩm của mình, chia sẻ quá trình xây dựng, kiến trúc, chi phí, và bài học kinh nghiệm.

## Mục tiêu sự kiện

- Trình diễn các giải pháp AI thực tế được xây dựng trên AWS trong thời gian ngắn.
- Chia sẻ quy trình thiết kế kiến trúc, tối ưu chi phí và lựa chọn dịch vụ.
- Thúc đẩy tư duy **Solution Architecture** và **AI-native development**.
- Tạo cơ hội học hỏi, trao đổi giữa các thành viên và đội ngũ tổ chức.

## Các dự án tiêu biểu

### 1. Signal Scout – Phát hiện thay đổi chiến lược doanh nghiệp

**Thành viên:** Lê Tấn Lực, Đỗ Hoàng Hiếu, Triệu Quốc Hào, Nguyễn Văn Duy Khiêm, Nguyễn Công Minh, Nguyễn Trần Minh Quân

**Vấn đề giải quyết:** Các đội ngũ chiến lược doanh nghiệp thường khó phát hiện sớm các thay đổi từ đối thủ cạnh tranh hoặc thị trường.

**Giải pháp:** Signal Scout là nền tảng kết nối các tín hiệu rời rạc từ dữ liệu doanh nghiệp và thị trường, xây dựng câu chuyện rõ ràng, hỗ trợ ra quyết định chiến lược (Maintain, Adapt, Accelerate).

**Kiến trúc:** Sử dụng AWS cho xử lý dữ liệu và AI, LangFuse để giám sát, Apify cho thu thập dữ liệu, TinyFish cho phân tích.

**Điểm nhấn:** Tập trung vào tính **minh bạch** và **khả năng kiểm chứng** – mọi kết luận đều được hỗ trợ bằng bằng chứng.

---

### 2. Solution Architect Professional Native App

**Thành viên:** Phạm Tiến Thuận Phát, Huỳnh Hoàng Long, Lê Minh Nghĩa, Trần Đại Vĩ, Nguyễn An

**Vấn đề giải quyết:** Kiến trúc sư giải pháp thường mất nhiều thời gian để đọc yêu cầu, phác thảo kiến trúc, vẽ diagram và ước tính chi phí.

**Giải pháp:** Ứng dụng AI native giúp tự động:
- Phân tích yêu cầu từ ngôn ngữ tự nhiên
- Phác thảo kiến trúc hybrid-cloud
- Tạo sơ đồ Draw.io với AWS Architecture Icons chính thức
- Ước tính chi phí AWS cho region ap-southeast-1
- Đưa ra khuyến nghị, giả định và xác định lỗ hổng yêu cầu
- Tinh chỉnh qua chat sidebar với custom instructions

**Tác động:** Giảm thời gian từ đọc BRD/PRD → kiến trúc sơ bộ từ nhiều giờ xuống còn vài phút, loại bỏ công việc thủ công lặp lại.

---

### 3. 3KA – Hackathon Journey

**Thành viên:** Huỳnh An Khương, Nguyễn Quốc Huy, Ngô Quang Khôi, Hoàng Lê Thành Đức, Đặng Nguyễn Phước Lộc, Đặng Trường Hưng

**Câu chuyện:** Bài thuyết trình kể lại hành trình cảm xúc của nhóm trong hackathon – từ **DOUBT** (nghi ngờ), qua **FLOW** (dòng chảy sáng tạo), đến **PRIDE** (tự hào về thành quả).

**Điểm nhấn:** Nhấn mạnh tinh thần đồng đội, sự kiên trì và khả năng thích ứng khi làm việc với công nghệ mới trong thời gian giới hạn.

---

### 4. OneTeam – AI-Powered Conversation Ordering

**Thành viên:** Anh Duy, Trần Đông, Đoàn Trung, Minh Việt, Anshul Roy

**Bối cảnh (The Trigger):**
- Khách hàng ngày càng mong đợi trải nghiệm đặt hàng nhanh chóng, tiện lợi và cá nhân hóa.
- Các hệ thống đặt hàng truyền thống thường yêu cầu nhiều thao tác thủ công, gây mất thời gian và giảm trải nghiệm người dùng.

**Vấn đề (The Problem):**
- Quy trình đặt hàng hiện tại phức tạp, yêu cầu người dùng điền nhiều thông tin.
- Thiếu khả năng hiểu ngôn ngữ tự nhiên, khiến người dùng phải tuân theo cấu trúc cứng nhắc.
- Không có khả năng gợi ý hoặc tùy chỉnh dựa trên ngữ cảnh hội thoại.

**Giải pháp (The Product):**
- **OneTeam** là giải pháp đặt hàng qua hội thoại được hỗ trợ bởi AI, cho phép người dùng tương tác bằng ngôn ngữ tự nhiên.
- Ứng dụng hiểu và xử lý các yêu cầu phức tạp từ người dùng, như thay đổi đơn hàng, thêm món, hoặc hỏi về khuyến mãi.
- Tích hợp với các hệ thống backend hiện có để xử lý đơn hàng, thanh toán và xác nhận.
- Sử dụng AI để gợi ý món ăn dựa trên sở thích và lịch sử đặt hàng.

**Kiến trúc:**
- Sử dụng **Amazon Lex** hoặc các dịch vụ AI tương tự để xử lý ngôn ngữ tự nhiên.
- **AWS Lambda** cho xử lý logic nghiệp vụ.
- **Amazon API Gateway** làm lớp API.
- Database cho lưu trữ đơn hàng và thông tin người dùng.

**Điểm nhấn:**
- Trải nghiệm người dùng mượt mà, giống như trò chuyện với nhân viên bán hàng thực tế.
- Tự động hóa quy trình đặt hàng, giảm thiểu lỗi thủ công.
- Khả năng mở rộng và tùy chỉnh cao.

---

## Điểm nổi bật

| Dự án | Công nghệ chính | Giá trị cốt lõi |
|-------|----------------|----------------|
| Signal Scout | AWS, LangFuse, Apify, AI/ML | Phát hiện sớm, ra quyết định dựa trên bằng chứng |
| SA Professional Native App | AWS, AI, Draw.io integration | Tự động hóa kiến trúc, tiết kiệm thời gian |
| 3KA | AWS, Full-stack development | Tinh thần hackathon, teamwork |
| OneTeam | AWS, Amazon Lex, Lambda, API Gateway | AI-powered conversational ordering, trải nghiệm người dùng |

---

## Bài học rút ra

### 1. Tư duy Solution Architecture
- Luôn bắt đầu từ **business domain**, không phải công nghệ.
- Mỗi kiến trúc cần đi kèm với **ước tính chi phí** và **giả định** rõ ràng.
- **AI-native apps** đang thay đổi cách kiến trúc sư làm việc.

### 2. Tối ưu chi phí là một phần của kiến trúc
- Các nhóm đều trình bày phần **Cost Analysis**, chứng tỏ chi phí là yếu tố không thể bỏ qua.
- Lựa chọn dịch vụ phù hợp (serverless vs container vs VM) ảnh hưởng lớn đến chi phí vận hành.

### 3. Hành trình quan trọng như kết quả
- Bài học từ nhóm 3KA: sự **kiên trì** và **tinh thần đồng đội** là chìa khóa vượt qua khó khăn.
- **DOUBT → FLOW → PRIDE** là một hành trình cảm xúc rất thực tế trong các dự án công nghệ.

### 4. Ứng dụng AI vào công việc hàng ngày
- Các công cụ AI có thể hỗ trợ đắc lực từ **phân tích yêu cầu** → **thiết kế** → **triển khai** → **bảo trì**.
- **Amazon Q Developer** và các AI tương tự đang trở thành trợ thủ đắc lực cho kỹ sư và kiến trúc sư.

### 5. AI trong trải nghiệm khách hàng
- Dự án OneTeam cho thấy AI có thể cách mạng hóa cách khách hàng tương tác với doanh nghiệp.
- **Conversational AI** không chỉ là xu hướng mà đang trở thành kỳ vọng của người dùng.
- Tích hợp AI vào sản phẩm giúp tăng trải nghiệm và hiệu quả vận hành.

---

## Áp dụng vào công việc

- ✅ Sử dụng tư duy **domain-driven** khi thiết kế kiến trúc cho dự án ML on AWS.
- ✅ Tích hợp **cost estimation** vào quy trình thiết kế.
- ✅ Khám phá **Amazon Q Developer** để tăng tốc độ phát triển.
- ✅ Đúc kết và chia sẻ hành trình học tập để truyền cảm hứng cho đồng đội.
- ✅ Nghiên cứu ứng dụng **conversational AI** trong các sản phẩm tương lai.

---

## Hình ảnh sự kiện

![Event Photo 1](/images/event1.png)
![Event Photo 2](/images/event2.png)

---

## Cảm nhận cá nhân

Sự kiện này là cơ hội quý giá để nhìn thấy **cách các dự án AI thực tế được xây dựng và vận hành trên AWS**. Tôi đặc biệt ấn tượng với:

- Cách **Signal Scout** kết nối các tín hiệu rời rạc thành câu chuyện chiến lược – một ứng dụng thực tế của AI vào kinh doanh.
- Ứng dụng **SA Professional Native App** cho thấy AI có thể thay đổi hoàn toàn workflow của một kiến trúc sư giải pháp.
- Hành trình cảm xúc của nhóm **3KA** nhắc nhở tôi về giá trị của sự bền bỉ và tinh thần đồng đội.
- Dự án **OneTeam** cho thấy tiềm năng to lớn của AI trong việc cải thiện trải nghiệm khách hàng – một hướng đi mà tôi muốn khám phá thêm.

Tôi nhận ra rằng việc xây dựng một hệ thống không chỉ là kỹ thuật, mà còn là **kể một câu chuyện** – từ vấn đề của khách hàng, đến giải pháp, đến giá trị mang lại. Đây là bài học quan trọng cho hành trình phát triển của tôi.
