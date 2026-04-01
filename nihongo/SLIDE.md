


Chào bạn, với tư cách là một Senior AI Engineer từng báo cáo tại các hội nghị lớn, tôi đã thiết kế cho bạn một slide deck (14 slides chính + Appendix) tập trung vào tính logic (narrative), nhấn mạnh sự sáng tạo trong Data Engineering (dùng LLM & Fuzzy Matching) và phân tích sâu về lý do chọn thuật toán. 

Cấu trúc này được tối ưu cho bài thuyết trình 15-20 phút, giúp hội đồng thấy rõ tư duy giải quyết vấn đề của nhóm.

---

# SLIDE DECK: 2023 LAPTOP PRICE ANALYSIS AND PREDICTION

## [Slide 1] Title: Laptop Price Analysis & Prediction
**Purpose:** Mở đầu và giới thiệu bối cảnh dự án.
**Key Points:**
- Dự án: Phân tích và dự đoán giá Laptop (2023).
- Phương pháp: Data Engineering & Machine Learning.
- Nguồn dữ liệu: Amazon, Newegg, B&H.
- Đóng góp cốt lõi: LLM Extraction & Fuzzy Matching.
**Visual Suggestions:** 
- Title lớn, logo trường (HUST), tên Instructor và nhóm. 
- Background: Hình ảnh abstract về data pipeline hoặc e-commerce.
**Speaker Notes:** 
- Chào hội đồng. Hôm nay nhóm chúng tôi xin trình bày dự án Dự đoán giá Laptop. 
- Khác với các bài toán có sẵn dataset sạch, thách thức lớn nhất của chúng tôi là xử lý dữ liệu thô từ các trang thương mại điện tử.
**Transition Sentence:** 
- Để hiểu rõ tại sao bài toán này khó, chúng ta hãy nhìn vào thực trạng dữ liệu hiện nay.

---

## [Slide 2] Title: Problem Definition
**Purpose:** Làm rõ bài toán và khó khăn từ góc độ Business & Data.
**Key Points:**
- **Business:** Định giá laptop phức tạp do nhiều cấu hình.
- **Consumer:** Khó ước tính giá trị thực trên các sàn TMĐT.
- **Data Challenge:** Dữ liệu phân mảnh, phi cấu trúc (unstructured text).
- **Goal:** Xây dựng mô hình Regression từ text thô sang giá (USD).
**Visual Suggestions:** 
- Chia 2 cột: Bên trái là góc nhìn người dùng/người bán, bên phải là góc nhìn Data (icon text lộn xộn -> $ Price).
**Speaker Notes:** 
- Giá laptop không chỉ là phép cộng linh kiện. Nó phụ thuộc vào sự tương tác phi tuyến tính giữa CPU, GPU, RAM. 
- Dữ liệu thu thập được cực kỳ hỗn loạn, không có format chuẩn giữa các sàn. Nhiệm vụ của chúng tôi là biến mớ hỗn độn này thành các con số dự đoán chính xác.
**Transition Sentence:** 
- Để giải quyết bài toán này, nhóm đề xuất một End-to-End Pipeline với 3 đóng góp chính.

---

## [Slide 3] Title: Key Contributions
**Purpose:** Highlight các điểm sáng tạo nhất của dự án (ăn điểm học thuật).
**Key Points:**
- **End-to-End Pipeline:** Scraping, làm sạch, và mô hình hóa.
- **LLM Information Extraction:** Trích xuất thực thể từ text thô (GPT-J-6B).
- **Entity Resolution:** Map tên CPU/GPU sang điểm Passmark (Fuzzy Matching).
- **Baseline Models:** So sánh KNN, Random Forest, MLP.
**Visual Suggestions:** 
- 4 block icon lớn thể hiện 4 contribution. Highlight block "LLM" và "Fuzzy Matching".
**Speaker Notes:** 
- Thay vì dùng Regex truyền thống vốn dễ gãy (brittle), chúng tôi ứng dụng LLM để trích xuất thông tin. 
- Thứ hai, chúng tôi giải quyết bài toán Entity Resolution bằng cách ánh xạ hàng ngàn tên gọi CPU/GPU khác nhau về một điểm chuẩn benchmark duy nhất.
**Transition Sentence:** 
- Quá trình này bắt đầu bằng việc thu thập dữ liệu từ 3 nền tảng lớn.

