# oauth-research
<h1>Oauth la gi</h1>
<p>Có thể hiểu đơn giản là OAuth là một phương thức chứng thực giúp các ứng dụng có thể chia sẻ tài nguyên với nhau mà không cần chia sẻ thông tin username và password như những cách truyền thống cũ. “Auth” là từ gồm 2 nghĩa khác nhau:

Nghĩa đầu tiên là ‘Authentication’ - nghĩa là xác thực người dùng thông qua việc đăng nhập. Nghĩa thứ 2 là ‘Authorization’ nghĩa là cấp quyền truy cập vào các Resource. Vì thế có thể hiểu là chúng ta đã đăng ký và có một tài khoản Facebook, và chúng ta sẽ dùng tài khoản này để đăng nhập ở 10-20 ứng dụng/web mà không cần mất công đăng kí hay đăng nhập.

Trong trường hợp 1 trong số 20 ứng dụng/web của chúng ta bị hack và hacker lấy được các thông tin người dùng của ứng dụng thì có phải bạn sẽ bị lộ thông tin mật trong tất cả tài khoản? Trong trường hợp này bạn cũng không phải lo lắng quá về việc sẽ mất tài khoản (username + password) Facebook vì ứng dụng bị mất của bạn chỉ được Facebook chia sẻ cho một chìa khóa (token) chứa quyền hạn nhất định và không được phép truy cập vào thông tin username cũng như password của bạn.</p>
<h1> Cách vận hành </h1>
<p>Ứng dụng có thể là website hoặc app điện thoại gửi yêu cầu ủy quyền để truy cập vào Resource Server (Gmail,Facebook, Twitter hay Github…) thông qua người dùng

Nếu người dùng đồng ý ủy quyền cho yêu cầu trên, Ứng dụng sẽ nhận được ủy quyền từ phía User (dưới dạng một token string)

Ứng dụng gửi thông tin định danh (ID) của mình kèm theo ủy quyền của User tới Authorization Server

Nếu thông tin định danh được xác thực và ủy quyền hợp lệ, Authorization Server sẽ trả về cho Ứng dụng access_token. Đến đây quá trình ủy quyền hoàn tất.

Để truy cập vào tài nguyên (resource) từ Resource Server và lấy thông tin, Ứng dụng sẽ phải đưa ra access_token để xác thực.

Nếu access_token hợp lệ, Resource Server sẽ trả về dữ liệu của tài nguyên đã được yêu cầu cho Ứng dụng.</p>
<p> Tóm lại Oauth tiện ích vì 1 tài khoản dùng được nhiều và có thể cho phép ứng dụng kia sử dụng những tài nguyên nào </p>
<p>Ứng dụng khách - Trang web hoặc ứng dụng web muốn truy cập dữ liệu của người dùng.(client application)</br>
Chủ sở hữu tài nguyên - Người dùng có dữ liệu mà ứng dụng khách muốn truy cập.(resource owner)</br>
Nhà cung cấp dịch vụ OAuth - Trang web hoặc ứng dụng kiểm soát dữ liệu của người dùng và quyền truy cập vào dữ liệu đó. Họ hỗ trợ OAuth bằng cách cung cấp API để tương tác với cả máy chủ ủy quyền và máy chủ tài nguyên.(Oauth service provider)</p>
<p> Có rất nhiều cách để quá trình Oauth có thể xảy ra , nhưng thông thường nó theo 1 flow </p>
<p> Đầu tiên là cái ứng dụng khách (client Application) sẽ yêu cầu vào tập dữ liệu người dùng để lấy ra những dữ liệu nó cần sử dụng và loại quyền truy cập nó muốn</p>
<p> Tiếp theo Người dùng được nhắc đăng nhập vào dịch vụ OAuth và confirm  đối với quyền truy cập được yêu cầu. </p>
<p> Ứng dụng khách (client Application) nhận được 1 cái access token duy nhất cung cấp quyền của user để truy cập những dữ liệu được yêu cầu</p>
<p> Ứng dụng khách (client Application) ![dsBuffer](https://user-images.githubusercontent.com/58453296/148363727-427d53eb-6c54-4d84-986e-c25490ed0e78.png)
sử dụng cái access token này để tìm gọi các API nạp các dữ liệu từ máy chủ </p>

<h1>OAuth grant types</h1>
<strong> Oauth grant type là gì : </strong>

