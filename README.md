# InfyOm Laravel Generator

1. **Cài đặt** - vào project có sẵn (Laravel v5.8)

Thêm các package cần thiết vào composer.json hoặc chạy lệnh `composer require` bao gồm:

   *infyomlabs/laravel-generator*
   
   *laravelcollective/html* - html builder
   
   *infyomlabs/adminlte-templates* hoặc *coreui-templates* - template
   
   *infyomlabs/swagger-generator* (nếu cần) - sau khi cài đặt, đổi tên hai thư mục controller_docs và model_docs ở đường dẫn `vendor/infyomlabs/swagger-generator/templates` thành controller và model
   
   *appointer/swaggervel* (nếu cần)
   
   *doctrine/dbal* (nếu cần)

Sau khi thêm các package xong, chạy lệnh `composer update` để tiến hành cập nhật các gói trên vào project

Chèn các class cần thiết vào providers trong `config/app.php`

``` php

Collective\Html\HtmlServiceProvider::class,
Laracasts\Flash\FlashServiceProvider::class,
Prettus\Repository\Providers\RepositoryServiceProvider::class,
\InfyOm\Generator\InfyOmGeneratorServiceProvider::class,
\InfyOm\AdminLTETemplates\AdminLTETemplatesServiceProvider::class

```

Chèn các alias để tiện cho quá trình gọi sử dụng các package

``` php

'Form'      => Collective\Html\FormFacade::class,
'Html'      => Collective\Html\HtmlFacade::class,
'Flash'     => Laracasts\Flash\Flash::class

```

Chạy lệnh `php artisan vendor:publish` để cập nhật quá trình chỉnh sửa project

Mở file app\Providers\RouteServiceProvider.php và cập nhật `mapApiRoutes` như sau:

``` php
Route::prefix('api')
    ->middleware('api')
    ->as('api.')
    ->namespace($this->namespace."\\API")
    ->group(base_path('routes/api.php'));
```

Cuối cùng chạy lệnh `php artisan infyom:publish` để publish các file cần thiết vào project

2. **Các chức năng chính**

#### Code Generator

Laravel Generator hỗ trợ tạo các file tương ứng với từng lệnh (tương tự lệnh `php artisan make` mặc định của laravel)

![Ảnh 1](https://images.viblo.asia/ae9cf0fd-0eef-4178-8ad5-39ff9b212abf.png)
