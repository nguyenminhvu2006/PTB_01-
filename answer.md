PHẦN A — KIỂM TRA ĐỌC HIỂU (20 điểm)

Câu A1 — HTTP & Browser
*Nguồn tham chiếu: 01_introduction_html_universe.md (Mục 0: Opening Hook, Mục 2: Client-Server Architecture & Mục 3: Browser Rendering Pipeline)*

1. Các bước xảy ra khi nhập https://shopee.vn và nhấn Enter:**
Dựa theo luồng hoạt động Client-Server, quá trình này diễn ra qua 5 bước chính như sau:

* Bước 1: DNS Lookup & Định tuyến:** Trình duyệt phân giải tên miền `shopee.vn` thành địa chỉ IP, sau đó request xuất phát từ máy tính, đi qua các tầng mạng (nhà mạng, cáp quang) để tìm đến máy chủ (Server) của Shopee.
* Bước 2: Gửi HTTP Request (Client to Server):** Trình duyệt (Client) đóng vai trò người hỏi, gửi một HTTP Request (sử dụng method GET) đến máy chủ Shopee để yêu cầu nội dung trang web.
* Bước 3: Nhận HTTP Response (Server to Client):** Máy chủ tìm kiếm dữ liệu, sau đó gửi trả lại một HTTP Response với Status Code (ví dụ: `200 OK`) kèm theo bộ ba file nền tảng: HTML, CSS và JavaScript.
* Bước 4: Parsing (Phân tích cú pháp):** Trình duyệt nhận file HTML và bắt đầu đọc từ trên xuống (Parse HTML) để dựng lên DOM Tree (bộ xương). Đồng thời, nó tải về và đọc các file CSS (Parse CSS) để tạo CSSOM Tree.
* Bước 5: Rendering (Dựng trang):** Trình duyệt thực thi JavaScript (Execute JS) nếu có. Cuối cùng, nó trải qua các bước Layout (tính toán vị trí) -> Paint (tô màu pixel) -> Composite để hiển thị giao diện hoàn chỉnh lên màn hình cho người dùng.

2. Tab Network trong Chrome DevTools:**

Tab **Network** cho thấy toàn bộ lịch sử giao tiếp giữa Client và Server. Cụ thể, nó ghi lại mọi HTTP Request mà trình duyệt đã gửi đi để tải file (HTML, CSS, JS, ảnh...), kèm theo các thông tin chi tiết như: Status Code (200, 404...), Method (GET, POST...), dung lượng file và thời gian phản hồi của Server.

**[Ảnh Screenshot tab Network]**
*(Hình ảnh đính kèm bên dưới)*
![Mô tả ảnh: Screenshot DevTools tab Network](network.png)

**Ghi chú các điểm đã đánh dấu trên ảnh:**
* Status Code của request đầu tiên:** Nằm ở dòng trên cùng của danh sách tải (thường là request xin file HTML chính), có Status Code là `200` (OK).
* Tổng thời gian load trang:** Nằm ở thanh trạng thái dưới cùng (ví dụ: hiển thị dòng chữ `Load: ... ms` hoặc `Finish: ... s`).
* Một request trả về file CSS:** Nằm ở dòng yêu cầu có đuôi file là `.css` (ở cột Name) và cột Type hiển thị là `stylesheet`.

Câu A2 (5đ) — Semantic HTML
*Nguồn tham chiếu: Chương 04 - PHẦN HIỂN THỊ (Mục 1: Why This Matters, Mục 2: Bản đồ <body>, Mục 3: Semantic Elements chi tiết & Mục 5: Real-world Layer)*

1. Tại sao trang web bị Google đánh giá SEO thấp?**
Trang web này mắc lỗi "Div Soup" (chỉ sử dụng toàn thẻ `<div>` vô nghĩa). Theo tài liệu, khi bạn dùng Div Soup, "Google không phân biệt được gì". Các thẻ Semantic HTML ảnh hưởng trực tiếp đến SEO vì Google cần đọc các thẻ có ý nghĩa (như `<article>`, `<section>`, `<h1>–<h6>`) để hiểu cấu trúc nội dung của trang.

