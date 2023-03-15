# OpenHuman.ai
OpenHuman.ai
## 1. Abstract
Bài báo đề cập đến thách thức của việc tạo ra các cử chỉ nói chuyện trong đa phương tiện, thật hơn và giống con người dựa trên dữ liệu đa phương tiện do thiếu sẵn các tập dữ liệu, mô hình và tiêu chuẩn đánh giá chuẩn. 

Để giải quyết vấn đề này, các tác giả đã xây dựng tập dữ liệu BEAT (Body-Expression-Audio-Text), bao gồm dữ liệu đa phương tiện chất lượng cao được thu thập từ 30 người nói nói chuyện với tám cảm xúc khác nhau và bốn ngôn ngữ khác nhau, cùng với 32 triệu chú thích về cảm xúc và tính ngữ nghĩa ở mức khung hình.

Phân tích thống kê trên BEAT cho thấy sự tương quan của các cử chỉ nói chuyện với biểu cảm khuôn mặt, cảm xúc và ngữ nghĩa. Các tác giả đề xuất một mô hình cơ sở gọi là Mạng chuyển động liên tiếp (CaMN) cho tổng hợp cử chỉ và giới thiệu một chỉ số gọi là SRGR để đánh giá tính liên quan ngữ nghĩa.

Các thí nghiệm định lượng và định tính cho thấy tính hợp lệ của chỉ số, chất lượng dữ liệu thực tế và hiệu suất đạt trạng thái tiên tiến của mô hình cơ sở.

BEAT được coi là tập dữ liệu chuyển động lớn nhất để nghiên cứu về cử chỉ con người, có thể đóng góp cho nhiều lĩnh vực nghiên cứu khác nhau, bao gồm tổng hợp cử chỉ có thể điều khiển, phân tích đa dạng ngôn ngữ và nhận dạng cử chỉ cảm xúc. Dữ liệu, mã và mô hình có sẵn trên https://pantomatrix.github.io/BEAT/.
## 1. Introduction
Những thách thức trong việc tạo ra các cử chỉ nói chuyện sống động và giống con người dựa trên âm thanh hoặc văn bản bao gồm:

* Quality and scale of the dataset: Chất lượng và quy mô hạn chế của tập dữ liệu, dẫn đến khả năng tổng quát hóa và độ ổn định thấp.
* Rich and paired multi-modal data: Thiếu dữ liệu đa dạng kết hợp nhiều phương tiện, dẫn đến việc thiếu phân tích về các phương tiện khác như biểu cảm khuôn mặt.
* Speaker style disentanglement: Thiếu nghiên cứu về phong cách của từng người nói do thiếu dữ liệu.
* Emotion annotation: Thiếu dữ liệu về cảm xúc, khiến các phương pháp hiện có không đủ để phủ hết các cảm xúc trong cuộc sống hàng ngày.
* Semantic relevance: Thiếu dữ liệu về ngữ nghĩa, làm cho việc tạo ra các cử chỉ có ý nghĩa liên quan đến bối cảnh trở nên khó khăn.
Có hai phương pháp chính để có dữ liệu học là:

* Chuyển từ video để trích xuất Gesture Dataset
* Sử dụng Motion capture để tạo bộ Gesture Dataset
Tập dữ liệu mang teen BEAT

Bao gồm các :

* Chú thích về ngữ nghĩa (Text - anotation)
* Tám cảm xúc khác nhau từ 30 người nói
    - Thân thể 
    - Biểu cảm
    - Âm thanh
    - Văn bản
* Tổng cộng 30 triệu khung hình (frame)
* Môi trường chuyển động được kiểm soát chặt chẽ để đảm bảo chất lượng và đa dạng
* Với 76 giờ và hơn 2500 chuỗi (sentence) được phân đoạn theo chủ đề.
* Tập dữ liệu bao gồm những người nói với trình độ tiếng nói khác nhau
* Cung cấp dữ liệu bằng ba ngôn ngữ khác nhau ở độ dài và định dạng khác nhau.
* Tỷ lệ nam/nữ, phạm vi âm vị và đa dạng ngôn ngữ được thiết kế cẩn thận để bao phủ các đặc điểm ngôn ngữ tự nhiên.
* Những người hướng dẫn chuyên nghiệp cung cấp phản hồi về biểu cảm của người nói trong quá trình thu thập để đảm bảo tính diễn đạt và chất lượng của toàn bộ tập dữ liệu. 

Sau khi phân tích thống kê trên BEAT, chúng ta quan sát được sự tương quan của các `cử chỉ nói chuyện` với `biểu cảm khuôn mặt (facial expressions)`, `cảm xúc emotions,` và `ngữ nghĩa (semantics,)`, ngoài sự tương quan đã biết với `âm thanh`, `văn bản` và `danh tính người nói (speaker identity)`.
Semantic-Relevant Gesture Recall (SRGR): đánh trọng số cho xác suất các điểm chính xác dựa trên điểm số ngữ nghĩa của dữ liệu thực tế

## 2. Related work
**Conversational Gestures Dataset**

Trong bài báo này, các tác giả xem xét các tập dữ liệu cử chỉ trong cuộc trò chuyện bằng mo-cap và pseudo-label. 
**Semantic or Emotion-Aware Motion Synthesis**
**Conditional Conversational Gestures Synthesis**

Đoạn văn miêu tả sự tiến bộ đã đạt được trong việc tổng hợp các cử chỉ trò chuyện có điều kiện. Các mô hình cơ sở đã được tạo ra bằng cách sử dụng các tập dữ liệu và kỹ thuật mô hình hóa khác nhau như CNN và LSTM. Hiệu suất của các mô hình này đã được cải thiện bằng cách lựa chọn đầu vào / đầu ra, đào tạo đối nghịch và các kỹ thuật mô hình tạo sinh. StyleGestures là một ví dụ về mô hình sử dụng mô hình dựa trên luồng và tín hiệu điều khiển bổ sung để lấy mẫu cử chỉ từ phân phối. Tuy nhiên, do thiếu dữ liệu đa phương tiện ghép đôi, phân tích các modalities khác, chẳng hạn như biểu hiện khuôn mặt, cho việc tổng hợp các cử chỉ vẫn còn thiếu.
## 3. BEAT: Body-Expression-Audio-Text Dataset
### 3.1 Data Acquisition
![image.png](attachment:image.png)

