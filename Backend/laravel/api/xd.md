# Api 
- 1 luồng xử lý login 
    - Route
        ```php 
        Route::post('auth/login', [PassportAuthController::class, 'login'])->name('login');
        ```
    - Controller 
        ```php 
        public function login(Request $request)
        {
            $data = [
                'username' => $request->username,
                'password' => $request->password,
            ];
            $status=$this->userRepository->check($request->username);
            if (auth()->attempt($data) && $status->status !=4) {
                $token = auth()->user()->createToken('LaravelAuthApp')->accessToken;
                return response()->json([
                    'status' => true,
                    'message' => 'Đăng nhập thành công',
                    'token' => $token,
                    'data' => Auth::user()
                ], 200);
            } else {
                return response()->json([
                    'status' => false,
                    'message' => 'Đăng nhập thất bại',
                    'error' => 'Unauthorised'
                ], 401);
            }
        }
        ```
        - `$data`: Lấy ra username, password 
        - `$status`: Check với DB 
            - `check`: Check và lấy user đầu tiên
        - Kiểm tra `status` != 4 là admin (4 là user)
        - Tạo token 
    - Trả về kiểu `json` gồm có: 
        - **status**: Trạng thái là gì 
        - **message**: Thông báo đăng nhập 
        - **token**: Để kiểm tra đối với mỗi phiên
        - **data**: Trả về data 