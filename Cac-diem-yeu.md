
<h1>Thiếu state dẫn đến tấn công csrf </h1>
<p>state trong Oauth là một mã tương tự như csrf token nếu thiếu cái mã này thì thằng tấn công có thể lừa thằng khác click vô cái link có code author của nó rồi server nó sẽ xử lí các bước tiếp theo => thằng attacker có thể take over account </p>
<h1>Leaking authorization codes and access tokens</h1>
<p> Trong một vài trường hợp nếu a