Hệ thống thu thập và phân bố chủ thể trong BEAT.

(a) Hệ thống chụp chuyển động 16 camera được sử dụng để ghi lại dữ liệu trong các phiên Conversation và (Self-Talk) Tự nói chuyện.

(b) Các cử chỉ được chia thành bốn danh mục trong phiên Conversation.

(c) Bảy danh mục cảm xúc bổ sung được thiết lập với tỷ lệ bằng nhau trong phiên Self-Talk

(d) Tập dữ liệu của chúng tôi bao gồm bốn ngôn ngữ chính gồm tiếng Anh

(e) do 30 người nói từ mười quốc gia khác nhau với thời lượng ghi âm khác nhau.
**Motion Capture System**

Hệ thống motion capture được thể hiện trong Hình 2a, dựa trên 16 camera được đồng bộ hóa ghi lại chuyển động với tốc độ 120 Hz.

Chúng tôi sử dụng bộ marker của hãng Vicon với 77 điểm đánh dấu (xem tài liệu bổ sung để biết vị trí của các điểm đánh dấu trên cơ thể).

Hệ thống capture khuôn mặt sử dụng ARKit với một camera độ sâu trên iPhone 12 Pro, trích xuất 52 trọng số blendshape ở tốc độ 60 Hz.

Các mục tiêu blendshape được thiết kế dựa trên Facial Action Coding System (FACS) và được sử dụng rộng rãi bởi người dùng mới trong ngành công nghiệp.

Âm thanh được ghi lại ở tần số 48KHz stereo.
**Design Criteria**

* Conversation: 10-min sequences
* Self-talk: 1-min sequences


* Speaker’s Gestures:
    * Talking
    * Instantaneous reactions to questions, 
    * The state of thinking (silence)
    * Asking

* Topic: 20 predefined topics
    * 33% debate
    * 67% description topics


* Emotion: 
    * neutral, anger, happiness, fear, disgust, sadness, contempt and surprise
**Speaker Selection and Language Ratio**

Việc lựa chọn người nói và tỉ lệ các ngôn ngữ để đảm bảo tính tổng quá hóa của dữ liệu. 

Language Ratio: 

* Engish 60h (81%)
    * 34h of 10 native English speakers including the US, UK, and Australia, and 26h of 20 fluent English speakers from other countries
    

* Chinese 12h
* 2h of Spanish and Japanese
**Recording**

Trong các phần tự nói, người nói được yêu cầu đọc câu trả lời một cách thành thạo. Tuy nhiên, họ không được hướng dẫn thực hiện một phong cách cử chỉ cụ thể mà được khuyến khích để thể hiện phong cách giao tiếp tự nhiên, cá nhân hàng ngày. Người nói sẽ xem các video kích thích cảm xúc trong 2-10 phút tương ứng với các cảm xúc khác nhau trước khi nói với cảm xúc cụ thể. Một người nói chuyên nghiệp sẽ hướng dẫn họ kích hoạt cảm xúc tương ứng một cách chính xác. Chúng tôi sẽ ghi lại lại bất kỳ dữ liệu không đủ điều kiện để đảm bảo tính chính xác và chất lượng của dữ liệu.
#### 3.2 Data Annotation
**Text Alignment**

Chúng tôi sử dụng một bộ nhận dạng giọng nói tự động (ASR) được xây dựng trong nhà để có được văn bản ban đầu cho phiên trò chuyện và sửa đổi bởi các nhà chú giải. Sau đó, chúng tôi áp dụng bộ căn chỉnh thời gian Montreal Forced Aligner (MFA) [38] để căn chỉnh thời gian văn bản với âm thanh.
**Emotion and Semantic Relevance**

Đối với phần cảm xúc và sự liên quan ngữ nghĩa, nhãn 8 lớp cảm xúc của phần tự nói được xác nhận và được giám sát trên hiện trường để đảm bảo tính chính xác. Đối với phần hội thoại, nhà chú giải sẽ xem video với âm thanh và cử chỉ tương ứng để thực hiện chú thích cấp khung thời gian. Đối với sự liên quan ngữ nghĩa, chúng tôi thu thập điểm số trên một thang điểm từ 0-10 từ 600 người chú thích được giao trên Amazon Mechanical Turk (AMT). Chúng tôi đã trả tiền khoảng 10 đô la cho mỗi người chú thích cho mỗi giờ làm việc trong nhiệm vụ này.
![image.png](attachment:image.png)

(a) Biểu đồ T-SNE cho các cử chỉ trong tám danh mục cảm xúc. Các cử chỉ với các cảm xúc khác nhau được phân thành các nhóm khác nhau, ví dụ, niềm vui (màu xanh) và giận dữ (màu cam).

(b) Các ví dụ về các cử chỉ của niềm vui (phía trên) và giận dữ (phía dưới) từ người nói thứ hai.

#### 3.3 Data Analysis
Việc thu thập và chú thích dữ liệu BEAT đã cho phép phân tích mối tương quan giữa các cử chỉ hội thoại và các modal khác. Trong khi mối liên hệ giữa cử chỉ và âm thanh, văn bản và danh tính người nói đã được nghiên cứu rộng rãi. Chúng tôi tiếp tục thảo luận về mối tương quan giữa cử chỉ, biểu cảm khuôn mặt, cảm xúc và ngữ nghĩa.
Facial expressions và cảm xúc có mối quan hệ mạnh mẽ với nhau (ngoại trừ một số chuyển động môi), và ta đầu tiên phân tích mối tương quan giữa các cử chỉ nói chuyện và các danh mục cảm xúc ở đây. Như được thể hiện trong hình 3a, chúng tôi đã minh họa các cử chỉ trong T-SNE dựa trên biểu diễn quay 2s, và kết quả cho thấy rằng các cử chỉ có các đặc điểm khác nhau trong các cảm xúc khác nhau. Ví dụ, như được thể hiện trong hình 3b, speaker-2 có các phong cách cử chỉ khác nhau khi tức giận và vui mừng, ví dụ, các cử chỉ lớn hơn và nhanh hơn khi tức giận. Kết quả T-SNE cũng khác biệt đáng kể giữa vui mừng (màu xanh) và tức giận (màu vàng). Tuy nhiên, các cử chỉ cho các cảm xúc khác nhau vẫn chưa thể hoàn toàn phân biệt được bởi biểu diễn quay. Hơn nữa, các cử chỉ của các cảm xúc khác nhau xuất hiện dễ bị lẫn lộn trong mỗi khu vực, điều này cũng phù hợp với nhận thức chủ quan.
**Distribution of Semantic Relevance**