---

## [Slide 4] Title: The Data Challenge
**Purpose:** Show độ khó của dữ liệu thô để nâng tầm giải pháp.
**Key Points:**
- **Amazon:** Format tốt, nhưng lẫn lộn hàng "refurbished" (nhiễu giá).
- **Newegg:** Hoàn toàn phi cấu trúc, anti-scraping (CAPTCHA).
- **B&H Photo Video:** Dữ liệu bổ sung để cân bằng.
- **Tổng cộng:** Hơn 7,000 records sạch sau xử lý.
**Visual Suggestions:** 
- Ảnh chụp màn hình (screenshot) một đoạn mô tả lộn xộn trên Newegg và một cảnh báo CAPTCHA.
**Speaker Notes:** 
- Thu thập dữ liệu không dễ dàng. Newegg chặn IP liên tục, buộc chúng tôi phải viết script chạy batch qua terminal. 
- Dữ liệu thô thu về là các đoạn text chứa đầy lỗi typo và format bất định, không thể đưa thẳng vào mô hình toán học.
**Transition Sentence:** 
- Đây là bức tranh tổng thể về Pipeline mà chúng tôi thiết kế để xử lý chúng.

---

## [Slide 5] Title: System Architecture Pipeline
**Purpose:** Trình bày dòng chảy dữ liệu (Data Flow).
**Key Points:**
- 1. Web Scraping (Raw Text).
- 2. LLM Extraction (JSON format).
- 3. Entity Resolution (Passmark mapping).
- 4. Cleaning & Scaling (Outliers, Imputation).
- 5. Predictive Modeling (KNN, RF, MLP).
**Visual Suggestions:** 
- Flowchart nằm ngang. Các mũi tên nối tiếp nhau. Highlight các bước số 2 và 3 bằng màu khác biệt.
**Speaker Notes:** 
- Pipeline của chúng tôi gồm 5 bước. Dữ liệu thô đi qua LLM để lấy cấu trúc, sau đó đi qua module Fuzzy Matching để chuẩn hóa. 
- Cuối cùng, dữ liệu được làm sạch và đưa vào train model. Hãy đi sâu vào bước đột phá nhất: LLM Extraction.
**Transition Sentence:** 
- Đối mặt với các đoạn text mô tả dài dòng, RegEx hoàn toàn vô dụng.

---

## [Slide 6] Title: Unstructured Data Parsing via LLM
**Purpose:** Giải thích cách dùng LLM để trích xuất thông tin (Information Extraction).
**Key Points:**
- **Vấn đề:** Format text đa dạng (VD: "16GB DDR5" vs "RAM 16G").
- **Giải pháp:** Few-Shot Prompting với GPT-6B API.
- **Input:** Đoạn mô tả sản phẩm thô.
- **Output:** Lược đồ JSON (Brand, CPU, GPU, RAM...).
- **Độ chính xác:** ~90% trên tập test thủ công.
**Visual Suggestions:** 
- Minh họa "Before - After": Một text box chứa text lộn xộn chỉ mũi tên sang một text box chứa định dạng JSON sạch sẽ.
**Speaker Notes:** 
- Chúng tôi thiết kế các prompt mẫu (Few-shot) để hướng dẫn GPT-6B bóc tách các thông số phần cứng. 
- Cách tiếp cận này giúp hệ thống linh hoạt với mọi kiểu viết tắt hoặc typo của người bán.
**Transition Sentence:** 
- Tuy nhiên, lấy được tên CPU ra vẫn chưa đủ để đưa vào model toán học.

---

##[Slide 7] Title: Entity Resolution (Fuzzy Matching)
**Purpose:** Trình bày cách mapping text thành continuous variable.
**Key Points:**
- **Vấn đề:** 1 CPU có hàng chục cách viết ("i7 13700h" vs "13700H").
- **Giải pháp:** Thư viện `fuzzywuzzy` (Levenshtein Distance).
- **Thuật toán:** Trung bình 4 chỉ số (Simple, Partial, Token Sort/Set).
- **Mapping:** Chọn điểm Passmark (`CPU_Mark`, `GPU_Mark`) cao nhất.
**Visual Suggestions:** 
- Biểu đồ minh họa 3 tên gọi khác nhau cùng trỏ về 1 điểm số (Ví dụ: 31,500 điểm Passmark).
**Equations (optional):** 
- $Levenshtein(a,b) = \text{min edit distance}$ (chèn nhỏ ở góc).
**Speaker Notes:** 
- Các thuật toán Regression cần số liệu, không cần text. Chúng tôi dùng khoảng cách Levenshtein để so khớp tên CPU vừa trích xuất với Database chuẩn của Passmark. 
- Qua đó, một cái tên dài dòng được biến thành một con số sức mạnh phần cứng duy nhất.
**Transition Sentence:** 
- Sau khi có các feature dạng số, bước tiếp theo là chuẩn hóa ma trận dữ liệu.

