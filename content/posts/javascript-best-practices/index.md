---
title: Các cách thực hành tốt nhất cho JavaScript
date: 2024-12-01
---

Các Quy Tắc Tốt Nhất Khi Lập Trình JavaScript
JavaScript không còn nghi ngờ gì nữa là ngôn ngữ lập trình được sử dụng nhiều nhất trên thế giới, đóng vai trò quan trọng trong công nghệ mà chúng ta đều phụ thuộc – Internet. Tuy nhiên, với sức mạnh này cũng đi kèm trách nhiệm lớn, và hệ sinh thái JavaScript đang thay đổi nhanh chóng, khiến việc bắt kịp các quy tắc tốt nhất trở nên khó khăn. Dưới đây là một số quy tắc giúp viết mã JavaScript sạch, dễ bảo trì và hiệu quả hơn.

![](/img/javascript-best-practices/1.jpg)


## Quy định dự án là ưu tiên hàng đầu

Dự án mà bạn làm việc có thể có những quy tắc nghiêm ngặt riêng. Quy định của dự án luôn quan trọng hơn bất kỳ quy tắc nào từ bài viết hoặc hướng dẫn – kể cả bài viết này!

➡️ Lời khuyên: Nếu bạn muốn áp dụng một quy tắc cụ thể, hãy đảm bảo nó phù hợp với quy định của dự án và được tất cả thành viên trong nhóm đồng thuận.

## Sử dụng JavaScript phiên bản mới nhất
JavaScript ra đời từ ngày 4/12/1995 và liên tục phát triển từ đó. Trên mạng, bạn có thể tìm thấy nhiều gợi ý đã lỗi thời.

➡️ Lời khuyên: Hãy kiểm tra xem quy tắc bạn muốn dùng có còn hợp thời hay không. Đồng thời, khi sử dụng tính năng JavaScript mới, hãy chọn những tính năng đã đạt Ecma TC39 Stage 3 trở lên để đảm bảo tính ổn định.

## Sử dụng let và const thay cho var

Trong JavaScript cũ, người ta thường dùng var để khai báo biến. Tuy nhiên, let và const hiện đại hơn và cung cấp phạm vi khối (block-scoping).

        for (let j = 1; j < 5; j ++ ) {
            console.log(j);
        }
        console.log(j); // Lỗi: 'j' không được định nghĩa ngoài vòng lặp

Ngược lại, nếu dùng var:

        for (var j = 1; j < 5; j++) {
            console.log(j);
        }
        console.log(j); // Kết quả: 5 (biến vẫn tồn tại ngoài vòng lặp)

➡️ Lời khuyên: Dùng let hoặc const giúp giảm lỗi ngoài ý muốn do phạm vi biến không rõ ràng khi dùng var.

## Ưu tiên class thay vì prototype

Trước đây, JavaScript sử dụng function prototype để mô phỏng lớp (class). Ngày nay, cú pháp class được khuyến khích vì gọn gàng và dễ đọc hơn.

Ví dụ cũ với prototype:

        function Person(name) {
            
        }
        Person.prototype.getName = function () {
            return this.name;
        };
Cách mới với class:

        class Person {
            constructor(name) {
                this.name = name;
            }
            getName() {
                return this.name;
            }
        }
➡️ Lời khuyên: Dùng class để mã ngắn gọn và dễ hiểu hơn.

## Sử dụng trường lớp riêng tư (Private Fields)

Trước đây, người ta dùng dấu gạch dưới _ để báo hiệu rằng thuộc tính là "riêng tư." Tuy nhiên, điều này không đảm bảo tính riêng tư thực sự.

        class Person {
            constructor(name) {
                this._name = name; // Chỉ mang tính ước lệ
            }
        }
        console.log(person._name); // Vẫn truy cập được từ bên ngoài

Hiện nay, JavaScript hỗ trợ trường riêng tư thực sự với ký hiệu #.

        class Person {
            #name;
            constructor(name) {
                this.#name = name;
            }
        }
        console.log(person.#name); // Lỗi: Không thể truy cập từ bên ngoài
➡️ Lời khuyên: Sử dụng # để đảm bảo thuộc tính thực sự riêng tư, giúp mã bảo mật hơn.

## Ưu tiên hàm mũi tên (Arrow Function)
Hàm mũi tên giúp mã ngắn gọn và tự động gắn kết this với phạm vi từ vựng (lexical scope), rất hữu ích khi làm việc với các hàm bậc cao như map, filter, hoặc reduce.

Ví dụ:

        const numbers = [1, 2];
        numbers.map(num => num * 2); // Gọn hơn so với function truyền thống

➡️ Lời khuyên: Dùng hàm mũi tên để mã ngắn gọn và tránh lỗi liên quan đến this.

7. Sử dụng Nullish Coalescing (??)

Trước đây, ta dùng toán tử || để gán giá trị mặc định, nhưng điều này có thể gây lỗi khi giá trị là 0, false, hoặc chuỗi rỗng.

        const value = 0;
        const result = value || 10; // Kết quả: 10 (không mong muốn)
Giải pháp:

        const result = value ?? 10; // Kết quả: 0 (như mong đợi)

➡️ Lời khuyên: Dùng ?? thay cho || để đảm bảo logic chính xác hơn.

## Sử dụng async/await thay cho .then()
Cách cũ với .then() có thể làm mã phức tạp và khó đọc:

        fetch('url')
        .then(response => response.json())
        .then(data => console.log(data))
        .catch(error => console.error(error));

Dùng async/await gọn gàng hơn:

javascript
Copy code
async function fetchData() {
  try {
    const response = await fetch('url');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}
➡️ Lời khuyên: async/await làm mã rõ ràng hơn, dễ đọc và dễ xử lý lỗi.

## Kết luận

Áp dụng các quy tắc tốt nhất trong JavaScript không chỉ giúp mã chạy hiệu quả, mà còn dễ bảo trì và hiện đại hơn. Việc thực hành các quy tắc này sẽ giúp bạn tránh những lỗi không đáng có và tự tin hơn khi làm việc với JavaScript.