Phân bố của liên quan ngữ nghĩa. Điều đó được biểu diễn trong hình 4, nơi tần suất, vị trí và nội dung của các cử chỉ có liên quan ngữ nghĩa thay đổi giữa các người nói khi cùng một nội dung văn bản được phát âm. Để hiểu rõ hơn về phân bố của sự liên quan ngữ nghĩa của các cử chỉ, chúng tôi đã tiến hành một nghiên cứu liên quan ngữ nghĩa dựa trên dữ liệu của hai người nói trong vòng 4 giờ. Như được thể hiện trong Hình 4b, đối với toàn bộ dữ liệu, 83% các cử chỉ có điểm ngữ nghĩa thấp (≤ 0,2). Đối với mức từ, phân bố ngữ nghĩa thay đổi giữa các từ, ví dụ như i và was có chia sẻ một điểm ngữ nghĩa tương tự nhau nhưng khác nhau trong phân bố điểm số. Ngoài ra, Hình 4c cho thấy điểm số ngữ nghĩa trung bình của chín từ phổ biến trong bộ văn bản. Cần nhắc lại rằng điểm số của động từ to be thể hiện khá thấp so với Đại từ và Giới từ được hiển thị bằng màu xanh và màu vàng, tương ứng. Cuối cùng, nó trình bày một phân phối xác suất khác nhau cho các cử chỉ liên quan ngữ nghĩa.
![image.png](attachment:image.png)

(a) Các ID người nói khác nhau trong cùng một phần khác nhau về mức độ liên quan ngữ nghĩa và phong cách cử chỉ khác nhau.

(b) Phân bố ngữ nghĩa tổng thể của BEAT.

(c) Liên quan ngữ nghĩa của các từ tần số cao được nhóm theo từ vựng khác nhau.

(d, e) Sự phân bố khác nhau của liên quan ngữ nghĩa xảy ra ở từ "i" và "was" ngay cả khi chúng chia sẻ gần như cùng mức độ liên quan ngữ nghĩa.
## 4. Multi-Modal Conditioned Gestures Synthesis Baseline
Cascaded Motion Network (CaMN)
Ở phần này, tác giả đề xuất một mô hình cơ sở để tạo ra các cử chỉ hội thoại sống động giống con người. Mô hình cơ sở này được gọi là Cascaded Motion Network (CaMN) và được trình bày trong hình 5. Nó mã hóa văn bản, điều kiện cảm xúc, định danh người nói, âm thanh và trọng số khuôn mặt blendshape để tổng hợp các cử chỉ cơ thể và tay trong một cấu trúc liên tiếp đa giai đoạn. Ngoài ra, tính liên quan ngữ nghĩa được áp dụng như một trọng số mất mát để khiến mạng tạo ra các cử chỉ liên quan đến ý nghĩa hơn. Các bộ mã hóa mạng văn bản, âm thanh và định danh người nói được tham khảserviceso từ [53] và được tùy chỉnh để đạt hiệu suất tốt hơn. Tất cả dữ liệu đầu vào có cùng độ phân giải thời gian như các cử chỉ được tổng hợp để mô hình cơ sở này có thể xử lý các cử chỉ được tổng hợp frame bởi frame thông qua một mô hình tuần tự. Trọng số khuôn mặt blendshape và cử chỉ được giảm mẫu xuống còn 15 FPS, và các từ của câu được chèn vào bằng các ký hiệu đệm để tương ứng với thời gian im lặng trong âm thanh.
#### Text Encoder

Trước hết, từ được chuyển đổi thành tập nhúng từ $\mathbf{v}^{\mathrm{T}} \in \mathbb{R}^{300}$ bằng mô hình được huấn luyện trước trong FastText [10] để giảm số chiều. Sau đó, các tập từ được điều chỉnh tinh chỉnh bởi bộ mã hóa tùy chỉnh ${E}_{T}$, đó là một mạng tích chập thời gian (TCN) [6] 8 tầng với skip connections [23], như sau:

$$z_i^{\mathrm{T}}=E_{\mathrm{T}}\left(v_{i-f}^{\mathrm{T}}, \ldots, v_{i+f}^{\mathrm{T}}\right)$$

Đối với mỗi khung $i$, TCN kết hợp thông tin từ $2f = 34$ khung để tạo ra đặc trưng tiềm ẩn cuối cùng của văn bản, tập các đặc trưng này được ghi chú là $\mathbf{z}^{\mathrm{T}} ∈ \mathbb{R}^{128} $
![image.png](attachment:image.png)

Để tạo động tác đàm thoại đa dạng, CaMN là một mô hình cơ bản cho việc tổng hợp đa phương tiện đầu vào bao gồm text, emotion label, speaker ID, audio and facial blendweight. Kiến trúc của CaMN có cấu trúc liên tiếp, nghĩa là các tính năng âm thanh và khuôn mặt sẽ được trích xuất bằng cách nối các tính năng của các phương tiện trước đó. Các tính năng kết hợp sẽ được tái tạo để tạo ra động tác thân và tay bằng hai bộ giải mã LSTM + MLP được xếp chồng lên nhau.
#### Speaker ID and Emotion Encoders

Biểu diễn ban đầu của danh tính người nói và cảm xúc đều là vector one-hot, tương ứng với $\mathbf{v}^{\text{ID}}$ thuộc $\mathbb{R}^{30}$ và $\mathbf{v}^{E}$ thuộc $\mathbb{R}^8$. Theo đề xuất trong [53], chúng tôi sử dụng lớp nhúng làm bộ mã hóa danh tính người nói, $E_{ID}$. Vì danh tính người nói không thay đổi ngay lập tức, chúng tôi chỉ sử dụng danh tính người nói của khung hiện tại để tính toán các đặc trưng tiềm ẩn của nó. Trong khi đó, chúng tôi sử dụng sự kết hợp giữa lớp nhúng và TCN 4 lớp làm bộ mã hóa cảm xúc, $E_{E}$, để trích xuất các biến thể cảm xúc theo thời gian.


