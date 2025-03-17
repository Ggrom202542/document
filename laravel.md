## 4. Laravel 10 (เริ่มต้นถึงขั้นสูง)

Laravel คือเฟรมเวิร์ค PHP ที่เน้นการเขียนโค้ดที่เป็นระเบียบและมีความยืดหยุ่นสูง โดยมีโครงสร้างโปรเจคที่แบ่งแยกหน้าที่ชัดเจน เราจะเริ่มจากพื้นฐานของ Laravel และอธิบายการทำงานของแต่ละไฟล์ รวมถึงการปรับ driver ต่าง ๆ เพื่อรองรับการใช้งานในสถานการณ์จริง

---

### 4.1 พื้นฐานและโครงสร้างโปรเจคของ Laravel

#### โครงสร้างหลักของ Laravel  
เมื่อคุณติดตั้ง Laravel ผ่าน Composer (เช่น `composer create-project laravel/laravel myapp`) คุณจะพบกับโครงสร้างไฟล์ที่แบ่งตามหน้าที่ดังนี้:

- **app/**  
  - **Console/**, **Exceptions/**, **Http/**  
  - โฟลเดอร์ **Http/** ประกอบด้วย Controllers, Middleware และ Requests  
  - **Models:** (ใน Laravel 8 ขึ้นไป Model อยู่ในโฟลเดอร์ `app/Models` แต่บางโปรเจคอาจปรับเปลี่ยนตำแหน่งได้)
  
- **bootstrap/**  
  - มีไฟล์ `app.php` ซึ่งใช้สำหรับโหลดและเริ่มต้นแอปพลิเคชัน

- **config/**  
  - เก็บไฟล์คอนฟิกทั้งหมด เช่น `app.php`, `database.php`, `cache.php` เป็นต้น  
  - ไฟล์เหล่านี้เป็นตัวกำหนด driver ที่ใช้ในแต่ละส่วน (เช่น session, cache, queue)

- **database/**  
  - มีไฟล์ migrations, seeders และ factories ที่ใช้ในการสร้างและจัดการฐานข้อมูล

- **public/**  
  - โฟลเดอร์นี้คือ entry point ของแอปพลิเคชัน โดยมีไฟล์ `index.php` ที่ทำหน้าที่ bootstrap แอปและโหลดทุกอย่างเข้าสู่เซิร์ฟเวอร์เว็บ  
  - ไฟล์ asset ต่าง ๆ (เช่น CSS, JS, รูปภาพ) จะถูกเก็บไว้ที่นี่

- **resources/**  
  - เก็บไฟล์ view (Blade templates),ไฟล์แปลภาษา (lang) และ assets ที่จะถูกคอมไพล์ (เช่น SASS, JavaScript)
  
- **routes/**  
  - กำหนดไฟล์ routing หลักของแอป เช่น `web.php` สำหรับหน้าเว็บ, `api.php` สำหรับ API
  - ไฟล์นี้เป็นที่ตั้งของการกำหนดเส้นทาง (routing) ที่เชื่อมต่อกับ Controller หรือ Closure ในการประมวลผลคำขอ

- **storage/**  
  - เก็บไฟล์ log, cache, session และไฟล์อื่น ๆ ที่แอปพลิเคชันต้องการบันทึกระหว่างการทำงาน

- **tests/**  
  - เก็บ Unit Test และ Feature Test สำหรับตรวจสอบความถูกต้องของแอปพลิเคชัน

- **vendor/**  
  - โฟลเดอร์ที่ Composer ใช้จัดการแพ็กเกจต่าง ๆ ที่ติดตั้งเข้ามา

#### การทำงานของไฟล์หลัก
- **public/index.php:**  
  เป็น entry point เมื่อผู้ใช้เข้าถึงเว็บแอป ทุกคำขอจะถูกส่งมาที่ไฟล์นี้ ก่อนที่จะโหลด Bootstrap และดำเนินการตามคำขอผ่าน Kernel ของ Laravel  
- **bootstrap/app.php:**  
  ทำหน้าที่สร้าง instance ของแอปพลิเคชันและตั้งค่าพื้นฐานต่าง ๆ ที่จำเป็น
- **routes/web.php และ routes/api.php:**  
  กำหนดเส้นทางของ URL เมื่อมีคำขอมาจากผู้ใช้ ระบบจะดูว่าควรส่งคำขอนั้นไปให้ Controller ไหนหรือประมวลผลผ่าน Closure ใด
- **app/Http/Controllers:**  
  อยู่ในโฟลเดอร์นี้คือ Controller ที่รับผิดชอบการประมวลผลคำขอและส่งข้อมูลไปยัง View
- **resources/views:**  
  ประกอบด้วยไฟล์ Blade Template ที่ทำหน้าที่แสดงผลข้อมูลและหน้าตา UI ของแอปพลิเคชัน

---

### 4.2 การทำงานของ Routing, Middleware และ Controller

#### Routing  
ในไฟล์ `routes/web.php` คุณจะกำหนดเส้นทางของ URL และระบุว่าควรใช้ Controller หรือ Closure ในการประมวลผลคำขอนั้น  
**ตัวอย่าง:**  
```php
// routes/web.php
Route::get('/', function () {
    return view('welcome'); // แสดง view 'welcome.blade.php'
});

Route::post('/submit', [FormController::class, 'submit']);
```
**การทำงาน:**  
- เมื่อผู้ใช้เข้าถึง URL `/` ระบบจะโหลดไฟล์ Blade `welcome.blade.php` จากโฟลเดอร์ resources/views  
- การส่งข้อมูลผ่านแบบฟอร์มไปยัง `/submit` จะถูกส่งไปยังเมธอด `submit()` ใน Controller ที่ชื่อว่า `FormController`

#### Middleware  
Middleware คือชั้นกลางที่ช่วยตรวจสอบหรือปรับแต่งคำขอก่อนที่จะถึง Controller  
**ตัวอย่าง:**  
```bash
php artisan make:middleware CheckUser
```
ในไฟล์ที่สร้างขึ้น (เช่น `app/Http/Middleware/CheckUser.php`) คุณสามารถกำหนดเงื่อนไขเพื่ออนุญาตหรือปฏิเสธคำขอ  
**ตัวอย่างโค้ดใน Middleware:**
```php
<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;

class CheckUser
{
    public function handle(Request $request, Closure $next)
    {
        // ตรวจสอบว่าผู้ใช้ล็อกอินหรือไม่
        if (!$request->user()) {
            return redirect('/login');
        }
        return $next($request);
    }
}
```
**การทำงาน:**  
- Middleware นี้จะถูกเรียกใช้ทุกครั้งที่คำขอเข้ามา หากผู้ใช้ยังไม่ได้ล็อกอินจะถูกเปลี่ยนเส้นทางไปที่หน้า login

#### Controller และ View (MVC)  
**Controller:** อยู่ใน `app/Http/Controllers` ทำหน้าที่รับคำขอ (request) ประมวลผล และส่งข้อมูลไปยัง View  
**ตัวอย่าง Controller:**
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Book;

class BookController extends Controller
{
    // เมธอดสำหรับแสดงรายการหนังสือ
    public function index()
    {
        $books = Book::all();
        return view('books.index', compact('books'));
    }
}
```
**View:** อยู่ใน `resources/views/books/index.blade.php` ซึ่งเป็นไฟล์ Blade ที่แสดงข้อมูลที่ส่งมาจาก Controller  
**ตัวอย่าง View:**
```blade
<!-- resources/views/books/index.blade.php -->
<!DOCTYPE html>
<html>
<head>
    <title>รายการหนังสือ</title>
</head>
<body>
    <h1>หนังสือในห้องสมุด</h1>
    <ul>
        @foreach($books as $book)
            <li>{{ $book->title }} โดย {{ $book->author }}</li>
        @endforeach
    </ul>
</body>
</html>
```
**การทำงาน:**  
- เมื่อผู้ใช้เข้าถึง URL ที่กำหนดใน routing (เช่น `/books`) Controller จะดึงข้อมูลหนังสือจาก Model แล้วส่งไปยัง View เพื่อแสดงผล

---

### 4.3 การเชื่อมต่อกับ Database และ Eloquent ORM

#### Eloquent ORM  
Laravel ใช้ Eloquent ORM ในการสื่อสารกับฐานข้อมูลในรูปแบบของออบเจ็กต์  
**ตัวอย่างการเรียกใช้ Eloquent ใน Controller:**
```php
public function index()
{
    // ดึงข้อมูลหนังสือทั้งหมด
    $books = Book::all();
    return view('books.index', compact('books'));
}
```
**การทำงาน:**  
- Eloquent ช่วยให้คุณสามารถเขียนโค้ดแบบออบเจ็กต์ในการเข้าถึงข้อมูล เช่น การค้นหา บันทึก หรืออัปเดตข้อมูลในตารางฐานข้อมูล โดยไม่ต้องเขียน SQL ทุกครั้ง

---

### 4.4 การใช้งาน Driver ใน Laravel

Laravel มีการตั้งค่าที่ยืดหยุ่นในแต่ละส่วนผ่านไฟล์คอนฟิกในโฟลเดอร์ **config/** ซึ่งสามารถปรับแต่งการทำงานของระบบผ่านการเลือก driver ที่ต้องการใช้ได้ ตัวอย่างที่สำคัญคือ:

#### 1. **Session Driver**  
กำหนดวิธีการจัดเก็บ session ของผู้ใช้ เช่น ผ่านไฟล์, database, Redis  
**ตัวอย่างไฟล์ `config/session.php`:**
```php
'driver' => env('SESSION_DRIVER', 'file'),
```
**การใช้งาน:**  
- สำหรับแอปพลิเคชันที่มีผู้ใช้ไม่มาก คุณอาจใช้ driver แบบ `file` เพื่อเก็บ session ลงในไฟล์ในโฟลเดอร์ `storage/framework/sessions`  
- หากแอปมีปริมาณผู้ใช้สูงและต้องการประสิทธิภาพที่ดีขึ้น สามารถเปลี่ยนเป็น `redis` หรือ `database`

#### 2. **Cache Driver**  
กำหนดวิธีการเก็บ cache เช่น file, database, Redis, Memcached  
**ตัวอย่างไฟล์ `config/cache.php`:**
```php
'default' => env('CACHE_DRIVER', 'file'),
```
**การใช้งาน:**  
- ในแอปพลิเคชันทั่วไป อาจเริ่มต้นด้วย `file` driver แต่ถ้าต้องการประสิทธิภาพสูงขึ้น สามารถเปลี่ยนเป็น `redis` เพื่อให้การดึงข้อมูล cache เร็วขึ้น

#### 3. **Queue Driver**  
Laravel มีระบบคิวที่ช่วยจัดการงานแบบ asynchronous (งานที่ต้องรันเบื้องหลัง)  
**ตัวอย่างไฟล์ `config/queue.php`:**
```php
'default' => env('QUEUE_CONNECTION', 'sync'),
```
**การใช้งาน:**  
- ในการพัฒนาเบื้องต้น คุณอาจใช้ `sync` (รันงานทันที) แต่สำหรับโปรดักชั่นที่มีงานที่ต้องทำในพื้นหลังจริง ๆ เช่นการส่งอีเมล คุณสามารถเปลี่ยนเป็น `database`, `redis` หรือ `sqs` (Amazon Simple Queue Service)

#### 4. **Filesystem Driver**  
กำหนดวิธีการจัดเก็บไฟล์ เช่น local, s3, ftp  
**ตัวอย่างไฟล์ `config/filesystems.php`:**
```php
'default' => env('FILESYSTEM_DRIVER', 'local'),
```
**การใช้งาน:**  
- สำหรับการเก็บไฟล์ในเซิร์ฟเวอร์ของตัวเองใช้ `local` แต่ถ้าต้องการจัดเก็บไฟล์บนคลาวด์เช่น Amazon S3 สามารถปรับค่าในไฟล์คอนฟิกและไฟล์ `.env`

---

### 4.5 การพัฒนา API ด้วย Laravel

Laravel รองรับการสร้าง API ผ่าน routing และ controller ที่ออกแบบมาเฉพาะสำหรับ API  
**ตัวอย่างการสร้าง API Controller:**
```bash
php artisan make:controller Api/BookController --api
```
**ตัวอย่างการกำหนดเส้นทางใน `routes/api.php`:**
```php
Route::apiResource('books', App\Http\Controllers\Api\BookController::class);
```
**การทำงาน:**  
- เส้นทางใน `api.php` จะมีการจัดการคำขอที่มาจาก client ในรูปแบบ JSON  
- Controller ที่สร้างขึ้นจะมีเมธอดสำหรับการทำงาน CRUD (Create, Read, Update, Delete) โดยอัตโนมัติ

---

### 4.6 การทดสอบระบบ (Testing) และ Deployment

#### การทดสอบระบบ  
Laravel มีระบบทดสอบในตัวที่รองรับ PHPUnit  
**ตัวอย่างการทดสอบ Controller:**
```php
<?php
// tests/Feature/BookTest.php
namespace Tests\Feature;

use Tests\TestCase;
use App\Models\Book;

class BookTest extends TestCase
{
    public function test_books_are_listed_correctly()
    {
        // สมมุติว่ามีการสร้างหนังสือในฐานข้อมูล
        Book::factory()->count(3)->create();

        $response = $this->get('/books');
        $response->assertStatus(200);
        $response->assertSeeText('หนังสือในห้องสมุด');
    }
}
```
**การทำงาน:**  
- การทดสอบช่วยให้มั่นใจว่าแต่ละส่วนของแอปพลิเคชันทำงานถูกต้องและสามารถจับปัญหาที่อาจเกิดขึ้นได้ตั้งแต่ระยะเริ่มต้น

#### Deployment และ Security  
- **.env File:**  
  ไฟล์ `.env` เป็นที่เก็บข้อมูลที่สำคัญสำหรับการตั้งค่า เช่น ฐานข้อมูล, session, cache driver, key ความปลอดภัย  
  **ตัวอย่าง:**
  ```env
  APP_DEBUG=false
  APP_KEY=base64:xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
  SESSION_DRIVER=redis
  CACHE_DRIVER=redis
  QUEUE_CONNECTION=redis
  ```
- **Security:**  
  Laravel มีระบบป้องกัน CSRF (Cross-Site Request Forgery) โดยอัตโนมัติในฟอร์มผ่าน Blade (`@csrf`) และมีการจัดการ sanitization และ validation ของข้อมูลเพื่อป้องกัน SQL Injection และการโจมตีอื่น ๆ

---

### 4.7 สรุปการทำงานและความสัมพันธ์ของไฟล์ใน Laravel

- **Public Index:**  
  `public/index.php` เป็น entry point ที่รับคำขอทั้งหมด แล้วโหลด Bootstrap ของ Laravel  
- **Bootstrap & Config:**  
  `bootstrap/app.php` สร้าง instance ของแอปและโหลดไฟล์คอนฟิกในโฟลเดอร์ `config/`  
- **Routing:**  
  ไฟล์ใน `routes/` เช่น `web.php` และ `api.php` ทำหน้าที่กำหนดเส้นทางและเชื่อมโยงกับ Controller  
- **Controller & Models:**  
  ใน `app/Http/Controllers` จะมีการรับคำขอและประมวลผลโดยเรียกใช้ Models (เช่น `app/Models/Book.php`) ในการดึงข้อมูล  
- **Views:**  
  ไฟล์ใน `resources/views` ใช้สำหรับแสดงผลข้อมูลผ่าน Blade Template ทำให้แยกการแสดงผลออกจากตรรกะ  
- **Drivers:**  
  การตั้งค่า driver ในไฟล์คอนฟิก (เช่น session, cache, queue) จะช่วยปรับแต่งพฤติกรรมของแอปพลิเคชันให้เหมาะสมกับสภาพแวดล้อมและปริมาณงาน

---

### ตัวอย่างการสร้างโปรเจค Laravel ที่ครอบคลุมพื้นฐานถึงขั้นสูง

**สถานการณ์:**  
สมมุติว่าเราต้องการสร้างแอปพลิเคชันจัดการห้องสมุดออนไลน์ ที่ให้ผู้ใช้สามารถดูรายการหนังสือ ยืมหนังสือ และมีระบบ API สำหรับเชื่อมต่อกับแอปพลิเคชันมือถือ

**แนวทาง:**  
1. กำหนดเส้นทางใน `routes/web.php` สำหรับหน้าเว็บแสดงรายการหนังสือ  
2. สร้าง Controller (เช่น `BookController`) เพื่อดึงข้อมูลหนังสือจากฐานข้อมูลและส่งต่อไปยัง View  
3. สร้าง Model `Book` ใน `app/Models` พร้อมกับ Migration สำหรับตารางหนังสือ  
4. สร้าง View (Blade Template) ใน `resources/views/books/index.blade.php` เพื่อแสดงข้อมูลหนังสือ  
5. กำหนด API routes ใน `routes/api.php` เพื่อรองรับการเชื่อมต่อกับแอปมือถือ

**ตัวอย่างโค้ดสั้น ๆ สำหรับแต่ละส่วน:**

- **Migration (สร้างตารางหนังสือ):**
  ```php
  // database/migrations/2025_03_16_000000_create_books_table.php
  use Illuminate\Database\Migrations\Migration;
  use Illuminate\Database\Schema\Blueprint;
  use Illuminate\Support\Facades\Schema;

  class CreateBooksTable extends Migration
  {
      public function up()
      {
          Schema::create('books', function (Blueprint $table) {
              $table->id();
              $table->string('title');
              $table->string('author');
              $table->timestamps();
          });
      }

      public function down()
      {
          Schema::dropIfExists('books');
      }
  }
  ```

- **Model:**
  ```php
  // app/Models/Book.php
  namespace App\Models;

  use Illuminate\Database\Eloquent\Factories\HasFactory;
  use Illuminate\Database\Eloquent\Model;

  class Book extends Model
  {
      use HasFactory;
      
      protected $fillable = ['title', 'author'];
  }
  ```

- **Controller สำหรับหน้าเว็บ:**
  ```php
  // app/Http/Controllers/BookController.php
  namespace App\Http\Controllers;

  use App\Models\Book;

  class BookController extends Controller
  {
      public function index()
      {
          $books = Book::all();
          return view('books.index', compact('books'));
      }
  }
  ```

- **Route สำหรับหน้าเว็บ:**
  ```php
  // routes/web.php
  use App\Http\Controllers\BookController;

  Route::get('/books', [BookController::class, 'index']);
  ```

- **View (Blade Template):**
  ```blade
  <!-- resources/views/books/index.blade.php -->
  <!DOCTYPE html>
  <html>
  <head>
      <title>รายการหนังสือ</title>
  </head>
  <body>
      <h1>หนังสือในห้องสมุด</h1>
      <ul>
          @foreach($books as $book)
              <li>{{ $book->title }} โดย {{ $book->author }}</li>
          @endforeach
      </ul>
  </body>
  </html>
  ```

- **API Controller (สำหรับ API):**
  ```php
  // app/Http/Controllers/Api/BookController.php
  namespace App\Http\Controllers\Api;

  use App\Http\Controllers\Controller;
  use App\Models\Book;
  use Illuminate\Http\Request;

  class BookController extends Controller
  {
      public function index()
      {
          return response()->json(Book::all());
      }
  }
  ```

- **Route สำหรับ API:**
  ```php
  // routes/api.php
  use App\Http\Controllers\Api\BookController;

  Route::apiResource('books', BookController::class);
  ```

---
