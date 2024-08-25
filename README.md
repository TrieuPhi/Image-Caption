Dưới đây là bản dịch tiếng Việt của file Markdown bạn cung cấp:

---

# Image-Caption

# Tạo Mô Tả Ảnh Sử Dụng Học Sâu

[![GitHub license](https://img.shields.io/github/license/Sajid030/image-caption-generator)](https://github.com/Sajid030/image-caption-generator/blob/master/LICENSE.md)
[![Python](https://img.shields.io/badge/-Python-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/-TensorFlow-FF6F00?logo=tensorflow&logoColor=white)](https://www.tensorflow.org/)
![Pandas](https://img.shields.io/badge/-Pandas-150458?logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/-NumPy-013243?logo=numpy&logoColor=white)
![Jupyter](https://img.shields.io/badge/-Jupyter-F37626?logo=jupyter&logoColor=white)
[![Streamlit](https://img.shields.io/badge/-Streamlit-FF4B4B)](https://www.streamlit.io/)

## Mục Lục

- [Image-Caption](#image-caption)
- [Tạo Mô Tả Ảnh Sử Dụng Học Sâu](#tạo-mô-tả-ảnh-sử-dụng-học-sâu)
  - [Mục Lục](#mục-lục)
  - [Demo](#demo)
  - [Tổng Quan](#tổng-quan)
  - [Về Bộ Dữ Liệu](#về-bộ-dữ-liệu)
  - [Cài Đặt](#cài-đặt)
  - [Triển Khai Trên Streamlit](#triển-khai-trên-streamlit)
  - [Cây Thư Mục](#cây-thư-mục)
  - [Báo Lỗi / Yêu Cầu Tính Năng](#báo-lỗi--yêu-cầu-tính-năng)
  - [Hướng Phát Triển Tương Lai](#hướng-phát-triển-tương-lai)

## Demo

- Liên kết: https://imgcaptiongen.streamlit.app/

`Lưu ý:` Nếu liên kết trang web trên không hoạt động, có thể là do quá trình triển khai đã bị dừng hoặc có vấn đề kỹ thuật. Chúng tôi xin lỗi vì bất kỳ sự bất tiện nào.

- Vui lòng xem xét tặng ⭐ cho kho lưu trữ nếu bạn thấy ứng dụng này hữu ích.
- Một bản xem trước nhanh của ứng dụng **Image Caption Generator**:

[![Caption Generator Demo](https://img.youtube.com/vi/7H2HXKssyv0/0.jpg)](https://youtu.be/7H2HXKssyv0)

## Tổng Quan

Kho lưu trữ này chứa mã nguồn cho hệ thống tạo mô tả ảnh sử dụng các kỹ thuật học sâu. Hệ thống sử dụng mô hình VGG16 được tiền huấn luyện để trích xuất đặc trưng và mô hình tạo mô tả được tùy chỉnh, huấn luyện bằng LSTM để tạo ra mô tả. Mô hình được huấn luyện trên bộ dữ liệu Flickr8k sử dụng cơ chế chú ý để cải thiện chất lượng mô tả.

**Lưu ý:** Khi sử dụng mô hình `VGG16` để trích xuất đặc trưng, kết quả rất chính xác, nhưng cần lưu ý về việc sử dụng bộ nhớ. Mô hình VGG16 có thể tiêu thụ một lượng lớn bộ nhớ, có thể gây ra các vấn đề trong môi trường giới hạn tài nguyên. Để giải quyết vấn đề này, bạn có thể xem xét sử dụng mô hình `MobileNetV2` cho việc trích xuất đặc trưng. MobileNetV2 đạt được sự cân bằng giữa hiệu suất và hiệu quả bộ nhớ, khiến nó trở thành lựa chọn phù hợp cho các kịch bản giới hạn tài nguyên. Do đó, trong ứng dụng triển khai của tôi, tôi đã chọn sử dụng `MobileNetV2`.

Các thành phần chính của dự án bao gồm:

- Trích xuất đặc trưng ảnh sử dụng mô hình VGG16 đã được tiền huấn luyện (Nên xem xét sử dụng MobileNetV2 để tiết kiệm bộ nhớ)
- Tiền xử lý và mã hóa mô tả
- Kiến trúc mô hình tạo mô tả tùy chỉnh với cơ chế chú ý
- Huấn luyện và đánh giá mô hình
- Ứng dụng Streamlit để tạo mô tả tương tác

## Về Bộ Dữ Liệu

Bộ dữ liệu [Flickr8k](https://www.kaggle.com/adityajn105/flickr8k) được sử dụng để huấn luyện và đánh giá hệ thống tạo mô tả ảnh. Nó bao gồm 8,091 ảnh, mỗi ảnh có năm mô tả về nội dung của ảnh. Bộ dữ liệu cung cấp một tập hợp đa dạng các ảnh với nhiều mô tả cho mỗi ảnh, làm cho nó phù hợp để huấn luyện các mô hình tạo mô tả.

Tải xuống bộ dữ liệu từ [Kaggle](https://www.kaggle.com/adityajn105/flickr8k) và sắp xếp các tệp như sau:

- flickr8k
  - Images
    - (các tệp ảnh)
  - captions.txt

## Cài Đặt

Dự án này được viết bằng Python 3.10.12. Nếu bạn chưa cài đặt Python, bạn có thể tải xuống từ [trang web chính thức](https://www.python.org/downloads/). Nếu bạn đang sử dụng phiên bản cũ hơn của Python, bạn có thể nâng cấp nó bằng cách sử dụng trình quản lý gói pip, cái mà đã được cài đặt sẵn nếu bạn đang sử dụng Python 2 >=2.7.9 hoặc Python 3 >=3.4 trên hệ thống của bạn.
Để cài đặt các gói và thư viện cần thiết, bạn có thể sử dụng pip và tệp requirements.txt được cung cấp. Đầu tiên, sao chép kho lưu trữ này về máy tính của bạn bằng lệnh sau:
```
git clone https://github.com/TrieuPhi/Image-Caption
```
Sau khi bạn đã sao chép kho lưu trữ, hãy điều hướng đến thư mục dự án và chạy lệnh sau trong terminal hoặc command prompt:
```bash
pip install -r requirements.txt
```
Lệnh này sẽ cài đặt tất cả các gói và thư viện cần thiết để chạy dự án.

## Triển Khai Trên Streamlit

1. Tạo một tài khoản trên Streamlit Sharing.
2. Fork kho lưu trữ này vào tài khoản GitHub của bạn.
3. Đăng nhập vào Streamlit Sharing và tạo một ứng dụng mới.
4. Kết nối tài khoản GitHub của bạn với Streamlit Sharing và chọn kho lưu trữ này.
5. Đặt các biến cấu hình sau trong bảng điều khiển Streamlit Sharing:
```
[server]
headless = true
port = $PORT
enableCORS = false
```
6. Nhấp vào "Deploy app" để triển khai ứng dụng trên Streamlit Sharing.

## Cây Thư Mục

```
|---image-caption-generator
|       data
|       model 
|       streamlit
|       tranning
|       requirements.txt
```

## Báo Lỗi / Yêu Cầu Tính Năng

Nếu bạn gặp bất kỳ lỗi hoặc vấn đề nào với ứng dụng dự đoán trạng thái khoản vay, vui lòng thông báo cho tôi bằng cách mở một vấn đề trên [kho lưu trữ GitHub của tôi](https://github.com/TrieuPhi/Image-Caption/issues). Hãy chắc chắn bao gồm các chi tiết về yêu cầu của bạn và kết quả mong đợi. Phản hồi của bạn rất quý giá trong việc giúp tôi cải thiện ứng dụng cho tất cả người dùng. Cảm ơn sự hỗ trợ của bạn!

## Hướng Phát Triển Tương Lai

1. **Tinh chỉnh**: Thử nghiệm tinh chỉnh kiến trúc mô hình tạo mô tả và các tham số siêu để cải thiện hiệu suất.
2. **Mở rộng bộ dữ liệu**: Tích hợp thêm các bộ dữ liệu để tăng sự đa dạng và phức tạp của mô hình huấn luyện, ví dụ như chúng ta có thể huấn luyện mô hình trên [bộ dữ liệu Flickr30k](https://www.kaggle.com/datasets/hsankesara/flickr-image-dataset).
3. **Beam Search**: Triển khai giải mã beam search để tạo nhiều mô tả và chọn mô tả tốt nhất.
4. **Cải tiến giao diện người dùng**: Cải thiện giao diện người dùng của ứng dụng Streamlit và thêm các tính năng như xem trước hình ảnh và điểm tin cậy của mô tả.
5. **Tạo mô tả đa ngôn ngữ**: Mở rộng mô hình để tạo mô tả bằng nhiều ngôn ngữ bằng cách tích hợp các bộ dữ liệu đa ngôn ngữ.