$$z_i^{\mathrm{ID}}=E_{\mathrm{ID}}\left(v_i^{\mathrm{ID}}\right), z_i^{\mathrm{E}}=E_{\mathrm{E}}\left(v_{i-f}^{\mathrm{E}}, \ldots, v_{i+f}^{\mathrm{E}}\right)$$


Ở đây, $\mathbf{z}^{\text{ID}} ∈ \mathbb{R}^8$ và $\mathbf{z}^{\text{E}} ∈ \mathbb{R}^8$ là các đặc trưng tiềm ẩn cho speaker ID và emotion.
#### Audio Encoder

Chúng tôi áp dụng biểu diễn sóng âm thanh gốc và giảm tốc độ mẫu xuống 16KHZ, xem xét âm thanh là 15FPS, cho mỗi khung hình, chúng tôi có $\mathbf{v}^{\text{A}} ∈ \mathbb{R}^{1067}$. Chúng tôi đưa đầu vào âm thanh kết hợp với các tính năng về văn bản, speakerID và cảm xúc vào bộ mã hóa âm thanh $E_{\text{A}}$ để học các đặc trưng âm thanh tốt hơn. Như sau:

$$z_i^{\mathrm{A}}=E_{\mathrm{A}}\left(v_{i-f}^{\mathrm{A}}, \ldots, v_{i+f}^{\mathrm{E}} ; v_i^{\mathrm{T}} ; v_i^{\mathrm{E}} ; v_i^{\mathrm{ID}}\right)$$

$E_{\text{A}}$ bao gồm 12 lớp TCN với kết nối bỏ qua và 2 lớp MLP, các tính năng trong các sửa đổi khác được ghép nối với các tính năng âm thanh lớp 12 và do đó các lớp MLP cuối cùng là để tinh chỉnh tính năng âm thanh, và tính năng âm thanh tiềm ẩn cuối cùng là $\mathbf{z}^{\text{A}} ∈ \mathbb{R}^{128}$
#### Facial Expression Encoder
Chúng tôi sử dụng biểu thức khuôn mặt ban đầu vF ∈ R52 như là biểu thức khuôn mặt ban đầu.

Chúng tôi áp dụng trình mã hóa $E_{\text{F}}$ dựa trên 8-layer TCN và 2-layer MLP để trích xuất đặc trưng tiềm ẩn của khuôn mặt $\mathbf{z}^F ∈ \mathbb{R}^{32}$, theo công thức
$$z_i^{\mathrm{F}}=E_{\mathrm{F}}\left(v_{i-f}^{\mathrm{F}}, \ldots, v_{i+f}^{\mathrm{F}} ; v_i^{\mathrm{T}} ; v_i^{\mathrm{E}} ; v_i^{\mathrm{ID}} ; v_i^{\mathrm{A}}\right)$$

các đặc trưng được ghép nối ở tầng thứ 8 và MLP được sử dụng cho việc tinh chỉnh.
#### Body and Hands Decoders

Mô hình giải mã cho cơ thể và tay được thiết kế với cấu trúc dạng rời rạc, dựa trên kết luận của [39] rằng các cử chỉ cơ thể có thể được sử dụng để ước tính các cử chỉ tay. Hai bộ giải mã này, DB và DF, được xây dựng dựa trên cấu trúc LSTM để trích xuất đặc trưng tiềm ẩn và 2 lớp MLP để tái tạo cử chỉ. Chúng kết hợp các đặc trưng của năm modalities với pose trước đó, tức là seed pose, để tổng hợp đặc trưng cử chỉ tiềm ẩn $\mathbf{z}^\mathrm{B} ∈ \mathbb{R}^{256}$ và $\mathbf{z}^\mathrm{H} ∈ \mathbb{R}^{256}$. Cơ thể ước tính cuối cùng $\hat{v}^{\mathrm{B}} ∈ \mathbb{R}^{27×3}$ và tay ước tính cuối cùng $\hat{v}^{\mathrm{H}} ∈ \mathbb{R}^{48×3}$ được tính toán như sau:
$$\begin{gathered}z_i^{\mathrm{M}}=z_i^{\mathrm{T}} \otimes z_i^{\mathrm{ID}} \otimes z_i^{\mathrm{E}} \otimes z_i^{\mathrm{A}} \otimes z_i^{\mathrm{F}} \otimes v_i^{\mathrm{B}} \otimes v_i^{\mathrm{H}} \\ \mathbf{z}^{\mathrm{B}}=D_{\mathrm{B}}\left(z_0^{\mathrm{M}}, \ldots, z_n^{\mathrm{M}}\right), \mathbf{z}^{\mathrm{H}}=D_{\mathrm{H}}\left(z_0^{\mathrm{M}}, \ldots, z_n^{\mathrm{M}} ; \mathbf{z}^{\mathrm{B}}\right) \\ \hat{\mathbf{v}}^{\mathrm{B}}=M L P_{\mathrm{B}}\left(\mathbf{z}^{\mathrm{B}}\right), \hat{\mathbf{v}}^{\mathrm{H}}=M L P_{\mathrm{H}}\left(\mathbf{z}^{\mathrm{H}}\right)\end{gathered}$$
với $\mathbf{z} ∈ \mathbb{R}^{549}$ được gộp từ tất cả các modalities. Trong phương trình 5, độ dài của pose seed là bốn khung hình.
#### Loss Functions.

Sự giám sát cuối cùng của mạng của chúng tôi dựa trên việc tái tạo cử chỉ và hàm mất mát đối nghịch (adversarial loss):