2. Liệt kê 4 lỗi semantic và cách sửa:**
* Lỗi 1: Dùng `<div class="header">` cho phần đầu trang. Phải sửa thành `<header>`.
* Lỗi 2: Dùng `<div class="menu">` cho điều hướng. Phải sửa thành `<nav>`.
* Lỗi 3: Dùng `<div class="main">` và `<div class="product">`. Phải sửa thành `<main>` (chỉ dùng 1 lần cho nội dung chính) và `<article>` (cho nội dung độc lập của sản phẩm).
* Lỗi 4: Dùng `<div class="title">` cho tên sản phẩm. Cần sửa thành thẻ tiêu đề như `<h1>` (giống như ví dụ trang sản phẩm Shopee trong tài liệu) để Google nhận diện được.
* Lỗi 5: Thẻ `<img>` thiếu thuộc tính `alt`. Thuộc tính `alt` bắt buộc phải có và phải mô tả nội dung ảnh để chuẩn SEO và người khiếm thị có thể hiểu.

3. Đoạn code sửa lại chuẩn Semantic HTML:**

```html
<header>
    <div class="logo">ShopTLU</div>
    <nav class="menu">
        <ul>
            <li><a href="/">Trang chủ</a></li>
            <li><a href="/products">Sản phẩm</a></li>
        </ul>
    </nav>
</header>
<main>
    <article class="product">
        <h1 class="title">iPhone 16 Pro</h1>
        <p class="price">25.990.000đ</p>
        <figure class="image">
            <img src="iphone.jpg" alt="Điện thoại iPhone 16 Pro" loading="lazy">
        </figure>
    </article>
</main>
<footer>
    &copy; 2026 ShopTLU
</footer>
```

Câu A3 — Block vs Inline
**Text Art:**

```text
[-------------------------- Hộp 1 --------------------------]
[Text A] [Text B]
[-------------------------- Hộp 2 --------------------------]
[Text C] [**Text D**]
[-------------------------- Hộp 3 --------------------------]
```

Trên trình duyệt, các phần tử sẽ được xếp chồng lên nhau và nối tiếp nhau theo cấu trúc sau (khung ngoặc vuông `[ ]` biểu diễn không gian mà phần tử chiếm dụng)

Câu A4 — Table
*Nguồn tham chiếu:** File `05_tables_hyperlinks.md` (Chương 05) - Phần 3: Core Technical Truth & Phần 5: Real-world Layer.

1. Sự khác nhau giữa `<thead>`, `<tbody>`, `<tfoot>`:**
Theo Mục 3 của tài liệu, đây là các thẻ Semantic dùng để phân định rõ cấu trúc của một bảng dữ liệu (`<table>`), giúp trình duyệt, CSS và trình đọc màn hình xử lý tốt hơn:
* `<thead>` (Header section):** Dùng để chứa phần tiêu đề của bảng (thường chứa các thẻ `<th>` để in đậm tiêu đề cột).
* `<tbody>` (Data section):** Dùng để chứa toàn bộ nội dung/dữ liệu chính của bảng.
* `<tfoot>` (Footer section):** Dùng để chứa các hàng tổng kết, tính tổng ở cuối bảng. Lợi ích kỹ thuật là trình duyệt có thể render (hiển thị) phần `<tfoot>` ngay cả khi dữ liệu trong `<tbody>` quá dài và chưa tải xong.

