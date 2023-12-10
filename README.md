
Contents
PART 1 DESCRIBING APIS
Chapter 01- Introducing APIs and OpenAPI
1.1 What is an API ecosystem?
1.2 Describing things
1.2.1 Bridget’s task
1.2.2 The potential of Bridget’s solution
1.3 What is OpenAPI?
1.3.1 Example OpenAPI definition
1.4 Where do OpenAPI definitions fit in?
1.5 What is Swagger?
1.6 What about REST?
1.7 When to use OpenAPI
1.7.1 For API consumers
1.7.2 For API producers
1.7.3 For API designers
1.8 This book
Summary
Nhảy cóc tới phần 2 -)))
Part 2 - Design-first
Chapter 09 - Designing a web
Application
9.1 The PetSitter idea
9.2 PetSitter project kickoff
9.2.1 Additional requirements
9.2.2 Team structure
9.2.3 API-driven architecture
9.3 Domain modeling and APIs
9.3.1 Domain modeling for API
9.4 A domain model for PetSitter
9.5 User stories for PetSitter
9.5.2 Collecting user stories
9.5.3 Mapping user stories
Chapter 10 - Creating an API
design using OpenAPI
10.1 The problem
10.1.1 Converting a domain model to OpenAPI
10.2 Creating the schemas
10.2.1 Starting an OpenAPI file with schemas
10.2.2 Referencing common schemas
10.2.3 The User schema
10.2.4 The Job schema
10.2.5 The Dog schema
10.2.6 The JobApplication schema
10.3 The CRUD approach to API operations
10.3.1 Defining API requests and responses
10.3.2 From user stories to CRUD design
10.4 API operations for PetSitter
10.4.1 User operations
10.4.3 JobApplication operations
Summary
Chapter 11 - Building a change workflow around API design–first
11.1 The problem
11.2 Communicating and reacting to change
11.3 GitHub as our workflow engine
11.3.1 A single source of truth
11.3.2 Suggesting a change
11.3.3 Agreeing on a change
11.3.4 A way of viewing changes (based on an older version)
11.4 Tying the GitHub workflow together
11.4.1 Setting up GitHub and the source of truth
11.4.2 Steps in our GitHub workflow
11.5 A practical look at the workflow
11.5.1 Creating and suggesting DELETE /jobs/{id}
11.5.2 Reviewing and accepting changes
11.5.3 Comparing older branches to the latest
Summary
Chapter 12 – Implementing frontend code and reacting to changes
12.1 The problem
12.2 Setting up Prism
12.2.1 Installing Prism
12.2.2 Verifying that Prism works
12.3 Building a frontend based on a mock server
12.3.1 Adding multiple examples into your OpenAPI definition
12.3.2 Using examples in Prism
12.4 Identifying a missing API operation
12.4.1 Due diligence for adding the operation
12.4.2 Designing the new operation
12.4.3 Choosing which mock data response to get from Prism
12.4.4 Formalizing and suggesting the change
Chapter 14 - Integrating
and releasing
the web application
14.1 The problems
14.1.1 Authentication
14.1.2 Organizing code

Designing APIs with Swagger and OpenAPI

brief contents

PART 1 DESCRIBING APIS
Chapter 01- Introducing APIs and OpenAPI

This chapter covers
 Describing an API ecosystem
 What OpenAPI and Swagger are
 When to use OpenAPI
 An overview of this book

Trong chương này, chúng ta sẽ tìm hiểu về thế giới của API và OpenAPI để có cái nhìn tổng quan về các chủ đề được đề cập trong cuốn sách này. Chúng ta sẽ bắt đầu bằng cách xem xét những lợi ích của việc mô tả một API, cách những mô tả này hình thành một phần của một hệ sinh thái API, và nơi mà OpenAPI đóng vai trò. Chúng ta sẽ xem xét một ví dụ về tài liệu OpenAPI và khi nào cần sử dụng OpenAPI trong thực tế. Hãy bắt đầu.

1.1 What is an API ecosystem?

Chúng tôi thích từ "ecosystem". Nó mô tả sự tương tác và mối quan hệ giữa các yếu tố sống và không sống trong một môi trường hoạt động đầy đủ. Chúng tôi thích tưởng tượng về một cái ao đầy ẩm với những chú ếch, cỏ hoang và những viên đá vì một lý do nào đó, nhưng bạn có thể tưởng tượng điều gì đó khác một chút - dù sao, nguyên tắc của một hệ thống tương tác interactive, cộng sinh symbiotic vẫn tồn tại. Nếu chúng ta mượn cough, (khm, có lẽ là ăn cắp steal) nguyên tắc này từ sinh học, chúng ta có thể sử dụng nó để mô tả thế giới của API trong một nhóm hoặc tổ chức organization::
- Những biến đổi, thay đổi đại diện cho các yếu tố chúng ta có thể kiểm soát. Đây là những điều chúng ta tạo ra, chẳng hạn như services, ngăn xếp stack, hoặc mã nguồn code.
- Những thành phần cố định, không sống là những điều hữu ích mà chúng ta có thể hưởng lợi, nhưng không thể thay đổi một cách dễ dàng. Đây là những thư viện libraries và dịch vụ bên ngoài mà chúng ta sử dụng.
- Và, tất nhiên, có môi trường. Nó có thể là internet, mạng nội bộ hoặc một thiết bị nhỏ gắn trên mái nhà của chúng tôi - có thể thậm chí là tất cả chúng.
Tất cả những mảnh ghép này cùng nhau tạo thành một hệ sinh thái đầy đủ. Khi những phần này di chuyển cùng nhau một cách hài hòa, hệ thống của chúng ta lành mạnh và các nhà phát triển, người tiêu dùng và người dùng đều hạnh phúc. Điều quan trọng là cách những tương tác và mối quan hệ này phát triển.

API định nghĩa những gì mỗi dịch vụ có khả năng cung cấp và cách người khác có thể tương tác với dịch vụ đó. Khi chúng ta đảm nhận vai trò của "API designer," công việc của chúng ta là tạo ra những API này cho các dịch vụ một cách tích hợp phản hồi từ người tiêu dùng và đảm bảo rằng các thay đổi được thông báo trước.

Tại sao lại là "API ecosystem" mà không phải là "service ecosystem" hoặc có lẽ chỉ là " ecosystem "? Bạn có thể hỏi như vậy. Trong cuốn sách này, chúng tôi quan tâm đến API, vì vậy tất nhiên chúng tôi sẽ tập trung vào khía cạnh đó. Vì API là những hợp đồng giữ chặt hệ sinh thái, nó không phải là một điểm tập trung không hợp lý. API là một phần rất quan trọng của hệ sinh thái, mà không có nó, các dịch vụ của chúng ta sẽ bị cô lập. Hiểu biết về API mang lại cho chúng ta một góc nhìn toàn diện. Cuốn sách này sẽ tập trung vào API và cách OpenAPI giúp làm cho chúng dễ làm việc hơn.

1.2 Describing things

Nếu chúng ta xem xét hệ sinh thái ecosystem của mình như là các dịch vụ cá nhân individual service, chúng ta sẽ không thể nhìn thấy cách chúng tạo thành một hệ thống hoàn chỉnh. Đó là cách chúng được kết nối với nhau mà mang lại cho chúng ta cái nhìn tổng thể. Khi những dịch vụ thay đổi mà không cập nhật tất cả các phụ thuộc của chúng, hệ sinh thái mất đi tính năng và trong một số trường hợp có thể hoàn toàn hỏng.
Hãy xem một câu chuyện để minh họa ý tưởng này.

1.2.1 Bridget’s task

Bridget được giao nhiệm vụ quản lý một bộ web stack kích thước trung bình. Stack của cô (hoặc hệ sinh thái) bao gồm các dịch vụ giao tiếp và phụ thuộc vào nhau. Stack cũng sử dụng các dịch vụ bên ngoài mà cô không kiểm soát.
Thỉnh thoảng, một trong những API sẽ thay đổi sao cho ảnh hưởng tiêu cực, và đôi khi làm hỏng các dịch vụ phụ thuộc vào nó. Điều này làm gián đoạn hệ sinh thái, làm sập một số phần của bộ ngăn xếp và cuối cùng gây ra sự cố.
Bridget cần giải quyết vấn đề này một cách hiệu quả. Khi một API thay đổi, cô cần có khả năng thông báo trước cho các nhà phát triển bị ảnh hưởng và duy trì hệ sinh thái hoạt động mượt mà.
Bridget dành một khoảnh khắc để suy nghĩ về cách hệ sinh thái này hoạt động. Cô biết rằng mỗi dịch vụ có một API, và mỗi API đó được tạo thành từ các thao tác nhỏ hơn. Mỗi thao tác mong đợi một đầu vào cụ thể và tạo ra một đầu ra tương ứng. Khi một thao tác thay đổi sao cho nó yêu cầu đầu vào khác, bất kỳ dịch vụ nào không thích nghi cùng với nó sẽ dẫn đến một sự cố hệ thống. Tương tự, nếu một thao tác thay đổi để tạo ra một đầu ra khác, nó sẽ khiến các dịch vụ phụ thuộc khác hỏng nếu chúng không được cập nhật để xử lý những thay đổi đó. Bridget kết luận rằng theo dõi sự thay đổi trong API là một phần quan trọng để duy trì chức năng tổng thể. Nhưng làm thế nào cô sẽ biết khi nào một API đã thay đổi?
Bridget quyết định cô cần một cách mô tả API để cô có thể so sánh một API cũ với một phiên bản mới để xem phiên bản mới có bất kỳ thay đổi đột ngột nào hay không. Cô viết một chương trình so sánh mô tả của một API cũ với mô tả của một phiên bản mới, tạo ra một báo cáo. Báo cáo đơn giản và chỉ thông báo cho cô biết liệu API mới có bất kỳ thay đổi đột ngột nào so với phiên bản cũ hay không.
Hài lòng với kế hoạch của mình, cô hướng dẫn các nhà phát triển mô tả API của họ bằng định dạng của cô để cô có thể so sánh giữa cũ và mới. Nhận thức rằng các dịch vụ bên ngoài không dưới sự kiểm soát của cô, cô theo dõi những phát triển đó và mô tả chúng mình—cô cảm thấy sẵn sàng khi những dịch vụ bên ngoài thay đổi.

1.2.2 The potential of Bridget’s solution

Giải pháp của Bridget tập trung vào ý tưởng rằng các API có thể được mô tả, mọi người có thể viết những mô tả này và phần mềm có thể hiểu chúng. Mặc dù cô chỉ sử dụng phương pháp đó để giải quyết một vấn đề cụ thể, nhưng có rất nhiều tiềm năng cho sự phát triển với những mô tả đó. Chúng có thể phục vụ làm cơ sở để tạo ra nhiều thứ hơn chỉ là báo cáo. Ví dụ, cô có thể tạo ra tài liệu, kiểm thử thay đổi trước khi xây dựng chúng, giảm thiểu công đoạn mã boilerplate và nhiều điều khác nữa.
Hãy xem cách giải pháp của Bridget được sử dụng trong thế giới thực. Hãy xem cách OpenAPI hoạt động.

1.3 What is OpenAPI?

OpenAPI quy định một cách để mô tả các API dựa trên giao thức HTTP, thường là các API theo mô hình REST (thêm thông tin về REST sẽ được đề cập sau). Một định nghĩa OpenAPI được biểu diễn dưới dạng tệp YAML hoặc JSON mô tả đầu vào và đầu ra của một API. Nó cũng có thể bao gồm thông tin như API được đặt ở đâu, quyền xác thực nào được yêu cầu để truy cập nó, và các chi tiết khác cần thiết cho người tiêu dùng và người sản xuất (như nhà phát triển web). Định nghĩa có thể được viết bằng tay hoặc bằng các công cụ, hoặc thậm chí có thể được tạo ra từ mã nguồn.
Một khi một API đã được viết xuống, chúng ta nói rằng nó đã được mô tả, và sau đó nó trở thành một nền tảng mà các công cụ và con người có thể sử dụng. Một cách phổ biến để sử dụng định nghĩa API là tạo tài liệu có thể đọc được cho con người từ đó.

1.3.1 Example OpenAPI definition

Dưới đây là một định nghĩa OpenAPI nhỏ gọn để mô tả một hoạt động cụ thể của API chứa thông tin về các giống chó và hình ảnh của chúng. API này được lưu trữ tại https://dog.ceo. Dưới đây là một ví dụ về cách mô tả một API bằng một tệp YAML: OpenAPI
Một định nghĩa OpenAPI có vẻ hơi dài dòng khi bạn nhìn vào lần đầu, nhưng bạn sẽ phát hiện có một số thông tin đặc biệt hữu ích chứa trong đó. Trong ví dụ này, chúng ta có thể tìm hiểu một số điều về phương thức duy nhất mà nó mô tả và cách tiêu thụ nó. Đừng lo lắng nếu bạn chưa thể kết nối giữa tệp YAML và mỗi statement dưới đây. Chúng ta chỉ mới bắt đầu, và chúng ta sẽ từng bước giải mã định nghĩa OpenAPI trong cuốn sách này. Tuy nhiên, dưới đây là những gì chúng ta có thể khám phá trong đoạn mã trước đó:
 API được lưu trữ tại https://dog.ceo/api.
 Có một phương thức GET với đường dẫn /breed/{breedName}/images.
 Đường dẫn này có một phần gọi là breedName, và đó là một chuỗi bắt buộc.
 Một phản hồi thành công sẽ cung cấp cho chúng ta một mảng JSON, trong đó mỗi mục là một đối tượng chứa các trường message và status.
 Trường message là một mảng các chuỗi là các URL của hình ảnh chó.
Đây là thông tin có thể sử dụng. Những nhà phát triển có thể xây dựng client để tiêu thụ API, quản lý sản phẩm có thể xác định xem API phù hợp với nhu cầu và đáp ứng tiêu chuẩn của họ, và nhóm tài liệu có thể sử dụng nó như cơ sở để hiển thị tài liệu có thể đọc được cho người dùng.

Để sử dụng định nghĩa OpenAPI này, chúng ta có thể tải nó vào một công cụ gọi là Swagger UI (chúng ta sẽ thảo luận về điều này sau trong cuốn sách), công cụ này tạo ra tài liệu thân thiện với con người dựa trên định nghĩa và cung cấp những tính năng nhỏ khác. Kết quả sẽ trông giống như hình 1.1.

 

1.4 Where do OpenAPI definitions fit in?

Khi chúng ta có một API definition, chúng ta có thể sử dụng các công cụ để tận dụng chúng, xây dựng các trừ tượng lớn hơn và tạo ra các quy trình tự động hóa hơn. Các định nghĩa Definitions là có thể đọc được bằng máy.
Hình 1.2 cho thấy làm thế nào OpenAPI definitions có thể phù hợp vào quy trình làm việc của tổ chức. Các định nghĩa The definitions có thể được tạo ra bằng các công cụ hoặc bằng cách trích xuất annotations từ mã nguồn. Sau đó, chúng được chuyển đổi thành API documentation, mã nguồn máy chủ server stubs, và SDK máy khách client SDKs. Đây chỉ là một ví dụ. Các quy trình làm việc khác có thể được thiết kế, phụ thuộc vào các trường hợp kinh doanh cụ thể.

 

Các quy trình làm việc khác có thể bao gồm:
- Tự động hóa một số phần của kiểm thử API
- Nhận phản hồi sớm về thiết kế của một API
- Đảm bảo tính nhất quán của API
- So sánh các thay đổi của API qua các phiên bản

The beauty of OpenAPI là một khi bạn có một OpenAPI definition, phần còn lại – the rest (đặt chơi chữ ý định) chỉ là một vấn đề của việc tận dụng nó cho nhu cầu của bạn.

1.5 What is Swagger?

Ở đầu, có Swagger UI và một hướng dẫn khá sơ bộ về việc viết các tệp YAML mô tả API HTTP. Sau đó, nhiều công cụ khác được xây dựng dựa trên hướng dẫn này, mà sau đó nhanh chóng trở thành một specification và một standard. Các công cụ và đặc tả này được gọi chung là "Swagger". Specification trở nên chín muồi hơn và được phát hành mã nguồn mở, khuyến khích cộng đồng tạo ra thêm nhiều công cụ khác nhau. Họ nhanh chóng bắt đầu đóng góp các tính năng cho specification, cuối cùng nó bắt đầu được các công ty lớn áp dụng.
Năm 2015, Swagger được SmartBear chấp nhận, sau đó họ quyên góp phần specification cho Linux Foundation (www.linuxfoundation.org). Trong quá trình chuyển giao đó, đặc tả được đổi tên thành "OpenAPI specification," và SmartBear giữ bản quyền cho thuật ngữ "Swagger."

Ngày nay, kết quả của sự trùng hợp lịch sử này, bạn sẽ thấy các thuật ngữ được sử dụng xen kẽ nhau. Trong tương lai, chúng ta được khuyến khích sử dụng thuật ngữ "OpenAPI" để chỉ specificationcủa hệ sinh thái này - và sử dụng "Swagger" để chỉ các bộ công cụ cụ thể được quản lý bởi SmartBear (bao gồm Swagger UI, Swagger Editor, Swagger Parser và ít nhất một tá công cụ khác). Nhiều công cụ khác cũng được xây dựng để sử dụng OpenAPI.

LƯU Ý: Có một tiêu chuẩn cũ, Web Application Description Language (WADL; phát âm là "waddle"), được lấy cảm hứng từ đặc tả WSDL của SOAP và sử dụng XML. Nó có thể đã được sử dụng thay thế cho Swagger để mô tả API HTTP. Đội ngũ làm việc trên Swagger thường đùa, "Tại sao lại chọn WADL khi có thể chọn Swagger?" Và từ đó, cái tên "Swagger" ra đời.

1.6 What about REST?

REST (Representational State Transfer) là một tập hợp các ý tưởng về cách design networked
systems (đặc biệt là server/client systems). Mặc dù REST không bị hạn chế chỉ đối với các API dựa trên HTTP, nhưng thực tế cho thấy chúng liên kết chặt chẽ. Hiện nay, các API RESTful thường chiếm ưu thế trong hầu hết các web servers trên internet.
Nguyên tắc của REST được mô tả bởi Roy Fielding trong luận án của ông về networked systems, được công bố vào năm 2000 (www.ics.uci.edu/~fielding/pubs/dissertation/top.htm). Việc xác định xem một API có đúng RESTful hay không phụ thuộc vào mức độ tuân thủ ý tưởng (hoặc ràng buộc) của luận án đó. Việc xem xét điều gì được coi là RESTful hay không có phần chủ quan và gây ra những cuộc tranh cãi gay gắt. Trong thực tế, các API based HTTP phải thực hiện các sự đánh đổi giữa những gì chúng đòi hỏi và mức độ tiêu chuẩn hoặc RESTful. Đó là một sự cân bằng mà tất cả các nhà sản xuất API đều phải quản lý.

Các ý tưởng trong REST nhằm mục đích đơn giản hóa và tách rời API khỏi các dịch vụ cơ bản phục vụ API. Nó sử dụng mô hình request-response và stateless, vì tất cả thông tin cần thiết để thực hiện một hành động nằm trong request.
Một trong những ý tưởng chính sau REST là khái niệm về resource. Các thứ như user accounts, thông báo thanh toán billing reminders, hoặc thậm chí là thời tiết ở San Francisco đều là resource, và mỗi resource được xác định bằng một URI. Đối với tài khoản người dùng, chúng ta có thể có URI /users/123, định danh duy nhất một user resource trong API.
Người tiêu dùng sẽ muốn thực hiện các hành động đối với và với các tài nguyên. Hãy nghĩ về những hành động này như là động từ. HTTP có một bộ các động từ được xác định rõ, như POST, GET, PUT, DELETE, và PATCH, tất cả đều phát sinh từ ý tưởng trong REST. Trong HTML, nếu bạn muốn lấy dữ liệu liên quan đến một tài nguyên, bạn sẽ sử dụng phương thức GET. Nếu bạn muốn tạo một tài nguyên mới, bạn có thể sử dụng phương thức POST. Trong chương 10, chúng ta sẽ đi sâu hơn vào cấu trúc URL và động từ HTTP.

Việc xác định nơi REST bắt đầu và HTTP kết thúc là một câu hỏi khó trả lời, nhưng nguyên tắc tổng quát là HTTP là giao thức và REST là một cách thiết kế API. HTTP đã tích hợp nhiều ý tưởng của REST vào giao thức của mình, đó là lý do tại sao chúng liên quan chặt chẽ. Thông thường, chúng ta thường chỉ lưu ý khi một API HTTP không phải là RESTful, có nghĩa là nó không tuân thủ các design pattern được đề cập trong REST.
OpenAPI được thiết kế để mô tả càng nhiều API dựa trên HTTP càng tốt, nhưng không phải tất cả. Ràng buộc chính của nó (và một lợi ích lớn của OpenAPI) là nó được thiết kế để cho phép các công cụ tạo mã có thể sinh ra từ các định nghĩa; điều này đi kèm với sự đánh đổi là không thể mô tả mọi khía cạnh của một API, vì chúng không thể được xác định đủ tốt trong đặc tả cho cả người và máy tính.
A quick note about hypermedia

Trong Fielding’s REST paper, ông đề cập đến ý tưởng về hypermedia: một hệ thống trả về các liên kết nhạy cảm với ngữ cảnh dưới dạng các URIs. Ví dụ, nếu bạn thực hiện một GET trên một resource /users/{userId}, nó có thể trả về một link (một URI) đến hoạt động đăng nhập cho người dùng đó và một liên kết khác để thực hiện đặt lại mật khẩu. Những links liên quan đến tài nguyên (tại điểm thời điểm đó), và chúng tách biệt client khỏi việc cần phải biết các URI đó ngoài phản hồi. Đây chỉ là mô tả tồn tại của một mô hình rất mạnh mẽ.
Nhiều người theo đường chủ nghĩa REST chỉ ra rằng đây là một thành phần đáng chú ý bị thiếu trong các API RESTful. Trong OpenAPI (đặc biệt là phiên bản 3.0.0+), hỗ trợ đã được thêm vào để giúp tài liệu hóa những liên kết hypermedia này, nhưng ngữ nghĩa của chúng không thuộc phạm vi của OpenAPI specificatoin. OpenAPI có thể mô tả những gì được yêu cầu bởi các API hypermedia, nhưng không mô tả những gì mỗi liên kết nên thực hiện. Dưới đây là một số specifications khác cố gắng mô tả những chi tiết đó:

- HATEOAS: https://restfulapi.net/hateoas/
- Siren: https://github.com/kevinswiber/siren/
- Hydra:  https://www.hydra-cg.com/

1.7 When to use OpenAPI

Luôn luôn.
Chúng tôi hy vọng rằng câu tuyên bố đó đã gợi lên hình ảnh của những tác giả mỉa mai. Chúng tôi không thể kiềm chế được tính châm chọc. Nhưng không, giống như tất cả các công nghệ khác, OpenAPI cũng không phải lúc nào cũng cần thiết. OpenAPI mô tả các API dựa trên HTTP (bao gồm cả API RESTful), vì vậy khi bạn được giao nhiệm vụ thiết kế, quản lý và tiêu thụ một API HTTP, sử dụng OpenAPI sẽ mang lại giá trị cho bạn. Nếu bạn đang xử lý các công nghệ API khác không tận dụng ngữ nghĩa HTTP (như các phương thức, URL, tiêu đề và thân bản), OpenAPI sẽ có giá trị hạn chế đối với bạn. Ví dụ về những loại API đó bao gồm gRPC và GraphQL.
Trong phần này, khi chúng tôi nói về API, chúng tôi đang đề cập đến cụ thể các API dựa trên HTTP.
1.7.1 For API consumers