$$\begin{gathered}\ell_{\text {Gesture Rec. }}=\mathbb{E}\left[\left\|\mathbf{v}^B-\hat{\mathbf{v}}^B\right\|_1\right]+\alpha \mathbb{E}\left[\left\|\mathbf{v}^H-\hat{\mathbf{v}}^H\right\|_1\right], \\ \ell_{\text {Adv. }}=-\mathbb{E}\left[\log \left(\operatorname{Dis}\left(\hat{\mathbf{v}}^B ; \hat{\mathbf{v}}^H\right)\right)\right],\end{gathered}$$
trong đó, đầu vào của bộ phân biệt trong quá trình huấn luyện đối nghịch chỉ là cử chỉ. Chúng tôi cũng áp dụng một trọng số $α$ để cân bằng các khoản phạt cho thân và tay. Sau đó, trong quá trình huấn luyện, chúng tôi điều chỉnh trọng số của hàm mất mát L1 và hàm mất mát đối nghịch sử dụng nhãn liên quan đến ý nghĩa ngữ nghĩa $λ$.

Hàm mất mát cuối cùng là:


$$\ell =\lambda \beta _{0} \ell _{\text {Gesture Rec.}}+\beta _{1} \ell _{\text {Adv}}$$


trong đó $\beta_0$ và $β_1$ là trọng số được xác định trước cho hàm mất mát L1 và hàm mất mát đối nghịch. Khi độ liên quan ý nghĩa ngữ cao, chúng tôi khuyến khích mạng tạo ra cử chỉ tương tự về mặt không gian so với đúng nhất có thể, do đó tăng cường khoản phạt L1 và giảm khoản phạt đối nghịch. 
## 5. Metric for Semantic Relevancy

Chúng tôi đề xuất độ đo Ghi nhớ Cử chỉ Liên quan Ngữ nghĩa (Semantic-Relevant Gesture Recall - SRGR) để đánh giá tính liên quan ngữ nghĩa của các cử chỉ, có thể được hiểu là các cử chỉ có sinh động và đa dạng hay không.
Chúng tôi sử dụng điểm số ngữ nghĩa là trọng số cho xác suất của Probability of Correct Keypoint (Keypoint Chính xác - PCK) giữa các cử chỉ được tạo ra và các cử chỉ thực tế. 

Trong đó, PCK là số khớp thành công đối với ngưỡng được chỉ định là δ. Độ đo SRGR có thể được tính như sau:

$$D_{S R G R}=\lambda \sum \frac{1}{T \times J} \sum_{t=1}^T \sum_{j=1}^J \mathbf{1}\left[\left\|p_t^j-\hat{p}_t^j\right\|_2<\delta\right]$$

trong đó $\mathbf{1}$ là hàm chỉ số và $T$, $J$ là tập hợp các khung và số khớp. Chúng tôi cho rằng SRGR, tập trung vào việc ghi nhớ các cử chỉ trong đoạn video quan tâm, phù hợp hơn với nhận thức chủ quan của con người về độ đa dạng hợp lệ của các cử chỉ so với sự biến thiên L1 của các cử chỉ được tổng hợp.


## 6. Experiments
Ở phần này, chúng ta đầu tiên đánh giá tính hợp lệ của độ đo SRGR, 
sau đó chứng minh chất lượng dữ liệu của tập dữ liệu của chúng ta dựa trên các thí nghiệm chủ quan. 

Tiếp theo, chúng ta chứng minh tính hợp lệ của mô hình cơ sở của chúng ta bằng các thí nghiệm chủ quan và khách quan, 

và cuối cùng, chúng ta thảo luận về đóng góp của mỗi modal dựa trên các thí nghiệm loại bỏ.
![image.png](attachment:image.png)

SRGR cho thấy sự nhất quán với nhận thức của con người, và độ biến động thấp hơn so với L1 Diversity trong đánh giá
### 6.1 Validness of SRGR

Một nghiên cứu người dùng được tiến hành để đánh giá tính hợp lệ của SRGR. 

Đầu tiên, chúng tôi cắt ngẫu nhiên các chuỗi chuyển động với kết quả đã được tạo ra thành các đoạn phim có khoảng 40 giây. 

Đối với mỗi đoạn phim, người tham gia được yêu cầu đánh giá cử chỉ dựa trên tính đa dạng của nó, đó là số lượng cử chỉ không lặp lại. 

Ngoài ra, các người tham gia cần đưa ra điểm số hấp dẫn của đoạn phim, nên dựa trên chuyển động chứ không phải nội dung của bài phát biểu. 

Tổng cộng có 160 người tham gia vào nghiên cứu đánh giá, và mỗi người đánh giá 15 đoạn phim cử chỉ ngẫu nhiên. 

Có tổng cộng 200 đoạn phim cử chỉ bao gồm các kết quả được tạo ra bằng các phương pháp từ Seq2Seq [54], S2G [21], A2G [33], MultiContext [53], và dữ liệu thực tế, 40 đoạn phim cho mỗi phương pháp với cùng dữ liệu người nói. 

Cả hai câu hỏi đều theo thang điểm Likert 5 điểm. Như được thể hiện trong hình 6, chúng tôi tìm thấy một phương sai lớn trong đa dạng L1 ngay cả khi chúng tôi sử dụng 100 đoạn phim cử chỉ để tính khoảng cách L1 trung bình (thường khoảng 40 đoạn phim [34,33]). 

Thứ hai, các kết quả được tạo ra với sự liên quan ngữ nghĩa mạnh mẽ nhưng có phạm vi chuyển động nhỏ hơn, chẳng hạn như Seq2Seq, đạt được đa dạng L1 thấp hơn so với A2G, có phạm vi chuyển động lớn hơn, nhưng các bằng chứng thống kê cho thấy con người cảm thấy Seq2Seq có đa dạng cao hơn A2G. 

Một giải thích là con người đánh giá đa dạng không chỉ dựa trên phạm vi chuyển động mà còn dựa trên một số đặc điểm ngụ ý khác, chẳng hạn như tính diễn đạt và liên quan ngữ nghĩa của chuyển động.
### 6.2 Data quality

Để đánh giá chất lượng dữ liệu chuyển động thực tế đã thu thập, chúng tôi so sánh tập dữ liệu đề xuất của mình với tập dữ liệu mocap phổ biến Trinity [18] và tập dữ liệu trong tự nhiên S2G-3D [21,22].

Chúng tôi tiến hành một nghiên cứu người dùng bằng cách so sánh các đoạn video được lấy mẫu từ dữ liệu thực và các kết quả được tạo ra bằng mạng tổng hợp chuyển động được huấn luyện trên mỗi tập dữ liệu.