---

## [Slide 8] Title: Data Cleaning & Transformation
**Purpose:** Trình bày các kỹ thuật Data Engineering nền tảng.
**Key Points:**
- **Outliers:** Loại bỏ bằng Interquartile Range (IQR).
- **Missing Values:** Median Imputation cho đa số features.
- **Encoding:** One-Hot Encoding (OHE) cho Brand, OS.
- **Scaling:** StandardScaler ($\mu=0, \sigma=1$) cho khoảng cách KNN.
**Visual Suggestions:** 
- Hình minh họa Boxplot trước và sau khi cắt Outlier.
- Bảng ngắn minh họa biến đổi OHE (0 và 1).
**Speaker Notes:** 
- Dữ liệu cào về có những laptop bị gắn nhầm giá 20 USD. Chúng tôi dùng IQR để cắt bỏ hoàn toàn các nhiễu này. 
- Đồng thời, StandardScaler là bắt buộc để các thông số như Passmark (hàng chục ngàn) không áp đảo các thông số như RAM (chỉ 16) khi tính khoảng cách.
**Transition Sentence:** 
- Với bộ dữ liệu đã sạch sẽ, chúng tôi tiến hành phân tích khám phá (EDA).

---

## [Slide 9] Title: Exploratory Data Analysis (EDA)
**Purpose:** Chứng minh giả thuyết bằng thống kê học.
**Key Points:**
- **Correlation:** Giá (Price) tương quan mạnh với GPU (0.63) & CPU (0.61).
- **Price Distribution:** Tập trung phân khúc tầm trung ($500 - $1,000).
- **Brand Segmentation:** MSI thống trị phân khúc high-end/gaming.
- **Market:** HP, Lenovo, Acer tập trung phân khúc giá rẻ.
**Visual Suggestions:** 
- Đặt Heatmap (tương quan CPU/GPU) bên trái.
- Đặt Boxplot theo Brand (Figure 8) bên phải.
**Speaker Notes:** 
- Heatmap xác nhận việc chúng tôi chuyển tên CPU thành điểm Passmark là hoàn toàn đúng đắn, vì nó tương quan rất cao với Giá. 
- Boxplot cho thấy MSI tập trung vào tệp khách hàng cao cấp, trong khi Lenovo và HP dàn trải ở phân khúc phổ thông.
**Transition Sentence:** 
- Dựa trên các insights này, chúng tôi thiết lập 3 kiến trúc học máy.

---

## [Slide 10] Title: Modeling Architecture Setup
**Purpose:** Điểm mặt các model được sử dụng và lý do.
**Key Points:**
- **KNN Regressor:** Dựa trên khoảng cách. K=7, Ball_tree.
- **Random Forest:** Ensemble học phi tuyến. 200 trees, Depth 20.
- **Multi-Layer Perceptron (MLP):** Mạng Neural (3 hidden layers x 128 nodes).
- **Mục tiêu:** So sánh thuật toán tuyến tính, ensemble và deep learning.
**Visual Suggestions:** 
- 3 icon đại diện: Mạng lưới điểm (KNN), Rừng cây (RF), và Mạng nơ-ron (MLP).
**Speaker Notes:** 
- Chúng tôi chọn KNN làm baseline cơ bản. Random Forest đại diện cho nhóm cây quyết định có khả năng chống nhiễu tốt. 
- Cuối cùng là MLP để kiểm tra xem cấu trúc dữ liệu bảng (tabular data) có phù hợp với Deep Learning trong bối cảnh ít dữ liệu hay không.
**Transition Sentence:** 
- Để đánh giá công bằng, chúng tôi chọn các metric có ý nghĩa thực tiễn nhất.

---