Khi bạn cần tiêu thụ một API, phản xạ đầu tiên của bạn có thể là sử dụng một SDK cho API đó được viết trong ngôn ngữ lập trình của bạn. Nhiều API phổ biến đã quan tâm và đầu tư nỗ lực lớn để đưa các SDK này sẵn có cho người tiêu dùng, nhưng nhiều API khác đơn giản không có tài nguyên để viết SDK cho một hoặc nhiều ngôn ngữ.
Nếu API đã được mô tả bằng OpenAPI (dù là do nhà sản xuất hay do bạn), bạn có thể tạo ra các SDK cho nhiều ngôn ngữ khác nhau. Các mẫu SDK được cung cấp bởi các công cụ như Swagger Codegen hoặc OpenAPI Generator thường là đủ và sẽ giúp bạn có một bắt đầu tốt cho việc phát triển các client. Nhưng bạn có thể tận dụng thêm sức mạnh bằng cách tùy chỉnh và tạo các mẫu đặc biệt cho nhu cầu cụ thể của bạn, mà sẽ hoạt động với bất kỳ API nào được mô tả bằng OpenAPI.

1.7.2 For API producers
Xây dựng API có thể rất thú vị, đặc biệt khi bạn có một hợp đồng để phát triển, nhưng xây dựng phần mở đầu của một máy chủ HTTP trở nên ít thú vị hơn sau khi bạn đã làm điều đó nhiều lần. Tự động tạo mã boilerplate và ghi chú từ định nghĩa OpenAPI mang lại cho bạn sự nhanh chóng và tính nhất quán (vì bạn có thể tùy chỉnh các template theo nhu cầu của mình).
Còn nhiều phương pháp phát triển API thú vị hơn, như sử dụng OpenAPI definition trong runtime để đóng vai trò như một bộ định tuyến router (với các API operations ánh xạ vào các lớp và phương thức trong mã) hoặc như một validation layer (nơi các request đến sẽ thất bại nếu chúng không tuân thủ theo kiểu dữ liệu được xác định trong định nghĩa OpenAPI). Những thực hành như vậy đang trở nên phổ biến hơn trong microservice-oriented architectures, nơi các services được xây dựng nhanh chóng hơn.
1.7.3 For API designers

API design cũng đã được chú ý nhiều hơn gần đây, và tầm quan trọng của nó không thể bị đánh giá thấp. Trong khi chúng tôi là người hâm mộ lớn của các thực hành Agile (chu kỳ phản hồi ngắn) và nghệ thuật thất bại nhanh chóng (đưa sản phẩm nhanh chóng ra thị trường để xác nhận sự thành công hoặc thất bại của chúng), API vẫn nên được thiết kế với tầm nhìn về sự bền vững vì thay đổi chúng có nghĩa là thay đổi người tiêu dùng, điều này thường là ngoài khả năng kiểm soát của bạn. (Không ai thích phải duy trì một API cũ!) OpenAPI là một phương tiện để truyền đạt đến cả người tiêu dùng và người sản xuất, cho phép người thiết kế nhận phản hồi sớm trong quá trình và lặp lại dựa trên phản hồi đó.
Thiết kế trở nên thú vị hơn khi bạn phải quản lý nhiều hơn một API. Trong những trường hợp đó, tính nhất quán consistency đóng một vai trò quan trọng. Việc tiêu chuẩn hóa tất cả các API của bạn theo các mẫu nhất quán consistent patterns trở nên khả thi khi bạn có thể đo lường những patterns đó. Định nghĩa OpenAPI cung cấp một phương tiện đo lường như vậy.

1.8 This book

Cuốn sách này nhằm giúp bạn hiểu cách OpenAPI hoạt động, cách sử dụng nó cùng các công cụ liên quan để thiết kế API, và cách bạn có thể tạo ra các luồng công việc nâng cao và cụ thể cho đội và tổ chức của bạn. OpenAPI hướng đến việc tự động hóa một số phần trong quy trình làm việc của bạn và giải phóng đội của bạn để đạt được nhiều hơn. Chi phí ban đầu nhỏ khi mô tả API bằng OpenAPI được đền đáp đáng kể bởi sức mạnh mà bạn có thể kiểm soát thông qua việc tận dụng nó và những cơ hội mới mà nó mang lại.
Cuốn sách được chia thành ba phần:
- Phần 1: Nói về sự hiểu biết về OpenAPI và giới thiệu bạn về cú pháp và cấu trúc của OpenAPI definition, mang lại khả năng mô tả API cho bạn. Trong suốt phần này, chúng tôi sẽ ghi chép một ví dụ về FarmStall API được lưu trữ trực tuyến và đơn giản đủ để hiểu mà không cần biết chi tiết. Chúng tôi sẽ sử dụng hình vẽ để chỉ ra vị trí của chúng ta trong kế hoạch tổ chức.

 
- Phần 2: Nói về giai đoạn thiết kế và cách chúng ta có thể sử dụng các công cụ để tạo ra một API mới và lặp lại thiết kế của nó. Chúng tôi sẽ thiết kế một API chăm sóc thú cưng từ đầu, cùng với các quy trình xung quanh nó.

- Phần 3: Là một đào sâu sâu hơn vào một số công cụ và luồng công việc cụ thể hơn, đặc biệt là liên quan đến việc phát hành một API cho công chúng.

Summary

- OpenAPI là một specification sử dụng để mô tả các API dựa trên HTTP, đặc biệt là các API RESTful.
- Swagger là một thuật ngữ chỉ một bộ công cụ của SmartBear. Trước đây, nó được sử dụng để chỉ chính OpenAPI specification và đôi khi vẫn được sử dụng như vậy.
- Việc mô tả API bằng cách viết một definition (một tệp YAML) cho phép bạn tận dụng các công cụ để tự động hóa nhiều quy trình liên quan đến API.
- OpenAPI hữu ích cho consumer, producer và API designer. Mỗi người đều có thể hưởng lợi từ việc biết và sử dụng các công cụ tiêu thụ OpenAPI definition.
- Cuốn sách này sẽ giải thích cách làm việc với OpenAPI. Với cơ sở kiến thức này, bạn có thể tích hợp OpenAPI vào luồng công việc của đội và tổ chức của mình.

Nhảy cóc tới phần 2 -)))

Part 2 - Design-first

Phần 2 bắt đầu từ đầu bằng cách giới thiệu một sản phẩm mới, với mục tiêu thiết kế API từ đầu, thay vì tài liệu hóa một API hiện tại như chúng ta đã làm trong phần 1. Chúng ta sẽ làm việc với một sản phẩm phần mềm hư cấu dành cho chủ nhân thú cưng cần thuê người trông nom cho đồng hành của họ khi họ vắng nhà - chúng tôi đã đặt tên cho nó là PetSitter với cái tên cực kỳ sáng tạo. Tình huống này cung cấp chủ đề nền cho phần còn lại của cuốn sách. Chúng tôi cũng sẽ giới thiệu về công ty và ba nhân vật mẫu sẽ giúp chúng ta hiểu rõ các vai trò chủ đạo trong quá trình thiết kế API.
Bộ công nghệ cho PetSitter được chia thành một phần backend (máy chủ) và một phần frontend (trang web) giao tiếp thông qua API.
Phần này của cuốn sách mở đầu bằng việc xác định defining các requirements, xem xét user stories và domain modeling (chương 9). Nó tiến triển bằng cách lấy những models đó và thiết kế một API sử dụng OpenAPI (chương 10). Các chủ đề trong quá trình thiết kế bao gồm quy trình thay đổi change workflow (chương 11), giả mạo mocking với Prism (chương 12), tạo ra server stubs với Swagger Codegen (chương 13) và tích hợp hai thành phần này thành một working system (chương 14).
Mỗi chương xây dựng trên chương trước, vì vậy chúng tôi khuyến khích đọc các chương này theo thứ tự.

Chapter 09 - Designing a web
Application
This chapter covers:
 Các mục tiêu, kịch bản và kế hoạch cho phần thứ hai của cuốn sách này.
 Tạo domain model cho ứng dụng PetSitter.
 Thêm chức năng vào domain model với các use stories.


Trong phần đầu của cuốn sách này, chúng ta đã đi qua các kiến thức cơ bản về API, cách sử dụng chúng và cách mô tả chúng một cách hình thức bằng OpenAPI. Chúng ta cũng đã làm việc với Swagger Editor để tài liệu hóa một API hiện tại - FarmStall API - bằng cách sử dụng OpenAPI. Bây giờ, trong phần thứ hai của cuốn sách này, chúng ta sẽ thiết kế một API mới cho một ứng dụng web từ đầu. Qua quá trình thiết kế API và qua toàn bộ vòng đời của API không chỉ là về việc sử dụng OpenAPI và các công cụ khác. Điều này cũng liên quan đến con người và quy trình. Luôn có yêu cầu mới và các tình huống không dự đoán được cần phải xử lý. Chúng tôi đã cố gắng làm cho phần thứ hai của cuốn sách này gần với thực tế nhất bằng cách làm việc thông qua quá trình với một công ty hư cấu.

Chúng ta sẽ bắt đầu với một người sáng lập tưởng tượng một ý tưởng và tổ chức một đội. Cùng nhau, họ sẽ tạo ra một kế hoạch để thực hiện dự án bắt đầu từ một domain model và user stories, tiếp theo là thiết kế API, và kết thúc bằng việc triển khai và tích hợp phần mềm. Chúng tôi sẽ giải thích những phương pháp này khi chúng ta tiến qua quá trình.

9.1 The PetSitter idea
José. Anh ấy là chủ một công ty phát triển web nhỏ. Mặc dù anh ấy kiếm được nhiều tiền từ việc thiết kế các trang web và ứng dụng web tùy chỉnh, nhưng anh ấy luôn suy nghĩ về việc phát triển doanh nghiệp của mình và bắt đầu một sản phẩm riêng. Và anh ấy đã có một ý tưởng kinh doanh.
José và vợ anh ấy là người yêu thú cưng, nhưng cả hai đều đang làm việc full time và không muốn để chó của họ ở nhà một mình. Đôi khi José mang theo chú chó đến văn phòng, nhưng điều đó không phải lúc nào cũng là một lựa chọn. Ngay cả khi có, có ai đó cũng cần đưa chó đi dạo khi José bận rộn như các chủ doanh nghiệp thường có thể. Việc tìm ai đó để chăm sóc chó là một công việc mà José và vợ anh ấy muốn đơn giản hóa. Tại sao không có ứng dụng cho việc đó?
Sau khi suy nghĩ về ý tưởng một chút, José lấy ra một quyển sổ và ghi chép một bộ requirements ban đầu cho chức năng của ứng dụng:
- Đăng ký Sign up: làm dog owner or dog walker.
- Dog owners có thể đăng công việc.
- Dog walkers có thể nộp đơn cho công việc đã đăng.
Mặc dù José chỉ nghĩ về chó, anh ấy quyết định sử dụng tựa đề là "PetSitter" (thay vì "DogSitter") như là tiêu đề làm việc cho dự án của mình. Với tiêu đề đó và một danh sách yêu cầu chức năng, José cảm thấy anh ấy đã sẵn sàng để bắt đầu.

9.2 PetSitter project kickoff
Để chuyển từ business of project idea thành một working produce đòi hỏi sự thực hiện. José có một nền tảng kinh doanh và không phải là một nhà phát triển, vì vậy anh ấy cần xây dựng một đội ngũ để triển khai ứng dụng của mình. May mắn thay, anh ấy có thể tận dụng đội ngũ nhân viên của mình.
Tuy nhiên, chỉ việc tập hợp một đội ngũ là chưa đủ. Mỗi dự án cũng cần một kế hoạch để mọi thành viên trong đội biết họ cần làm gì. Hãy cùng tham gia với José trong việc xây dựng đội và phác thảo kế hoạch của họ.

9.2.1 Additional requirements

Trong khi suy nghĩ về các nguồn lực mà anh ấy có để thực hiện kế hoạch, José thêm các ghi chú sau:
- Build web app với đội ngũ nội bộ - hai người.
- Mobile app - hợp tác với một công ty phát triển khác (sau này!).
- Cơ hội thử nghiệm với công nghệ mới.
- Phát hành phiên bản nguyên mẫu prototype hoạt động đầu tiên càng sớm càng tốt.

Khác với các functional requirements mà anh ấy đã viết xuống, các nonfunctional requirements này không trực tiếp liên quan đến chức năng của ứng dụng, mà thay vào đó đề cập đến những đặc điểm khác nhau của sản phẩm cũng như các hạn chế xung quanh quá trình phát triển.
Khi chúng ta tiến triển, chúng ta sẽ kiểm tra thường xuyên để xem liệu kế hoạch của chúng ta có phù hợp với các yêu cầu hay không, với một bảng tóm tắt như bảng 9.1.

Type	Requirement	In plan?
Functional	Sign up: as a dog owner or dog walker	
Functional	Dog owners can post jobs.	
Functional	Dog walkers can apply for posted jobs.	
Nonfunctional	Build web app với đội ngũ nội bộ - hai người.	
Nonfunctional	Mobile app - hợp tác với một công ty phát triển khác (sau này!).	
Nonfunctional	Cơ hội thử nghiệm với công nghệ mới.	
Nonfunctional	Phát hành phiên bản nguyên mẫu prototype hoạt động đầu tiên càng sớm càng tốt.
	

9.2.2 Team structure
José đi qua danh sách nhân viên của mình và xem xét kỹ năng cũng như loại dự án mà họ đang tham gia vào lúc này. Sau đó, anh ấy sắp xếp một cuộc họp với hai người trong số họ, Nidhi và Max. Cả hai nhà phát triển đã làm việc với José một thời gian và đã thể hiện khả năng học hỏi và giải quyết vấn đề một cách độc đáo.
Cả hai đồng ý tham gia dự án, vì vậy chúng ta có một đội ba người. Là người sáng tạo, José đóng vai trò làm trưởng dự án. Các vai trò của các nhà phát triển chưa được định rõ.
Trong cuộc họp đầu tiên của họ, José trình bày kế hoạch dựa trên ghi chú của mình về yêu cầu chức năng và phi chức năng. Nidhi nói với anh ấy rằng nếu họ muốn mở rộng vào lĩnh vực di động sau này, họ nên làm việc trên sự phân tách rõ ràng giữa backend và frontend. "Như vậy," cô ấy nói, "chúng ta có thể có một backend với một API mà các khách hàng khác nhau, chẳng hạn như ứng dụng web của chúng ta và sau đó là ứng dụng di động, có thể sử dụng!" "Tuyệt vời," Max nói một cách hứng khởi. "Sau đó, chúng ta có thể xây dựng một SPA, một ứng dụng trang duy nhất. Tôi đã thử nghiệm với React gần đây và tôi nghĩ chúng ta có thể sử dụng nó ở đây!"
Ba người tiếp tục nói chuyện và mọi người đều hứng thú với dự án. "Tuy nhiên, José," Nidhi thêm, "nhớ rằng tôi có vài khách hàng để hỗ trợ. Chúng ta nên cố gắng làm việc độc lập và không đồng bộ nhiều nhất có thể. Chúng ta không thể luôn gặp nhau để đồng bộ." Max gật đầu đồng tình, "Tôi cũng vậy." Trong cuộc thảo luận này, các nhà phát triển đề xuất một kiến trúc trong đó backend và frontend là hai thành phần được phát triển độc lập, và Max đã có một đề xuất về công nghệ cho phần frontend.

Trước khi chúng ta tiếp tục, hãy xem xét ý nghĩa của frontend và backend trong ngữ cảnh của một ứng dụng web:
- Frontend: Là mọi thứ xảy ra trên máy tính của người dùng trong trình duyệt của họ. Frontend được tạo bằng HTML, sử dụng JavaScript để tương tác. Max đã nói về React, đó là một framework JavaScript để tạo giao diện người dùng ứng dụng web.
- Backend: Là mọi thứ xảy ra trên máy chủ của ứng dụng web, ở bất kỳ nơi đặt máy chủ nào. Backend có thể sử dụng nhiều ngôn ngữ lập trình và framework khác nhau, và thường sử dụng cơ sở dữ liệu để lưu trữ dữ liệu.

Sự thiết lập và sự quan tâm cũng như sự sẵn có của các nhà phát triển dẫn tự nhiên đến một cấu trúc đội với một nhà phát triển frontend và một nhà phát triển backend:
- Nidhi triển khai backend.
- Max triển khai frontend.
Yêu cầu phi chức năng đầu tiên của José về việc có thể xây dựng ứng dụng với hai nhà phát triển đã được đáp ứng. Chúng ta sẽ xem xét chi tiết hơn về công nghệ và quy trình xây dựng mỗi phần sau trong cuốn sách này.

9.2.3 API-driven architecture

Đôi mắt của José sáng lên khi nghe từ "API" đến từ miệng Nidhi. Đội của anh ấy đã tích hợp một số API vào các client projects, chẳng hạn như APIs để gửi thông báo qua SMS, hoặc tích hợp dữ liệu thương mại điện tử, hoặc cho tự động hóa tiếp thị. Tuy nhiên, cho đến nay, họ chưa xây dựng API của riêng mình. "Chúng ta có thể phát hành API sau này để mọi người có thể xây dựng các ứng dụng," anh ấy đề xuất. "Có thể là một thiết bị thông minh nào đó cho phép người chăm sóc thú cưng của tôi tự động vào? Hoặc một cái gì đó cho trợ lý giọng nói của tôi?"
Với tất cả những gì có thể thực hiện với kiến trúc dựa trên API API-driven architecture, yêu cầu thứ hai của anh ấy về việc có thể làm việc với một công ty ngoại vi để xây dựng ứng dụng di động dễ dàng được đáp ứng. Và yêu cầu thứ ba về việc thử nghiệm công nghệ mới cũng được đáp ứng, vì đây là lần đầu tiên công ty của José sẽ xây dựng một API của riêng họ. Chúng ta có thể cập nhật danh sách requirements của mình như trong bảng 9.2.

 

Các ứng dụng web truyền thống chạy mã backend để động lực hóa HTML cho phía frontend. Tuy nhiên, trong kiến trúc dựa trên API, frontend tạo HTML bằng mã JavaScript chạy trên máy khách dựa trên các phản hồi API từ backend, thường là ở định dạng JSON. Như vậy, backend không liên kết với logic trình bày trên máy khách (xem hình 9.1).  

9.2.4 The plan
Trong setup của chúng tôi với API-driven architecture, các nhà phát triển backend và frontend có thể làm việc độc lập, nhưng điều này đòi hỏi họ đồng thuận về API trước. Như bạn biết từ việc đọc cuốn sách này, bạn có thể sử dụng OpenAPI để tạo mô tả chính thức của một API. Và, như bạn sẽ học khi chúng ta tiến triển, có các công cụ có thể giúp bạn xây dựng ứng dụng dựa trên một mô tả OpenAPI.

Chúng ta có một đội ngũ bây giờ, và chúng ta có kiến trúc cơ bản của phần mềm. Điều thiếu sót là một kế hoạch. Mục đích của kế hoạch là đưa đội từ ý tưởng đến việc triển khai. Vì có hai phần của việc triển khai mà các nhà phát triển đang xử lý một cách độc lập, kế hoạch cần bao gồm bước ngay lập tức là thiết kế API. Làm cơ sở của API design, đội cần tạo một domain model. Chúng ta sẽ tìm hiểu về điều đó trong một ít phút.
Khi tổng hợp mọi thứ lại, đội viết xuống các bước hành động sau đây:
1. Đội sẽ cùng nhau tạo một domain model.
2. Max sẽ tạo bản nháp đầu tiên của API design. 
3. Nidhi sẽ xem xét bản nháp đó.
4. Cả hai sẽ hoàn thiện specification, hoặc chỉnh sửa và xem xét lại nếu cần thiết.
5. Cả hai sẽ làm việc độc lập trên các phần triển khai của họ.
6. Sau khi hoàn thành, họ sẽ tích hợp mã của mình vào một ứng dụng.
Chúng ta sẽ tuân theo kế hoạch này và đi qua tất cả các bước trong chương này và các chương sắp tới của cuốn sách này. Hình 9.2 minh họa quy trình, với các con số trong biểu đồ tham chiếu đến các chương khác nhau. Như bước đầu tiên của chúng ta, chúng ta sẽ tập trung vào domain model.

 

9.3 Domain modeling and APIs

Domain model là gì???
Domain model là quá trình lấy được một problem domain (một lĩnh vực các cái sự liên quan, quan hệ, vấn đề, area of interest). Từ domain model tạo ra một description có thể được triển khai trong phần mềm máy tính. Một [domain] model là một nhóm các khái niệm và mối quan hệ giữa chúng. Bởi vì model là trừu tượng, chúng cho phép chúng ta nói về bất kỳ vấn đề nào trong thế giới thực mà chúng ta muốn. Chúng ta có thể nói về một con chó mà không cần lo lắng ban đầu về điều gì làm cho một con chó trở thành một con chó.
Trong các phần sắp tới, chúng ta sẽ trước tiên xem xét về domain model nói chung. Sau đó, chúng ta sẽ thảo luận về các điều cụ thể mà chúng ta cần xem xét nếu muốn tạo ra một domain model hoạt động tốt với một API. Như bước thứ ba, chúng ta sẽ nhìn lại FarmStall API từ phần 1 của cuốn sách này, mà có một domain model ngay cả khi chúng ta không mô tả rõ nó như vậy. Hình 9.3 cung cấp một cái nhìn sơ bộ về cái mà domain model của chúng ta sẽ trông như thế nào ở cuối chương này. Trong đó, bạn sẽ thấy một số khái niệm và mối quan hệ giữa chúng.
Để tạo ra một domain model, chúng ta ánh xạ các concepts từ thế giới thực vào một biểu diễn trừu tượng. Chúng ta gọi biểu diễn này là một model, mặc dù chúng ta hoàn toàn nhận thức được rằng điều này tạo ra một số mơ hồ - thuật ngữ "model" có thể ám chỉ sự biểu diễn của một khái niệm duy nhất single concept (ví dụ, "Dog Model") hoặc của toàn bộ lĩnh vực quan tâm (domain model).
LƯU Ý: Chúng tôi thường sử dụng chữ thường (ví dụ, "dog") để chỉ đến khái niệm trong thế giới thực và viết hoa tên các model ("Dog"). Bạn có thể coi concept như thứ gì đó trong thế giới thực và model là thứ chúng ta sẽ có trên giấy, mặc dù đôi khi chúng tôi có thể sử dụng từ "concept" cho biểu diễn này nốt, để tránh việc sử dụng từ "model" cho cả hai ý nghĩa trong cùng một câu. Ngôn ngữ là tuyệt vời!
 