Tập dữ liệu Trinity có tổng cộng 23 chuỗi, mỗi chuỗi có độ dài 10 phút.

Chúng tôi ngẫu nhiên chia dữ liệu thành tỷ lệ 19:2:2 cho tập huấn luyện / xác thực / kiểm tra vì không có tiêu chuẩn chia tập dữ liệu.
![image.png](attachment:image.png)

So sánh với Trinity [18], BEAT có điểm ưu tiên người dùng cao hơn về chất lượng dữ liệu thực tế. “-b” và “-h” chỉ ra thân và tay, tương ứng.
![image.png](attachment:image.png)

Đối chiếu với S2G-3D, BEAT đạt được sự ưa thích của người dùng tương đương về mặt tự nhiên. Dựa trên điểm số, mô hình được huấn luyện trên tập dữ liệu BEAT sẽ phù hợp hơn với phân bố vật lý chính xác, đa dạng và hấp dẫn hơn.
Chúng tôi đã sử dụng S2G [21], cũng như thuật toán SoTA A2G [33], để bao phủ cả các mô hình GAN và VAE.

Lớp đầu ra của mô hình S2G đã được điều chỉnh để đầu ra là các tọa độ 3D.

Trong nghiên cứu phân tích thành phần, các kết quả xương 3D đã được tạo ra và ghép với âm thanh để so sánh trong cuộc thử nghiệm người dùng.

Tổng số 120 người tham gia so sánh các clip được chọn ngẫu nhiên từ Trinity và tập dữ liệu của chúng tôi, có độ dài từ 5-20 giây.

Người tham gia được yêu cầu đánh giá tính chính xác của cử chỉ, tức là tính chính xác vật lý, tính đa dạng và đồng bộ giữa cử chỉ và âm thanh.

Ngoài ra, thân và tay được đánh giá riêng biệt cho bài kiểm tra tính chính xác của cử chỉ.

Kết quả được thể hiện trong Bảng 2, chứng tỏ tập dữ liệu của chúng tôi nhận được sự ưa thích cao hơn của người dùng ở mọi khía cạnh.

Đặc biệt là động tác của tay, chúng tôi vượt xa tập dữ liệu Trinity một khoảng lớn.

Điều này có thể do nhiễu của các thiết bị chụp chuyển động trước đây và thiếu các đánh dấu trên tay.

Bảng 3 cho thấy tỷ lệ ưu thích (%) của 60 người tham gia xem 20 cặp xương 3D ngẫu nhiên cho mỗi bài kiểm tra chủ quan.

Dựa trên điểm số, mô hình được huấn luyện trên tập dữ liệu BEAT sẽ được phù hợp với phân phối vật lý chính xác, đa dạng và hấp dẫn hơn.
### 6.3 Evaluation of the baseline model
**Training Setting** (Cấu hình huấn luyện)

Chúng tôi sử dụng trình tối ưu hóa Adam [30] để huấn luyện ở tỷ lệ học tập là 2e-4, và dữ liệu của 4 loại người nói được huấn luyện trên môi trường NVIDIA V100. 
Đối với các đánh giá định lượng, L1 đã được chứng minh là không thích hợp để đánh giá hiệu suất cử chỉ [33,53] do đó, chúng tôi áp dụng FGD [53] để đánh giá khoảng cách phân phối của các cử chỉ được tạo ra so với thực tế. 
Nó tính toán khoảng cách giữa các tính năng tiềm ẩn được trích xuất bởi mạng đã được huấn luyện trước, chúng tôi sử dụng một bộ mã hóa tự động dựa trên LSTM làm mạng đã được huấn luyện trước. 

Ngoài ra, chúng tôi áp dụng SRGR và Beat-Align để đánh giá độ đa dạng và đồng bộ. 
BeatAlign [34] là một Khoảng cách Chamfer giữa nhịp đập âm thanh và cử chỉ để đánh giá sự tương đồng giữa nhịp đập âm thanh và cử chỉ.

**Quantitative Results** (Kết quả định lượng)

Kết quả cuối cùng được hiển thị trong Bảng 4. 
Ngoài S2G và A2G, chúng tôi cũng so sánh kết quả của chúng tôi với thuật toán chuyển đổi văn bản thành cử chỉ và chuyển đổi âm thanh và văn bản thành cử chỉ, Seq2Seq [54] và MultiContext [53]. 

Kết quả cho thấy cả mô hình end2end và mô hình dãy được lập thành kỷ lục SoTA ở tất cả các độ đo (xem tài liệu bổ sung cho kết quả video).
![image.png](attachment:image.png)
### 6.4 Ablation Study

**Effectiveness of Cascaded Connection** (Hiệu quả của kết nối dạng liên tiếp)

Như được thể hiện trong Bảng 5, trái ngược với phương pháp end-to-end, kết nối dạng liên tiếp có thể đạt được hiệu suất tốt hơn vì chúng tôi giới thiệu kiến thức trước đó về con người để giúp mạng trích xuất các tính năng của các modalities khác nhau.
**Effectiveness of Each Modality**

Ở bảng 5, chúng tôi đã loại bỏ dần dần dữ liệu của một tính năng trong quá trình thực nghiệm. Đồng bộ sẽ bị giảm đáng kể sau khi loại bỏ âm thanh, điều này khá hiển nhiên. Tuy nhiên, nó vẫn giữ được một số đồng bộ hơi như thời gian đệm và chú thích căn chỉnh thời gian của văn bản và chuyển động môi của biểu cảm khuôn mặt. Ngược lại, việc loại bỏ mất lỗ lực mất cân bằng ngữ nghĩa giúp đồng bộ hóa được cải thiện, điều này có nghĩa là các cử chỉ ngữ nghĩa thường không được điều chỉnh hoàn hảo với âm thanh. Cũng có một mối quan hệ giữa cảm xúc và đồng bộ, nhưng ID người nói chỉ có ít ảnh hưởng đến đồng bộ. Việc loại bỏ âm thanh, cảm xúc và biểu hiện khuôn mặt không ảnh hưởng đáng kể đến việc thu hồi cử chỉ liên quan đến ngữ nghĩa, điều này phụ thuộc chủ yếu vào văn bản và ID người nói. Dữ liệu từ mỗi tính năng đóng góp vào việc cải thiện FGD, điều này có nghĩa là sử dụng các tính năng dữ liệu khác nhau cải thiện khả năng ánh xạ của mạng. Sự kết hợp của âm thanh và biểu hiện khuôn mặt, đặc biệt là biểu hiện khuôn mặt, cải thiện FGD đáng kể. Chúng tôi phát hiện rằng việc loại bỏ cảm xúc và ID người nói cũng ảnh hưởng đến điểm FGD. Điều này bởi vì việc sử dụng mạng tích hợp tăng cường đa dạng của tính năng, dẫn đến đa dạng của kết quả, tăng phương sai của phân phối và làm cho nó giống hơn với dữ liệu ban đầu.
**Emotional Gestures**

