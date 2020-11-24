Setting di terminal :
1. Install : composer create-project --prefer-dist laravel/laravel:^7.0 blog
2. Buat Databasenya di localhost/phpmyadmin (Pake Aplikasi XAMPP)
3. Samain nama Database nya di .env
4. Ketik Perintah Terminal : php artisan migrate
5. Ketik Perintah Terminal : composer require laravel/ui:^2.4
6. Ketik Perintah Terminal : php artisan ui vue --auth
7. Ketik Perintah Terminal : npm install
8. Ketik Perintah Terminal : npm run dev
9. Ketik Perintah Terminal : php artisan serve

Setting koding di laravel 7 :
1. Siap kan gmail yang menjadi master servernya lalu setting akun gmailnya seperti ini :
    - Buka gmail
    - Kelola Akun Gmail Anda
    - Pilih Keamanan -> Cari Akses Aplikasi Yang Kurang Aman
    - Nonaktif dijadikan Aktif
2. Tambahin ini di .env :
    MAIL_MAILER=smtp
    MAIL_HOST=smtp.googlemail.com
    MAIL_PORT=465
    MAIL_USERNAME=adityacontoh2@gmail.com
    MAIL_PASSWORD=aditya050398aditya
    MAIL_ENCRYPTION=ssl
    MAIL_FROM_ADDRESS=adityacontoh2@gmail.com
    MAIL_FROM_NAME=noreply
3. Ubah kodingan di config/main.php :
    - Ubah Bagian Mailers dan ubah host nya :
        'mailers' => [
            'smtp' => [
                'host' => env('MAIL_HOST', 'smtp.googlemail.com'),
            ],
        ]
    - Ubah bagian From nya :
        'from' => [
            'address' => env('MAIL_FROM_ADDRESS', 'adityacontoh2@gmail.com'),
            'name' => env('MAIL_FROM_NAME', 'noreply'),
        ],

Cara Ubah Template Message Text Email yang di kirim :
1. Ketik Perintah Terminal : php artisan make:notification ForgotPassword
2. Edit ForgotPassword.php yang berada di app/Notifications/ForgotPassword :
    - Tambahin :
        public $token;
    - Tambahin :
        public function __construct($token)
        {
            $this->token = $token;
        }
    - Tambahin :
        public function toMail($notifiable)
        {
            return (new MailMessage)
                    ->subject('Reset Password')
                    ->line('Anda menerima email ini karena kami menerima permintaan pengaturan ulang kata sandi untuk akun Anda.')
                    ->action('Reset Password', url('password/reset', $this->token))
                    ->line('Jika Anda tidak meminta pengaturan ulang kata sandi, tidak ada tindakan lebih lanjut yang diperlukan.');
        }
3. Daftarkan ForgotPassword.php di App/User.php :
    - Daftarkan terlebih dahulu paling atas :
        use App\Notifications\ForgotPassword as ForgotPasswordNotification;
    - Taruh di bawahnya :
        public function sendPasswordResetNotification($token)
        {
            $this->notify(new ForgotPasswordNotification($token));
        }

Cara Ubah Kalimat yang ada di body template Email :
1. Ketik Perintah Terminal :
    - Ketik ini :
        php artisan vendor:publish --tag=laravel-notifications
    - Ketik ini :
        php artisan vendor:publish --tag=laravel-mail
2. Cari HTML nya di resources/views/vendor :
    - Bisa Edit di mail atau notifications (cari sendiri aja edit2 sendiri)

Note : Kalau pake antivirus semacam Avast, matiin terlebih dahulu
di karenakan ga akan support SSL