2. Tại sao KHÔNG NÊN dùng table để tạo layout trang web?**
Dựa vào Mục 1 và Mục 5 của tài liệu, sử dụng `<table>` để dàn bố cục (layout) là một "anti-pattern" (cách làm sai lầm) từ năm 2005. Dưới đây là 3 lý do chính:
* Mất khả năng tiếp cận (Accessibility):** Các trình đọc màn hình (dành cho người khiếm thị) được thiết kế để đọc cấu trúc `<table>` theo thứ tự hàng/cột dữ liệu. Nếu dùng table để làm layout, phần mềm sẽ đọc sai thứ tự logic của nội dung, gây nhầm lẫn lớn cho người dùng.
* Mã nguồn bị lạm dụng và phức tạp (Abuse of code):** Để tạo một layout đơn giản, người lập trình sẽ phải lồng ghép vô số các thẻ `<tr>`, `<td>` vào nhau một cách không cần thiết, làm mã nguồn trở nên rác, cồng kềnh và cực kỳ khó bảo trì sau này.
* Thiếu linh hoạt (So với công cụ hiện đại):** Table được thiết kế cứng nhắc cho dữ liệu dạng bảng. Để tạo bố cục trang (như layout 2 cột), việc sử dụng các công cụ hiện đại như CSS Grid hay Flexbox sẽ tối ưu, gọn gàng và dễ dàng Responsive (tương thích đa màn hình) hơn rất nhiều.

PHẦN B THỰC HÀNH CODE
Câu B3 - Debug HTML

Lỗi 1: Dòng 1 - Lỗi cú pháp (Syntax) - Khai báo DOCTYPE thiếu chữ html.
Cách sửa: Đổi <!DOCTYPE> thành <!DOCTYPE html>.

Lỗi 2: Dòng 2 - Lỗi ngữ nghĩa (Semantic) - Thẻ <html> thiếu thuộc tính ngôn ngữ lang, điều này không tốt cho SEO và trình đọc màn hình.
Cách sửa: Sửa thành <html lang="vi"> (hoặc en).

Lỗi 3: Dòng 4 - Lỗi cú pháp (Syntax) - Thẻ <title> chưa được đóng.
Cách sửa: Thêm thẻ đóng: <title>Trang web</title>.

Lỗi 4: Dòng 5 - Lỗi cú pháp (Syntax) - Giá trị charset viết sai định dạng chuẩn.
Cách sửa: Đổi "utf8" thành "utf-8".

Lỗi 5: Dòng 8 - Lỗi cú pháp (Syntax) - Thẻ đóng <h1> bị sai cú pháp (thiếu dấu gạch chéo /).
Cách sửa: Đổi <h1>Welcome to ShopTLU<h1> thành <h1>Welcome to ShopTLU</h1>.

Lỗi 6: Dòng 12 - Lỗi cú pháp (Syntax) - Thẻ đóng <a> bị sai cú pháp (viết thành thẻ mở).
Cách sửa: Đổi <a> ở cuối thành </a>.

Lỗi 7: Dòng 19 & 26 - Lỗi ngữ nghĩa (Semantic) - Nhảy cấp heading. Trang web đang từ <h1> nhảy thẳng xuống <h3> mà bỏ qua <h2>.
Cách sửa: Đổi các thẻ <h3> thành <h2>.

Lỗi 8: Dòng 20 - Lỗi cú pháp và ngữ nghĩa - Thuộc tính src không có ngoặc kép bọc giá trị và thiếu thuộc tính alt mô tả ảnh (bắt buộc trong chuẩn HTML5).
Cách sửa: Đổi thành <img src="iphone.jpg" alt="Ảnh iPhone 16 Pro">.

Lỗi 9: Dòng 22 - Lỗi lồng thẻ (Syntax - Nesting error) - Thẻ <p> và <b> đóng sai thứ tự (thẻ nào mở sau phải đóng trước).
Cách sửa: Đổi <b>25.990.000đ</p></b> thành <b>25.990.000đ</b></p>.

Lỗi 10: Dòng 29 & 30 - Lỗi ngữ nghĩa (Semantic) - Hàng đầu tiên của bảng là tiêu đề cột, nên dùng thẻ <th> thay vì <td> (dữ liệu thường).
Cách sửa: Đổi <td&gt;Tên</td&gt; và <td&gt;Giá</td&gt; thành <th&gt;Tên</th&gt; và <th&gt;Giá</th&gt;.