Mỗi model của một concept có các thuộc tính và mối quan hệ với các model khác cũng như các hành động hoặc hành vi. Thuộc tính là dữ liệu mô tả concept, chẳng hạn như tên, và các hành động là những điều mà concept có thể làm hoặc những điều mà người dùng có thể làm với concept đó. Một domain model không phụ thuộc vào một cài đặt kỹ thuật cụ thể, và chúng ta có thể biểu diễn nó theo cách khác nhau. Trong chương này, chúng ta sẽ sử dụng biểu diễn văn bản dưới dạng danh sách đánh dấu và biểu diễn hình ảnh thông qua các hình được loosely dựa trên Unified Modeling Language (UML). Trong hình thức này của biểu diễn, mỗi model là một hộp với ba khu vực. Hộp trên cùng chứa tên, hộp giữa chứa các thuộc tính và hộp dưới cùng chứa functional. Mũi tên giữa các hộp này tượng trưng cho mối quan hệ giữa các model tương ứng.
Bạn đã thấy biểu diễn này trong hình 9.3. The diagram chứa các thuộc tính attribute, hành động actions và mối quan hệ relationship mà chúng ta sẽ xác định khi chúng ta đi qua chương này. Đối với một ví dụ domain model tổng quát hơn, bao gồm hai biểu diễn concept và mối quan hệ của chúng, hãy xem hình 9.4.

 
Other applications of models 
Các model xuất hiện ở mọi nơi trong lĩnh vực máy tính, tuy nhiên ở các hình thức khác nhau. Trong lập trình hướng đối tượng (OOP), ví dụ, chúng xuất hiện dưới dạng các class. Trong cơ sở dữ liệu quan hệ (như MySQL hoặc PostgreSQL), chúng xuất hiện dưới dạng các table. Luôn có những khác biệt nhỏ, nhưng ý tưởng chung vẫn giữ nguyên. Mặc dù việc tạo mối liên kết giữa các triển khai hiện tại và những gì bạn sắp học về domain model cho API có thể hữu ích, nhưng điều đó không quan trọng để hiểu các phần tiếp theo. 

9.3.1 Domain modeling for API

Việc tạo một domain model cho một API là một công việc quan trọng. Một class hoặc relationship database chủ yếu là một chi tiết triển khai có liên quan đến những người xử lý bên trong. Ngược lại, một API có sự tương đồng hơn với view layer của một ứng dụng. Nó là ranh giới được xác định rõ ràng giữa các phần của một hệ thống, và nó có thể tiềm ẩn làm tăng lớp trừu tượng và che giấu sự phức tạp ở bên dưới. Một người thiết kế API luôn nên nhìn vào API từ góc độ của khách hàng và không phải máy chủ.
Theo quan điểm hướng tới khách hàng client-side perspective này, nhóm của José đã thực hiện một điều có thể coi là thực hành tốt khi thiết kế API cho các ứng dụng web: họ giao cho Max, nhà phát triển frontend, trách nhiệm của bản nháp đầu tiên. Anh ấy không phải là người xây dựng API mà là người sử dụng nó.

A word on autogenerating API domain models
Nếu bạn có kinh nghiệm trước đó với các ứng dụng web dựa trên cơ sở dữ liệu có kích thước trung bình hoặc lớn và các framework được sử dụng để xây dựng chúng, bạn có thể biết rằng bạn cần tạo ra các biểu diễn khác nhau cho domain của mình. Bạn sẽ có các classes trong layer ứng dụng của bạn, và bạn sẽ có các bảng trong cơ sở dữ liệu của bạn. Và tùy thuộc vào cách ứng dụng được xây dựng, có thể có một sự dịch chuyển thủ công giữa chúng hoặc một hệ thống tự động gọi là một object-relationship mapper (ORM). API có thể được coi là third layer với domain model của riêng nó.
Bạn có thể cảm thấy cám dỗ tìm cách tránh thiết kế API cho một ứng dụng hiện tại và tự động kết nối với các tầng khác. Hãy cẩn trọng! Chúng tôi sẽ giải thích sau trong cuốn sách này tại sao đây là lãnh thổ nguy hiểm. Tuy nhiên, ở đây, chúng tôi đang bắt đầu từ đầu mặc dù.
9.3.2 Looking back on FarmStall
Trong phần đầu của cuốn sách này, bạn đã tìm hiểu về OpenAPI sử dụng API FarmStall như là một ví dụ cơ bản. Domain model của nó là gì? Như đã đề cập trước đó, chúng ta chưa bao giờ nói rõ về một domain model, nhưng chúng ta có thể suy luận ra các concepts của problem domain bằng cách xem xét API description.
Hai concepts xuất hiện trong phiên bản cơ bản của API FarmStall là user và review. Hãy xem xét những khái niệm này và suy nghĩ về chúng theo các thuộc tính, mối quan hệ và hành động.Người dùng có ba thuộc tính: username,password và fullname. Họ cũng có khả năng đăng ký (xem hình 9.5).
 
Reviews có ít nhất ba thuộc tính: rating, message và một UUID. Nếu chúng không ẩn danh, chúng cũng có một user ID. Trong OpenAPI description, đó là thuộc tính thứ tư. Do đó, vì nó là một tham chiếu đến một concept khác, tuy nhiên, trong một domain model, chúng ta sẽ không bao gồm nó như là một thuộc tính mà thay vào đó mô tả một mối quan hệ giữa user và rating. Rating cũng có thể được tạo và truy xuất. Đối với việc truy xuất, có thể lấy tất cả các đánh giá, tùy chọn được lọc theo đánh giá, hoặc lấy một đánh giá duy nhất dựa trên ID của nó (xem hình 9.6).
 
Mà không cần biết đến nó, bạn đã tạo ra một biểu diễn của domain model này trong OpenAPI, sử dụng JSON Schema cho các thuộc tính và đường dẫn API cho các hành động. Ngay bây giờ, chúng ta đã lấy  API  description này và tạo ra một domain model từ nó.
Trong chương tiếp theo, chúng ta sẽ đảo ngược quá trình này. Chúng ta sẽ lấy domain model PetSitter và biến đổi nó thành OpenAPI.

9.4 A domain model for PetSitter

José, Nidhi và Max gặp nhau lần thứ hai. José nhắc nhở họ về yêu cầu phi chức năng thứ tư và cuối cùng của mình, nơi ông nói rằng ông muốn có một prototype hoạt động càng sớm càng tốt. Prototype này nên có thể sử dụng và mang lại giá trị cho người dùng nhưng không chứa bất kỳ chức năng không quan trọng nào. Bằng cách tập trung vào những điều cần thiết của ứng dụng, nhóm có thể tạo ra một domain model, API và triển khai đơn giản hơn.



9.4.1 Concepts in the model
Là bước đầu tiên, nhóm liệt kê tất cả các concept mà domain model của họ có thể chứa:
- Chủ thú cưng và người giữ thú cưng sử dụng ứng dụng, vì vậy chúng ta cần một model User.
- Vì chủ thú cưng đăng job và người giữ thú cưng nộp đơn cho chúng, chúng ta có thể cần một model Job.
- Các công việc liên quan đến chó, nên có thể chúng ta cũng cần một Dog model.
Chúng ta sẽ xem xét ba models này (xem hình 9.7) và liệt kê các thuộc tính và mối quan hệ của chúng.

 
9.4.2 The User model
Một user xuất hiện trong gần như mọi domain model. Điều đó không có nghĩa là model User luôn giống nhau. Các thuộc tính, hành động và mối quan hệ có thể thay đổi đáng kể, tùy thuộc vào trường hợp sử dụng. Trong PetSitter, chúng ta đã nói về hai loại user: pet owners and pet sitters. Mô hình của chúng ta cần phải tích hợp điều đó bằng cách bao gồm một role attribute.
Ngoài hai roles đã đề cập, chúng ta có thể có các quản trị viên administrators giữ vai trò quản lý toàn bộ thị trường marketplace. Việc bao gồm vai trò này và suy nghĩ về các nhiệm vụ quản trị sẽ xảy ra trong ứng dụng luôn hữu ích, ngay cả khi chúng không phải là một phần của bộ tính năng của người dùng thông thường.
Nhóm thu thập các thuộc tính sau đây trên bảng trắng của họ:
- Email address
- Password
- Full name
- User’s role: pet owner, pet sitter, or admin
User role attribute dẫn đến một chút thảo luận trong nhóm của chúng ta, tập trung vào câu hỏi sau: "Mỗi người dùng có một vai trò duy nhất hay họ có thể có nhiều vai trò?" José tin rằng một người có thể có một con thú cưng hoặc muốn chăm sóc các con thú cưng khác. Max đồng ý rằng các trường hợp nơi một người có thể muốn làm cả hai là hiếm gặp. "Tuy nhiên," anh ta lập luận, "trong những trường hợp hiếm này, việc phải đăng ký hai lần cho cùng một ứng dụng sẽ làm phiền." Một câu hỏi như vậy có vẻ như là nhỏ nhưng không chỉ thay đổi trải nghiệm người dùng mà còn yêu cầu các biểu diễn khác nhau bên trong API. Và đây là những thay đổi có thể phá vỡ breaking changes. Đây là một lời nhắc khác về việc quan trọng của việc có được domain model chính xác. Cuối cùng, nhóm quyết định hỗ trợ nhiều vai trò.
Từ góc nhìn của một nhà phát triển backend, Nidhi đưa ra một đề xuất khác: "Một địa chỉ email có thể thay đổi, nhưng định danh người dùng không nên phải. Chúng ta có thể thêm một thuộc tính ID." Nhóm đồng ý và thêm "ID" vào danh sách của họ. Hình 9.8 cho thấy mô hình Người dùng kết quả.
 

9.4.3 The Job and Dog models
José yêu cầu nhóm nhà phát triển ý tưởng: "Nếu tôi yêu cầu bạn chăm sóc chó của tôi và hãy tưởng tượng đây là lần đầu tiên và bạn chưa gặp nó, bạn muốn biết gì?" Việc đặt câu hỏi như vậy trong quá trình domain modeling giúp chúng ta phải nhìn vào model từ góc độ của một new application user.
Anh ấy cũng nhắc nhóm rằng họ nên giữ mọi thứ đơn giản và, mặc dù tên là PetSitter, họ có thể hạn chế model chỉ đến chó trong lúc này. Nhìn thấy sự phức tạp tiềm ẩn của một model thú cưng chung hơn, nhóm đồng ý. (Như tác giả, chúng tôi cũng rất hạnh phúc với quyết định đó, vì chúng tôi không muốn đào sâu quá mức vào domain model phức tạp ngay bây giờ, tại chi phí của các khía cạnh khác của API design.)

Nidhi và Max viết lại suy nghĩ của họ, so sánh ghi chú và trình bày danh sách chung sau đây cho José:
- Khi công việc bắt đầu và kéo dài bao lâu?
- Bạn muốn tôi làm gì? Đi dạo, chăm sóc chó tại nhà, hoặc điều gì khác?
- Ai là chó? Tên, tuổi, giống, v.v.?

Hai câu hỏi đầu tiên dẫn đến một danh sách thuộc tính cho công việc:
- Thời gian bắt đầu
- Thời gian kết thúc
- Hoạt động

Thay vì thời gian bắt đầu và kết thúc, một khả năng khác có thể là bao gồm thời gian bắt đầu và thời lượng. Cả hai phiên bản đều truyền đạt cùng một thông tin. Cũng giống như model User, chúng ta sẽ thêm một ID để có thể xác định duy nhất mỗi công việc được đăng trên PetSitter. Hình 9.9 cho thấy mô hình Job kết quả.
 

Câu hỏi thứ ba dẫn đến một danh sách thuộc tính cho chó:
- Tên
- Tuổi (theo năm)
- Giống
- Kích thước (trong trường hợp mọi người không quen với giống chó)

Hình 9.10 thể hiện mô hình Chó.
 
Tại điểm này, chúng ta đã ánh xạ three concepts vào domain model của chúng ta, nhưng chỉ xem xét về thuộc tính của chúng. Chúng ta sẽ để lại domain model ở trạng thái hiện tại và hoàn thiện nó sau, sau khi xem xét ứng dụng thông qua góc độ của các user stories.

9.5 User stories for PetSitter

Để hoàn tất domain model và bắt đầu triển khai ứng dụng PetSitter, chúng ta cần thảo luận về các kết nối giữa các models và các actions mà chúng có thể thực hiện, hoặc có thể được thực hiện trên chúng. Nhóm quyết định viết user stories để làm điều đó. Đầu tiên, chúng ta sẽ giới thiệu user stories như một công cụ instrument để mô tả chức năng ứng dụng, sau đó thu thập các stories cho PetSitter, và cuối cùng hợp nhất kết quả với domain model.
9.5.1 What are user stories?
User stories là một phương pháp quản lý dự án không chính thức để phân tích requirements trong quá trình phát triển phần mềm. Mỗi user story được viết từ góc nhìn perspective của người sử dụng một sản phẩm phần mềm và mô tả một hoạt động mà họ thực hiện trong phần mềm để đạt được một điều gì đó. Thông thường, user story được viết với một biểu mẫu như sau:
As a <role> I can <capability>, so that <receive benefit>. Biểu mẫu này bao gồm một vai trò, điều này làm cho nó hoạt động tốt trong các ứng dụng nơi người dùng có các vai trò khác nhau với các khả năng khác nhau. Mệnh đề " so that " không bắt buộc và cung cấp thông tin nền về mục đích của user story.
Đối với những user stories phụ thuộc vào những stories khác, chúng ta có thể sử dụng biểu mẫu này:
Given <prerequisite>, I can <capability>. 
 (As a pet owner I can post a pet-sitting job, so that I can go on holiday.)
Với tư cách là chủ nhân thú cưng, tôi có thể đăng một công việc trông nom thú cưng, để tôi có thể đi nghỉ.
 (Given that I posted a job, I can view its status.)
Cho trước rằng tôi đã đăng một công việc, tôi có thể xem trạng thái của nó.

9.5.2 Collecting user stories
Chúng ta đã thấy rằng user stories hỗ trợ các vai trò và có ba vai trò trong PetSitter: pet owner, pet sitter, and admin. Thật ý nghĩa khi xem xét từng cái một cách riêng biệt, và với một nhóm đa người, chúng ta có thể chia công việc tư duy và viết user stories. Trong đội ngũ PetSitter, José nhìn nhận từ góc nhìn của một pet owner, và Max đặt mình vào vị trí của một pet sitter. Trong khi đó, Nidhi nghiên cứu về vai trò của admin.
Để giữ cho câu chuyện ngắn gọn, chúng ta sẽ trình bày chúng trong các danh sách riêng biệt và loại bỏ tiền tố " as a <role> ". Các danh sách sau đây sẽ là một bảng tổng quan. Chúng ta sẽ xem xét kỹ hơn từng user story đó, khi ánh xạ chúng với các hành động và mối quan hệ cho domain model.

Dưới đây là kết quả của José cho vai trò pet owner:
 I can register a new account and choose my role, so that I can log in. 
 I can log in to my account, so that I can use the marketplace.
 I can post a job on PetSitter, including a description of one of my dogs, so that
pet sitters can apply.
 I can see a list of jobs I have posted.
 Given that I have posted a job, I can view and modify its details.
 Given that I have posted a job, I can delete it.
 Given that I have posted a job, I can see the pet sitters that applied.
 Given that I have found a suitable candidate, I can approve them.
 I can modify my account details.
 I can delete my account.

Dưới đây là kết quả của Max cho vai trò pet sitter:
 I can register a new account and choose my role, so that I can log in.
 I can log in to my account, so that I can use the marketplace.
 I can view a list of pets that need looking after.
 Given that I have found a job, I can apply for it. 
 I can modify my account details.
 I can delete my account. 

Dưới đây là kết quả của Nidhi cho vai trò administrator:
 I can log in to my account, so that I can access the admin functionality.
 I can modify my account details.
 I can modify other users’ account details.
 I can edit jobs that other users have posted.
 I can delete users.

Bốn trong số các user stories (những stories được in đậm) trực tiếp tương ứng với các functional
Requirements mà José đã ghi chú ban đầu, vì vậy có vẻ như đội của anh ấy đang trên đúng đường để xây dựng ứng dụng mà anh ấy muốn. Chúng ta có thể đánh dấu chúng trong requirements
checklist (xem bảng 9.3).

 
Sau khi thu thập tất cả các stories, chúng ta có thể nghiên cứu chúng và cập nhật model của mình khi cần thiết.
9.5.3 Mapping user stories
Trước đó, chúng ta đã tạo ba models: User, Job và Dog. Tất cả chúng đã có một tập hợp các thuộc tính. Để tìm hiểu về chức năng và mối quan hệ của chúng, chúng ta nên đi qua các user stories và xem xét xem chúng ảnh hưởng đến model nào. Nếu chúng chỉ ảnh hưởng đến một trong các model, chúng ta có thể thêm một hành động vào model đó. Nếu chúng ảnh hưởng đến nhiều model, chúng ta cũng phải xem xét chúng từ góc độ mối quan hệ.
Để bắt đầu, chúng ta sẽ xem xét những user stories đó là giống nhau hoặc tương tự cho nhiều vai trò.
I CAN REGISTER A NEW ACCOUNT AND CHOOSE MY ROLE
User story này xuất hiện đối với cả chủ nhân thú cưng và người chăm sóc thú cưng. Register là một tiên quyết để sử dụng ứng dụng và nó độc lập với bất kỳ công việc nào. Đối với mô hình User, chúng ta có thể suy ra hành động " Register " từ nó.
I CAN LOG IN TO MY ACCOUNT
User story này xuất hiện cho cả ba vai trò và cũng độc lập với bất kỳ công việc nào. Chúng ta có thể giả định rằng chúng ta sẽ có một hành động "Log in" trong mô hình User của ứng dụng.
I CAN MODIFY MY ACCOUNT DETAILS
User story này cũng xuất hiện cho cả ba vai trò, vì vậy chúng ta có thể thêm một hành động "Modify" vào mô hình User. Mặc dù không được đề cập rõ ở đây, nhưng chúng ta có thể an tâm giả định rằng người dùng cần phải lấy và xem chi tiết của họ trước khi thực hiện bất kỳ thay đổi nào. Do đó, chúng ta cũng có thể thêm một hành động "View" vào mô hình người dùng.

I CAN DELETE MY ACCOUNT
User story này xuất hiện cho cả pet owners và pet sitters, và thêm một hành động " Delete" vào mô hình User. Đến nay, chúng ta đã xác định một số hành động cho mô hình User, nhưng chưa chạm vào các mô hình Job, Dog hoặc bất kỳ mối quan hệ nào. Dưới đây là các hành động của User (hiển thị trong hình 9.11):

 User: "Register”
 User: "Login”
 User: "View”
 User: "Modify”
 User: "Delete”
Bây giờ chúng ta hãy xem danh sách các User stories cho pet owners.

I CAN POST A JOB ON PETSITTER, INCLUDING A DESCRIPTION OF ONE OF MY DOGS
Story này yêu cầu một hành động "Create" liên quan đến model Job. Nó cũng bao gồm model Dog, vì vậy hãy xem xét kỹ hơn về mô hình đó.
According  user story, việc post một job và bao gồm dog mà công việc đó liên quan đến là một bước duy nhất. Không có user story trước đó về việc thêm một con chó vào ứng dụng PetSitter, điều này có thể dẫn đến việc cần user story để liệt kê, chỉnh sửa và xóa chó. Đây là một lựa chọn thiết kế. José nói rằng điều này giữ cho ứng dụng đơn giản, và các nhà phát triển hoàn toàn đồng ý, vì nó yêu cầu ít hành động hơn để triển khai. 
Còn về mối relationships? Well Có một kết nối mạnh mẽ giữa các domain Dog và Job do việc bao gồm chó trong mỗi công việc. Đây là một ánh xạ one-to-one, có nghĩa là với mỗi công việc có đúng một con chó và mỗi con chó được gán cho đúng một công việc. Do đó, chúng ta có thể bỏ ID từ model Dog, vì chúng ta có thể xác định mỗi con chó bằng job mà nó thuộc về.
Tất nhiên, có thể có các kịch bản trong đó công việc yêu cầu người giữ chó chăm sóc nhiều chó. Tuy nhiên, chúng không được đề cập trong user story này, mà đã chỉ rõ "một trong những con chó của tôi", và như chúng ta đã nói trước đó, chúng ta muốn giữ mô hình đơn giản (xem hình 9.12). Đồng thời, rất có thể một chủ nhân thú cưng sẽ tạo nhiều công việc cho cùng một con chó qua thời gian. Tuy nhiên, vì mô tả của con chó được bao gồm trong công việc, nó sẽ là một mô hình Dog khác nhau ngay cả khi đó là cùng một con chó trong thế giới thực.

 


Có hai bài học có thể rút ra từ đây. Một là không có sự ánh xạ hoàn hảo giữa một trường hợp của một concept trong thực tế với một trường hợp của cùng một concept trong domain model. Bài học thứ hai là cách chúng ta viết user story và, do đó, cách chúng ta muốn người dùng tương tác với ứng dụng của chúng ta, có thể làm suy luận chệch hướng.
I CAN SEE A LIST OF JOBS I HAVE POSTED
Từ story này, chúng ta có thể giả định một hành động "List my own" cho job, điều này cũng đòi hỏi biết user đã tạo chúng. Vì kết nối đó cần thiết để người dùng liệt kê công việc của họ, chúng ta có thể vẽ một mối quan hệ giữa model User và Job và gọi nó là "user creates job" (xem hình 9.13).
 
GIVEN THAT I HAVE POSTED A JOB, I CAN VIEW AND MODIFY ITS DETAILS

User story này thêm các hành động "View” và "Modify" cho model Job. Nó không cung cấp thông tin mới về mối quan hệ.

GIVEN THAT I HAVE POSTED A JOB, I CAN DELETE IT
User story này tương tự như story trước đó và thêm hành động "Delete" cho model Job.

GIVEN THAT I HAVE POSTED A JOB, I CAN SEE THE PET SITTERS THAT APPLIED
User với role pet-sitter có thể nộp đơn xin việc. Quá trình nộp đơn chính nó là một user story khác mà chúng ta sẽ xem xét khi đi qua các user story cho pet sitters. User story hiện tại nhìn nhận từ góc nhìn của người chủ nuôi muốn xem những người giữ chó này. Để hỗ trợ nó, chúng ta có thể vẽ một mối quan hệ thứ hai giữa các mô hình Người dùng và Công việc, gọi là " applies for" (xem hình 9.14).


 


Câu hỏi là: Hành động tương ứng với user story này nên được đặt tên là gì, và nó thuộc về model nào? Nó có thể được đặt tên là "Liệt kê đơn xin việc." Có lẽ nó không thuộc về mô hình Dog, nhưng nó là về User hay Job? Một cách nào đó, nó liên quan đến cả hai, và chúng ta đã giới thiệu một danh từ mới, "application," trong tên hành động. Có lẽ chúng ta cần phải xem xét lại domain model? Nếu chúng ta không thể đặt tên cho một hành động mà không cần một danh từ mới, điều này là một dấu hiệu cho thấy chúng ta cần thêm các concepts mới trong domain model. Chúng ta có thể tạo một model có tên là JobApplication và kết nối nó với cả User và Job. Như vậy, chúng ta có thể có một hành động "List for Job" cho model mới (xem hình 9.15). Hành động này cũng bao gồm một danh từ, nhưng điều này hoàn toàn chấp nhận được vì nó là một danh từ đã tồn tại như một concept.

 

GIVEN THAT I HAVE FOUND A SUITABLE CANDIDATE, I CAN APPROVE THEM
Một candidate cho một công việc là một người dùng đã nộp đơn cho công việc đó, hay nói cách khác, là who created an application. Chúng ta có thể thêm một hành động vào mô hình JobApplication và gọi nó là "Approve” Trong giai đoạn ban đầu khi chúng ta tạo các attribute cho domain model của chúng ta, chúng ta chưa có model JobApplication. Tuy nhiên, domain model của chúng ta nên bao gồm kết quả của hành động "Approve," vì vậy nhóm quyết định thêm một thuộc tính "Status," có thể chỉ applying hoặc accepted.. Ngoài ra, để phù hợp với các mô hình khác, JobApplication cũng có một thuộc tính "ID" (xem hình 9.16). 
 
