
# Các khái niệm trong Triton

## Triton Inference Server là gì?
Triton Inference Server là một nền tảng phục vụ mô hình máy học (ML) và học sâu (DL) được thiết kế để tối ưu hóa quy trình triển khai và thực thi các mô hình ML/DL. Nó cho phép các nhà phát triển triển khai các mô hình trên nhiều framework khác nhau như TensorFlow, PyTorch, ONNX, và nhiều nền tảng khác, từ đó cải thiện hiệu suất và tính linh hoạt khi xử lý mô hình trong môi trường sản xuất.

## Model Repository là gì?
Model Repository là nơi chứa các mô hình đã được huấn luyện, sẵn sàng để sử dụng với Triton. Mỗi mô hình trong Model Repository được tổ chức theo một cấu trúc nhất định để Triton có thể quản lý và truy vấn mô hình một cách hiệu quả.

### Cấu trúc của Model Repository:
- Mỗi mô hình được đặt trong một thư mục riêng, bên trong chứa các phiên bản khác nhau của mô hình.
- Mỗi phiên bản mô hình có thể có các cấu hình khác nhau để tối ưu hóa cho các tác vụ khác nhau.

Ví dụ:
```
model_repository/
    my_model/
        1/
            model.onnx
        2/
            model.onnx
```

## Backend là gì?
Backend trong Triton là thành phần chịu trách nhiệm chạy các mô hình cụ thể. Mỗi backend hỗ trợ một framework hoặc định dạng mô hình cụ thể, chẳng hạn như TensorFlow, PyTorch, ONNX, hoặc TensorRT.

### Backend phổ biến trong Triton:
- **TensorFlow backend**: Hỗ trợ mô hình TensorFlow (SavedModel, GraphDef).
- **PyTorch backend**: Hỗ trợ mô hình được tạo ra từ PyTorch (TorchScript).
- **ONNX backend**: Hỗ trợ các mô hình sử dụng định dạng ONNX.
- **TensorRT backend**: Dùng để tối ưu hóa và chạy mô hình trên GPU với hiệu suất cao.

## Ensemble Model là gì?
Ensemble Model là một tập hợp của nhiều mô hình hoặc nhiều bước tính toán được kết hợp lại với nhau trong Triton để tạo thành một pipeline inference hoàn chỉnh. Mỗi bước trong Ensemble có thể là một mô hình hoặc một phép tính toán đơn lẻ.

### Ví dụ về Ensemble Model:
Một Ensemble Model có thể bao gồm:
- **Bước 1**: Chạy mô hình tiền xử lý dữ liệu.
- **Bước 2**: Chạy mô hình chính để dự đoán.
- **Bước 3**: Thực hiện mô hình hậu xử lý để tạo ra kết quả cuối cùng.

Ensemble giúp dễ dàng kết hợp nhiều mô hình và xử lý dữ liệu phức tạp mà không cần phải thực hiện riêng lẻ từng bước.

## Inference Request là gì?
Inference Request là quá trình gửi dữ liệu đầu vào tới Triton để mô hình thực hiện dự đoán và trả về kết quả. Mỗi request có thể chứa nhiều thông tin như loại mô hình cần sử dụng, phiên bản mô hình, và dữ liệu cần dự đoán.

## Model Optimization là gì?
Model Optimization là các kỹ thuật tối ưu hóa mô hình nhằm giảm thời gian suy luận và cải thiện hiệu suất tổng thể của mô hình khi chạy trên Triton. Các kỹ thuật tối ưu hóa thường sử dụng bao gồm:
- **Quantization**: Giảm độ chính xác của mô hình để tăng tốc độ suy luận mà vẫn duy trì độ chính xác đủ cao.
- **TensorRT**: Sử dụng nền tảng TensorRT để tối ưu hóa và thực hiện mô hình trên GPU với hiệu suất cao.

## Model Repository Polling là gì?
Model Repository Polling là cơ chế tự động phát hiện và tải lại các mô hình từ Model Repository khi có sự thay đổi. Điều này giúp Triton có thể cập nhật mô hình mà không cần khởi động lại server, tạo điều kiện cho quá trình triển khai và duy trì mô hình dễ dàng hơn.

## Metrics và Logs là gì?
Triton cung cấp các metrics (chỉ số) và logs (nhật ký) để theo dõi hiệu suất của mô hình, thời gian xử lý, và các thông tin khác liên quan đến inference. Các metrics này có thể được xuất ra các hệ thống giám sát như Prometheus hoặc các hệ thống logging khác để phân tích và tối ưu hóa quá trình suy luận.

## Model Control Mode là gì?
Model Control Mode cho phép kiểm soát cách Triton tải và quản lý các mô hình từ Model Repository. Có hai chế độ chính:
- **Explicit Mode**: Mô hình chỉ được tải khi có yêu cầu cụ thể.
- **Poll Mode**: Triton sẽ tự động phát hiện và tải lại các mô hình khi có sự thay đổi trong Model Repository.

## Ray là gì?
Ray là một framework mã nguồn mở được phát triển để giúp các ứng dụng phân tán quy mô lớn, đặc biệt là trong các tác vụ như huấn luyện mô hình, tối ưu hóa, và suy luận. Ray giúp dễ dàng phân phối các nhiệm vụ máy học (ML) và học sâu (DL) trên nhiều máy tính hoặc trên môi trường đám mây với khả năng mở rộng tốt.

Ray có thể được tích hợp với Triton để tối ưu hóa quá trình suy luận cho các mô hình lớn và phức tạp, bằng cách phân tán các yêu cầu suy luận trên nhiều máy chủ hoặc nhiều GPU.

### Các tính năng chính của Ray:
- **Ray Core**: Phần chính của Ray, hỗ trợ chạy các tác vụ phân tán và cung cấp các API đơn giản để quản lý cluster.
- **Ray Tune**: Một thư viện mạnh mẽ trong Ray dùng để hyperparameter tuning cho các mô hình ML và DL, giúp tối ưu hóa quá trình huấn luyện.
- **Ray Serve**: Một nền tảng phục vụ mô hình ML/DL có khả năng mở rộng cao. Ray Serve có thể được tích hợp với Triton Inference Server để quản lý các yêu cầu infer với tốc độ cao và khả năng mở rộng theo nhu cầu.
- **Ray Train**: Giúp hỗ trợ huấn luyện phân tán các mô hình học sâu bằng cách chia nhỏ quá trình huấn luyện trên nhiều GPU hoặc nhiều máy.

### Tích hợp Ray với Triton:
Ray Serve có thể được sử dụng để phân phối các yêu cầu infer tới Triton Inference Server, tối ưu hóa hiệu suất của hệ thống khi số lượng yêu cầu lớn. Ray sẽ giúp điều phối và phân chia các yêu cầu, trong khi Triton sẽ chịu trách nhiệm thực hiện suy luận cho từng mô hình cụ thể.

Ví dụ về quá trình tích hợp:
1. **Ray Serve** sẽ điều phối các yêu cầu suy luận từ người dùng hoặc các ứng dụng khác.
2. **Triton** sẽ thực hiện suy luận cho các mô hình đã được huấn luyện và lưu trữ trong Model Repository.
3. Kết quả của suy luận sẽ được trả về qua Ray Serve.

Tích hợp Ray và Triton giúp xây dựng hệ thống phục vụ mô hình mạnh mẽ, hiệu suất cao và có khả năng mở rộng dễ dàng.
