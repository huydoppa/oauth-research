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
<p> Ứng dụng khách (client Application) <imsg src="https://user-images.githubusercontent.com/58453296/148363727-427d53eb-6c54-4d84-986e-c25490ed0e78.png" style="width:128px;height:128px">
sử dụng cái access token này để tìm gọi các API nạp các dữ liệu từ máy chủ </p>

<h1>OAuth grant types</h1>
<strong> Oauth grant type là gì : </strong>
<p> Oauth grant type xác định chính xác các bước trong quá trình của các bước liên quan đến quá trình Oauth . grant type cũng ảnh hưởng đến cách client application  liên hệ với với dịch vụ Oauth trong mỗi giai đoạn bao gồm cả cách gửi mã thông báo truy cập. Vì lý do này, các loại tài trợ thường được gọi là "Oatuh flow".</p>

<strong>Oauth scope</strong>
<p>scope là những gì mà oauth muốn truy cập sử dụng tham số scope để ủy quyền cho các yêu cầu gửi tới dịch vụ Oauth</br>
scope có thể là 1 string hoặc là 1 url</br>
scope=contacts</br>
scope=contacts.read</br>
scope=contact-list-r</br>
scope=https://oauth-authorization-server.com/auth/scopes/user/contacts.readonly</br>

<p>openid connect thường được sử dụng thay thế</p>
<h1> Authorization code grant type </h1>
<p> ![image](https://user-images.githubusercontent.com/58453296/148369154-bd7231cf-5cd9-4627-a09f-d51364f01e12.png) </p>
<h1> Bước 1 : Yêu cầu ủy quyền </h1>
<p>GET /authorization?client_id=12345&redirect_uri=https://client-app.com/callback&response_type=code&scope=openid%20profile&state=ae13d489bd00e3c24 HTTP/1.1</br>
Host: oauth-authorization-server.com </br>
client id : mỗi cái client application sẽ có 1 cái id riêng để xác định </br>
redirect_url : cái URL mà browser của người dùng sẽ được chuyển hướng khi gửi code ủy quyền cho client application . Gọi là callback url hoặc là callback endpoint rất nhiều cuộc tấn công Oauth dựa theo khai thác nguyên tắc xác thực của tham số này</br>
response_type : Xác định loại phản hồi mà client application mong đợi nếu mà loại cấp mã ủy uyền thì giá trị trả về sẽ là code</br>
scope : loại trả về được cho phép yêu cầu</br>
state : Lưu trữ một giá trị duy nhất, không thể đoán được được gắn với phiên hiện tại trên client application Dịch vụ OAuth sẽ trả về giá trị chính xác này trong phản hồi, cùng với mã ủy quyền. Tham số này đóng vai trò như một dạng mã thông báo CSRF cho ứng dụng khách bằng cách đảm bảo rằng yêu cầu tới điểm cuối / gọi lại của nó là từ cùng một người đã khởi tạo luồng OAuth. </br>
<h1> Bước 2 : User login </h1>
<p> khi mà server ủy quyền nhận được yêu cầu nó chuyển người dùng đến trang đăng nhập rồi khi đăng nhập nó hiện ra một list danh sách mà client application yêu cầu truy cập , rồi phiên đăng nhập valid thì người dùng sẽ tự động đăng nhập </p>
<h1> Bước 3 : Code ủy quyền </h1>
<p> Nếu người dùng đồng ý với quyền truy cập được yêu cầu , trình duyệt sẽ chuyển đến endpoint /callback đã được tham só redirect_url chỉ định của bước 1 Yêu cầu GET kết quả sẽ chứa mã ủy quyền dưới dạng tham số truy vấn. Tùy thuộc vào cấu hình, nó cũng có thể gửi tham số trạng thái có cùng giá trị như trong yêu cầu ủy quyền. </p>
<p>GET /callback?code=a1b2c3d4e5f6g7h8&state=ae13d489bd00e3c24 HTTP/1.1</br>
Host: client-app.com </p>
<h1> Bước 4 :  Access token request </h1>
<p> Sau khi ứng dụng khách nhận được mã ủy quyền, ứng dụng cần đổi mã đó để lấy mã thông báo truy cập. Để thực hiện việc này, nó sẽ gửi một yêu cầu POST từ máy chủ đến máy chủ đến /token của dịch vụ OAuth .Tất cả thông tin liên lạc từ thời điểm này trở đi diễn ra trong một kênh trở lại an toàn và do đó, kẻ tấn công thường không thể quan sát hoặc kiểm soát được.</p>
POST /token HTTP/1.1</br>
Host: oauth-authorization-server.com</br>
…</br>
client_id=12345&client_secret=SECRET&redirect_uri=https://client-app.com/callback&grant_type=authorization_code&code=a1b2c3d4e5f6g7h8 </br>
<h1> Bước 5 : Access token grant </h1>
<p> Dịch vụ 0auth sẽ xác minh các access token request . Nếu mọi thứ ok , server sẽ phản hồi bằng cách gán cho client application 1 access token cùng với scope yêu cầu
</br>  {
  "access_token": "z0y9x8w7v6u5",</br> 
  "token_type": "Bearer",</br> 
  "expires_in": 3600,</br> 
  "scope": "openid profile",</br> 
  …</br> 
}</br> 
</p>
<h1> Bước 6 :  API call </h1>
Bây giờ client application đã có access code , nó có thể lấy user data từ server mã truy cập để làm được thế nó cần gọi API tới dịch vụ Oauth /userinfo . cái access token được xác minh ở trong header Authorization: Bearer để chứng minh là nó có quyền lấy data 
<h1> Bước 7: cấp data </h1>
gửi data dựa vào scope của access_token




