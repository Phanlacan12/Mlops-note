# Các khái niệm trong feathr

## Observation và source là gì?

Observation data là tập hợp data trung tâm để làm input cho model ML và DL, ngoài ra nó còn để chúng ta kết hợp các feature khác bổ sung. 

Ví dụ trong bài toán recommnedation system, thì Observation data là data mỗi cú click chuột của user, còn các feature bổ sung sẽ là lịch sử giao dịch, giới tính, trình độ học vấn, ... được lấy từ nguồn khác. Nguồn này được gọi là source.

Trong mỗi Observation data, chúng ta sẽ có key để có thể dễ dàng truy vấn với các source khác.

## Anchor là gì?

Khi ta lấy các feature từ nhiều source khác nhau để kết hợp với Observation data, Anchor là một tập hợp các features được liên kết với cùng một Source. 

### Tại sao lại cần anchor?

Ví dụ:

Trong bài toán recsys cho phim, giả sử có 2 source:
- source 1: Dữ liệu Lịch sử Xem Phim của Người Dùng: Bao gồm các thông tin như: ai đã xem phim gì, thời gian xem, và đánh giá cho mỗi bộ phim.
- source 2: Thông Tin Phim: Bao gồm các thông tin như: thể loại phim, năm sản xuất, và đạo diễn.

Trong bài toán này, anchor sẽ đóng vai trò như những ngăn kéo chứa các feature của các source:
- Anchor 1 (ngăn kéo 1): chứa các feature liên quan đến lịch sử xem: Số lượng phim mà người dùng đã xem trong tuần qua, Số lượng phim mà user đã rate trên 4 sao, average duration per film, ...
- Anchor 2 (ngăn kéo 2): chứa các feature liên quan đến thông tin về các bộ phim: Thể loại phim, Điểm trung bình, đạo diễn, ...

Hiểu 1 cách đơn giản thì nó giống ta sắp xếp ngăn nắp vào các ngăn kéo, như vậy thì khi cần feature nào, chúng ta hoàn toàn có thể dễ dàng trong việc truy vấn. Và chúng ta có thể add các feature mới vào các anchor tương ứng mà không cần chạy lại toàn bộ hệ thống.

## Derived Feature là gì?
Derived Feature là một tính năng mới được tạo ra bằng cách sử dụng các tính năng khác đã có sẵn. 
Ví dụ: tính similarity dựa trên user embedding và item embedding

## INPUT_CONTEXT là gì?
INPUT_CONTEXT là các feature được xây dựng dựa trên Observation data chứ không phải từ các source.

## Feature Query là gì?
Feature Query là việc ta lấy các feature từ feature store và kết hợp với Observation Data.

## Materialization là gì?
Materialization là quá trình trích xuất, tính toán, và lưu trữ các feature đã định nghĩa vào một hệ thống lưu trữ để sử dụng sau này 