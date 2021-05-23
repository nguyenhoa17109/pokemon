# Pokemon
1. Tổng quan.
     
- Đối tượng: 1 người chơi.
- Số lượng vòng chơi: 1
2. Ý tưởng: 
- Tạo ma trận 10x10, các hình ảnh được lưu ở trong file "icon" có tên "icon+i" (trong đó 0<i<38)
- Đọc các hình ảnh lên một cách ngẫu nhiên
- Số hình ảnh hiện lên là chẵn và có thể lặp lại.
3. Thuật toán chi tiết.

Toàn bộ các ô hình ảnh pokemon được sắp xếp theo mô hình của ma trận vuông. Thực hiện trên console rồi đưa lên giao diện chính của game.

Để thực hiện giải thuật của game có các trường hợp từ đơn giản đến phức tạp để tìm đường đi (có thể ăn được) của 2 con pokemon, tổng quan có 3 trường hợp chính.

Ở đây các trường hợp có thể được gộp lại. Tuy nhiên, điềy này làm tăng độ phức tạp của code với nhiều lệnh if else. Nên các trường hợp được chia ra như sau:
        
 a. Trường hợp 2 hình ảnh cùng nằm trên 1 hàng(cột).
 - 2 hình ảnh cùng nằm trên 1 hàng(đường thẳng theo trục x)
 - 2 hình ảnh cùng nằm trên 1 cột(đường thẳng theo trục y)

Với 2 TH cơ bản này chỉ cần dùng vòng lặp for từ điểm đầu đến điểm cuối và kiểm tra xem đường thẳng đó có thông với nhau được không? Để xét 2 TH này ta sử dụng hai hàm là checkLineX(int y1, int y2, int x) và checkLineY(int x1, int x2, int y) tương ứng là xét theo hàng và xét theo cột. Hàm trả về true nếu đi được giữa 2 điểm, false nếu không đi được. Nếu không được ta sẽ sử dụng các TH mở rộng theo chiều ngang hoặc dọc

   b. Trường hợp đường nối 2 hình ảnh là hình chữ Z:
- Xét duyệt các đường đi theo chiều ngang trong phạm vi hình chữ nhật. Ta xây dựng hàm checkRectX(Point p1, Point p2), (kiểm tra trong phạm vi hình chữ nhật theo chiều ngang mà 2 điểm p1 và p2 tạo ra). Trước tiên sẽ tìm xem điểm nào có tọa độ cột (y) nhỏ hơn (pMinY), điểm nào lớn hơn (pMaxY). Tiếp theo cho y chạy từ bé đến lớn (từ trái sang phải), với mỗi cột (y) tương ứng chúng ta sẽ xét xem 3 đường thẳng nhỏ gấp khúc có liền mạch không bằng cách sử dụng hàm checkLineX và checkLineY đã xây dựng. Nếu tồn tại một cột y nào đó mà làm cho 3 đường này thông nhau chứng tỏ chúng ta có đường đi được giữa 2 điểm và ta sẽ trả về giá trị y là cột đó. Nếu không thì trả về -1.

 - Xét duyệt các đường đi theo chiều dọc: xây dựng hàm checkRectY(Point p1, Point p2) tương tự như trường hợp trên nhưng xét theo chiều dọc.
 
  c. Xét mở rộng theo chiều ngang, dọc (trường hợp đường đi có hình dạng chữ U hoặc chữ L)
- Xét mở rộng theo chiều ngang:
Trong TH này chúng ta sẽ xét mở rộng chiều ngang về phía bên trái hoặc bên phải bằng hàm checkMoreLineX(Point p1, Point p2, int type) Trong đó p1, p2 là 2 điểm cần kiểm tra, tìm đường đi, type là loại, type sẽ nhận giá trị là 1 (đi về phải) hoặc -1 (đi về trái). Trước tiên ta tìm xem điểm có cột (y) nào nhỏ hơn (pMinY), điểm nào có y lớn hơn (pMaxY). Vì khi xét trong phạm vi hình chữ nhật hoặc trên đường thẳng thì 2 điểm đều không đến được với nhau, do đó chúng ta mở rộng nó ra bằng cách xét về bên trái từ cột pMaxY.y (cột của điểm chứa cột lớn hơn) và về bên phải từ cột pMinY. Và cứ tăng hoặc giảm dần chỉ số cột lên khi 2 điểm (pMinY.x, y) và (pMaxY.x, y) không phải chướng ngại vật. Nếu gặp giá trị y nào mà làm cho đường thẳng đứng (màu xanh lục) được thông thì chứng tỏ đã tìm thấy đường đi. Khi đó hàm trả về giá trị là cột y tìm được, nếu không thì trả về -1. Tuy nhiên trước khi xét từng cột như vậy chúng ta cần xét đoạn từ pMinY đến pMaxY (doạn màu xanh lá) có thông không đã.
- Xét duyệt các đường đi theo chiều dọc: xây dựng hàm checkMoreLineY(Point p1, Point p2, int type) tương tự như TH5 nhưng duyệt theo từng hàng. Cuối cùng là hàm checkTwoPoint(Point p1, Point p2) để kiểm tra và tìm đường đi gữa 2 điểm p1, p2 bất kỳ. Hàm sẽ trả về đối tượng là MyLine gồm 2 điểm p1 và p2. Trong TH đường thẳng giữa 2 điểm p1, p2 được thông thì trả về MyLine gồm p1 và p2, trong TH đường đi là gấp khúc thì trả về MyLine gồm 2 điểm ở đoạn gấp khúc.

  
  