Tốt quá, chúng ta đã hoàn thành tất cả các user stories cho pet owner, và chúng ta đã cập nhật domain model của mình với các relationship. Trước khi chúng ta chuyển sang các user story cho pet sitters,hãy nhớ lại tất cả các hành động chúng ta đã xác định cho đến nay: 
 Job: “Create”
 Job: “List my own”
 Job: “View”
 Job: “Modify”
 Job: “Delete”
 JobApplication: “List for job”
 JobApplication: “Approve”
Bây giờ hãy xem xét các user stories cho pet sitter.
I CAN VIEW A LIST OF PETS THAT NEED LOOKING AFTER
Như chúng ta đã thiết lập trong domain model của mình, thú cưng hoặc chó được tạo ra và được liệt kê như một phần của công việc. Do đó, danh sách mà pet sitter có thể xem không phải là danh sách thú cưng mà thay vào đó là danh sách công việc. Chúng ta có thể thêm một hành động vào mô hình Job và gọi nó là "List all." User story này không đòi hỏi bất kỳ thay đổi nào đối với các mối quan hệ.

GIVEN THAT I HAVE FOUND A JOB, I CAN APPLY FOR IT
User story này thiết lập một người dùng muốn chăm sóc thú cưng, bằng cách kết nối họ với công việc thông qua một đơn đăng ký công việc. Chúng ta có thể thêm hành động "Create" để kết nối các model User và JobApplication.
Tuyệt vời, chúng ta đã đi qua tất cả các user stories về pet sitter. Chúng hoạt động với doamain model của chúng ta và không đòi hỏi bất kỳ mối quan hệ mới hoặc được sửa đổi nào. Chúng ta có thể thêm vào bộ sưu tập các hành động sau:
 Job: “List all”
 JobApplication: “Create” 

Cuối cùng, nhưng không kém quan trọng, hãy xem xét user stories cho administrator:
 I can modify other user profiles.
 I can edit jobs that other users have posted.
 I can delete users.
Một điều chung cho những story này là chúng ta đã xác định các hành động như "View", "Modify" và "Delete" cho user và job. Sự khác biệt duy nhất là rằng người dùng thông thường chỉ có thể thực hiện những hành động này cho bản thân họ hoặc cho công việc mà họ đã tạo ra, trong khi người quản trị có thể thực hiện chúng cho bất kỳ người dùng nào. Chúng ta sẽ phải xem xét những user stories này khi triển khai quyền hạn trong phần backend, nhưng chúng không gây ra thay đổi đối với domain model của chúng ta.
Tuyệt vời, có vẻ như chúng ta đã hoàn thành giai đoạn này của dự án. José, Nidhi và Max mỗi người rời cuộc họp với một bức ảnh của bảng trắng chứa toàn bộ domain model (xem hình 9.17). Theo kế hoạch, bây giờ đến lượt Max đảm nhiệm việc biến nó thành phiên bản đầu tiên của OpenAPI description.
 

Summary
 PetSitter là ứng dụng kết nối chủ nhân chó bận rộn với những người đang tìm việc muốn chăm sóc chúng. Đây là nền tảng chúng ta sẽ xây dựng trong phần thứ hai của cuốn sách này.

 Kế hoạch phát triển liên quan đến một đội ngũ với hai nhà phát triển, một tập trung vào backend và người còn lại tập trung vào frontend. Chúng ta sẽ thiết kế một API cho ứng dụng trước, sau đó xây dựng hai phần và cuối cùng là tích hợp cả hai. Quá trình này sẽ được mô tả chi tiết trong các chương sắp tới.

 Domain modeling là quá trình tạo ra một biểu diễn về các concept trong một lĩnh vực vấn đề. Đây là bước đầu tiên trong việc xây dựng một API và bắt đầu trước khi viết OpenAPI description. Domain model của PetSitter bao gồm User, Job, Dog và JobApplication.

 User stories có thể giúp trong việc domain modeling, đặc biệt là khi xác định các hành động cho các models và mối quan hệ giữa chúng. Kết quả của việc viết và phân tích user stories đã cập nhật domain model với bốn mối quan hệ và một danh sách các hành động cho Users, Jobs và JobApplication. Model hoàn chỉnh này tạo nền tảng cho công việc OpenAPI sắp tới.


Chapter 10 - Creating an API
design using OpenAPI

This chapter covers

 Tạo reusable schemas (lược đồ có thể tái sử dụng) trong OpenAPI
 Chuyển đổi PetSitter domain model thành schemas
 Thiết kế một API theo phương pháp CRUD
 Tạo các paths và operations cho API của PetSitter API

Trong chương trước, chúng ta đã làm quen với José và nhóm của anh ấy, đang xây dựng ứng dụng PetSitter. Chúng ta đã đi cùng họ qua cuộc họp ban đầu, trong đó họ tạo kế hoạch hành động cho việc xây dựng ứng dụng. Chúng ta cũng tham gia vào phiên làm domain model trên bảng trắng, trong đó họ chuẩn bị một doamain model cấp cao.

Phiên làm mô hình miền là mục đầu tiên trong kế hoạch hành động của họ, để lại cho chúng ta các bước sau đây:
1. Max, nhà phát triển frontend, sẽ tạo bản nháp đầu tiên của API design của họ.
2. Nidhi, nhà phát triển backend, sẽ xem xét bản nháp đó.
3. Cả hai sẽ đồng ý hoàn thiện đặc tả hoặc chỉnh sửa và xem xét lại nếu cần thiết.
4. Cả hai sẽ làm việc độc lập trên phần thực hiện của họ.
5. Sau khi hoàn thành, họ sẽ tích hợp mã của mình.

Trong chương này, chúng ta sẽ đi qua bước đầu tiên của những bước còn lại.

10.1 The problem

Trong chương trước, chúng ta đã tạo một domain model. Model là một không chính thức informal, cấp cao highlevel về các representation concept cơ bản của ứng dụng PetSitter. Sau đó, ở giai đoạn triển khai của dự án, chúng ta sẽ phát triển các phần frontend và backend, kết nối với một API. Bây giờ, chúng ta phải nối cầu giữa hai phần đó, và chúng ta sẽ làm điều này với formal description of the API using OpenAPI.
Cuối chương này, chúng ta nên có một tệp OpenAPI thỏa mãn ba mục tiêu sau đây:
 Nó là một valid representation của domain model, đáp ứng các requirements cho dự án.
 Một backend developer có thể sử dụng nó để tạo ra một triển khai của API.
 Một frontend developer có thể viết mã để tích hợp API.

10.1.1 Converting a domain model to OpenAPI
Trong domain model, chúng ta gán các attributes, relationships và functionality cho các khái niệm khác nhau various concepts. Để hiểu cách chúng ta có thể chuyển đổi mỗi khía cạnh này sang OpenAPI, hãy quay lại nhìn vào API của FarmStall. Chúng ta đã xem xét một domain model cho FarmStall trong chương trước (phần 9.3.2), trong đó chúng ta xác định user và reviews là những khái niệm chính. Bây giờ chúng ta sẽ xem xét lại model này và xem xét mô tả OpenAPI để thấy làm thế nào chúng ta có thể thực hiện một ánh xạ giữa chúng.

Để retrieve a list of reviews trong API của FarmStall, người dùng có thể thực hiện cuộc gọi API đến hoạt động GET /reviews. Trong chương 5, chúng ta đã sử dụng JSON Schema để mô tả phản hồi. Làm một lời nhắc, dưới đây là phần schema của mô tả OpenAPI cho phản hồi này.
 

Các schema mô tả các thuộc tính của một đối tượng: trong trường hợp này, là uuid, message, rating, và userId. Trong chương trước, chúng ta đã xem xét một mô hình miền cho các đánh giá trong đó UUID, message và rating là các thuộc tính, và user ID đã trở thành một mối quan hệ giữa các model Review và User (xem hình 9.6).
Nói chung, các schema trong các OpenAPI definition là biểu diễn của các thuộc tính và mối quan hệ cho các concept trong một domain model. Chúng ta sẽ tiếp tục sử dụng các thuật ngữ "model" hoặc "concept" để biểu diễn domain model cấp cao và từ "schema" để chỉ sự triển khai kỹ thuật của nó dưới dạng một cấu trúc dữ liệu. Tuy nhiên, trong tài liệu về domain model với OpenAPI, bạn cũng có thể thấy các từ "model" và "schema" được sử dụng có thể thay thế nhau.

Nếu bạn nhìn vào phương thức HTTP GET và URL /reviews, bạn có thể đọc nó như là " Get Reviews." Đây là một hành động " Get” " thực hiện trên reviews concept trong domain model. Các phần chức năng hoặc hành vi của domain model được đại diện qua các hoạt động API trong OpenAPI. Chúng ta sẽ xem xét các hoạt động sau trong chương này và tập trung vào các schema trước.

10.2 Creating the schemas
Trong phần này, chúng ta sẽ tạo các schema có thể tái sử dụng, và bạn sẽ biết chúng được đặt ở đâu trong một tệp OpenAPI. Tuy nhiên, để đến được đó, chúng ta phải trước tiên tạo một tệp OpenAPI mới.