##[Slide 11] Title: Evaluation Metrics Selection
**Purpose:** Lập luận tại sao chọn MAPE và R2.
**Key Points:**
- **MSE (Mean Squared Error):** Dùng làm Loss function khi train.
- **MAPE (Mean Abs % Error):** Metric quan trọng nhất cho Business.
- **$R^2$ Score:** Đo lường phần trăm phương sai giải thích được.
- **Lý do:** MAPE độc lập với tỷ lệ giá (scale-independent).
**Visual Suggestions:** 
- Chữ MAPE và $R^2$ được phóng to.
**Equations (optional):** 
- $MAPE = \frac{100\%}{n} \sum \left| \frac{y_i - \hat{y}_i}{y_i} \right|$
**Speaker Notes:** 
- MSE rất tốt để tính đạo hàm, nhưng vô nghĩa khi đọc kết quả. 
- Chúng tôi dùng MAPE vì nó nói cho Business biết mô hình lệch bao nhiêu phần trăm so với giá trị thực. $R^2$ cho biết các features có thực sự quyết định giá hay không.
**Transition Sentence:** 
- Và đây là kết quả đối đầu giữa 3 mô hình.

---

## [Slide 12] Title: Experimental Results
**Purpose:** Show bảng kết quả tổng hợp.
**Key Points:**
- **Random Forest (Winner):** $R^2$ = 0.6439 | MAPE = 21.78%.
- **KNN (Tuned):** $R^2$ ~ 0.6120 | MAPE = 23.66%.
- **MLP (All features):** $R^2$ = 0.5481 | MAPE = 29.71%.
- Kết luận: RF hoạt động tốt nhất trên dữ liệu dạng bảng (Tabular).
**Visual Suggestions:** 
- Bảng 3 cột ngang. Tô đậm hàng của Random Forest.
**Speaker Notes:** 
- Bảng kết quả chỉ ra Random Forest chiến thắng tuyệt đối. Nó giải thích được hơn 64% sự biến thiên của giá và có sai số trung bình khoảng 21%. 
- Mạng Neural (MLP) biểu diễn kém nhất do tập dữ liệu ~7,000 dòng là quá nhỏ để nó hội tụ toàn cục.
**Transition Sentence:** 
- Tại sao Random Forest lại phù hợp nhất cho bài toán này?

---

## [Slide 13] Title: Why Random Forest Won?
**Purpose:** Giải thích tính chuyên môn đằng sau kết quả.
**Key Points:**
- **Non-linear interactions:** Bắt được tương tác phức tạp (CPU mạnh + RAM ít).
- **Robustness:** Kháng nhiễu tốt với các Outlier còn sót lại.
- **No strict scaling:** Không phụ thuộc vào chuẩn hóa như KNN/MLP.
- **Ensemble Power:** Bagging giảm thiểu Overfitting hiệu quả.
**Visual Suggestions:** 
- Biểu đồ minh họa một cây quyết định đơn giản (Decision Tree phân nhánh Giá theo CPU > 15000).
**Speaker Notes:** 
- Random Forest thắng vì giá laptop không tuyến tính. Khách hàng không trả gấp đôi tiền cho một CPU mạnh gấp đôi nếu RAM chỉ có 4GB. 
- Cấu trúc rẽ nhánh của RF bắt được các quy luật "combo" phần cứng này rất tự nhiên.
**Transition Sentence:** 
- Dù đạt kết quả khả quan, dự án vẫn còn những giới hạn cần khắc phục.

---

## [Slide 14] Title: Limitations & Future Work
**Purpose:** Thể hiện tư duy phản biện (Critical Thinking).
**Key Points:**
- **Limitations:** Thiếu feature ẩn (Brand tax, chất liệu, OLED vs IPS).
- **Data Gap:** Imputation cho cột Weight cần gom nhóm (Groupby).
- **Future 1:** Thay LLM API bằng Local NLP (RoBERTa) để giảm cost.
- **Future 2:** Nâng cấp thuật toán sang XGBoost / LightGBM.
**Visual Suggestions:** 
- Chia 2 cột: Limitations (icon dấu X) và Future Work (icon bóng đèn).
**Speaker Notes:** 
- Hạn chế lớn nhất là chúng tôi không có dữ liệu về vật liệu vỏ máy hay độ chuẩn màu màn hình. 
- Trong tương lai, việc thay thế RF bằng XGBoost và chuyển từ GPT-6B sang các mô hình NLP cục bộ nhỏ hơn sẽ tối ưu hóa pipeline này cho môi trường Production.
**Transition Sentence:** 
- Cảm ơn hội đồng đã lắng nghe. Chúng tôi rất sẵn lòng trả lời các câu hỏi.

