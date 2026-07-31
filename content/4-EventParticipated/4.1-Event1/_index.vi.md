---
title: "Event 1"
date: 2026-06-06
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Bài thu hoạch sự kiện “AWS First Cloud Journey - Event 1” (06/06/2026)

### Mục Đích Của Sự Kiện
- Khám phá các phương pháp hiện đại trong bảo mật đám mây và phát hiện xâm nhập mạng
- Tìm hiểu sâu về công nghệ container hóa để tối ưu hóa việc triển khai và quản lý ứng dụng
- Lắng nghe những chia sẻ thực tế về lộ trình phát triển sự nghiệp từ vận hành hệ thống đến Cloud và DevOps
- Nắm bắt kiến trúc kết nối thời gian thực cho ứng dụng đa người chơi trên nền tảng AWS
- Tiếp cận các giải pháp Trí tuệ Nhân tạo tiên tiến, đặc biệt là nâng cấp hệ thống RAG với mô hình đồ thị

### Danh Sách Diễn Giả
- **Le Hoang Gia Dai** - Trình bày về AWS WAF & Machine Learning NIDS.
- **Bao Huynh** - Junior Cloud Native Developer, trình bày về Docker và Container hóa.
- **Tran Trung Vinh** - System Administrator tại Central Retail Group, chia sẻ hành trình nghề nghiệp IT.
- **Nguyen Quoc Bao** - Hướng dẫn kết nối Godot Clients với AWS WebSockets.
- **Viet Phat** - Khám phá kiến trúc GraphRAG với Amazon Bedrock và Neptune.

### Nội Dung Nổi Bật

#### Bảo mật thông minh với AWS WAF và Học máy (NIDS)
- WAF truyền thống hoạt động dựa trên các quy tắc định sẵn (Rule-Based) nên gặp nhiều khó khăn trước các kỹ thuật tấn công zero-day hoặc hành vi bất thường mới.
- Giải pháp NIDS sử dụng Machine Learning (huấn luyện trên tập dữ liệu đa dạng CSE-CIC-IDS2018) giúp hệ thống tự động học hỏi, liên tục thích ứng và phát hiện các mẫu tấn công lạ chưa từng có.
- Kiến trúc tích hợp linh hoạt với nhiều dịch vụ AWS như API Gateway, Lambda, Kinesis Data Firehose và Guard Duty để giám sát và xử lý thời gian thực.

#### Công nghệ Container hóa với Docker
- Khắc phục nhược điểm nặng nề của máy ảo (VMs) vốn yêu cầu cấp phát hệ điều hành riêng, gây tiêu tốn tài nguyên và khởi động chậm chạp.
- Docker container dùng chung hệ điều hành máy chủ, siêu nhẹ, khởi động trong tính bằng mili-giây và loại bỏ hoàn toàn vấn đề xung đột môi trường.
- Cấu trúc từng lớp (layers) của Docker image giúp tối ưu hóa quá trình build thông qua cơ chế tái sử dụng cache khi có thay đổi.

#### Trải nghiệm thực tế hành trình System Administrator & DevOps
- Bước đệm vững chắc từ IT Helpdesk cần sự thấu hiểu quy trình giải quyết vấn đề, sau đó tiến tới xây dựng môi trường lab thực hành Linux và Networking chuyên sâu.
- Sự chuyển dịch sang tư duy Cloud tập trung vào Infrastructure as Code (như Terraform), thiết lập luồng CI/CD và văn hóa DevOps nhằm tự động hóa tối đa các tác vụ lặp lại.
- Kinh nghiệm thực tiễn: Việc triển khai các dự án thực tế và thấu hiểu kịch bản sự cố luôn mang lại lợi thế cao hơn so với việc chỉ sở hữu chứng chỉ lý thuyết.

#### Kiến trúc Multiplayer thời gian thực trên AWS
- WebSocket là giao thức lý tưởng cho các ứng dụng cần giao tiếp hai chiều liên tục, đảm bảo độ tin cậy hơn UDP và khắc phục độ trễ cao của HTTP Polling.
- Giải pháp kết hợp Godot + AWS sử dụng API Gateway để định tuyến bản tin, Lambda để xử lý logic ghép trận (matchmaking) và DynamoDB để lưu trạng thái người chơi.
- Mặc dù mô hình Serverless mang lại độ mở rộng linh hoạt, nhà phát triển cần lưu ý đến các thách thức về giới hạn lưu trữ trạng thái trong bộ nhớ và chi phí khi quét (scan) DynamoDB.

#### Mở rộng giới hạn RAG với GraphRAG
- Truy xuất tăng cường thế hệ (RAG) thông thường bộc lộ giới hạn khi phải theo dõi các mối quan hệ phức tạp xuyên suốt nhiều tài liệu phân tán.
- GraphRAG vượt qua rào cản này bằng cách bổ sung khả năng suy luận đa bước (Multi-hop Reasoning), nhận thức rõ ràng các mối liên kết thông qua cấu trúc của cơ sở dữ liệu đồ thị.
- Hệ thống có thể được triển khai theo hướng Fully Managed (sử dụng Amazon Bedrock Knowledge Bases và Neptune Analytics) hoặc Custom Route (sử dụng LlamaIndex) để tối ưu hóa đường ống dữ liệu.

