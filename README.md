## Link GitHub
## Thông tin nhóm
- Phạm Trương Hải Đoàn - MSSV: 20520046
- Mai Phạm Quốc Hưng - MSSV: 20521366

## Sản phẩm
- Mô hình OutfitTransformer để giái quyết bài toán Outfit Compatibility Prediction (Dự đoán độ đồng bộ của trang phục).
- Link GitHub: https://github.com/Doan-Pham/outfit_recommendation
- Bài báo tham khảo: [OutfitTransformer: Outfit Representations for Fashion Recommendation](https://arxiv.org/abs/2204.04812) của nhóm tác giả Rohan Sarkar, Navaneeth Bodla, Mariya I. Vasileva, Yen-Liang Lin, Anurag Beniwal, Alan Lu và Gerard Medioni

## Hướng dẫn cài đặt
1. Clone repo này về với [Git](https://git-scm.com)
```bash
git clone https://github.com/Doan-Pham/outfit_recommendation.git
```
2. Tải file [data.zip (2.3GB)](https://drive.google.com/file/d/1696cpHFamwTH9ViyUYlPHCvL0X52Ww16/view?usp=sharing) về cùng thư mục với repo vừa clone và giải nén
3. Cài đặt miniconda3 (Một trình quản lý package và virtual environment cho Python) từ [trang chủ của miniconda3](https://docs.conda.io/projects/miniconda/en/latest/)
4. Sau khi cài đặt, mở Anaconda Prompt (miniconda3)
![Untitled](https://github.com/Doan-Pham/outfit_recommendation/assets/85011400/c0d78c1b-19a8-44bd-ba78-327e13379994)

5. Chạy lệnh sau để tạo Anaconda virtual environment cùng với các package cần thiết.
```bash
conda create -n outfit_recommendation --file requirements.txt
```

## Hướng dẫn chạy source
1. Mở Anaconda Prompt và di chuyển đến thư mục chứa source,
```bash
cd path/to/your/repo/outfit_recommendation
```
2. Kích hoạt môi trường đã tạo ở bước cài đặt
```bash
conda activate outfit_recommendation
```
Lúc này khi môi trường được kích hoạt, chương trình đã có đủ các package cần thiết để chạy

3. Chạy lệnh sau để tiến hành train model. Sau khi train, các tham số của model sẽ được lưu trong thư mục `checkpoint/disjoint`, trong đó các file với định dạng `checkpoint_0.pt`, `checkpoint_1.pt` lưu kết quả train của từng vòng lặp, còn file `best_state.pt` lưu kết quả train với chỉ số chính xác cao nhất. 
```bash
python main.py
```
Có thể nhập lệnh sau để biết các argument có thể sử dụng với lệnh `python main.py` ở trên
```bash
python main.py --help
```
Kết quả khi chạy lệnh `python main.py --help`
```bash
usage: main.py [-h] [--datazip DATAZIP] [--log_level LOG_LEVEL] [--datadir DATADIR]
               [--polyvore_split POLYVORE_SPLIT] [--epochs EPOCHS]

options:
  -h, --help            show this help message and exit
  --datazip DATAZIP     Path to input data zip file
  --log_level LOG_LEVEL
                        0 = Print >= warnings, 1 = print >= info, 2 = print all
  --datadir DATADIR     Path to data directory
  --checkpoint_dir CHECKPOINT_DIR
                        Path to the directory to save checkpoints
  --batch_size BATCH_SIZE
                        Batch size in training, default is 50
  --polyvore_split POLYVORE_SPLIT
                        sThe split of the polyvore data (either disjoint or nondisjoint)  
  --epochs EPOCHS       Number of epochs to train for (default: 10)
```
Ví dụ sử dụng lệnh `python main.py` để huấn luyện model trong 15 epoch với số lượng mẫu mỗi đợt huấn luyện là 30, đồng thời lấy dữ liệu từ file data.zip thay vì lấy từ thư mục đã được giải nén.
```bash
python main.py --epochs 15 --batch_size 30 --datazip data.zip
```
4. Khi đã train xong model với ít nhất 1 vòng lặp, có thể chạy lệnh sau để mở app demo. App này sẽ sử dụng tham số trong file `best_state.pt` để áp dụng cho model và đưa ra dự đoán
```bash
streamlit run demo_app.py
```