Điều này cho thấy rằng bộ phân loại có khả năng phân biệt đúng các động作 biểu cảm về cảm xúc.

Cụ thể, bộ phân loại này được huấn luyện trên dữ liệu thực tế của người nói số 4 và được sử dụng để phân loại 12 đoạn video thử nghiệm ngẫu nhiên. Tổng cộng, chúng ta mời 60 người tham gia phân loại các đoạn video này (được cung cấp cả âm thanh).
![image.png](attachment:image.png)
### 6.5 Limitation
**Impact of Acting**

Đóng góp của Acting. 
Các phiên Tự nói có thể phản ánh sự ảnh hưởng của diễn xuất, điều không thể tránh khỏi và được kiểm soát. 
Không tránh khỏi: Tác động có thể do nội dung đã được định trước. 

Tuy nhiên, để khám phá tính liên quan đến ý nghĩa và tính cách, cần phải kiểm soát các biến, tức là các người nói khác nhau nên nói chung một văn bản và cùng một cảm xúc để tính cách có thể được khám phá cẩn thận. 

Được kiểm soát: Các người nói đã ghi lại phiên nói chuyện trước và được khuyến khích giữ cùng một phong cách như trong phiên nói chuyện. 
Chúng tôi cũng đã loại bỏ khoảng 21 giờ dữ liệu và sáu người nói do không đồng nhất về phong cách của họ.
**Calculation of SRGR**

Tính toán SRGR. Hiện tại, SRGR được tính dựa trên nhãn ngữ nghĩa, điều này có giới hạn đối với tập dữ liệu chưa được gắn nhãn. Để giải quyết vấn đề này, huấn luyện mạng điểm số hoặc bộ phân biệt ngữ nghĩa là một hướng đi có thể.
## 7. Conclusion
Chúng tôi đã xây dựng một tập dữ liệu đánh dấu ngữ nghĩa và cảm xúc đa dạng, quy mô lớn và chất lượng cao để tạo ra các cử chỉ giao tiếp mang tính con người hơn.

Kết hợp với tập dữ liệu này, chúng tôi đề xuất một mô hình cơ sở dựa trên chuỗi truyền dẫn cho tổng hợp cử chỉ dựa trên sáu dạng dữ liệu và đạt được hiệu suất tốt nhất.

Cuối cùng, chúng tôi giới thiệu SRGR để đánh giá tính liên quan ngữ nghĩa.

Trong tương lai, chúng tôi kế hoạch mở rộng kiểm tra dữ liệu chéo cho các tiêu chuẩn nhận dạng AU và cảm xúc.

Tập dữ liệu của chúng tôi và các thực nghiệm thống kê liên quan có thể hỗ trợ nhiều lĩnh vực nghiên cứu khác nhau, bao gồm tổng hợp cử chỉ có thể điều khiển, phân tích đa dạng và nhận dạng chuyển động cảm xúc trong tương lai.
* A. Annotation Interface and Measurement of Agreement.
* B. Details of Text Content and Speaker Information.
* C. Details of Data Release Formats.
* D. Additional Discussions for SRGR, FGD and BeatAlign.
* E. More Subjective Results and Videos.
* F. Details of Baselines Training Setting.
* G. Answers in Self-Talk Session (cf. answers.doc).
#### A. Annotation Interface and Measurement of Agreement.


Chúng tôi sử dụng giao diện chú thích được thích ứng từ một phiên bản được chỉnh sửa của VGG Image Annotator (VIA) [17] bởi [42], như được thể hiện trong hình 7a. 
Chúng tôi sử dụng cùng một giao diện để chú thích cảm xúc và ý nghĩa. 
Tuy nhiên, các chú thích được thực hiện bởi một nhóm chú thích khác nhau cho mỗi nhiệm vụ. 
Đối với chú thích cảm xúc, hai chú thích đánh dấu thời gian bắt đầu và kết thúc của mỗi đoạn video của các phiên Đối thoại. 
Đối với chú thích ý nghĩa, người chú thích sẽ: 

- i) đồng ý hoặc không đồng ý rằng cử chỉ hiện tại liên quan về ý nghĩa đến nội dung văn bản theo cảm nhận của họ; 

- ii) nếu đồng ý, họ chú thích thời gian bắt đầu và kết thúc cho cử chỉ hiện tại; 

- iii) và sau đó, họ chọn từ khóa mà họ cho rằng cử chỉ chính xác tương ứng từ danh sách các từ khóa được phân tách bằng dấu phẩy. 


Thuật toán xử lý sau đó sẽ sử dụng các từ khóa đã tách, sự căn chỉnh văn bản và chú thích ngữ nghĩa từng đoạn cử chỉ để tạo ra chú thích từng khung hình. 
Như được thể hiện trong hình 7b, sự liên quan ngữ nghĩa cuối cùng cho mỗi khung hình được tính bằng cách nhân điểm số ngữ nghĩa của đoạn cử chỉ với điểm số ngữ nghĩa của từ khóa. 
Cần lưu ý rằng hai cấp độ chú thích ngữ nghĩa có thể được sử dụng riêng lẻ.
![image.png](attachment:image.png)

**Annotation Interface and Post-Processing**.  Giao diện chú thích và xử lý sau khi chú thích.

(a) Những người chú thích sẽ đưa ra các chú thích cấp đoạn chuyển động và cấp từ khóa.