### Những Gì Học Được

#### Tư Duy Thiết Kế
- **Tư duy vận hành (Operations Mindset)**: Luôn phải có kịch bản giám sát, kịch bản tự động hóa và nguyên tắc tối thượng là không bao giờ thử nghiệm trực tiếp trên môi trường production.
- **Tối ưu hóa kiến trúc theo mục đích**: Cần đánh giá kỹ lưỡng đặc thù của hệ thống để chọn giao thức và dịch vụ phù hợp, ví dụ như chọn WebSocket thay vì HTTP Polling cho tính năng matchmaking thời gian thực.

#### Kiến Trúc Kỹ Thuật
- Nắm vững cách một luồng dữ liệu bất đồng bộ được xử lý từ client qua API Gateway, kích hoạt Lambda và quản lý trạng thái tại DynamoDB.
- Hiểu rõ quy trình từ làm sạch, tiền xử lý, đến cân bằng dữ liệu (để khắc phục class imbalance) nhằm huấn luyện các mô hình Machine Learning phát hiện rủi ro hiệu quả hơn.
- Nắm bắt được phương pháp tổ chức và lưu trữ tri thức dưới dạng đồ thị (Knowledge Graph) để tăng cường độ chính xác khi LLM thực thi các truy vấn ngữ nghĩa phức tạp.

#### Chiến Lược Định Hướng
- Lộ trình phát triển hạ tầng cần hướng tới sự tự động hóa cao thông qua Docker, CI/CD và Infrastructure as Code.
- Sự kết hợp giữa các dịch vụ Cloud-native mang lại khả năng mở rộng vô hạn nhưng cũng đòi hỏi kỹ năng giám sát và chiến lược kiểm soát chi phí (như bài toán quét cơ sở dữ liệu liên tục).

### Ứng Dụng Vào Công Việc
- Tích hợp kỹ thuật GraphRAG (với LlamaIndex) kết hợp cùng vector database để nâng cấp nền tảng News RAG, giúp tăng cường khả năng bóc tách, truy xuất đa chiều và suy luận ngữ nghĩa phức tạp từ nguồn dữ liệu tin tức.
- Ứng dụng trực tiếp Docker để đóng gói toàn bộ các Kafka container và cơ sở dữ liệu (như PostgreSQL), đảm bảo môi trường phát triển hệ thống ETL pipeline và kho dữ liệu (data warehouse) luôn nhất quán trên mọi máy trạm.
- Khảo sát và vận dụng luồng xử lý dữ liệu tự động qua AWS Lambda và Kinesis Data Firehose để tối ưu hóa quy trình thu thập dữ liệu streaming, làm nền tảng vững chắc cho các hệ thống phân tích và bảng điều khiển (dashboard) sau này.

### Trải nghiệm trong event
Tham dự sự kiện "AWS First Cloud Journey" là một trải nghiệm mở mang tầm nhìn về cách các công nghệ đám mây hiện đại đang tái định hình lại toàn bộ quy trình phát triển, vận hành và quản lý dữ liệu phần mềm.

Điểm nhấn ấn tượng nhất đối với tôi trong toàn bộ sự kiện chính là phần trình bày chi tiết về **Docker** của diễn giả Bảo Huỳnh. Cách diễn giả bóc tách sự cồng kềnh, tốn kém tài nguyên của máy ảo truyền thống và đối chiếu với tính linh hoạt của container đã làm sáng tỏ rất nhiều vấn đề thực tế. Trong quá trình xây dựng các kiến trúc hệ thống dữ liệu lớn, việc đồng bộ môi trường phát triển và triển khai luôn là một thách thức lớn. Giải pháp từ Docker, với khả năng khởi động nhanh chóng, tận dụng tối đa sức mạnh phần cứng và cơ chế tái sử dụng image layer thông minh, thực sự là chìa khóa then chốt để chuẩn hóa các luồng công việc phức tạp.

Bên cạnh đó, sự kiện còn mang đến một bức tranh toàn cảnh về việc kết nối các công nghệ chuyên sâu. Từ việc thiết lập hệ thống bảo mật chủ động bằng Machine Learning, xử lý sự kiện thời gian thực thông qua WebSockets, cho đến việc nâng tầm tư duy suy luận cho AI bằng GraphRAG – tất cả đều củng cố thêm tầm quan trọng của việc xây dựng nền móng dữ liệu vững chắc. Những bài học chân thực về sự kiên trì tự học và tư duy phòng ngừa của một DevOps chắc chắn sẽ là kim chỉ nam định hướng cho quá trình phát triển sự nghiệp kỹ thuật trong thời gian tới.

#### Một số hình ảnh khi tham gia sự kiện
![Event](../../../images/4-EventParticipated/event1.png)