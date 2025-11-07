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
    <![WhatsApp Image 2025-11-07 at 17 34 43_146a6e4d](https://github.com/user-attachments/assets/07f30884-5a34-42f3-a08a-7b9a996cc2be)>
>

    <br>

    <span style="color:gray">Edit app/filament/Resource/Kegiatans/Schemas/KegiatansForm.php</span>
    <br> 
    <![WhatsApp Image 2025-11-07 at 17 34 45_d773c767](https://github.com/user-attachments/assets/3e900d17-8f8a-46e2-97f6-71732c2c94c8)>

    <br> 

    <span style="color:gray">Edit app/filament/Resource/Kegiatans/Tables/KegiatansTable.php</span>
    <br> 
    <![WhatsApp Image 2025-11-07 at 17 34 44_60301ea4](https://github.com/user-attachments/assets/75af2b4b-d50b-4d4e-9afd-5974dea7cd11)>

14. Form & Tabel Siswa 
    <span style="color:gray">Edit app/filament/Resource/Siswas/SiswaResource.php</span>
    <br> 
    <![WhatsApp Image 2025-11-07 at 17 34 45_c9c127ef](https://github.com/user-attachments/assets/8113f2b9-05e1-4b38-a63a-19005867952d)>

    <br>

    <span style="color:gray">Edit app/filament/Resource/Siswas/Schemas/SiswaForm.php</span>
    <br> 
    <![WhatsApp Image 2025-11-07 at 17 34 45_591a9f26](https://github.com/user-attachments/assets/213aa039-039b-46fb-9758-49217effe9fa)>

    <br> 

    <span style="color:gray">Edit app/filament/Resource/Siswa/Tables/SiswaTable.php</span>
    <br> 
    <![WhatsApp Image 2025-11-07 at 17 34 44_64177eb7](https://github.com/user-attachments/assets/0831f537-db5f-4617-9f9d-b2f41641ed8e)

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

![Login](![WhatsApp Image 2025-11-07 at 17 20 22_a6195d59](https://github.com/user-attachments/assets/13c14011-05b7-46b2-900d-bffa060c753a)
)

2. Admin
<br>


![Admin](![WhatsApp Image 2025-11-07 at 17 21 30_ab5be516](https://github.com/user-attachments/assets/3183c187-7ed5-451a-bba5-f29ffc203498)
)

3. Kegiatan
<br>

![Kegiatan](![WhatsApp Image 2025-11-07 at 17 20 08_e753b6b3](https://github.com/user-attachments/assets/ab9538b9-4e7f-4ba2-97b9-0d94cd1a6261)
)