10.2.1 Starting an OpenAPI file with schemas
Để bắt đầu định nghĩa OpenAPI mới cho PetSitter, chúng ta sẽ sử dụng Swagger Editor (https://editor.swagger.io), công cụ mà bạn đã làm quen trong chương 4. Mở trang web và làm trống trình soạn thảo để bạn có thể bắt đầu viết trên một bảng trắng.
Như một lời nhắc, bạn cần thực hiện các bước sau khi tạo một tệp OpenAPI mới:
 Xác định Specify phiên bản của OpenAPI bạn đang sử dụng.
 Thêm một phần info với title và version. 
 Thêm một đối tượng paths trống rỗng ngay cả khi bạn chưa định nghĩa bất kỳ hoạt động nào, vì nếu không bạn sẽ nhận được một lỗi cú pháp.

Tệp đầu tiên của bạn nên trông như sau:
openapi: 3.0.3
info:
title: PetSitter API
version: "0.1"
paths: {}

Còn một phần tử cấp cao khác cho các tệp OpenAPI: components. Đây là một container trong đó bạn có thể định nghĩa các phần của API của bạn mà không thuộc về một đường dẫn cụ thể nào. Bạn có thể thêm các tham chiếu đến components ở nhiều nơi khác nhau trong API description của bạn. Bạn đã thấy phần tử này trong chương 7, nơi chúng ta đã sử dụng nó để tạo security scheme definition cho API. Bây giờ, chúng ta sẽ sử dụng components và phần tử con của nó là schemas để định nghĩa các schema có thể tái sử dụng cho API.

Sau khi thêm các phần tử container này, tệp OpenAPI của bạn nên trông như sau:


openapi: 3.0.3
info:
  title: PetSitter API
  version: "0.1"
paths: {}
components:
  schemas:
    {}

OpenAPI Description đã sẵn sàng để các mô tả schema của các concept User, Job, Dog, và JobApplication từ domain model của chúng ta.

10.2.2 Referencing common schemas
Khi chúng ta đã tạo các schema chung trong phần components của tệp OpenAPI, chúng ta có thể sử dụng từ khóa $ref để thêm các tham chiếu đến chúng. Các tham chiếu này có thể được sử dụng trong các request, response, và thậm chí trong các schema khác.

Giá trị cho từ khóa $ref là một con trỏ JSON JSON pointer mô tả nơi chúng ta có thể tìm thấy schema trong cấu trúc phân cấp của tệp OpenAPI của chúng ta. Con trỏ JSON bắt đầu bằng ký hiệu thăng dấu (#), tiếp theo là đường dẫn /components/schemas/, và nó kết thúc bằng tên của schema:
$ref: '#/components/schemas/User'
10.2.3 The User schema
According to the domain model discussions in the previous
chapter, a User (see figure 10.1) has the following attributes: 
 ID
 Email address
 Password
 Full name
 Roles	
 

Những vai trò chỉ ra liệu họ có thú cưng và muốn cung cấp công việc, hay họ đang tìm kiếm công việc trông nom thú cưng, hay họ là quản trị viên, hoặc một sự kết hợp nào đó của ba vai trò này. Chúng ta phải tạo một schema đối tượng với nhiều trường, trong đó mỗi trường, hoặc thuộc tính, đại diện cho một trong những thuộc tính này.
Khi chuyển đổi các thuộc tính, chúng ta nên tuân theo quy tắc đặt tên cho các đối tượng JSON, nói rằng tất cả các thuộc tính đều viết thường và không có khoảng trắng. Chúng ta cũng phải thêm một type cho mỗi thuộc tính. Xem xét hai yêu cầu này, bảng 10.1 liệt kê các thuộc tính.
 

ID là một số nguyên. Các trường cho email, password, và full name có kiểu string, đây là một giá trị mặc định hợp lý trừ khi chúng ta chắc chắn rằng chúng chỉ chứa giá trị số hoặc Boolean. Trường roles là một mảng vì người dùng có thể có nhiều vai trò. Mỗi vai trò là một chuỗi, vì vậy chúng ta có thể đặt từ khóa kiểu của mảng thành string.

Bây giờ hãy thêm schema của chúng ta vào OpenAPI description. Để làm điều này, bạn cần cung cấp tên của schema của bạn như là YAML key dưới phần schemas, với mô tả ở dưới nó. Khác với tên thuộc tính, được viết thường, tên schema thường bắt đầu bằng một chữ cái viết hoa - một quy ước chúng ta đã sử dụng cho domain model. Do đó, chúng ta sẽ tạo một schema với tên là User. Đoạn mã OpenAPI dưới đây hiển thị tệp OpenAPI của chúng ta với schema đầu tiên. Bạn có thể sao chép định nghĩa này từ https://designapis.com/ch10/01.yml.
openapi: 3.0.3
info:
  title: PetSitter API
  version: "0.1"
paths: {}
components:
  schemas:
    User:
     type: object
     properties:
        id:
          type: string
        email: 
          type: string
        password: 
          type: string
        full_name:
          type: string
        roles:
          type: array
          items:
            type: string

Khi bạn thêm mã này vào Swagger Editor, bạn sẽ thấy một phần mới được gọi là "Schemas" xuất hiện trong bảng điều khiển panel bên phải của trình soạn thảo. Trong phần đó, bạn có thể mở rộng mô hình User và xem các thuộc tính bạn đã định nghĩa (xem hình 10.2).

 

GHI CHÚ: Trong hình 10.2, bạn có thể nhận ra hình tam giác màu vàng ở cột bên trái. Điều này là cảnh báo rằng một schema không được sử dụng trong định nghĩa. Chúng ta có thể bỏ qua điều này vì bây giờ, chúng ta đang bắt đầu bằng cách tạo các schema; sau này, chúng ta sẽ định nghĩa các hoạt động sử dụng chúng.

10.2.4 The Job schema
Trong domain model của PetSitter, một Job (xem hình 10.3) có các thuộc tính sau đây:
 ID
 Start time
 End time
 Activity
 

Như chúng ta đã làm trong schema User, chúng ta sẽ đặt ID là một số nguyên và sử dụng kiểu string cho mọi thứ khác. Mối quan hệ trong domain model cũng dẫn đến các thuộc tính trong schema. Chúng ta đã thấy điều này trong API FarmStall với một trường user_id trong một Reviews. Do đó, chúng ta cũng phải xem xét các mối quan hệ.
Đến nay, chúng ta có các schema User và Job, vì vậy chúng ta chỉ có thể xem xét mối quan hệ giữa chúng: " user creates job " (xem hình 10.4).
 

Để tham chiếu đến user who created the job, chúng ta có thể thêm một field chứa ID của user. Một cách đặt tên phổ biến cho những trường này là sử dụng tên (viết thường) của schema đích, tiếp theo là dấu gạch dưới, và sau đó là tên của trường trên schema đích chứa định danh duy nhất, như là id. Với cách tiếp cận này, tên thuộc tính sẽ là user_id. Chúng ta cũng có thể cụ thể hơn và bao gồm một mô tả về mối quan hệ trong tên, điều này đặc biệt hữu ích nếu chúng ta có nhiều hơn một mối quan hệ giữa hai schema giống nhau. Với những lời nói đó, chúng ta hãy gọi nó là creator_user_id.

Dưới đây là một ví dụ về tệp OpenAPI sau khi chúng ta đã thêm schema thứ hai của mình (từ bảng 10.2):
 

openapi: 3.0.3
#...
  schemas:
    User:
     #...
    Job:
      type: object
      properties:
        id: 
          type: integer
        create_user_id: 
          type: integer
        start_time: 
          type: string
        end_time:
          type: string
        activity: 
          type: string	




10.2.5 The Dog schema
Trong chương trước, nhóm đã liệt kê các thuộc tính sau cho model Chó:
 Name
 Age (tính bằng năm in years)
 Breed (giống)
 Size (in case people are not familiar with the breed)Chúng ta có thể sử dụng một số nguyên cho tuổi, vì đó là một số, và kiểu string cho mọi thứ khác. Giống như trước đây, chúng ta sẽ liệt kê các thuộc tính trong một bảng trước (xem bảng 10.3).

 

    Dog:
      type: object
      properties:
        name:
          type: string
        age:
          type: integer
        breed: 
          type: string
        size:
          type: string

Vậy mối quan hệ "chó thuộc về công việc dog belongs to job" thì sao? Như chúng ta nhận ra khi xử lý các user stories, đây là một ánh xạ one-to-one, và pet owner tạo ra chó như một phần của công việc họ đăng. Do đó, chúng ta cần phải bao gồm schema Chó vào schema Công việc một cách nào đó. Chúng ta có thể thực hiện điều này bằng cách sử dụng một tham chiếu: schema Job có một thuộc tính bổ sung được gọi là dog với một con trỏ $ref trỏ đến schema mới. Như vậy, mô tả của chó trở thành một phần của công việc, đúng như mong muốn. Đoạn mã OpenAPI dưới đây cho thấy cách điều đó trông như thế nào.
    Job:
      type: object
      properties:
        id: 
          type: integer
        create_user_id: 
          type: integer
        start_time: 
          type: string
        end_time:
          type: string
        activity: 
          type: string
        dog:
          $ref: '#/components/schemas/Dog'
10.2.6 The JobApplication schema
Schema thứ tư và cuối cùng của chúng ta là JobApplication, có các thuộc tính sau đây:

 ID
 Status

ID có thể lại là một integer, và status có thể là một chuỗi. Chúng ta cũng có các mối quan hệ với schema Job và User, vì mỗi đơn xin việc được tạo ra bởi một người dùng và được dành cho một công việc cụ thể. Để hỗ trợ điều này, chúng ta có thể thêm các trường user_id và job_id với kiểu số nguyên (vì id trên Job và User là số nguyên), như được hiển thị trong bảng 10.4.
 
Tuyệt vời. Bây giờ hãy cập nhật tệp OpenAPI với schema cuối cùng.


    JobApplication:
      type: object
      properties:
        id: 
          type: integer
        status:
          type: string
        user_id: 
          type: integer
        job_id:
          type: integer

Tuyệt vời, bây giờ chúng ta đã có bốn schema hoàn chỉnh trong tệp OpenAPI của chúng ta. Làm việc tốt, Max!
Hãy tiếp tục với các hành động trong domain model của chúng ta. Trước khi chúng ta có thể xem xét chúng, tuy nhiên, là lúc để tìm hiểu thêm về CRUD.

10.3 The CRUD approach to API operations

Viết tắt CRUD đại diện cho Create-Read-Update-Delete. Ban đầu, CRUD xuất phát từ thế giới của hệ thống quản lý cơ sở dữ liệu database management systems - nó mô tả những thao tác thiết yếu essential có thể được thực hiện trên một mảnh dữ liệu certain piece cụ thể.
CRUD như một mô hình thiết kế API phù hợp tốt với một số khái niệm của REST, mà bạn đã đọc về trong chương 1. Các URL đại diện cho tài nguyên resource và các phương thức HTTP khác nhau (hoặc động từ) đại diện cho các thao tác. Điều đó dẫn đến một cách tiếp cận cụ thể trong việc thiết kế đường dẫn URL và các thao tác có sẵn trên chúng. Bạn đã thấy cách tiếp cận này trong API FarmStall cũng như trong một số ví dụ bên ngoài trong phần 1 của cuốn sách này. Trước khi tái tạo nó cho PetSitter, tuy nhiên, hãy nhìn lại vào cách tiếp cận này và làm rõ các chi tiết.
Thường ta có thể phân biệt giữa hai loại URL paths trong một API:
 Resource endpoints
 Collection endpoints
Sau này trong chương này, bạn sẽ tìm hiểu về một loại endpoint thứ ba, nhưng hãy tập trung vào hai loại này trước. Hãy đồng thuận định nghĩa cho thuật ngữ "resource." Resources là các trường hợp cụ thể của một concept trong domain model. Chẳng hạn, chúng ta có các model User và Job, vì vậy mỗi người dùng cụ thể là một resource, và mỗi job cụ thể cũng vậy.
Thực hành tốt nhất cho việc đặt tên cho đường dẫn đến một tài nguyên riêng biệt là sử dụng tên số nhiều của model, tiếp theo là dấu gạch chéo slash, và sau đó là một định danh identifier duy nhất cho trường hợp đó. Ví dụ, nếu có một người dùng với ID là 123, bạn có thể truy cập nó như là /users/123. Nếu bạn nghĩ về URL như một cấu trúc thư mục (điều này thực sự đúng đối với các trang web tĩnh!), bạn có thể tưởng tượng một thư mục có tên là users chứa một tệp tin cho mỗi user.
Chúng ta gọi URL đến một tài nguyên cụ thể là resource endpoint. Trên một resource endpoint, bạn có thể sử dụng HTTP GET để lấy tài nguyên, PUT hoặc PATCH để cập nhật nó và DELETE để xóa nó.

Tuy nhiên, việc truy cập individual resources. Thường xuyên bạn sẽ phải lấy list of resources cùng loại - các trường hợp của cùng một concept trong domain model. Đối với mục đích này, bạn có thể sử dụng tên số nhiều của mô hình mà không thêm hậu tố ID. Để theo định nghĩa của hệ thống tệp tin, bạn mở một thư mục thay vì một tệp tin cụ thể.

Chúng ta gọi URL đến resource listing là collection endpoint. Trên một collection endpoint, bạn có thể sử dụng HTTP GET để lấy tất cả các resources cùng loại. Bạn có thể bảo rằng việc lấy tất cả các resources nếu có hàng ngàn hoặc triệu resources không thực tế. Do đó, có các khái niệm như phân trang pagination và filters. Bạn đã thấy bộ lọc trong chương 2 khi collection endpoint GET /reviews trong API FarmStall cho phép một tham số max-Rating để nó chỉ trả về đánh giá với một giá trị xác định. Chúng ta sẽ thảo luận về phân trang (và thêm về bộ lọc) trong chương 17.
Thường xuyên cũng sử dụng URL collection endpoint kết hợp với phương thức HTTP POST để tạo một phần tử mới mà ID chưa biết trước, vì nó được gán bởi máy chủ.
Bạn có thể tìm thấy một tóm tắt về những ý này trong bảng 10.5.

 


10.3.1 Defining API requests and responses

Trong tương tác với một API, thao tác defines URL, HTTP method và, tùy chọn, các request parameters và một response body mà client gửi đến server. Sau đó, server gửi lại một response, chứa một status code HTTP và một response body.

Chương 5 giới thiệu về HTTP status codes, nên bạn có thể tham khảo chương đó để biết thêm thông tin về chúng.

CRUD approach trong designing an API bao gồm một số quy tắc cho requests và responses. Chúng tôi sẽ đề cập đến lý thuyết trong phần này và sau đó làm rõ thông qua việc thực hành khi thêm các thao tác vào mô tả OpenAPI của PetSitter.

REQUESTS



Đối với các thao tác "Read" và "Delete", không có request body. Nếu cần thiết, đầu vào cho các thao tác "Read", như filter criteria, thường được đặt trong các query parameters.

Đối với các thao tác "Create" và "Update", bạn cần gửi biểu diễn JSON của tài nguyên (một cấu trúc JSON theo các quy tắc) như là request body.

RESPONSES

Đối với các thao tác "Read" trên các resource endpoints, response là một đối tượng JSON theo quy tắc của tài nguyên. Cuộc gọi API thành công nhận được mã trạng thái 200 OK. Nếu tài nguyên được yêu cầu không tồn tại, API nên trả về mã 404 Not Found.

Đối với các thao tác "Read" trên collection endpoints, phản hồi là một đối tượng collection chứa một mảng các resource objects, tùy chọn kèm theo các trường bổ sung với siêu dữ liệu. Trường chứa mảng các mục thường được gọi là items hoặc name of the resource.

Listing 10.10 A collection endpoint response example

#...
responses:
  '200':
    description: A list of items
    content:
      application/json:
        schema:
        type: object
        properties:
          items:
            type: array
            items:
              $ref: '#/components/schemas/Item'

Why not return a top-level array?

Chúng ta có thể đơn giản hóa cấu trúc trong danh sách 10.10 bằng cách không có một object với trường items và thay vào đó chỉ làm cho toàn bộ phản hồi là một array. Có hai lý do mà điều này không được khuyến khích.

Một lý do là có một lỗ hổng bảo mật trong một số trình duyệt cũ cho phép vượt qua các hạn chế Cross-Origin Resource Sharing (CORS) khi phần tử cấp cao là một array. Lý do thứ hai là chúng ta có thể cần các trường bổ sung additional fields với metadata, đặc biệt là khi sử dụng phân trang. Một ví dụ về metadata liệu như vậy có thể là số lượng các mục có sẵn nhưng không được trả lại trong phản hồi API hiện tại.

Ngay cả khi chúng ta không có vẻ sử dụng cho các trường bổ sung, chúng ta nên tuân theo thực hành tốt nhất của việc không bao giờ trả lại các mảng cấp cao trong các API chúng ta thiết kế. Có lẽ chúng ta cũng cần phải trò chuyện với bản thân trong quá khứ của mình, người đã làm điều này theo cách sai trong chương 5 với bộ sưu tập GET /reviews của FarmStall. 

Đối với collection endpoints, mọi cuộc gọi API nên trả về mã trạng thái 200, ngay cả khi bộ sưu tập là trống rỗng.

Why not use 404 for empty collections?
Một cuộc gọi API đến một điểm cuối tài nguyên nhận được mã trạng thái 200 nếu tài nguyên tồn tại và 404 nếu không tồn tại, nhưng một điểm cuối bộ sưu tập luôn trả về mã trạng thái 200, ngay cả khi bộ sưu tập là trống rỗng. Lý do là bởi vì bộ sưu tập vẫn tồn tại, ngay cả khi không có tài nguyên nào trong đó. Nếu bạn nghĩ về nó như là một cái xô, điều này là hợp lý, vì một cái xô trống vẫn là một cái xô, và bạn có thể nắm lấy nó và thực hiện một số hành động với nó.
Đối với các thao tác "Update," resource endpoints responds với một đối tượng JSON theo quy tắc của tài nguyên. Điều này tạo ra sự đối xứng giữa yêu cầu và phản hồi và cũng tính nhất quán giữa "Read" và "Update," vì resource endpoints đưa ra phản hồi giống nhau, độc lập với phương thức HTTP. Để duy trì sự đối xứng, các yêu cầu cập nhật cũng trả về mã trạng thái 200.
Đối với các thao tác "Delete," resource endpoints responds thường là trống rỗng. Điều này không nhất quán với các thao tác khác trên resource endpoints, nhưng có ý  nghĩa, vì sau một "Delete," tài nguyên không còn tồn tại. Một yêu cầu xóa thành công trả về mã trạng thái 204 No Content, vì mã 200 mong đợi một thân phản hồi.
Đối với các thao tác "Create," là các yêu cầu POST trên endpoint resource, response body thường là trống rỗng. Thay vào đó, response chứa một tiêu đề Location trỏ đến endpoint resource cho tài nguyên mới được tạo. Một yêu cầu tạo thành công trả về mã trạng thái 201 Created.
Chúng tôi đã thu thập những thực hành này trong bảng 10.6.

 

10.3.2 From user stories to CRUD design

Bạn có thể kết luận rằng API design liên quan đến quá trình cơ khí của việc lấy models  của bạn, thêm các collection and resource endpoints cho mỗi mô hình đó, và chỉ định tất cả các thao tác CRUD - GET và POST cho collection endpoints, và GET, PUT và DELETE cho resource endpoints. Và thực sự, API thu được từ quá trình này có thể là điều API designers gọi là một API thiết kế tốt, nhất quán. Tuy nhiên, đáng tiếc, đó có thể không phải là API mà người tiêu dùng của bạn (như ứng dụng web của bạn) cần.

Trong chương trước, đội của José đã viết các user stories để bao gồm các requirements của ứng dụng PetSitter. Là một người thiết kế API, bạn nên xem xét những stories đó và đặt cho mình một số câu hỏi:
- User story này có khớp với một hoặc nhiều thao tác CRUD không? Nếu có, hãy đảm bảo bạn bao gồm chúng trong API design của bạn.
- Story yêu cầu một loại thao tác khác không? Nếu có, có cách nào bạn có thể bao gồm nó trong API của bạn mà vẫn đúng, từ hướng tới tài nguyên resource-oriented (CRUD/RESTful)?
- Có những thao tác CRUD mà không có user stories nào cần không? Nếu có, bạn có thể và nên bỏ chúng ra khỏi thiết kế API.

10.4 API operations for PetSitter

Với bộ công cụ của chúng tôi đã được chuẩn bị, chúng ta có thể tiến đến triển khai các thao tác cho API PetSitter. Không có hành động nào trên Dog concept, nhưng chúng ta vẫn phải xem xét các hành động cho User, Job và JobApplication.

10.4.1 User operations
Xem xét model User của chúng ta trong API PetSitter (xem hình 10.5), chúng ta tìm thấy các hành động sau:
 “Register”
 “Login”
 “View”
 “Modify”
 “Delete” 

 
Hãy xem xét chi tiết mỗi hành động và xem nó tương ứng với các thao tác CRUD như thế nào.
REGISTER
Việc " Register" là hành động ban đầu mà một người dùng thực hiện để tạo ra biểu diễn của họ (tài khoản) trong ứng dụng. Do đó, chúng ta có thể ánh xạ hành động này với "Create" và thêm một hoạt động POST trên đường dẫn /users, đó là endpoint collection cho các resources User, vào OpenAPI description của chúng ta. The request cho hoạt động đó bao gồm schema User như là một tham chiếu thành phần với $ref, và phản hồi có một mã trạng thái 201 và một Location header.
paths: 
  /users:
    post:
      summary: Register User
      responses:
        '201':
          description: Created
          headers:
            Location:
              schema:
                type: string
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/User'

LOGIN

Người dùng đăng nhập vào một ứng dụng khi họ muốn bắt đầu sử dụng nó. Trong quá trình đăng nhập, người dùng xác thực bản thân, và ứng dụng đảm bảo rằng họ được cấp quyền truy cập. Chúng ta đã thảo luận về xác thực trong API trong chương 7, nên chúng ta có thể giả sử rằng hành động này không được biểu diễn dưới dạng một hoạt động mà thay vào đó liên quan đến phần bảo mật của mô tả OpenAPI. Max quyết định bỏ qua hành động này tạm thời và làm việc về phần security sau.
VIEW
Chúng tôi đã thêm hành động này từ user story về việc sửa đổi thông tin người dùng, giả định rằng người dùng cần lấy hồ sơ của họ trước khi có thể sửa đổi nó. Trong mô hình CRUD, đây sẽ là một "Read" trên một resource duy nhất. Trong API, chúng ta có thể thêm một hoạt động GET trên resources endpoint cho người dùng, GET /users/{id}.
MODIFY
Sau khi xem hồ sơ, người dùng có thể sửa đổi nó. Nói cách khác, họ có thể thực hiện một "Update." Một lần nữa, điều này sẽ được thực hiện trên một nguồn tài nguyên duy nhất single resource, vì vậy chúng ta có thể thêm một hoạt động PUT trên resource endpoint cho người dùng, PUT /users/{id}.
DELETE
Người dùng có thể tự xóa mình. Điều này có thể là một hoạt động DELETE trên resource endpoint cho người dùng, DELETE /users/{id}.
Trong tệp OpenAPI, chúng ta chỉ định các đường dẫn và sau đó tất cả các hoạt động dưới chúng. Đối với ba hành động sử dụng resource endpoint cho người dùng, chúng ta cần một path parameter chung cho ID. (Như một lời nhắc, chúng ta đã giới thiệu tham số đường dẫn trong chương 6.) Chỉ "Modify" cần một request body.
Dưới đây là ba hoạt động này trong tệp OpenAPI. Khi bạn xem mã, hãy chú ý đến các tham chiếu references đến User schema và đặc biệt là cách chúng ta đã đặt một tham chiếu đến cùng một schema cho request and response bodies cho hoạt động PUT.
paths: 
  /users:
  #...          
  /users/{id}:
    parameters:
      - schema:
          type: integer
        name: id
        in: path
        required: true
    get:
      summary: View User
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
    put:
      summary: Modify User
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/User'
    delete:
      summary: Delete User
      responses:
        '204':
          description: No content

10.4.2 Job operations

Trong chương trước, chúng ta đã thu thập các hành động sau đây cho model Job (xem hình 10.6):

 “Create”
 “List my own”
 “View”
 “Modify”
 “Delete”
 “List all”

 

CREATE
Tạo một job là hành động tạo ra một resource mới. Chúng ta có thể thêm một hoạt động POST trên đường dẫn /jobs, collection endpoint cho các resources Job, vào mô tả OpenAPI của chúng ta. Nó tuân theo một thiết kế rất tương tự như hành động "Register" cho schema User.

Listing 10.13 PetSitter OpenAPI Create Job

paths: 
  /users: 
  /users/{id}:

#...

  /jobs:
    post:
      summary: Create Job
      responses:
        '201':
          description: Created
          headers:
            Location:
              schema:
                type: string
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Job'

LIST MY OWN

Để liệt kê công việc list jobs, chúng ta có thể sử dụng Jobs collection endpoint, /jobs, với một hoạt động GET. Tuy nhiên, nếu chúng ta làm điều đó cho "List my own," chúng ta sẽ xung đột với một hành động khác cho model Job, "List all." Như bạn đã học, collection endpoints thường được sử dụng để liệt kê tất cả các instances of a resource, vì vậy hoạt động này phù hợp với "List all" hơn là "List my own." Chúng ta nên làm gì?

Trước hết, it seems like a good idea để extend "List my own" thành một "List for user," vì cái sau bao gồm cái trước và giúp hỗ trợ các trường hợp sử dụng bổ sung. Ví dụ, trong khi chúng ta có thể không muốn người chăm sóc và chủ nhân thú cưng xem công việc của người dùng khác, đó có thể là một chức năng quản trị hữu ích. Chúng ta sẽ thiết kế "List for user" nhưng vẫn giữ tên là "List my own," vì đó là điều chúng ta cần ở thời điểm này.

Chúng ta đã học rằng chúng ta có thể sử dụng các query parameters để triển khai filter criteria và sử dụng các collection endpoints cho các tìm kiếm. Một lựa chọn cho hành động "Lists my own" có thể là sử dụng một filter parameter trên collection endpoint, vì vậy chúng ta có thể sử dụng GET /jobs?user_id= để lấy user’s jobs. Tuy nhiên, có một lựa chọn khác, vì vậy là lúc để chúng ta nói về loại endpoint thứ ba trong API CRUD mà chúng tôi hứa.

Cấu trúc thư mục Directory structures, mà chúng tôi sử dụng như một phương pháp tương tự cho đường dẫn trong URL, có thể được lồng vào nhau. Bạn có thể tạo một thư mục trong một thư mục khác. Bây giờ, hãy tưởng tượng bạn có một thư mục cho users, và không chỉ là một file cho mỗi người dùng, mà còn là một thư mục con cho người dùng, trong đó bạn có thể lưu các tệp khác liên quan đến người dùng đó. 

Trong PetSitter, bạn có thể nghĩ về mỗi chủ thú cưng có một thư mục chứa tất cả công việc họ đã đăng. Trong thuật ngữ CRUD của chúng tôi, chúng tôi gọi đó là một subresource collection endpoint. Cấu trúc chung của nó là /{schema}s/{id}/{subschema}s. Đối với trường hợp cụ thể của chúng tôi, đường dẫn sẽ là /users/{id}/jobs. Các end point này sử dụng các phương pháp CRUD theo cùng một cách như collection endpoint cấp cao, có nghĩa là chúng ta sử dụng động từ GET.



Đối với response format, chúng ta sẽ tuân theo cấu trúc bộ sưu tập mà chúng tôi đã giới thiệu trước đó. Để làm điều này, chúng ta sẽ tạo một đối tượng collection với một trường items là một mảng. Tất cả các mục trong mảng đó là các phiên bản của schema Job của chúng ta, mà chúng ta liên kết ở đây với từ khóa $ref.

/users/{id}/jobs:
    parameters:
      - schema:
          type: integer
        name: id
        in: path
        required: true
    get:
      summary: List Jobs for User
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                type: object
                properties:
                  items:
                    type: array
                    items:
                      $ref: '#/components/schemas/Job'

Shouldn’t we use a subresource collection endpoint for “Create” as well?
Nếu /users/{id}/jobs là vị trí tài nguyên cho tất cả công việc được tạo bởi một người dùng, liệu chúng ta không nên tái cấu trúc định nghĩa OpenAPI của chúng ta và sử dụng POST /users/{id}/jobs để tạo một công việc mới thay vì POST /jobs ngắn gọn chúng ta đã sử dụng trước đây? Điều đó là một lo ngại hợp lý. 

Tuy nhiên, nói chung, khi thiết kế API theo cách tiếp cận CRUD, chúng ta cố gắng giữ việc sử dụng các tài nguyên con ở mức tối thiểu và luôn sử dụng đường dẫn ngắn nhất có thể. Lý do duy nhất chúng ta đang sử dụng subresource ở đây là vì có một xung đột với một hành động khác trong một user story dùng hiện tại. Không có xung đột hoặc sự mơ hồ tương tự cho hành động "Create."


VIEW

Người dùng có thể lấy thông tin chi tiết về một công việc cụ thể. Điều này là một "Read" trên resource, vì vậy chúng ta có thể thêm một hoạt động GET trên resource endpoint cho job, GET /jobs/{id}.

MODIFY

Chủ nhân thú cưng có thể thực hiện một "Update” trên các job mà họ đã đăng, vì vậy chúng ta có thể thêm một hoạt động PUT trên resource endpoint tương ứng, PUT /jobs/{id}. 

Hai hoạt động cuối cùng này không có gì đặc biệt cả - chúng là các hoạt động CRUD cơ bản, và chúng tuân theo cùng định dạng như các hành động tương tự chúng ta có cho người dùng. Dưới đây là hai hoạt động này trong tệp OpenAPI.

LIST ALL
Chúng ta đã đề cập đến hành động "List all”. Và, vì chúng ta đã sử dụng GET /users/{id}/jobs cho "List my own," chúng ta giờ có thể tự do sử dụng collection endpoint cho "List all," nên chúng ta có thể thêm GET /jobs vào tệp OpenAPI của chúng ta.

/jobs:
    post:
      summary: Create Job
      responses:
        '201':
          description: Created
          headers:
            Location:
              schema:
                type: string
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Job'
    get:
      summary: List All Jobs
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                type: object
                properties:
                  items:
                    type: array
                    items:
                      $ref: '#/components/schemas/Job'


Như bạn có thể tưởng tượng, nếu PetSitter phát triển thành công, có thể có rất nhiều công việc trong cơ sở dữ liệu của nó. Thêm các tham số cho phân trang và lọc là một ý tưởng tốt, nhưng chúng ta muốn giữ mọi thứ đơn giản trong thời điểm hiện tại, nên chúng ta sẽ quay lại vấn đề này trong chương 17.


Vậy "Delete" cho Job thì sao?
Liệu có một hành động "Delete" trong domain model của chúng ta mà đang thiếu trong tệp OpenAPI không? Có! Dường như bạn đang chú ý nhiều hơn nhà phát triển frontend Max, người tình cờ bỏ qua nó. 

Điều này là tốt vì chúng ta có một chu kỳ đánh giá. Đội ngũ sẽ chú ý và thêm hoạt động thích hợp vào OpenAPI của chúng ta sau trong cuốn sách này. Hãy giữ suy nghĩ đó.

10.4.3 JobApplication operations

Trong JobApplication model mà chúng ta đã tạo cho PetSitter (xem hình 10.7), chúng ta có các hành động sau:
- "Liệt kê cho công việc List for job"
- "Chấp nhận Approve”
- "Tạo Create”
 

LIST FOR JOB

Khi chúng ta xem xét hành động " List for job," chúng ta có thể nhận thấy rằng nó tương tự như hành động "List my own" cho Job. Chúng ta đang làm việc với resources từ một schema có mối quan hệ với một nguồn resources từ schema khác. Trong " List my own," chúng ta có các công việc cho một người dùng. Trong " List for job," chúng ta có các đơn xin việc applications cho một Job. Do đó, đây là một trường hợp khác, nơi subresource là phù hợp. Trong phần giả định thư mục của chúng ta, chúng ta có thể nghĩ về mỗi công việc có một thư mục cho tất cả các đơn xin việc mà nó nhận được. Đường dẫn đó là /jobs/{id}/job-applications. Và vì đây là một hoạt động "Read," chúng ta sẽ sử dụng động từ GET.

/jobs/{id}/job-applications:
    parameters:
      - schema:
          type: integer
        name: id
        in: path
        required: true
    get:
      summary: List applications for Job
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                type: object
                properties:
                  items: 
                    type: array
                    items: 
                      $ref: '#/components/schemas/JobApplication'

Why use the format job-applications?
Chúng ta không muốn sử dụng JobApplications hoặc jobApplications trong đường dẫn /jobs/{id}/job-applications vì đó là một thực hành tốt để giữ mọi thứ trong các URL ở dạng chữ thường. Điều này là vì tên máy chủ trong các URL không phân biệt chữ hoa chữ thường, nhưng đoạn đường dẫn lại phân biệt chữ hoa chữ thường. Giữ mọi thứ ở dạng chữ thường giảm sự nhầm lẫn. Chúng ta cũng không nên sử dụng job_applications, vì URL thường được hiển thị như được gạch chân, nên gạch chân không thể phân biệt được với một khoảng trắng. Vì những lý do này, việc tách từ bằng dấu gạch ngang (gọi là "dash case" hoặc "kebab case") đã trở thành một thực hành tốt trong thiết kế URL.

APPROVE
Chủ nhân thú cưng phê duyệt đơn xin việc cho công việc của họ. Schema JobApplication chứa một trường trạng thái có thể được sử dụng để chỉ định liệu đơn xin việc đó có đang chờ xử lý, đã được chấp nhận, hay bị từ chối không. Do đó, hành động "Approve" là một phiên bản cụ thể hơn của hành động "Modify" thay đổi một JobApplication resource. Để tuân theo cách tiếp cận CRUD, chúng ta có thể tạo hoạt động tổng quát hơn với một phương thức PUT trên đường dẫn /job-applications/{id}. Để thực hiện hành động "Approve," chủ nhân thú cưng gửi một yêu cầu theo schema JobApplication với trường trạng thái được đặt thành đã chấp nhận.

Nếu có một hành động khác, như "Từ chối," có thể xuất hiện trong ứng dụng PetSitter ở tương lai, nhưng chúng ta chưa bao gồm trong domain model hiện tại, thì cũng có thể sử dụng cùng một hoạt động. Bài học ở đây là không phải mọi hành động action domain model đều tương ứng với một hoạt động operation duy nhất; đôi khi một hoạt động có thể bao gồm nhiều hành động khác nhau được phân biệt thông qua các tham số yêu cầu.


/job-applications/{id}:
    parameters:
      - schema:
          type: integer
        name: id
        in: path
        required: true
    put:
      summary: Modify Job Application
      requestBody:
        description: Update the application details
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/JobApplication'
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/JobApplication'

CREATE

Người chăm sóc thú cưng nộp đơn xin việc bằng cách tạo đơn xin việc. Một "Create" đòi hỏi một phương thức POST trên một collection endpoint. Trong trường hợp này, có hai lựa chọn cho thiết kế API:

- Chúng ta có thể sử dụng collection endpoint cho job applications, /job-applications. Thông tin về công việc mà người dùng nộp đơn áp dụng được bao gồm trong phần request body thông qua trường job_id trong schema JobApplication.
- Chúng ta có thể sử dụng subresource collection endpoint cho các đơn xin việc cho một công việc cụ thể, /jobs/{id}/job-applications, đó là end point giống như chúng ta đã sử dụng cho action "List for job." Người dùng có thể bỏ qua trường job_id từ phần request body vì đó là thông tin dư thừa.

Có lập luận ủng hộ cả hai phương pháp, vì vậy không có đúng hay sai tuyệt đối ở đây. Nhà thiết kế API của chúng ta, Max, quyết định sử dụng phương pháp thứ hai. Lập luận của anh ấy là chúng ta chưa sử dụng điểm cuối /job-applications cho đến nay, và bằng cách sử dụng /jobs/{id}/job-applications, hành động "Create (cho công việc)" đi kèm tốt với "List for job," tạo ra sự nhất quán consistency hơn trong thiết kế API.

post:
      summary: Create Job Application
      responses:
        '201':
          description: Created
          headers:
            Location: 
              schema:
                type: string
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/JobApplication'

Tuyệt vời, chúng ta đã hoàn thành toàn bộ mô hình domain và tạo một tệp OpenAPI!
Định nghĩa API mà chúng ta có là một biểu diễn của mô hình domain đó. Bạn có thể
tìm thấy định nghĩa đầy đủ tại đây: https://designapis.com/ch10/openapi.yml. Xem
hình 10.8 để biết nó trông như thế nào trong Swagger Editor.

 

Bây giờ đã có thể phát triển một frontend và một backend có thể giao tiếp với nhau thông qua API này, và cùng nhau, tạo ra một ứng dụng PetSitter đáp ứng đầy đủ các requirements đã được đề cập trong các user stories từ chương trước. Đồng thời, có lẽ vẫn còn không gian để cải thiện OpenAPI definition. Nếu bạn đã từng làm việc trên một dự án phần mềm thực tế, bạn chắc chắn biết rằng thiết kế ban đầu không bao giờ hoàn hảo và đòi hỏi sự điều chỉnh do vấn đề nảy sinh trong vòng đời phát triển.

Dựa trên kế hoạch chúng ta trình bày trong chương 9, nhà phát triển frontend Max gửi tệp OpenAPI của mình đến nhà phát triển backend Nidhi để đưa ra phản hồi trước khi triển khai. Trong chương tiếp theo, chúng ta sẽ giới thiệu một quy trình để xử lý các thay đổi cho API và xem xét một thay đổi cụ thể trong định nghĩa API.

Summary

 Mỗi concept từ domain model đều có một schema tương ứng trong tệp OpenAPI. Các attributes từ model trở thành các thuộc tính có một kiểu dữ liệu cụ thể. Mối quan hệ giữa các concept thường xuất hiện dưới dạng một thuộc tính trong một schema trỏ đến ID của schema khác. Ví dụ, một job trỏ đến người tạo nó với trường creator_user_id. Cũng có thể bao gồm một schema trong schema khác, điều này đã xảy ra với Dog và Job.
  
 OpenAPI cung cấp phần components nơi chúng ta có thể định nghĩa các schema chung, có thể tái sử dụng. Như vậy, chúng ta không cần phải lặp lại các schema ở nhiều nơi khác nhau. Thay vào đó, chúng ta có thể thêm các tham chiếu với từ khóa $ref. Ví dụ, chúng ta có thể sử dụng cùng một schema Job để create, view, list và modify công việc.

 Phương pháp CRUD cung cấp các mẫu chung để diễn đạt các hành động trong domain model như các hoạt động trong một API. Bốn hành động, create, read, update và delete, được ánh xạ vào các phương thức HTTP. Mỗi instance của một concept được gọi là "resource," và có các resource endpoint cho mỗi resource và collection endpoints để lấy nhiều resource với cùng một schema. Cũng có các subresource endpoints để liệt kê resource liên quan đến một resource khác.

 Khi chúng ta đi qua các hành động trong domain model, chúng ta cố gắng ánh xạ chúng vào CRUD và thêm các đường dẫn và hoạt động tương ứng vào tệp OpenAPI. Một số hành động tương ứng trực tiếp, như "View" với "Read" hoặc "Modify" với "Update." Đôi khi chúng ta cần diễn đạt các hành động theo cách khác. Ví dụ, chúng ta đã mô hình hóa "Approve" (đối với đơn xin việc) như một "Update" trên nguồn lực JobApplication với một giá trị cụ thể cho trường status của nó.


Chapter 11 - Building a change workflow around API design–first

This chapter covers
 Xác định các vấn đề quan trọng xung quanh phương pháp thiết kế API
 Thiết lập một quy trình để giải quyết những vấn đề đó bằng cách sử dụng GitHub
 Đi qua một ví dụ thay đổi trong định nghĩa API của chúng ta cho PetSitter

Đã định nghĩa một API, bước tiếp theo tự nhiên của chúng ta là bắt đầu xây dựng nó. Khi làm như vậy, chúng ta sẽ không tránh khỏi việc thiếu điều gì đó quan trọng sẽ gây ra vấn đề trong tương lai. Chúng ta phải xem xét cách thức thay đổi trong API definition sẽ được truyền đạt khi chúng ta không cùng nhau trong cùng một phòng - những thay đổi xuất phát từ các vấn đề được phát hiện trong quá trình triển khai hoặc yêu cầu business requirements. Trước khi bắt đầu triển khai mã, chúng ta nên dành thời gian để thiết lập một quy trình thay đổi change workflow để có thể thích nghi một cách tự tin khi có thay đổi xuất hiện.

Liên quan đến kế hoạch hành động được tạo ra trong chương 9, hiện tại chúng ta đang trong chu kỳ nháp/đánh giá. Chúng ta sẽ lặp lại API definition cho đến khi chúng ta hoàn thành thiết kế của nó, để bước tiếp theo là triển khai có thể bắt đầu.

Việc mô tả API trước khi xây dựng nó - theo cách tiếp cận thiết kế API trước - mặc dù có lợi ích rất lớn, nhưng điều này đi kèm với sự đánh đổi mà chúng ta cần phải nhận thức và có câu trả lời. Chúng ta sẽ xem xét những đánh đổi này, đặc biệt là những đánh đổi liên quan đến việc thay đổi trong API definition và giữ cho tất cả mọi người trên cùng một trang.

LƯU Ý: Phương pháp API design–first cũng có thể được gọi là contract-first, trong đó API definition hoạt động như hợp đồng giữa provider và consumer API.

Ở cuối chương này, chúng ta sẽ xây dựng một quy trình thay đổi dựa trên GitHub. Để minh họa quy trình này, chúng ta sẽ đi qua một ví dụ thực tế trong API PetSitter.

CẢNH BÁO: The change workflow trong chương này dành cho những thay đổi xảy ra trước khi một ứng dụng được phát hành. Chúng ta sẽ không tăng phiên bản hoặc thông báo những thay đổi này cho công chúng. Quy trình làm việc này sẽ làm nền tảng cho khi chúng ta cần xem xét những thay đổi công khai và đập vỡ API của chúng ta. Chúng ta sẽ bàn về phiên bản trong chương 20.

11.1 The problem

Hãy xem xét điều gì xảy ra khi một bên liên quan stakeholder phát hiện ra một vấn đề với API design. Điều này có thể là vấn đề với các phụ thuộc giữa các bên liên quan, trong đó một hoặc nhiều người bị chặn bởi người khác, như một kỹ sư frontend phải đợi một kỹ sư backend xây dựng một tính năng. Bất kỳ vấn đề nào ảnh hưởng đến một hoặc nhiều bên liên quan nên được giải quyết sớm, thay vì chờ đến sau cùng, để giảm thiểu thời gian và năng lượng lãng phí. Và, lý tưởng nhất, nó nên được giải quyết một cách nhất quán.

Chúng ta chưa sử dụng từ "stakeholder" trước đây - trong ngữ cảnh này, nó đề cập đến những người có vai trò trong dự án. Điều này bao gồm những người phát triển developers, kiến trúc sư architects, quản lý sản phẩm product managers, nhà thiết kế UX designers, v.v. Ví dụ, José có hai nhà phát triển (frontend và backend) và chính anh ấy là người điều hành dự án, tạo nên ba bên liên quan. Đó thực sự chỉ là một cách tiện lợi để nói "stakeholders." Trong toàn bộ chương này, chúng ta sẽ giả định một cấu trúc nhóm như José's, với những người làm việc độc lập trên phần frontend và backend của ứng dụng và những người khác đưa ra business requirements. Nếu điều này không phản ánh cấu trúc nhóm của bạn, bạn có thể xem xét chúng như "vai trò" có thể được chia nhỏ hơn (tạo ra các vai trò tinh tế hơn) hoặc có thể được kết hợp (dưới dạng một người với nhiều trách nhiệm).

Việc phát triển phần mềm (và API) ngày càng trở nên "nghệ thuật" hơn khi đến việc tìm ra những quy trình làm việc tốt nhất để tổ chức và quản lý một dự án thành công, với các triết lý mới xuất hiện liên tục. Hầu hết các vấn đề và giải pháp của chúng sẽ phát sinh từ cấu trúc của tổ chức, như Conway's Law đã gợi ý. Nếu bạn là một nhà phát triển độc lập làm việc hoàn toàn một mình, vấn đề của bạn sẽ khác biệt đáng kể so với tổ chức có hàng nghìn nhà phát triển và một chương trình thực tập hoạt động.

Các quy trình làm việc Workflows giống như lựa chọn đồ uống: khá cá nhân đối với cả tình huống và những người liên quan. Không có một lựa chọn nào phù hợp cho tất cả mọi người. Khi đến việc đề xuất một quy trình làm việc workflow, chúng tôi không muốn sử dụng những từ ghê tởm như "nó phụ thuộc it depends." Ôi, ghê tởm! Chúng tôi mạnh mẽ tin rằng việc hiển thị một quy trình làm việc cụ thể - một quy trình làm việc cho một nhóm như đội ngũ PetSitter của chúng tôi - là hữu ích để bắt đầu. Điều này không có nghĩa là bạn có thể luôn thoát khỏi trách nhiệm và luôn có thể áp đặt quy trình này cho mọi dự án. Bạn vẫn cần xem xét các sự tinh tế của tình huống cụ thể của bạn và điều chỉnh quy trình để phù hợp.

Trong thiết kế và triển khai API, có một số điểm chung quan trọng qua cấu trúc tổ chức, đặc biệt là khi có nhiều người tham gia vào thiết kế hoặc triển khai API:

- Cần tìm nguồn thông tin chính xác cho API - nơi duy nhất bạn luôn có thể tìm thấy phiên bản API được thống nhất nhất mới nhất.
- Sẽ không tránh khỏi việc cần thay đổi thiết kế API khi gặp vấn đề trong quá trình triển khai. Quan trọng là phải thông báo những thay đổi đó đến các bên liên quan khác.
- Sau khi thông báo các thay đổi, cũng cần một cách để đạt được sự nhất trí để tích hợp những thay đổi đó.
- Cần biết những thay đổi gì đã xảy ra kể từ lần cuối cùng bạn, một bên liên quan, xem xét API definition.

What’s a “single source of truth,” and why is it important?

Nguồn dữ liệu đơn duy nhất
single source of truth cho một API là hợp đồng của nó hoặc API definition của nó. Vì mã nguồn sẽ được triển khai để phù hợp với thiết kế đó, API definition sẽ cung cấp câu trả lời nếu có câu hỏi như "Cái nào đúng, A hay B?"

Một API - application programming interface - là một giao diện theo định nghĩa. Mỗi API xác định ranh giới giữa hai thành phần phần mềm riêng biệt, nhưng cũng giữa con người humans đứng sau những thành phần đó. Cả hai bên, nhà sản xuất và người tiêu dùng, cần tuân theo API contract để làm cho toàn bộ hệ thống hoạt động. Đây là nơi mà những đau đầu của việc phát triển phần mềm thực sự bắt đầu trở nên rõ ràng, và đó là lý do tại sao việc đồng thuận về nguồn dữ liệu đơn duy nhất source of truth cho một API là rất quan trọng.


Khi thiết kế một API từ đầu (và sau đó thêm vào đó), bạn sẽ tự nhiên phát hiện ra những thách thức của việc triển khai một API theo phương pháp thiết kế trước. Hãy tóm tắt và khám phá chúng dưới dạng các bước (xem cũng hình 11.1) chúng ta cần thực hiện:

- Xem API definition mới nhất
- Đề xuất các thay đổi Suggest changes
- So sánh các thay đổi với bản sao làm việc
- Chấp nhận các thay đổi

Chúng ta cần một hệ thống có nhịp điệu để đưa stakeholders hướng về một mục tiêu chung.

 

Trong chương này, chúng ta sẽ xây dựng một quy trình làm thay đổi workflow for making changes đối với API definition. Quá nhiều lý thuyết khiến cho Jack trở nên nhàm chán (hoặc có phải là không đủ thời gian chơi?), vì vậy ở phần cuối của chương này, chúng ta sẽ thực hiện một thay đổi cho API PetSitter và xem làm thế nào mỗi trong ba bên liên quan đến thay đổi đó. Đến cuối chương, chúng ta sẽ đã thiết lập một quy trình sử dụng GitHub, giải quyết vấn đề quan trọng về cách thông báo về các thay đổi trong quá trình thiết kế API dựa trên design–first approach.

11.2 Communicating and reacting to change

Ở trung tâm của quy trình là ý tưởng rằng các thay đổi trong thiết kế API là không thể tránh khỏi. Các thay đổi chúng ta quan tâm cụ thể là những thay đổi xuất hiện trong quá trình triển khai - những điều chúng ta không thể dự đoán được khi thiết kế API - mặc dù có những lý do khác khiến một thiết kế phải thay đổi sau khi bắt đầu triển khai (như là business requirement bị thiếu, ví dụ).

Chúng ta phải cân nhắc giữa việc bỏ bao nhiêu thời gian cho việc thiết kế so với thời gian cần để triển khai. Nếu chiếm ít thời gian hơn trong việc thiết kế, chúng ta có thể cần phải thực hiện những thay đổi đắt tiền sau này. Nếu chiếm quá nhiều thời gian trong việc thiết kế, chúng ta có nguy cơ phải chờ đợi quá lâu để triển khai. Chúng ta không thể giải quyết tất cả các vấn đề ngay tại thời điểm thiết kế, nhưng đó là thời điểm rẻ nhất để giải quyết chúng.

Do đó, chúng ta có thể giả định rằng sẽ có các thay đổi. Câu hỏi là làm thế nào để xây dựng một quy trình để làm điều này. Stakeholders sẽ cần có khả năng đặt ra một vấn đề trong thiết kế, đề xuất một thay đổi và đạt được sự đồng thuận về thay đổi đó. Họ cũng sẽ cần phải phản ứng lại các thay đổi được thực hiện bởi các bên liên quan khác. Những thay đổi này cần phải dựa trên source of truth cho thiết kế. Mà không có một source of truth, chúng ta có thể lãng phí thời gian làm việc trên các tính năng cũ, không còn hiệu lực!

Đây là những điểm quan trọng mà quy trình làm việc của chúng ta cần giải quyết để trở nên hiệu quả. Hãy mở rộng thêm một chút về chúng:

 single source of truth for the API definition - Mọi người cần biết phiên bản định nghĩa hiện tại và được thống nhất là phiên bản nào. Rất nhiều sự nhầm lẫn xảy ra khi có nhiều tài liệu đang tồn tại (trong email, Slack, GitHub pull requests, v.v.), và điều này gây trễ thời gian thực sự. Chúng ta cần tìm một nơi duy nhất mà API definition của chúng ta có thể tồn tại và đồng thuận rằng nó nói lên sự thật truth và là truth toàn bộ.

 A way to suggest a change, and a way to agree to that change - Có nhiều stakeholders, và mỗi bên sẽ có các ưu tiên và nhu cầu riêng của mình. Mỗi bên cần có khả năng đề xuất một thay đổi đối với API definition, và cần có một cơ quan (hoặc quyền lực, v.v.) chấp nhận thay đổi đó.

 A way of viewing changes made since you last saw the API definition - Là một bên liên quan stakeholders, bạn có thể có một ý tưởng cũ về API là gì, vì vậy bạn cần một cách để xem sự khác biệt giữa phiên bản API bạn nhớ và API hiện tại. Nếu bạn là một nhà phát triển, điều này sẽ mang lại cho bạn các requirements cho các thay đổi API bạn cần triển khai.

Bảng 11.1 liệt kê các yêu cầu này để chúng ta có thể giải quyết và tìm ra các giải pháp.


 

Là một nhà phát triển phần mềm, bạn có lẽ đã có một workflow đáp ứng được những nhu cầu này trong mã nguồn của bạn. Tất cả những vấn đề này có thể được giải quyết một cách hợp lý bằng hệ thống quản lý phiên bản, như Git. Trong luồng công việc đầu tiên của chúng ta cho thiết kế API, đó chính xác là điều chúng ta sẽ sử dụng. Cụ thể hơn, chúng ta sẽ sử dụng GitHub và tính năng pull request của nó, mặc dù bạn có thể sử dụng hệ thống quản lý phiên bản yêu thích của mình và vẫn làm tốt.

LƯU Ý: GitHub có đủ cho một phương pháp API design-first không? Chắc chắn có thể; có các công cụ cụ thể cho API cung cấp nhiều tính năng hơn cho API design và quản lý API definition. Mặc dù có vẻ hấp dẫn để đề cập đến chúng trong cuốn sách này, chúng tôi đã nỗ lực giữ nó linh hoạt nhất có thể và tập trung vào các tuyên bố vấn đề gốc problem statements root liên quan đến OpenAPI và các ứng dụng của nó. Các công cụ cụ thể (như SwaggerHub, Stoplight và Apiary) sẽ thay đổi để thích ứng với thị trường, nhưng các problem statements sẽ không thay đổi trong thời gian dài.

Chúng ta đã thảo luận về các điểm quan tâm trong luồng công việc thay đổi của chúng ta. Bây giờ hãy xem làm thế nào chúng ta có thể sử dụng GitHub để giải quyết chúng.

11.3 GitHub as our workflow engine

GitHub là một dịch vụ tuyệt vời để quản lý mã nguồn, và nó được xây dựng trên Git version
control system tuyệt vời. Có hai lý do chúng ta muốn sử dụng GitHub (hoặc BitBucket, GitLab, v.v.) thay vì chỉ sử dụng Git:

 Chúng ta muốn một nơi rõ ràng nơi các stakeholders mới và hiện tại có thể lấy phiên bản mới nhất của API definition.
 Chúng ta muốn một nơi trung tâm để đề suất suggest, review và merge các thay đổi.

Điều này không có nghĩa là bạn không thể sử dụng Git một mình để đạt được những mục tiêu này. Điều này có nghĩa là bạn sẽ cần tìm ra một cách khác để tập trung hệ thống hoặc ít nhất là làm cho nó truy cập được cho tất cả các bên liên quan, chính xác như GitHub đang làm cho chúng ta.

Chúng tôi có ba mối quan tâm concerns  liên quan đến API workflow của chúng tôi, vì vậy hãy bắt đầu giải quyết chúng với GitHub.


11.3.1 A single source of truth

Tạo ra một nguồn thông tin duy nhất single source of truth cho API definition là một công việc dễ dàng, vì nó là một phần cốt lõi của GitHub. GitHub sử dụng các nhánh (branches), và chúng ta có thể chọn một nhánh để làm vai trò của chúng ta là phiên bản "mới nhất và tốt nhất". Sau này, chúng ta có thể khai báo một nhánh tính năng feature branch là nguồn thông tin chính khi chúng ta phát triển các tính năng cụ thể, nhưng cuối cùng, chúng ta sẽ hợp nhất chúng trở lại vào phiên bản "mới nhất và tốt nhất". Vì sự đơn giản, chúng ta sẽ không đi sâu vào tên của các nhánh có thể là gì. Chúng ta chỉ nói rằng nhánh chính (main branch) giữ phiên bản mới nhất của API definition.

11.3.2 Suggesting a change

Để đề xuất một thay đổi trong hệ thống workflow của chúng ta, chúng ta sẽ nói rằng bạn có thể sửa đổi bất kỳ phần nào của API definition trong nhánh Git của bạn, và sau đó sử dụng nó để đề xuất các thay đổi vào nhánh Git main. Nếu ngược lại, nếu bạn có một vấn đề nhưng không có ý tưởng về cách thay đổi API, bạn có thể đơn giản là đưa ra một vấn đề (issue) trên GitHub thay vì.

11.3.3 Agreeing on a change

Đồng thuận về các thay đổi có thể khá khó khăn. Dưới đây là một số cách chúng ta có thể thực hiện điều đó:

 Đặt một người hoặc nhóm có trách nhiệm duy nhất đối với API, và người đó hoặc nhóm đó sẽ 
phê duyệt sign off mọi thay đổi trong API.

 Tất cả các bên liên quan cần phải đồng thuận. Điều này thích hợp cho các nhóm nhỏ, nhưng không phải là lựa chọn phù hợp cho các nhóm lớn.

 Chấp nhận phiếu bầu về một thay đổi. Tùy thuộc vào kích thước của nhóm, có thể chỉ cần hai phiếu là đủ để chấp nhận một thay đổi trong API.

Bạn sẽ cần quyết định phương án nào phù hợp với cấu trúc tổ chức của bạn - bạn có thể xem các lựa chọn trong hình 11.2. Một điểm quan trọng cần nhấn mạnh là độc lập tương đương với tốc độ, nhưng nhiều ánh mắt hơn trên một vấn đề giảm thiểu sai sót. Hãy cân nhắc kỹ lưỡng về sự cân bằng đó! Đối với José và đội của anh ấy, chúng ta sẽ nói rằng ít nhất một bên liên quan khác cần đồng thuận. Điều này sẽ giữ cho tiến triển diễn ra.

 

Bất kể chúng ta ủy quyền cho ai, cơ chế để chấp nhận một thay đổi là giống nhau trên GitHub: đó là pull request (yêu cầu kéo).

GITHUB PULL REQUESTS

Dưới đây là các bước chúng ta sẽ thực hiện trên GitHub để chấp nhận một thay đổi:

1. Tạo một pull request từ nhánh của bạn đến nhánh main để hiển thị thay đổi đề xuất.
2. Add reviewers vào pull request. Mỗi reviewer có thể phê duyệt pull request.
3. Hợp nhất (merge) pull request sẽ chấp nhận thay đổi và cập nhật nhánh chính.

Đối với stakeholders không tham gia cuộc trò chuyện, họ sẽ cần một cách để xem xét tất cả các thay đổi được thực hiện kể từ khi họ cuối cùng xem định nghĩa API. Điều này dẫn đến mục tiếp theo của quy trình làm việc của chúng ta, một cách để xem xét các thay đổi viewing changes.

11.3.4 A way of viewing changes (based on an older version)

Đây là một phần khó khăn nhất cho đến nay. Chúng tôi sẽ sử dụng một cách tiếp cận khá tẻ nhạt và dựa vào tính năng text-diffing của Git để hiển thị sự khác biệt giữa hai API definitions. Chúng tôi đã mong muốn có thể giới thiệu cho bạn một công cụ chuyên dụng so sánh OpenAPI definitions, nhưng không có cái nào đủ ổn định để đưa vào in ấn. Và trong khi một công cụ như vậy sẽ tuyệt vời và hữu ích, chúng tôi đã thấy rằng việc so sánh các tệp văn bản hoạt động đủ tốt trong thực tế.

Mỗi bên liên quan stakeholder sẽ cần biết phiên bản của API definition mà họ đã xem cuối cùng để so sánh với phiên bản mới nhất. Trong hệ thống workflow của chúng tôi trên GitHub, chúng tôi có ít nhất hai (và có thể nhiều hơn) cách để đạt được điều này:

 Chúng ta có thể dựa vào stakeholders checking for changes trước khi thực hiện git pull (trên cùng một nhánh), nhưng điều này có chút rủi ro. Trong Git, có lý do tốt để khuyến khích việc kéo (pull) càng thường xuyên càng tốt vì các lý do không liên quan, vì vậy việc dựa vào bên liên quan để so sánh định nghĩa API trước khi kéo là không khả thi, chủ yếu là do không có tuyên bố rõ ràng về định nghĩa API bạn đang làm việc.

 Hoặc, chúng ta có thể thiết lập một quy trình rõ ràng bằng cách yêu cầu mọi bên liên quan merge các thay đổi từ nhánh main vào một nhánh cụ thể cho từng bên liên quan. Chúng ta có thể tạo ra một nhánh như vậy cho mỗi bên liên quan. Họ chỉ merge khi họ sẵn sàng, và lúc đó họ có thể so sánh để xem liệu có bất kỳ thay đổi nào có thể thực hiện được cho họ hay không.

Làm thế nào họ có thể xem xét các thay đổi? Bởi vì họ có nhánh riêng của mình, họ có thể sử dụng GitHub để so sánh nhánh của họ với nhánh main và xem xét những thay đổi đã được thực hiện (xem hình 11.3). Như một ưu điểm bổ sung, họ có thể thực hiện các thay đổi trên nhánh của họ để đề xuất những thay đổi cho nhánh chính. Điều này sẽ hoạt động tốt cho mục đích của chúng tôi.


 
11.4 Tying the GitHub workflow together

Bây giờ khi chúng ta đã xử lý từng điểm trong ba điểm của mình một cách riêng biệt, chúng ta cần kết hợp chúng lại thành một hệ thống hợp nhất. Chúng ta có thể liệt kê các bước cho các hành động phổ biến (như đề xuất một thay đổi) và hiển thị một biểu đồ thân thiện để tạo ra một mô hình tư duy về những gì đang diễn ra.
Bước đầu tiên là thiết lập quy trình làm việc của chúng ta và cài đặt GitHub.

11.4.1 Setting up GitHub and the source of truth
Chúng ta sẽ bắt đầu với một GitHub repository (còn được gọi là "repo"). Chúng tôi sẽ cung cấp mô tả chi tiết về những gì chúng tôi đang làm, nhưng chúng tôi không khuyến nghị bạn coi chúng như là hướng dẫn từng bước và thực hiện theo khi đang đọc. Thay vào đó, đọc chúng đến cuối để hiểu những gì chúng tôi đang làm, và sau đó quyết định liệu bạn muốn thực hành sử dụng GitHub với API PetSitter hay bạn muốn điều chỉnh quy trình cho dự án API của bạn.

SETTING UP AN API REPOSITORY
Trước tiên, bạn nên thiết lập một kho lưu trữ GitHub sao cho những điều sau đây là đúng:
1. Có một nhánh main được đặt làm nhánh mặc định.
2. Có một nhánh cho mỗi bên liên quan, chẳng hạn như frontend, backend và business.
3. Nhánh main nên chứa định nghĩa OpenAPI (ví dụ: petsitter.0.0.oas.yml).
Bạn sẽ tìm thấy một hướng dẫn chính thức của GitHub tại đây: https://guides.github.com/activities/hello-world. Trong đó, bạn sẽ thấy cách tạo một kho lưu trữ GitHub mới, các nhánh và commit đầu tiên của bạn. Nếu bạn đã quen thuộc với những khái niệm này, bạn có thể thoải mái đọc nhanh.
NAMING CONVENTIONS
Trong ví dụ của chúng ta, tệp OpenAPI definition được đặt tên là petsitter.0.0.oas.yml. Hãy xem xét quy ước đặt tên này và phân tích nó:
 Đương nhiên, bạn cần đặt tên cho API, và ở đây nó được đặt tên theo tên sản phẩm, PetSitter.
 API của bạn sẽ có các phiên bản. Không nên có bất kỳ version changes nào trong giai đoạn tiền phát hành prerelease, vì API có thể coi là linh hoạt fluid. Bạn có thể sử dụng 0.0 làm số phiên bản tiền phát hành.
 Thêm ".oas" cho biết rằng đó là OpenAPI definition mà không cần người dùng phải nhìn vào bên trong.
 Đó là một tệp YAML, vì vậy bạn sẽ cần một phần mở rộng là .yml hoặc .yaml.

LƯU Ý: OAS trong tên tệp của PetSitter (petsitter.0.0.oas.yml) là viết tắt của OpenAPI Specification, và từ viết tắt này thường được sử dụng như một cách ngắn gọn hơn để nói "OpenAPI." Điều này khác biệt với OpenAPI Initiative (OAI), đề cập đến folks những người giúp hướng dẫn specification.
Chúng tôi sẽ giải thích về phiên bản hóa versioning của API definitions trong chương 20. Tại thời điểm đó, sau khi PetSitter ra mắt, điều này sẽ trở nên ngày càng quan trọng. Hiện tại, chúng tôi chỉ sẽ giữ ở phiên bản 0.0.
LƯU Ý: Một cái nhìn nhanh cho những người đã quen thuộc với ngữ nghĩa versioning:
Thêm các phiên bản chính major version và phụ minor version chỉ ra liệu version có thêm tính năng (minor version) hay không, hoặc liệu API có thay đổi đột ngột (major version).

Chúng tôi đã rõ ràng bỏ qua các phiên bản vá patch versions, vì chúng không ảnh hưởng đến ngữ nghĩa của API, và chúng tôi không muốn có một tệp cho mỗi thay đổi nhỏ chúng tôi thực hiện, trừ khi nó ảnh hưởng đến ngữ nghĩa. Nếu chúng tôi thực hiện một thay đổi thêm vào (thêm một hoạt động mới), chúng tôi có thể tăng minor version. Nếu chúng tôi thực hiện một thay đổi đột ngột (như loại bỏ một tham số), chúng tôi có thể tăng major version.
11.4.2 Steps in our GitHub workflow
Mỗi stakeholder cần một cách để thực hiện các công việc sau:
 Xem API definition mới nhất
- Truy cập GitHub repo và xem nhánh main. Trong đó sẽ có API definition mới nhất và tốt nhất.
Đề xuất một thay đổi mới 
1. Tạo một nhánh mới với thay đổi.
2. Tạo một pull request đối với nhánh chính. Thêm mô tả vào pull request để hiển thị động cơ đằng sau thay đổi.
3. Thêm đồng nghiệp của bạn như người xem (reviewers).

Xem xét và chấp nhận một thay đổi 
1. Khi bạn nhận được thông báo về một pull request đang chờ, xem xét các thay đổi và thêm ý kiến của bạn.
2. Nếu bạn hài lòng, approve pull request.
3. Quyền lực (hoặc chủ sở hữu của pull request) sau đó có thể merge thay đổi sau khi đủ người xem đã chấp nhận.

So sánh thay đổi với bản sao làm việc working copy
1. Khi nhánh chính có thay đổi mới, so sánh nó với nhánh của bạn để xem các thay đổi kể từ lần hợp nhất cuối cùng, sử dụng Git(Hub) diffs.
2. Ghi chú bất kỳ công việc nào bạn cần thực hiện dựa trên các thay đổi (nếu có).
3. Hợp nhất nhánh main vào nhánh của bạn để giữ nó được cập nhật keep it up to date.

Xem lại bảng 11.1, bây giờ chúng ta có thể điền vào chỗ trống xem bảng 11.2.
 
Bây giờ khi chúng ta đã mô tả cách GitHub hoạt động, hãy quay lại thế giới của API definitions. Với việc chúng ta đã có một quy trình làm việc GitHub (ít nhất là trên giấy), đã đến lúc thử nghiệm một thay đổi thiết kế cho API definitions của chúng ta, PetSitter.

11.5 A practical look at the workflow
Đội của José đã quyết định áp dụng một workflow chính thức hơn để thực hiện các thay đổi thiết kế cho API definition của họ. Điều này là hợp lý, vì mặc dù đội của họ nhỏ, họ không thể tổ chức cuộc họp cho mọi thay đổi nhỏ trong API design, nhưng họ cần biết đến từng thay đổi. Một workflow chính thức đã trở thành điều cần thiết đối với họ.
Hãy xem cách một thay đổi duy nhất đi vào thiết kế bằng cách sử dụng quy trình GitHub mới của chúng ta. Nidhi (kỹ sư backend của PetSitter) đang xem xét các thiết kế backend cho ứng dụng khi cô phát hiện rằng mặc dù domain model nói rằng cần có một cách để xóa công việc, nhưng API definition mà Max chia sẻ lại thiếu thao tác này. Điều này chỉ là một sơ ý đơn giản từ phía anh ấy. Cô biết rằng điều này sẽ cần thiết, vì vậy cô muốn đề xuất điều này như một thay đổi nhỏ cho thiết kế. Hãy xem quy trình của cô ấy.

11.5.1 Creating and suggesting DELETE /jobs/{id}
Thay đổi này khá nhỏ, và Nidhi không gặp vấn đề gì khi viết trực tiếp vào file definition trên nhánh của mình. Cô không dự kiến rằng điều này sẽ cần một phiên thiết kế, cũng như cô không cần phải thực hiện bất kỳ nghiên cứu nào về điều này.
Cô mở Swagger Editor (công cụ yêu thích của cô cho công việc này, tuy nhiên bất kỳ công cụ nào cũng có thể sử dụng được) và sao chép định nghĩa vào đó. Cô thêm các thay đổi của mình và commit thay đổi vào nhánh của mình trên GitHub – backend branch.

/jobs/{id}:
#...
delete:
summary: Delete Job
responses:
'204':
description: No Content

Sau khi commit thay đổi của mình, cô ấy tạo một pull request để đề xuất thay đổi này đến đồng nghiệp của mình. Cô ấy thêm một message mô tả đơn giản các thay đổi của mình, theo dạng sau:

Title:
> Add the missing DELETE /job/{id} operation.
Description:
> Add the missing DELETE /job/{id} operation.
> I believe we’ll need this when the user wants to delete the Job.

Cô ấy cũng thêm các reviewers, Max và José. Hình 11.4 hiển thị pull request của cô ấy trong giao diện người dùng GitHub, đầy đủ với title, description và reviewers ngay trước khi nộp.
 
 

11.5.2 Reviewing and accepting changes
José đang đi nghỉ, điều này khiến Max trở thành stakeholder duy nhất khác có thể approve thay đổi. Sau khi Nidhi tạo pull request và tùy thuộc vào cách Max đã thiết lập thông báo của mình, anh ta sẽ nhận được thông báo gần như ngay lập tức.
Ngay khi Max sẵn sàng, anh ta có thể xem xét pull request và đưa ra phản hồi của mình. Anh ta xem xét ba điều:
1. Phần động cơ đằng sau thay đổi có ý nghĩa không? Liệu điều này cần nghiên cứu thêm không?
2. Thay đổi chính nó có ý nghĩa không?
3. Đây có phải là một thay đổi gây ra sự phá vỡ không breaking change?

Max nghĩ trong lòng, "Ồ, cái này là một điều quên lơ là - tôi chỉ đơn giản quên thêm nó vào. Anh ta không cần phải nghiên cứu thêm về thay đổi vì nó rất rõ ràng. Nhìn vào pull request, Max có thể thấy rõ thay đổi duy nhất trong định nghĩa API, và nó trông nhất quán với các hoạt động DELETE khác. Thay đổi này là bổ sung - nó không loại bỏ chức năng nào khỏi API, nên không có sự thay đổi làm hỏng gì cả. Anh ấy hài lòng với pull request.

Anh ấy kiểm tra tâm lý qua ba câu hỏi:
1. Động cơ có ý nghĩa. Họ sẽ cần có khả năng xóa công việc trong tương lai.
2. Thay đổi là hợp lệ và phù hợp với động cơ. Một hoạt động đơn đã được thêm vào và trông có vẻ hợp lệ.
3. Thay đổi sẽ không làm hỏng người tiêu dùng; nó chỉ thêm một hoạt động.

Anh ấy không có vấn đề gì khi approve thay đổi, mặc dù anh ấy không thể kiềm chế được bản thân và thảo luận thêm một chút về điều gì đó mà anh ấy để ý (xem hình 11.5).

 
Nidhi nhận thấy rằng description cũng bị thiếu, và cô ấy thêm một commit mới. Điều này sẽ tự động cập nhật pull request sau khi cô ấy đẩy commit. Bây giờ thay đổi có thể được hợp nhất.

11.5.3 Comparing older branches to the latest
Thời gian trôi qua và José trở lại từ kỳ nghỉ (xứng đáng). Anh ta bây giờ cần phải nhanh chóng bắt kịp với thiết kế API đã diễn ra. Anh ta có một số lựa chọn, tùy thuộc vào thông tin anh ta đang tìm kiếm. Ví dụ, nếu anh ta chỉ quan tâm đến API definition mới nhất trông như thế nào, anh ta có thể ghé thăm nhánh main và quét qua - không cần thêm hành động. Nhưng nếu anh ta muốn xác nhận chính xác những thay đổi nào đã xảy ra để xem liệu bất kỳ chi tiết nào sẽ ảnh hưởng đến anh ta, anh ta có thể so sánh bằng cách sử dụng nhánh của mình (nhánh business).

Khi so sánh các nhánh, anh ta quan tâm đến việc trả lời những câu hỏi sau:
 Những sự khác biệt chính xác giữa lần cuối cùng anh ta xem API definition và phiên bản hiện tại là gì?
 Có ảnh hưởng nào từ những thay đổi đó đối với sự quan tâm của anh ta đến API không? Đối với một bên liên quan kinh doanh, điều này có thể liên quan đến việc liệu một thay đổi có tăng chi phí hay cho phép thêm tính năng trong tương lai không.
Thay vì tạo một pull request giữa <some-branch> và main, José tạo một pull request giữa main và nhánh của anh ta, business (nói cách khác, ngược lại, để main sẽ được hợp nhất vào business). Điều này sẽ cho phép anh ta xem xét các thay đổi. Khi đó, anh ta có thể cập nhật nhánh của mình đến phiên bản mới nhất bằng cách merging pull request himself (tự hợp nhất với pull request).

Để hợp nhất nhánh main vào nhánh business trên máy của José, anh ta có thể sử dụng các bước sau bằng sử dụng Git:
1. Đảm bảo José đang ở trên nhánh business
   git checkout business
2. Fetch các thay đổi mới nhất từ nhánh main
   git fetch origin main
3. So sánh sự khác biệt giữa nhánh main và nhánh business
   git diff business..main
4. Nếu không có sự không nhất quán nào, hợp nhất nhánh main vào nhánh business  
   git merge main
5. Giải quyết xung đột nếu có
   Trong trường hợp có xung đột (conflicts), Git sẽ thông báo và José cần giải quyết chúng. Anh ta có thể sử dụng các lệnh như `git mergetool` hoặc chỉnh sửa các tệp xung đột trực tiếp.
6. Commit thay đổi sau khi hợp nhất:
   git commit -m "Merge main into business"
7. Push nhánh `business` lên remote repository (GitHub):
   git push origin business

Vì Nidhi chỉ thêm một hoạt động duy nhất, sự khác biệt sẽ trông như hình 11.6.
José chỉ thấy một thay đổi và nó không ảnh hưởng đến anh ta. Anh ta có thể hợp nhất nhánh và tiếp tục với công việc hàng ngày của mình, tự tin về những gì đã xảy ra với thiết kế API trong thời gian anh ta vắng mặt.


 

11.5.4 What we’ve done
Trong chương này, chúng tôi đã đề xuất một quy trình làm việc cho các thay đổi thiết kế API dựa trên ba điểm quan trọng và sử dụng GitHub như một cách cụ thể để thực hiện những thay đổi thiết kế đó. Có nhiều công cụ quy trình làm việc cụ thể cho API mà chúng tôi khuyến khích bạn xem xét những công cụ giảm đi nhiều công sức thủ công  nhưng chúng hướng đến các đối tượng khác nhau, và bạn sẽ cần xem xét mức độ quan trọng của các tính năng mỗi nền tảng đối với quy trình làm việc thiết kế API của bạn. Hy vọng giải pháp GitHub sẽ đủ để giúp bạn khám phá cách thiết kế API có thể đồng thời là một quá trình tăng dần, không đồng bộ và tổng thể là mượt mà.

Summary
 API design–first là một phương pháp giải quyết các vấn đề thiết kế một cách chi phí thấp nhất, nhưng có những điểm quan trọng quyết định để quá trình diễn ra mượt mà: làm thế nào để source of truth cho một API; làm thế nào để tạo ra hoặc đề xuất các thay đổi, xem xét chúng và chấp nhận chúng; và làm thế nào để so sánh các thay đổi được thực hiện, từ góc độ của bạn (so với lần cuối cùng bạn xem xét thiết kế API).
 Có nhiều cách để accept các thay đổi được thực hiện trong thiết kế. Tùy thuộc vào kích thước của đội của bạn, bạn có thể chỉ định ai đó làm một cơ quan duy nhất và chỉ cho phép họ chấp nhận các thay đổi. Thường thì bạn sẽ cho phép các thay đổi được chấp nhận nếu một hoặc nhiều người xem xét đồng ý với thay đổi. Phương pháp sau cùng là phương pháp có khả năng mở rộng nhất.
 GitHub có thể được sử dụng để quản lý quy trình làm việc thiết kế API, và chúng tôi đã tạo ra một cách tiếp cận đơn giản để giải quyết ba vấn đề quan trọng của phương pháp API design–first. Source of truth là một nhánh được gọi là main. Chúng tôi sử dụng pull requests để suggest, review và accept các thay đổi. Và chúng tôi đã tạo ra một nhánh riêng cho mỗi bên liên quan và sử dụng pull requests để cập nhật chúng một cách rõ ràng khi bên liên quan quan tâm đến việc xem xét và xử lý các thay đổi.

Chapter 12 – Implementing frontend code and reacting to changes
 Triển khai mã nguồn frontend và phản ứng với các thay đổi


This chapter covers
 Xây dựng phần frontend với một máy chủ giả mạo mock server (Prism) dựa trên OpenAPI 
 Xác định các vấn đề thiết kế design issues phát hiện trong quá trình triển khai 
 Sử dụng OpenAPI examples để xác minh rằng các thay đổi API có ý nghĩa 



Khi chia một ứng dụng web thành phần frontend và backend, chúng ta tạo ra một vấn đề phụ thuộc dependency issue. Thông thường, backend cần được xây dựng trước khi frontend có thể bắt đầu. Trong chương này, chúng ta sẽ xem xét cách xây dựng frontend mà không cần backend đã triển khai. Điều này sẽ giúp chúng ta bắt đầu phát triển ngay lập tức và cũng cho phép chúng ta phát hiện các vấn đề thiết kế sớm hơn, khi việc thêm chúng vào backend vẫn chi phí thấp.

Tuy nhiên, trước khi xây dựng frontend, chúng ta có một số lựa chọn để xem xét, chủ yếu liên quan đến câu hỏi "Nơi chúng ta nên giả mạo?" Chúng ta có các lựa chọn sau đây:
 Giả mạo dữ liệu trên view layer.
 Giả mạo dữ liệu trong một trung tâm lưu trữ dữ liệu central data store (nghĩ đến Redux, MobX, RxJS, v.v.).
 Thiết lập một máy chủ API giả mạo mock API server.

Lựa chọn đầu tiên là nhanh nhất, nhưng làm mọi thứ trở nên lộn xộn. Chúng ta cần cẩn thận về nơi chúng ta đã thêm dữ liệu giả mạo và khi nào chúng ta loại bỏ nó. Phương pháp này chỉ nên được sử dụng cho các bài kiểm tra ngắn hạn rất ngắn.

Việc giả mạo dữ liệu trong một trung tâm lưu trữ dữ liệu tốt hơn, vì chúng ta có một nơi nơi nó sẽ được giả mạo. Điều này cho phép chúng ta cũng chuyển đổi nó bật/tắt trong mã khi đến lúc tích hợp với backend. Nhược điểm là chúng ta vẫn có mã giả mạo trong các tệp nguồn của mình.

Lựa chọn cuối cùng là giữ mã nguồn frontend sạch sẽ (không làm nó bẩn bởi dữ liệu giả mạo) và thay vào đó thiết lập một máy chủ giả mạo. Phương pháp này có nhược điểm của nó, nhưng nó là phương pháp sạch sẽ nhất và yêu cầu ít (gần như không có) thay đổi mã khi đến lúc chuyển sang backend thực tế. Một trong nhược điểm của phương pháp này là chúng ta không thể viết logic trong máy chủ giả mạo của mình nó chỉ phục vụ dữ liệu mà chúng ta bảo nó phục vụ.

12.1 The problem
Để xây dựng frontend mà không cần backend, chúng ta sẽ sử dụng một mock server được gọi là Prism. Chúng ta cũng sẽ đối mặt với thách thức không tránh khỏi khi xử lý một thay đổi thiết kế API đã bị bỏ sót trong quá trình thiết kế ban đầu. Chúng ta sẽ cập nhật local API definition của mình và sử dụng các ví dụ để kiểm thử các tình huống khác nhau và các trường hợp biên của API. Đến cuối chương này, chúng ta sẽ đề xuất một thay đổi thiết kế cho các bên liên quan dựa trên yêu cầu cần thiết và chúng ta sẽ đã xác minh rằng thay đổi đó sẽ giải quyết vấn đề của chúng ta.

LƯU Ý: Thay đổi mà chúng ta sẽ thực hiện đối với API sẽ sửa một thiếu sót từ OpenAPI definition hiện tại. Đó là một sai lầm mà chúng tôi, những người tác giả, phát hiện ra trong quá trình triển khai trang web minh họa. Đúng, chúng tôi thậm chí còn mắc sai lầm trong quá trình thiết kế các API mock!
Chúng ta sẽ thực hiện các bước sau đây:
1. Thiết lập một mock server.
2. Học cách build trên against một mock server.
3. Xác định một hoạt động bị thiếu.
4. Thiết kế một giải pháp khả thi possible solution.
5. Xác minh rằng solution hoạt động cho trường hợp sử dụng của chúng ta.

12.2 Setting up Prism
Prism là một open source mocking server đọc một OpenAPI definition và cung cấp các phản hồi phù hợp với cấu trúc dữ liệu. Nói cách khác, nó cung cấp những gì bạn đã mô tả trong OpenAPI definition. Đó là một công cụ đơn giản và đang ngày càng được ủng hộ.

12.2.1 Installing Prism

12.2.2 Verifying that Prism works
Để kiểm thử Prism, chúng ta sẽ cần một định nghĩa OpenAPI. Hãy lấy định nghĩa API PetSitter mới nhất từ đây: https://designapis.com/ch12/openapi.yml. Lưu tệp đó vào máy cục bộ và đặt tên là openapi.yml.

Bây giờ bạn có thể khởi chạy một máy chủ Prism bằng lệnh sau:
prism mock -p 8080 ./openapi.yml
Điều đó sẽ tạo ra đầu ra tương tự như sau.
 
Voilà! Nó sẽ tồn tại cho đến khi bạn cần. Khi bạn đã sử dụng xong, bạn có thể nhấn Ctrl-C (hoặc Cmd-C) để thoát khỏi nó.

Như bạn đã đoán, máy chủ giả mạo sẽ chạy trên cổng 8080. Nếu bạn thử truy cập 127.0.0.1:8080 hoặc localhost:8080 trong trình duyệt, bạn sẽ thấy một lỗi 404 nào đó. Điều này là bình thường, vì nó đang nói cho chúng ta biết rằng chúng ta không có một tuyến đường cho /, điều này là đúng.

LƯU Ý: Nếu Prism không khởi động được, hãy kiểm tra tài liệu xem nó có yêu cầu một phiên bản mới hơn của Node.js hoặc một phụ thuộc khác không: https://github.com/stoplightio/prism. Các chi tiết có thể thay đổi sau khi cuốn sách này được in.

Để kiểm tra xem Prism có phục vụ phản hồi đúng cách hay không, bạn có thể sử dụng trình quản lý API ưa thích của mình để thử nghiệm nó. Postman (đã thảo luận trong chương 2) là một lựa chọn hữu ích, hoặc bạn có thể sử dụng lệnh curl như sau:
curl http:/ /localhost:8080/jobs
LƯU Ý: Đối với các yêu cầu GET, bạn cũng có thể mở URL trong trình duyệt của mình.
Bạn nên thấy một phản hồi JSON tương tự như sau.
 
12.3 Building a frontend based on a mock server
Để làm việc với Prism, bạn cần chấp nhận rằng bạn đang làm việc với các phản hồi tĩnh hoặc được định trước, không phải là một máy chủ API thực sự. Khi nói không thực sự, chúng tôi có nghĩa là nó không có bất kỳ logic nào để lưu trữ dữ liệu hoặc phản hồi với các số được hình thành đúng cách (ví dụ, chỉ có một mục trong một mảng). Thay vào đó, chúng ta sẽ chỉ nhận được dữ liệu có hình dạng đúng. Điều này sẽ mang lại cho chúng ta một API thô sơ, nhưng như bạn sẽ thấy, làm việc được.
Trong thời điểm hiện tại, chúng ta sẽ tập trung vào xử lý hình dạng của dữ liệu và tạo ra các đường ống từ API vào ứng dụng frontend của chúng ta. Điều này sẽ bao gồm việc thiết lập thư viện HTTP, quản lý trạng thái state management, lớp hiển thị view layer, v.v. Mock API sẽ hoạt động đủ để hỗ trợ một quy trình hạnh phúc, và nó sẽ giúp nhóm tập trung vào những điều quan trọng - xây dựng frontend.
Đối với triggering errors hoặc mô phỏng lượng dữ liệu nhỏ hoặc lớn hơn, chúng ta sẽ cần sáng tạo.
Hãy bắt đầu bằng cách xây dựng một trang của PetSitter. Chúng ta có thiết kế UI trong hình 12.1 để làm việc (nhờ vào José). Đối với mỗi job, chúng ta có một row với một số dữ liệu và một button. Để điền trang đó, chúng ta cần lấy list of jobs từ API, với GET /jobs. Frontend của chúng ta tự nhiên sẽ mong đợi một phản hồi 200 với dữ liệu có hình dạng đúng. Và may mắn thay, đó chính xác là những gì Prism sẽ cung cấp.
 

Sau khi chỉ vào mã nguồn của chúng ta để sử dụng máy chủ giả mạo, chúng ta có thể nhận được một cái gì đó giống như hình 12.2. Điều đó trông ... trần trụi. Bạn có thể thấy rằng chỉ có một dòng dữ liệu, và nội dung của các trường chỉ là chuỗi!
 

Nếu nhóm frontend đã đạt được đến đây, đó chắc chắn là một thành công (API được kết nối đúng cách, trang web hiển thị đúng cách, v.v.). Nhưng chúng ta không thể kiểm thử bất kỳ điều gì đáng kể. Sẽ tốt nếu chúng ta có thể xem nhiều dữ liệu hơn, và là dữ liệu có tính thực tế hơn. Nếu dữ liệu do Prism tạo ra cho đến nay trông quen lạ, đó là vì công cụ này sử dụng các quy tắc tương tự để xây dựng một đối tượng từ một lược đồ như Swagger UI đã làm cho tính năng thử nghiệm của nó, mà chúng ta đã thảo luận trong chương 6. Vì vậy, bạn có thể đoán được điều tiếp theo.
Bằng cách sáng tạo một chút, chúng ta có thể kiểm thử nhiều hơn "frontend đã được kết nối đúng cách với API". Để kiểm thử frontend với dữ liệu thực tế hơn, chúng ta có thể sử dụng examples trong OpenAPI definition. Điều này sẽ giúp chúng ta tiến xa hơn nhiều, nhưng chúng ta sẽ không thể kiểm thử tất cả những điều mà một API thực sự cung cấp; chúng ta sẽ cần phải làm một số điều nhượng bộ, bởi vì đó là một máy chủ tĩnh.

Virtualization
Một chủ đề khác là virtualization và cách mô phỏng đầy đủ business logic, request và response của một API. Mặc dù có một số sản phẩm có sẵn (như ReadyAPI và Postman), nhưng hầu hết chúng đều có độ phức tạp cấp doanh nghiệp, với nhiều tính năng hơn là những gì chúng ta cần cho mục đích của mình. Thường xuyên, việc mô phỏng một API có kích thước nhỏ như vậy đòi hỏi nhiều năng lượng hơn giá trị mà nó mang lại.

Nếu bạn thực sự cần nhiều sức mạnh hơn, hãy kiểm tra các liên kết sau đây:
 ReadyAPI’s API virtualization services http://mng.bz/q2AE
 Postman mock servers www.postman.com/features/mock-api/
12.3.1 Adding multiple examples into your OpenAPI definition
Trong chương 6, chúng ta đã thảo luận về trường "example", mà bạn có thể sử dụng để thêm một chút màu sắc vào các schema, cho thấy dữ liệu trong thế giới thực có thể trông như thế nào. Ngoài trường "example", còn có trường "examples" (số nhiều), được giới thiệu sau đó vào OpenAPI specification với mục đích rõ ràng là cho phép nhiều ví dụ trong một yêu cầu, phản hồi, tham số, v.v. Sau này trong chương này, chúng ta sẽ tận dụng nhiều example trong mock server của mình, vì vậy hãy tìm hiểu một chút về cách chúng ta có thể mô tả chúng.
Trong OpenAPI specification, trường "examples" có thể được tìm thấy dưới đối tượng Media Type (https://designapis.com/oas/3#media-type-object). Bạn có thể xem một đối tượng Media Type - đó là tên chính thức của một đoạn của OpenAPI specification mô tả nội dung của một yêu cầu hoặc phản hồi - có các ví dụ trong đoạn mã sau.

 

Công cụ OpenAPI có thể tận dụng các examples trong definition. Swagger UI, ví dụ, thường mặc định hiển thị example đầu tiên, điều này thường minh họa hình dạng của dữ liệu hơn là các quy tắc schema được sử dụng khi không có ví dụ nào xuất hiện. Nếu có nhiều ví dụ, người dùng Swagger UI có thể chọn một từ menu thả xuống. Menu này hiển thị tóm tắt và sẽ sử dụng tên nếu không có tóm tắt nào xuất hiện.
Trong đoạn mã trước đó, chúng ta đã định nghĩa giá trị bằng YAML. Dưới đây là cách nó sẽ trông như khi sử dụng JSON.
 
Bây giờ bạn đã biết cách mô tả một hoặc nhiều ví dụ, hãy tiếp tục sử dụng chúng trong máy chủ giả mạo của chúng ta.

12.3.2 Using examples in Prism

Như bạn đã thấy, Prism sẽ tạo ra một simple mock response dựa trên schema của chúng ta, sử dụng các giá trị như `string` cho chuỗi và `0` cho số giống như Swagger UI. Điều này là chấp nhận được, nhưng nó hạn chế khả năng kiểm thử của chúng ta trên frontend. Chúng ta có thể sử dụng ví dụ để thể hiện rõ hơn dữ liệu có thể đến từ một máy chủ sản xuất thực tế.
Hãy thêm ví dụ sau vào definition của chúng ta để phù hợp với dữ liệu trong thiết kế UI của chúng ta. Nếu Prism đang chạy trong khi bạn thực hiện những thay đổi này, nó sẽ tự động khởi động lại bản thân.

/jobs:
    post:
      #...
    get:
      summary: List All Jobs
      responses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                # type: object
                # properties:
                #   items:
                #     type: array
                #     items:
                #       $ref: '#/components/schemas/Job'
              examples:
                with-some-data:
                  summary: With some data
                  value:
                    items:
                    - id: 123
                      create_user_id: 345
                      start_time: 2023-12-31T12:12:12Z
                      end_time: 2024-01-05T12:12:12Z
                      dog:
                        name: Fido
                        age: 3
                        breed: Doberman
                        size: medium
                      activity: walk
                    - id: 234
                      create_user_id: 345
                      start_time: 2024-01-10T12:12:12Z
                      end_time: 2024-01-15T12:12:12Z
                      dog:
                        name: Rex
                        age: 2
                        breed: Rottweiler
                        size: large
                      activity: sit

 

12.4 Identifying a missing API operation
 
Max có UI mockup như trong hình 12.3 mà anh ta sắp xây dựng. Anh ta nhận thấy rằng anh ta cần một cách để lấy tất cả các job applications cho người dùng đã đăng nhập, nhưng sau khi nhìn lại API design (định nghĩa OpenAPI), anh ta không thể tìm thấy một thao tác nào có thể thực hiện điều đó cho anh ta. Ngay cả khi triển khai đã bắt đầu, anh ta muốn đề xuất suggest một thay đổi mới  new
change (như chúng ta đã thảo luận trong chương 11).
Dưới đây là những gì Max sẽ thực hiện:
1. Max cần nêu rõ những gì anh ta cần—một cách để lấy tất cả job applications cho người dùng đã đăng nhập.
2. Anh ấy cần phải thực hiện sự thẩm định của mình  và đảm bảo rằng anh ta thực sự cần một thao tác mới.
3. Max có thể thiết kế thao tác mới sau đó design the new operation.
4. Trước khi đề xuất nó, anh ta cần thử nghiệm và đảm bảo rằng nó thực sự đáp ứng nhu cầu của anh ta.
5. Cuối cùng, Max có thể tự tin đề xuất thay đổi API mới và đưa nó vào thiết kế đã thống nhất.

Bước đầu tiên rất dễ dàng. Max viết ra những gì anh ta cần: "A way to fetch the job applications
for the logged-in user " Sau đó, anh ta bắt đầu bước chấp hành công việc cần làm.

12.4.1 Due diligence for adding the operation
Due diligence: Thẩm định
Bản UI mockup trong hình 12.3 hiển thị tất cả các job applications  cho người dùng đã đăng nhập. Làm thế nào Max có thể lấy chúng?
- Cố gắng attempt đầu tiên sẽ là tải xuống các jobs belong to the user, với GET /users/{id}/jobs, và sau đó xem xét các đơn ứng tuyển công việc của họ. Tuy nhiên, theo API definition, đây là những công việc được tạo ra bởi người dùng (như một chủ nhân thú cưng), không phải là những công việc mà người dùng (như một người trông nom thú cưng) đã đăng ký. Trừ khi người dùng đăng ký công việc của chính họ, điều này sẽ không dẫn đến đâu cả.
- Anh ta có thể lấy tất cả các công việc với GET /jobs, sau đó lấy tất cả các đơn ứng tuyển công việc của chúng và lọc chúng theo user_id trong bộ nhớ. Nhưng điều này hơi ngớ ngẩn—rõ ràng nó sẽ không mở rộng tốt khi dữ liệu trở nên lớn hơn.
Vì cả hai phương án này đều không khả thi, Max kết luận rằng một thao tác mới là cần thiết.
12.4.2 Designing the new operation
Để lấy tất cả đơn ứng tuyển công việc cụ thể đối với người dùng đã đăng nhập, Max có thể nghĩ đến hai phương pháp khác nhau:
- GET /job-applications?user_id={id}
- GET /users/{id}/job-applications

Phương pháp đầu tiên là khá đủ, cho phép chúng ta thêm các tham số truy vấn để lọc đơn ứng tuyển công việc dựa trên các tiêu chí khác. Tuy nhiên, chúng ta đang sử dụng mẫu thứ hai trong /jobs/{id}/job-applications, và có mẫu thống nhất trong API của chúng ta là có giá trị (nguyên tắc ít bất ngờ). Vì vậy, Max quyết định tuân theo mẫu hiện tại và chọn GET /users/{id}/job-applications.
Bắt đầu với API definition của chúng ta, chúng ta có thể thêm vào một phác thảo sketch của một operation (không phải là một mô tả hoàn chỉnh của thao tác). Ngoài ra, chúng ta sẽ để chỗ cho một ví dụ mà sau này chúng ta sẽ điều chỉnh, để kiểm tra xem thao tác có đáp ứng nhu cầu của chúng ta không.

/users/{id}/jop-applications:
    parameters:
      - schema:
          type: integer
        name: id
        in: path
        required: true
    get:
      summary: List Application for User
      reponses:
        '200':
          description: OK
          content:
            application/json:
              schema:
                type: object
              examples: #: đây là nơi chúng tôi thêm các examples để test UI
                
    two-items: #: đây là ví dụ về có 2 job applications
                  summary: Two Job Applications
                  value: #...
		    empty: #: đây là ví dụ về không có job applications nào
                  summary: Zero Job Applications
                  value: # ...
                many:	#: đây sẽ là ví dụ về nhiều job applications
                  summary: A lot of Job Applications
                  value: # ...


EXAMPLE: TWO JOB APPLICATIONS
examples:
                two-items:
                  summary: Two Job Applications
                  value:
                    items:
                    - id: 123
                      user_id: 123
                      job_id: 123
                      status: PENDING
                    - id: 123
                      user_id: 123
                      job_id: 123
                      status: COMPLETE






EXAMPLE: NO DATA

examples:
                two-items:
                  #...
                empty:
                  summary: Zero Job Applications
                  value:
                    items: []

                
EXAMPLE: LOTS OF DATA
Chúng tôi đã sử dụng JSON Generator (www.json-generator.com) và JSON to YAML (www.json2yaml.com) để tạo ra một loạt dữ liệu và sao chép nó vào đây: https://designapis.com/ch12/02.yml. Đoạn mã dưới đây chỉ hiển thị một số dòng đầu tiên. Chúng tôi đã sử dụng giá trị ngẫu nhiên cho tất cả các job_id và user_id, nhưng không cho id. id cho các job applications là một số liên tục, vì ứng dụng web của chúng tôi yêu cầu sự duy nhất.

12.4.3 Choosing which mock data response to get from Prism

Bây giờ là lúc để kiểm thử API giả mạo. Việc sử dụng Prism với một examples được mô tả hoạt động hoàn hảo, như bạn đã thấy. Nhưng chúng tôi đã mô tả nhiều example và muốn có khả năng chọn lựa ví dụ nào để sử dụng. Để giúp chúng tôi, Prism cho phép gửi tùy chọn thông qua Prefer request header. Hai cách sử dụng header này mà chúng tôi sẽ tập trung là mã và ví dụ. Với hai cách đó, chúng tôi sẽ có khả năng chọn lựa mã phản hồi và dữ liệu ví dụ mà Prism sẽ trả về.

Để làm rõ hơn cách điều này hoạt động, hãy quay lại từ API PetSitter và sử dụng một API definition đơn giản, cơ bản chỉ đủ chi tiết để giới thiệu cách Prism có thể biến đổi dữ liệu phản hồi được trả về. Bạn có thể tải API definition sau từ https://designapis.com/ch12/03.yml; lưu nó trong một tệp gọi là tiny.yml.

openapi: 3.0.3
info:
  title: Tiny API
  version: "1.0.0"
paths:
  /foo:
    get:
      description: Simple get
      responses:
        '200':
          description: Get Foo
          content:
            application/json:
              examples:
                one:
                  value:
                    foo: 1
                two:
                  value:
                    foo: 2
              schema:
                type: object
        '404':
          description: No Foo
          content:
            application/json:
              examples:
                error:
                  value:
                    msg: I am an error example

Trong tiny.yml, chúng ta có thể thấy rằng GET /foo có hai phản hồi được mô tả: một phản hồi 200 với hai ví dụ, được đặt tên là one và two, và một phản hồi 404 với một ví dụ duy nhất, đơn giản là có tên là error.
LƯU Ý: Nếu bạn vẫn đang chạy một máy chủ giả mạo Prism, hãy tắt nó trước khi chạy các lệnh tiếp theo để khởi động lại nó.

Bắt đầu Prism với lệnh `prism mock -p 8080 ./tiny.yml` để chúng ta có thể thực hiện một số thí nghiệm. Việc khởi động Prism với định nghĩa mới sẽ trông giống như sau đây.
Sử dụng curl (hoặc Postman), chúng ta muốn thực hiện GET /foo nhưng nhận các phản hồi khác nhau dựa trên ba ví dụ được mô tả (one, two và error). Để làm điều đó, chúng ta sẽ thực hiện request với Prefer header được thiết lập.
Để nhận phản hồi lỗi, chúng ta sẽ sử dụng Prefer:code=404 header và giá trị để truyền một tùy chọn đến Prism, cho biết chúng ta muốn một phản hồi với mã trạng thái 404. Thực hiện lệnh sau với curl.

 
Bạn sẽ nhận được một phản hồi với {"msg": "I am an error example"}. Nếu bạn thêm -i flag vào curl, bạn sẽ nhận thấy mã trạng thái là 404.
Bây giờ hãy thử mã trong hai danh sách sau để trả về hai ví dụ khác nhau.

 
Đây là một kỹ thuật đơn giản nhưng đủ mạnh mẽ để chúng ta có thể kiểm soát các phản hồi mà chúng ta nhận được từ mã nguồn của chúng ta. Trong mã nguồn frontend của chúng ta, chúng ta có thể thiết lập các tiêu đề này trong quá trình kiểm thử và loại bỏ chúng khi mã nguồn được triển khai vào môi trường sản xuất.

Để biết thêm thông tin về ví dụ phản hồi trong Prism, bạn có thể kiểm tra tài liệu của Prism tại:.
http://mng.bz/wnAW

12.4.4 Formalizing and suggesting the change
Sau khi chúng ta đã kiểm thử và vẽ đồ thị và hài lòng với việc rằng thay đổi sẽ giải quyết vấn đề của chúng ta, chúng ta sẵn sàng đề xuất nó. Hãy dọn dẹp tệp định nghĩa của chúng ta và tạo một yêu cầu kéo (pull request) trên GitHub để đề xuất thay đổi này đến các bên liên quan khác.
Trong ví dụ của chúng ta, chúng ta đã sử dụng hình dạng sau, đó là một object chứa các items và list các job applications.
items:
- id: 123
user_id: 123
job_id: 123
status: PENDING
- #...

Chúng ta đã định nghĩa job applications trong schema của chúng ta, vì vậy chúng ta sẽ sử dụng nó và cập nhật hoạt động của chúng ta như sau:
Đó là tất cả! Chúng ta có thể đề xuất một thay đổi mà chúng ta tự tin sẽ hoạt động, vì chúng ta đã có cơ hội kiểm thử các phản hồi khác nhau từ bên trong frontend của mình dựa trên thiết kế đề xuất của chúng ta.
Việc phát hiện vấn đề thiết kế trong quá trình triển khai gần như là không tránh khỏi. Quan trọng là phải có cách để thích ứng với những vấn đề này, xác minh các giải pháp mới và tích hợp những giải pháp đó trở lại vào thiết kế API.

Chapter 14 - Integrating
and releasing
the web application

14.1 The problems
Trong chương này, chúng ta sẽ giải quyết ba câu hỏi kỹ thuật còn lại mà đội ngũ PetSitter cần giải đáp trước khi họ có thể thiết lập phiên bản triển khai đầu tiên của mình:
- Làm thế nào chúng ta có thể xác định một người dùng và triển khai hành động "Đăng nhập" với sự nỗ lực tối thiểu, đủ cho mục đích triển khai?
- Làm thế nào chúng ta có thể tổ chức và duy trì mã nguồn và API definition của mình sao cho nó sẵn sàng cho việc deployment?
- Làm thế nào chúng ta có thể phục vụ ứng dụng, cả frontend và backend, từ một máy chủ mà José và những người thử nghiệm beta khác có thể tương tác?

Trong phần vấn đề này, chúng ta sẽ giải thích tại sao quan trọng để giải đáp từng câu hỏi này trước khi triển khai và mỗi câu hỏi mang lại điều gì. Phần còn lại của chương sẽ bao gồm các giải pháp.

14.1.1 Authentication
Domain model mà đội ngũ PetSitter thiết kế trong chương 9 bao gồm một hành động "Login" trong concept User. Khi Max chuyển đổi domain model thành API design trong chương 10, anh ta đã bỏ qua hành động " Login", dưới giả định rằng không có hoạt động API tương ứng với hành động này.
Tất nhiên, mọi người trông nom thú cưng và chủ thú cưng đã đăng ký trong ứng dụng PetSitter nên chứng minh rằng họ được phép truy cập vào tài khoản của mình trước khi có thể đăng tải công việc, đăng ký công việc, hoặc thực hiện bất kỳ hành động nào khác trong hệ thống. Mà không có một loại bảo mật nào đó, người dùng có thể giả mạo lẫn nhau, có thể dẫn đến gian lận trong thị trường. Thậm chí khi chúng ta chỉ đang kiểm thử và chưa có người dùng thực sự, chúng ta có thể dự kiến sẽ gặp vấn đề hoặc sự nhầm lẫn. Do đó, việc triển khai mà không có xác thực đúng đắn không phải là một lựa chọn.

Nếu ta nhìn kỹ hơn, ta có thể xác định các yêu cầu sau đây:
- Hành động "Register” cho users (POST /register) không nên yêu cầu xác thực, để nó có sẵn cho mọi người (vì một người dùng mới chưa có bất kỳ thông tin đăng nhập nào).
- Mọi hành động khác (ngoại trừ hành động "Login," mà chúng ta chưa có) đều liên quan đến một người dùng đã xác thực, vì vậy chúng ta phải yêu cầu xác thực để truy cập chúng.
- Do cấu trúc CRUD, nhiều cuộc gọi API đòi hỏi ID của người dùng, như là GET /users/{id}. ID là một định danh tùy ý mà máy chủ, hoặc cụ thể hơn, cơ sở dữ liệu, gán cho người dùng của mình. Tuy nhiên, trên giao diện người dùng, người dùng thường sử dụng địa chỉ email và mật khẩu của họ để đăng nhập và không biết ID nội bộ của mình.
Để đáp ứng các yêu cầu, chúng ta sẽ thực hiện những bước sau:
- Tạo một OpenAPI security scheme mô tả cách user  có thể ủy quyền các yêu cầu - một token bí mật trong trường hợp này.
- Thêm action "Login" vào domain model của chúng ta và sau đó là một hoạt động vào OpenAPI của chúng ta cho phép người dùng chuyển đổi thông tin đăng nhập của họ (địa chỉ email và mật khẩu) thành ID và một token bí mật.
- Chỉ định rằng xác thực là bắt buộc cho mọi hoạt động ngoại trừ "Register" và "Login."
Chúng ta sẽ xem xét một giải pháp vào cuối chương này. Vấn đề tiếp theo của chúng ta là quyết định cách tổ chức mã nguồn.
14.1.2 Organizing code
Cho đến nay, Max và Nidhi đã cùng nhau làm việc trên tệp OpenAPI bằng cách sử dụng GitHub và quy trình mà chúng ta mô tả trong chương 11. Mỗi người trong họ cũng đã thiết lập một kho chứa cho các tệp mã nguồn của thành phần của mình một cách riêng lẻ, vì vậy có tổng cộng ba kho chứa. Để quyết định liệu chúng ta có nên giữ ba kho chứa hiện tại hay không, hãy dừng lại và xem xét các lựa chọn chúng ta có:
- Giữ cấu trúc hiện tại.
- Tạo một Git repo chung cho việc triển khai cả hai thành phần both components.
- Tích hợp mã nguồn và API definition trong cùng một repository.
Hãy giải quyết một vấn đề trước tiên: vì chúng ta có một API hoạt động như một ranh giới rõ ràng giữa frontend và backend và chúng ta đã sử dụng phương pháp API design-first, không có lý do gì mà một nhà phát triển nào đó cần truy cập mã nguồn của một thành phần mà họ không đang làm việc OpenAPI definition nói cho họ biết những gì họ cần biết để tương tác với nó. Bạn có thể triển khai từng thành phần một cách riêng lẻ, trao đổi các URL và ứng dụng kết quả sẽ hoạt động mà không cần bất kỳ nhà phát triển nào nhìn thấy bên trong của một thành phần khác. Vậy tại sao chúng ta lại cân nhắc đưa cả hai vào cùng một kho chứa?

Lý do mà nhóm PetSitter muốn chia sẻ mã là họ muốn cộng tác để thiết lập một máy chủ kiểm thử duy nhất chứa cả hai thành phần cùng một lúc. Lý tưởng nhất, máy chủ nên có thể di động đến mức có thể được tải xuống và chạy như một phiên bản kiểm thử cục bộ hoặc tải lên trong một bước duy nhất lên hạ tầng của công ty. Cũng quan trọng là các phiên bản tương thích của mã được triển khai cùng nhau, vì chúng ta chưa bao giờ nói về việc quản lý phiên bản. Việc có cả hai thành phần trong một nơi có thể hữu ích.
Chúng ta sẽ xem xét ba lựa chọn và chọn một trong chúng vào cuối chương này. Trước khi làm điều đó, tuy nhiên, hãy xem xét vấn đề thứ ba và cuối cùng của chúng ta, đó là cách phục vụ cả hai thành phần cùng một lúc.