---
---

# APPENDIX & Q&A PREPARATION (For Speaker Only)

##[Appendix Slide 1] Hyperparameter Tuning Grid
- **KNN:** K=(3,5,7,9), Weights=(Uniform, Distance), Algo=(Ball_tree, KD_tree).
- **Random Forest:** N_estimators=(100, 200, 300), Max_depth=(10, 20, None).
- **MLP:** Hidden_layers=( (128,128,128), (128,64,32,16) ), L2_penalty=(0.001, 0.0001).

## [Appendix Slide 2] The Fuzzy Matching Logic
- **Simple Ratio:** So sánh độ giống nhau chuỗi gốc.
- **Partial Ratio:** Tìm chuỗi con (substring) giống nhau.
- **Token Sort Ratio:** Sắp xếp alphabet các từ rồi so sánh (Bỏ qua thứ tự).
- **Token Set Ratio:** Loại bỏ từ trùng lặp rồi so sánh.
- **Công thức tính điểm:** Tỉ lệ trung bình = $(Simple + Partial + Sort + Set) / 4$.

---

## Q&A PREPARATION (5 Khả năng bị hỏi & Cách trả lời)

**Q1: Tại sao nhóm dùng Linear Interpolation cho cột Weight? Dữ liệu này đâu có tính chuỗi thời gian (Time-series)?**
> *Trả lời:* Cảm ơn thầy/cô. Đây đúng là một hạn chế về mặt lý thuyết toán học mà nhóm đã nhận ra sau quá trình implement. Vì dữ liệu là Cross-sectional, đáng lẽ nhóm nên dùng phương pháp Median Imputation có gom nhóm (Groupby) theo `Brand` và `Monitor Size`. Nhóm ghi nhận đây là Technical Debt cần sửa ở version sau.

**Q2: Tại sao kết quả $R^2$ chỉ đạt khoảng 64% và MAPE tận 21%? Như vậy là cao hay thấp?**
> *Trả lời:* Với bài toán giá cả trên sàn TMĐT mở, giá bị nhiễu rất nhiều bởi chiến lược của người bán thứ 3 (giảm giá tồn kho, bán phá giá), và các "Hidden variables" (tiền thương hiệu Apple, chất liệu vỏ nhôm vs nhựa) mà không có trong spec. Do đó $R^2 \sim 0.65$ là mức baseline rất hợp lý đối với Tabular feature.

**Q3: Tại sao lại chọn Random Forest mà không dùng XGBoost/LightGBM?**
> *Trả lời:* Mục tiêu của scope môn học là nắm vững các thuật toán cốt lõi. Random Forest cung cấp một baseline Ensemble rất vững chắc. Nhóm hiểu rằng XGBoost sử dụng Gradient Boosting sẽ bắt lỗi residuals tốt hơn và thường là State-of-the-Art cho Tabular data, đây là định hướng Future Work số 1 của nhóm.

**Q4: Việc dùng LLM API (GPT-6B) để parse Data có vẻ "overkill" (dùng dao mổ trâu giết gà) và tốn kém?**
> *Trả lời:* Dạ đúng, đối với Real-time inference thì API call gây latency và tốn cost. Tuy nhiên, trong pha Data Engineering (tạo dataset một lần), sự hỗn loạn của văn bản Newegg khiến RegEx tốn quá nhiều giờ để bảo trì. LLM giúp nhóm tiết kiệm hàng tuần manual labeling. Ở môi trường Production, nhóm sẽ train một mô hình Named Entity Recognition (NER) nhẹ như BERT để thay thế.

**Q5: Khi dùng StandardScaler, nhóm có fit trên toàn bộ tập dữ liệu trước khi chia Train/Test không? (Data Leakage)**
> *Trả lời:* Nhóm hiểu rõ rủi ro Data Leakage. Pipeline chuẩn là `fit_transform` trên tập Training Set để tìm $\mu$ và $\sigma$, sau đó chỉ dùng `transform` trên tập Test Set để mô phỏng dữ liệu thực tế (Unseen data).