(b) Thuật toán xử lý sau khi chú thích sẽ tạo ra một điểm số liên quan ngữ nghĩa cấp khung hình bằng cách sử dụng chú thích cấp đoạn, từ khóa và phù hợp văn bản.
Chúng tôi tính tỉ lệ đồng ý giữa các người đánh giá cho các chú thích bằng cách đo lường độ tin cậy giữa các người đánh giá cho cả chú thích về cảm xúc và chú thích về ý nghĩa. 
Đối với chú thích về cảm xúc, chúng tôi trình bày điểm số trong Bảng 7, sự đồng ý được đánh dấu chỉ khi hai người đánh giá cùng cho cùng một nhãn. 
Sự đồng ý cuối cùng cho khoảng 16 triệu khung hình là 96%, đây là mức độ đồng ý cao đến mức chúng tôi không thực hiện chú thích về cảm xúc với nhiều hơn hai người đánh giá.
![image.png](attachment:image.png)

**Statistic on Emotion Annotation**

Left: The sum of duration in emotion annotations (in seconds).

Right: Distribution of annotations number in each clip.

![image.png](attachment:image.png)
#### B. Details of Text Content and Speaker Information.

Chúng tôi trình bày phân bố các nguyên âm và phụ âm cho tập dữ liệu BEAT trong Hình 9, đó tương thích với danh sách 3000 từ thường được sử dụng [25]. 
Đối với các phiên Hội thoại, các câu hỏi được chọn từ Bảng 8. 

Có mười chủ đề để tranh luận và giới thiệu, tương ứng, liên quan đến các chủ đề giao tiếp hàng ngày. 

Đối với phiên Tự nói chuyện, danh sách câu trả lời đầy đủ, bao gồm 120 câu trả lời, được đính kèm ở cuối tài liệu bổ sung này, bao gồm bản dịch của bốn ngôn ngữ cho 30 câu trả lời được xác minh bởi người bản ngữ.


![image.png](attachment:image.png)
Giữ động lực cho việc điều tra sự khác biệt phong cách giữa các người nói, chúng tôi thu thập dữ liệu từ người nói của các quốc gia, giới tính, độ tuổi và chủng tộc khác nhau. Chúng tôi đã mô hình hóa những khác biệt này với các điều khiển rõ ràng về phong cách. Trong quá trình thu thập dữ liệu, chúng tôi đảm bảo phong cách của người diễn viên là nhất quán. Chúng tôi đã lọc ra khoảng 21 giờ dữ liệu và 6 người nói do không đồng nhất về phong cách của họ. Diễn viên thể hiện các cử chỉ khác nhau đáng kể trong các phiên Tự nói chuyện và Hội thoại. Ví dụ, một số người nói động tay rất nhiều trong các phiên Hội thoại nhưng không có hầu hết các cử chỉ trong các phiên Tự nói chuyện. Số lượng người nói hiệu quả là 30 và thời lượng ghi âm tương ứng là 76 giờ. Thông tin về người nói và thời lượng ghi âm của họ có sẵn trong Bảng 9. Chúng tôi có 34 và 26 giờ ghi âm từ người nói tiếng Anh bản địa và lưu loát, tương ứng, và tỷ lệ thời lượng bản ngữ / lưu loát là 1,307.
![image.png](attachment:image.png)
![image.png](attachment:image.png)

Speaker information in terms of gender, originating country, native English
speaker, recording duration in English and in the second language, age and ethnicity.
In the gender column, M and F stand for male and female speakers, respectively.
The native column shows whether the speaker is a native English speaker. Duration is
represented in hours (h).



#### C. Details of Data Release Formats.

Định dạng các tệp dữ liệu của chúng tôi được liệt kê dưới đây:

* i) Dữ liệu bắt chuyển động trong định dạng tệp BVH cho các cử chỉ của cơ thể và tay.
* ii) Bản ghi âm trong định dạng tệp WAV stereo.
* iii) Trọng số blendshape của khuôn mặt trong định dạng tệp JSON.
* iv) Dữ liệu lưới khuôn mặt trong định dạng tệp FBX cho 8 người nói.
* v) Dữ liệu chú thích đồng bộ văn bản-âm thanh trong định dạng tệp TextGrid.
* vi) Chú thích về nghĩa và cảm xúc trong định dạng tệp văn bản.


Đối với các cử chỉ của cơ thể và tay, vị trí các đánh dấu được hiển thị trong Hình 9 (hình ảnh từ [1]), và tên của các khớp được hiển thị trong Hình 11, tương ứng. Chúng tôi sử dụng thông tin xoay theo góc Euler như là biểu diễn chuyển động, tức là 75 xoay + 1 dịch chuyển gốc.
![image.png](attachment:image.png)
![image.png](attachment:image.png)
![image.png](attachment:image.png)
activates one part of the face (e.g., mouth area, eyes, eye-brows) at a time
considering the human facial anatomy.
All avatars used for demonstration were built by a Blender tool called Hu-
manGeneratorv32 . We created avatars for 8 speakers. Furthermore, we also pro-
cessed motion retargeting on the body bone animation. Thanks for giving the
exception of license from the HumanGenerator team. These facial mesh data will
be released together to better visualize the facial data recordings as an asset of
the BEAT dataset.
![image.png](attachment:image.png)

The names for FACs (Facial Action Coding system) based blend-
shapes.
#### D. Additional Discussions for SRGR, FGD and BeatAlign.
![image.png](attachment:image.png)
$$\operatorname{FGD}(\mathbf{m}, \hat{\mathbf{m}})=\left\|\mu_r-\mu_g\right\|^2+\operatorname{Tr}\left(\Sigma_r+\Sigma_g-2\left(\Sigma_r \Sigma_g\right)^{1 / 2}\right)$$


 

$$\text{BeatAlign}=\frac{1}{G} \sum_{b_G \in G} \exp \left(-\frac{\min _{b_A \in A}\left\|b_G-b_A\right\|^2}{2 \sigma^2}\right)$$


#### E. More Subjective Results and Videos.

![image.png](attachment:image.png)

Results Visualization. Ground truth (top) and generated results with
neutral (middle) and fear (down) emotions.

#### F. Details of Baselines Training Setting.

![image.png](attachment:image.png)

#### G. Answers in Self-Talk Session (cf. answers.doc).