Lỗi 11: Dòng 40 - Lỗi ngữ nghĩa (Semantic) - Theo chuẩn HTML5, mỗi trang chỉ được có duy nhất một thẻ <main>. Đoạn này chứa nội dung sidebar nên dùng thẻ <aside>.
Cách sửa: Đổi <main> và </main> thành <aside> và </aside>.

Lỗi 12: Dòng 45 - Lỗi cú pháp (Syntax) - Thẻ <p> trong footer chưa có thẻ đóng.
Cách sửa: Sửa thành <p>Copyright 2026</p>.

Lỗi 13: Dòng cuối cùng - Lỗi cú pháp (Syntax) - Thiếu thẻ đóng </html> cho toàn bộ tài liệu.
Cách sửa: Thêm </html> vào dưới cùng, sau thẻ </body>.

Bài B4: Phân tích trang web thật
Trang web phân tích: thegioididong.com

1. Phân tích tab Elements (Thẻ Semantic & Non-semantic)
(Tham khảo ảnh đính kèm: anh1.png, anh2.png, anh3.png)

3 thẻ semantic HTML5 mà trang web sử dụng:

<header>: Nằm ở đầu trang, bọc toàn bộ khu vực điều hướng, tìm kiếm và banner đầu trang (Ghi nhận tại anh1.png).

<h1>: Thẻ tiêu đề chính, nằm lồng bên trong khu vực header (có class sc-only) (Ghi nhận tại anh1.png).

<form>: Nằm ở khu vực thanh tìm kiếm, bọc thẻ input để xử lý gửi từ khóa tìm kiếm đi (Ghi nhận tại anh3.png).

2 thẻ trang web KHÔNG dùng đúng semantic (Anti-pattern):

Dùng quá nhiều <div> lồng nhau (Div soup) chỉ để tạo lớp phủ (overlay) giao diện mà không mang ý nghĩa nội dung, ví dụ: <div class="header-overlay">, <div class="header-mask"> (Ghi nhận tại anh1.png).

Dùng thẻ <div> để làm nút bấm: Cụ thể là thẻ <div class="btn-view-more is-desktop">. Đáng lẽ ra trang web nên sử dụng thẻ <button> để đúng chuẩn ngữ nghĩa cho chức năng "Xem thêm" (Ghi nhận tại anh2.png).

2. Phân tích thẻ <table>
(Tham khảo ảnh đính kèm: anh2.png)

Table đó hiển thị nội dung gì?

Dựa vào thanh đường dẫn (breadcrumb) ở góc dưới cùng màn hình DevTools chứa đoạn div#product-comparison-table, có thể khẳng định bảng này dùng để hiển thị bảng so sánh thông số giữa các sản phẩm.

Có dùng <thead>, <tbody> không?

Trong bức ảnh chụp, thẻ <table> hiện đang ở trạng thái thu gọn (hiển thị ...). Vì vậy, không thể nhìn trực tiếp code bên trong qua ảnh này. Tuy nhiên, theo cơ chế hiển thị của trình duyệt, nó sẽ luôn tự động tạo thẻ <tbody> bọc dữ liệu bên trong.

3. Phân tích thẻ <form> (Ô tìm kiếm)
(Tham khảo ảnh đính kèm: anh3.png)

Form đó có action và method gì?

action: "/tim-kiem" (Điều hướng người dùng đến trang xử lý kết quả tìm kiếm).

method: Thẻ <form> trong ảnh không khai báo tường minh thuộc tính method. Do đó, trình duyệt sẽ tự động áp dụng phương thức mặc định là GET.

Input types nào được dùng?

Trang web sử dụng <input type="text"> (hiển thị rõ qua đoạn mã <input id="skw" type="text"...>), giúp người dùng có thể gõ văn bản tự do để tìm kiếm thiết bị.
