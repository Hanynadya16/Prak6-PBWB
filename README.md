# Praktikum 6 : Web SMP Mentari Filament

## Langkah - Langkah

1. Buat empty project

bash
   composer create-project laravel/laravel smpmentari_filament

   # Masuk ke folder nya
   cd smpmentari_filament


2. Coba jalankan server

bash
   php artisan serve


3. Konfigurasi pada .env

bash
    DB_CONNECTION=sqlite
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=smpmentari_filament
    DB_USERNAME=root
    DB_PASSWORD=


4. Migrasi (Membuat database sesuai dengan file yang terdapat pada folder database/migrations)

bash
   php artisan migrate


5. Install filament

bash
   composer require "filament/filament"

    > Kalau error : di php.ini bagian ;extension=zip di aktifin -> extension.zip (tanpa ;)


6. Generate Panel Admin

bash
   php artisan filament:install --panels

   # What is the panel’s ID?(admin)


7. Buat Akun filament

bash
    php artisan make:filament-user

    # Ikuti prompt: name (admin), email(admin@example.com), password(admin123)


8. Link storage untuk upload file
bash
    php artisan storage:link


9. Jalankan menggunakan

bash
    php artisan serve

    # Akses :  http://localhost:8000/admin


10. Buat Model & Migrasi

bash
    php artisan make:model Kegiatan -m
    php artisan make:model Siswa -m


11. Edit Migrasi  
    <span style="color:gray">Edit pada database/migrations/ xxxx_xx_xx_xxxxxx_create_kegiatans_table.php</span>
    <br> 
    <![WhatsApp Image 2025-11-07 at 17 34 44_fb3a7209](https://github.com/user-attachments/assets/cfca9213-4cd0-40ae-afbb-26c928755541)>

    <span style="color:gray">Edit pada database/migrations/xxxx_xx_xx_xxxxxx_create_siswa_table.php</span>
    <br> 
    <![WhatsApp Image 2025-11-07 at 17 34 43_50aae2d0](https://github.com/user-attachments/assets/b4fb0401-7d5a-4b8e-87a4-feee0504efaf)>


Jalankan Migrasi   
bash
    php artisan migrate 

<br>

12. Generate Filament Resource (CRUD Otomatis)
bash
    php artisan make:filament-resource Kegiatan --generate  
    php artisan make:filament-resource Siswa --generate

- Perintah ini akan membuat beberapa file, yaitu :  
    1. app/Filament/Resources/KegiatanResource.php 
    2. app/Filament/Resources/KegiatanResource/Pages/{Create,Edit,List}Kegiatans.php 
    3. app/Filament/Resources/SiswaResource.php 
    4. app/Filament/Resources/SiswaResource/Pages/{Create,Edit,List}Siswas.php

13. Form & Tabel Kegiatan
    <span style="color:gray">Edit app/filament/Resource/Kegiatans/KegiatanResource.php</span>
    <br> 
  ![WhatsApp Image 2025-11-07 at 17 34 43_305f8d2d](https://github.com/user-attachments/assets/e1a6c065-d886-4e8b-b280-2e6bb12d76a4)


    <br>

    <span style="color:gray">Edit app/filament/Resource/Kegiatans/Schemas/KegiatansForm.php</span>
    <br> 
  ![WhatsApp Image 2025-11-07 at 17 34 45_88a98485](https://github.com/user-attachments/assets/c5e37f85-ced8-4394-8d97-3c7dfcc1f52c)
    <br> 

    <span style="color:gray">Edit app/filament/Resource/Kegiatans/Tables/KegiatansTable.php</span>
    <br> 
   ![WhatsApp Image 2025-11-07 at 17 34 44_c7b49a07](https://github.com/user-attachments/assets/c4f58581-fa76-421d-83dd-d4794909a8dc)

14. Form & Tabel Siswa 
    <span style="color:gray">Edit app/filament/Resource/Siswas/SiswaResource.php</span>
    <br> 
   ![WhatsApp Image 2025-11-07 at 17 34 45_9ec0927d](https://github.com/user-attachments/assets/6f0ec8f1-a192-4453-8093-eefcd94cc8a3)
    <br>

    <span style="color:gray">Edit app/filament/Resource/Siswas/Schemas/SiswaForm.php</span>
    <br> 
   ![WhatsApp Image 2025-11-07 at 17 34 45_f0d50789](https://github.com/user-attachments/assets/b1dbc6c3-a414-4c7b-bc8a-529918531cb2)
    <br> 

    <span style="color:gray">Edit app/filament/Resource/Siswa/Tables/SiswaTable.php</span>
    <br> 
  ![WhatsApp Image 2025-11-07 at 17 34 44_c7557f6d](https://github.com/user-attachments/assets/0cf7c7a8-8f87-41e9-8ab0-35624cde4d92)
    <br> 

    <span style="color:gray">Edit app/Models/Kegiatan.php</span>
    <br> 
    <img src="Image/image-8.png" alt="Kegiatan.php" width="500">

    <br> 

    <span style="color:gray">Edit app/Models/Siswa.php</span>
    <br> 
    <img src="Image/image-9.png" alt="Siswa.php" width="500">

15. Branding Panel : Identitas SMP Mentari  
Buka app/Providers/Filament/AdminPanelProvider.php dan tambahkan :
bash
    ->brandName('SMP Mentari')
    ->navigationGroups([
        'Akademik', 'Publikasi'])
    ->sidebarCollapsibleOnDesktop(true). 


16. Buat Halaman Depan (Public)
Pada routes/web.php
bash
    Route::get('/', function () {
        return view('welcome');
    });

    Route::get('/kegiatan', function () {
        return view('kegiatan-public', [
            'items' => \App\Models\Kegiatan::latest()->paginate(9),
        ]);
    });


Lalu pada resources/views/kegiatan-public.blade.php 
dan resources/views/layouts/app.blade.php  

> Pastikan sudah menjalankan 
bash
    php artisan storage:link 

> agar gambar dari FileUpload tampil di halaman publik. 

<br>

## View
1. Login  
<br>

![WhatsApp Image 2025-11-07 at 17 20 22_c0e035f3](https://github.com/user-attachments/assets/348c361d-7826-4804-ad90-c2532dbbcf74)
)

2. Admin
<br>


![WhatsApp Image 2025-11-07 at 17 21 30_1092695c](https://github.com/user-attachments/assets/64b6d47a-8a16-4695-bb7a-dde5ddfab47e)
)

3. Kegiatan
<br>

![WhatsApp Image 2025-11-07 at 17 20 08_4855098c](https://github.com/user-attachments/assets/f786d96b-00a1-44b6-a595-826c5eb7a152)
)
