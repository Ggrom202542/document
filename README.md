### 📌 แผนการสอน PHP และ Laravel 10 (ฉบับละเอียด) 🚀

---

#### 🔰 1. พื้นฐาน PHP (สำหรับมือใหม่)
  
**1.1 แนะนำ PHP และสภาพแวดล้อมการพัฒนา**  
- **PHP คืออะไร? ทำไมต้องใช้?**  
  - PHP (Hypertext Preprocessor) เป็นภาษาสคริปต์สำหรับพัฒนาเว็บเซิร์ฟเวอร์  
  - **เหตุผล:** มีความยืดหยุ่น รองรับฐานข้อมูล และมีคอมมูนิตี้ใหญ่  
- **ติดตั้ง PHP, Composer และเครื่องมือที่จำเป็น (XAMPP, Laragon, VS Code)**  
  - **XAMPP/Laragon:** จำลองสภาพแวดล้อมเว็บ (Apache, MySQL, PHP) บนเครื่อง  
  - **Composer:** ตัวจัดการแพ็กเกจสำหรับ PHP  
  - **VS Code:** Editor ที่ใช้งานง่าย พร้อมส่วนเสริมสำหรับ PHP  
  - **สถานการณ์:** สำหรับพัฒนาเว็บหรือแอปขนาดเล็กบนเครื่องคอมพิวเตอร์ของคุณ  
- **การตั้งค่า php.ini และความสำคัญของมัน**  
  - กำหนดพารามิเตอร์ เช่น ขนาดไฟล์อัปโหลด, การแสดงข้อผิดพลาด  
  - **เหตุผล:** ปรับแอปพลิเคชันให้ทำงานตามที่ต้องการและเพิ่มความปลอดภัย

---

**1.2 Syntax และโครงสร้างของ PHP**  
- **การเริ่มต้นไฟล์ PHP (`<?php ... ?>`)**  
  - ทุกไฟล์ PHP ควรเริ่มต้นด้วย `<?php`  
  - **ตัวอย่าง:**  
    ```php
    <?php
      echo "สวัสดีชาว PHP!";
    ?>
    ```
- **คอมเมนต์ใน PHP (`//`, `/* ... */`)**  
  - ใช้สำหรับอธิบายโค้ดเพื่อให้เข้าใจง่าย  
  - **ตัวอย่าง:**  
    ```php
    // คอมเมนต์บรรทัดเดียว
    /* คอมเมนต์หลายบรรทัด */
    ```

---

**1.3 ตัวแปรและชนิดข้อมูล**  
- **ตัวแปร (`$var`) และกฎการตั้งชื่อ**  
  - ตัวแปรเริ่มต้นด้วย `$`  
  - **ตัวอย่าง:**  
    ```php
    <?php
      $name = "John";
      $age = 25;
    ?>
    ```
- **ชนิดข้อมูลพื้นฐาน:**  
  - string, integer, float, boolean, array, object  
  - **ตัวอย่าง:**  
    ```php
    <?php
      $greeting = "สวัสดี";
      $number = 100;
      $pi = 3.1416;
      $isActive = true;
      $colors = array("แดง", "เขียว", "น้ำเงิน");
    ?>
    ```
- **Type Casting & Type Juggling:**  
  - แปลงชนิดข้อมูลโดยชัดเจนหรืออัตโนมัติ  
  - **ตัวอย่าง:**  
    ```php
    <?php
      $number = "123";
      $intNumber = (int)$number;
      $sum = "10" + 5;
    ?>
    ```

---

**1.4 คำสั่งควบคุมเงื่อนไข (Conditional Statements)**  
- **if-else และ switch-case**  
  - **ตัวอย่าง if-else:**  
    ```php
    <?php
      $score = 75;
      if ($score >= 80) {
          echo "เกรด A";
      } else {
          echo "ต้องพยายามอีกหน่อย";
      }
    ?>
    ```
  - **ตัวอย่าง switch-case:**  
    ```php
    <?php
      $day = "อาทิตย์";
      switch ($day) {
          case "จันทร์":
              echo "เริ่มสัปดาห์ใหม่";
              break;
          case "อาทิตย์":
              echo "วันหยุด";
              break;
          default:
              echo "วันปกติ";
      }
    ?>
    ```
- **Ternary Operator:**  
  - รูปแบบย่อของ if-else  
  - **ตัวอย่าง:**  
    ```php
    <?php
      $age = 20;
      echo ($age >= 18) ? "ผู้ใหญ่" : "ไม่บรรลุนิติภาวะ";
    ?>
    ```

---

**1.5 วนลูป (Loops)**  
- **for, while, do-while, foreach**  
  - **ตัวอย่าง for loop:**  
    ```php
    <?php
      for ($i = 0; $i < 5; $i++) {
          echo "รอบที่ " . $i . "<br>";
      }
    ?>
    ```
  - **ตัวอย่าง while loop:**  
    ```php
    <?php
      $i = 0;
      while ($i < 5) {
          echo "รอบที่ " . $i . "<br>";
          $i++;
      }
    ?>
    ```
  - **ตัวอย่าง foreach loop:**  
    ```php
    <?php
      $fruits = array("แอปเปิ้ล", "กล้วย", "ส้ม");
      foreach ($fruits as $fruit) {
          echo $fruit . "<br>";
      }
    ?>
    ```
- **break และ continue:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      for ($i = 0; $i < 10; $i++) {
          if ($i == 5) {
              break;
          }
          echo $i . "<br>";
      }
    ?>
    ```

---

**1.6 ฟังก์ชัน (Functions) และ Scope ของตัวแปร**  
- **การสร้างฟังก์ชัน:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      function sayHello() {
          echo "สวัสดี!";
      }
      sayHello();
    ?>
    ```
- **พารามิเตอร์และค่าเริ่มต้น:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      function greet($name = "Guest") {
          echo "สวัสดี, " . $name;
      }
      greet("Alice");
      greet();
    ?>
    ```
- **Global vs Local Scope:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      $globalVar = "ฉันอยู่ใน global";
      function testScope() {
          $localVar = "ฉันอยู่ใน local";
          echo $localVar;
          // echo $globalVar; // จะเกิด error ถ้าไม่ใช้ global keyword
      }
      testScope();
    ?>
    ```
- **return กับ echo:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      function sum($a, $b) {
          return $a + $b;
      }
      $result = sum(5, 10);
      echo $result;
    ?>
    ```

---

**1.7 Array และการจัดการข้อมูลใน Array**  
- **Indexed Array, Associative Array, Multidimensional Array:**  
  - **Indexed Array:**  
    ```php
    <?php
      $fruits = array("แอปเปิ้ล", "กล้วย", "ส้ม");
    ?>
    ```
  - **Associative Array:**  
    ```php
    <?php
      $person = array("name" => "John", "age" => 30);
    ?>
    ```
  - **Multidimensional Array:**  
    ```php
    <?php
      $students = array(
          array("name" => "Alice", "score" => 85),
          array("name" => "Bob", "score" => 90)
      );
    ?>
    ```
- **การเพิ่ม, ลบ, ค้นหา และเรียงลำดับ:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      $numbers = array(3, 1, 4, 2);
      array_push($numbers, 5);
      unset($numbers[1]);
      sort($numbers);
      print_r($numbers);
    ?>
    ```

---

**1.8 String Handling และ Regular Expressions**  
- **การเชื่อม, หาความยาว, ตัดข้อความ:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      $text1 = "Hello";
      $text2 = "World";
      $fullText = $text1 . " " . $text2;
      echo strlen($fullText);
      echo substr($fullText, 0, 5);
    ?>
    ```
- **การใช้ preg_match(), preg_replace():**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      $pattern = "/\d+/";
      $string = "มีตัวเลข 123 อยู่ในข้อความ";
      if (preg_match($pattern, $string, $matches)) {
          echo "พบตัวเลข: " . $matches[0];
      }
      $newString = preg_replace($pattern, "[number]", $string);
      echo $newString;
    ?>
    ```

---

**1.9 Superglobal Variables และการใช้งาน**  
- **Superglobals:**  
  - **$_GET:** รับค่าจาก URL  
  - **$_POST:** รับค่าจากฟอร์ม  
  - **$_SESSION:** เก็บข้อมูลเซสชัน  
  - **$_COOKIE:** เก็บข้อมูลคุกกี้  
  - **ตัวอย่าง:**  
    ```php
    <?php
      echo "ID ที่ส่งมาคือ " . $_GET['id'];
    ?>
    ```

---

#### 🛠 2. การเขียนโปรแกรมเชิงวัตถุ (OOP) ใน PHP  
*(สำหรับมือใหม่ถึงระดับกลาง)*

**2.1 การสร้างคลาสและออบเจ็กต์ (Class & Object)**  
- **วิธีสร้างคลาสและออบเจ็กต์:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      class Car {
          public $color;
          public function drive() {
              echo "รถกำลังวิ่ง";
          }
      }
      $myCar = new Car();
      $myCar->color = "แดง";
      $myCar->drive();
    ?>
    ```

**2.2 Access Modifiers (Encapsulation)**  
- **public, private, protected:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      class Person {
          private $name;
          public function setName($name) {
              $this->name = $name;
          }
          public function getName() {
              return $this->name;
          }
      }
      $person = new Person();
      $person->setName("Alice");
      echo $person->getName();
    ?>
    ```

**2.3 Constructors และ Destructors**  
- **__construct() และ __destruct():**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      class User {
          public $name;
          public function __construct($name) {
              $this->name = $name;
              echo "สร้างออบเจ็กต์สำหรับ " . $name . "<br>";
          }
          public function __destruct() {
              echo "ทำลายออบเจ็กต์สำหรับ " . $this->name;
          }
      }
      $user = new User("Bob");
    ?>
    ```

**2.4 Inheritance (การสืบทอดคลาส)**  
- **extends และ parent::__construct():**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      class Animal {
          public function makeSound() {
              echo "เสียงสัตว์";
          }
      }
      class Dog extends Animal {
          public function makeSound() {
              echo "สุนัขเห่า";
          }
      }
      $dog = new Dog();
      $dog->makeSound();
    ?>
    ```

**2.5 Polymorphism (เมธอดที่มีชื่อเดียวกันแต่ทำงานต่างกัน)**  
- **การใช้ interface และ abstract class:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      interface Shape {
          public function area();
      }
      class Square implements Shape {
          private $side;
          public function __construct($side) {
              $this->side = $side;
          }
          public function area() {
              return $this->side * $this->side;
          }
      }
      class Circle implements Shape {
          private $radius;
          public function __construct($radius) {
              $this->radius = $radius;
          }
          public function area() {
              return pi() * $this->radius * $this->radius;
          }
      }
      $square = new Square(4);
      $circle = new Circle(3);
      echo "พื้นที่สี่เหลี่ยม: " . $square->area() . "<br>";
      echo "พื้นที่วงกลม: " . $circle->area();
    ?>
    ```

**2.6 Trait (แนวคิดการใช้โค้ดร่วมกัน)**  
- **วิธีใช้ trait:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      trait Logger {
          public function log($message) {
              echo "[LOG]: " . $message;
          }
      }
      class Order {
          use Logger;
          public function process() {
              $this->log("กำลังประมวลผลคำสั่งซื้อ");
          }
      }
      $order = new Order();
      $order->process();
    ?>
    ```

---

#### 🗄 3. การเชื่อมต่อฐานข้อมูล (MySQL + PDO + Eloquent ORM)  
*(สำหรับมือใหม่ถึงระดับกลาง)*

**3.1 พื้นฐาน MySQL และการออกแบบฐานข้อมูล**  
- **คำสั่ง SQL:**  
  - CREATE TABLE, INSERT, SELECT, UPDATE, DELETE  
  - JOIN, GROUP BY, HAVING, INDEX  
  - **ตัวอย่าง:**  
    ```sql
    CREATE TABLE users (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(100),
        email VARCHAR(100)
    );
    INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');
    ```

**3.2 การเชื่อมต่อฐานข้อมูลด้วย PDO**  
- **PDO คืออะไร?**  
  - ใช้เชื่อมต่อฐานข้อมูลได้แบบเป็นกลางและปลอดภัย  
  - **ตัวอย่าง:**  
    ```php
    <?php
      try {
          $pdo = new PDO("mysql:host=localhost;dbname=mydb", "username", "password");
          $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
          echo "เชื่อมต่อฐานข้อมูลสำเร็จ";
      } catch (PDOException $e) {
          echo "เชื่อมต่อไม่สำเร็จ: " . $e->getMessage();
      }
    ?>
    ```
- **try-catch และ prepared statements:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      $stmt = $pdo->prepare("SELECT * FROM users WHERE email = :email");
      $stmt->execute(['email' => 'alice@example.com']);
      $user = $stmt->fetch();
      print_r($user);
    ?>
    ```

**3.3 Eloquent ORM (ใช้ใน Laravel 10)**  
- **การสร้าง Model และ Query Builder:**  
  - **ตัวอย่าง:**  
    ```php
    // สร้าง Model ด้วยคำสั่ง: php artisan make:model User
    <?php
      $users = User::where('name', 'John')->get();
      foreach ($users as $user) {
          echo $user->email;
      }
    ?>
    ```

---

#### 🚀 4. Laravel 10 (เริ่มต้นถึงขั้นสูง)

**4.1 การติดตั้ง Laravel และโครงสร้างโปรเจค**  
- **ติดตั้งด้วย Composer:**  
  ```bash
  composer create-project laravel/laravel myapp
  ```
- **โครงสร้างไฟล์หลัก:**  
  - **app/**: Controllers, Models, Middleware  
  - **bootstrap/**: bootstrap/app.php (เริ่มต้นแอป)
  - **config/**: ไฟล์คอนฟิกต่าง ๆ (app.php, database.php ฯลฯ)
  - **database/**: Migrations, Seeders, Factories
  - **public/**: Entry point (index.php) และไฟล์ Asset  
  - **resources/**: Views (Blade Templates), Assets (SASS, JS)
  - **routes/**: web.php (สำหรับหน้าเว็บ), api.php (สำหรับ API)
  - **storage/**: Log, Cache, Session files
  - **tests/**: Unit Test, Feature Test
  - **vendor/**: แพ็กเกจจาก Composer

---

**4.2 Routing และ Middleware**  
- **Routing:**  
  - กำหนดเส้นทาง URL ใน `routes/web.php`  
  - **ตัวอย่าง:**  
    ```php
    // routes/web.php
    Route::get('/', function () {
        return view('welcome');
    });
    Route::post('/submit', [FormController::class, 'submit']);
    ```
- **Middleware:**  
  - สร้างและใช้งาน Middleware ด้วยคำสั่ง:  
    ```bash
    php artisan make:middleware CheckUser
    ```
  - **ตัวอย่างโค้ด Middleware:**  
    ```php
    <?php
    namespace App\Http\Middleware;

    use Closure;
    use Illuminate\Http\Request;

    class CheckUser
    {
        public function handle(Request $request, Closure $next)
        {
            if (!$request->user()) {
                return redirect('/login');
            }
            return $next($request);
        }
    }
    ```

---

**4.3 Controller และ View (MVC)**  
- **Controller:**  
  - สร้าง Controller ด้วยคำสั่ง:  
    ```bash
    php artisan make:controller UserController
    ```
  - **ตัวอย่าง Controller:**  
    ```php
    <?php
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
- **View (Blade Templates):**  
  - ไฟล์ใน `resources/views` เช่น `books/index.blade.php`  
  - **ตัวอย่าง:**  
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

---

**4.4 เชื่อมต่อกับ Database และการใช้งาน Eloquent ORM**  
- **Eloquent ORM:**  
  - ใช้ในการเข้าถึงฐานข้อมูลแบบออบเจ็กต์  
  - **ตัวอย่าง:**  
    ```php
    public function index()
    {
        $books = Book::all();
        return view('books.index', compact('books'));
    }
    ```

---

**4.5 Authentication & Authorization**  
- **ติดตั้งระบบ Authentication:**  
  - ใช้แพ็กเกจ Breeze (หรือ Jetstream/Fortify)  
    ```bash
    php artisan breeze:install
    ```
- **การใช้ Middleware ตรวจสอบสิทธิ์:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
      if (Auth::check()) {
          echo "ผู้ใช้ล็อกอินแล้ว";
      } else {
          echo "กรุณาล็อกอิน";
      }
    ?>
    ```

---

**4.6 API Development (สร้าง REST API ด้วย Laravel)**  
- **สร้าง API Controller:**  
  - คำสั่ง:  
    ```bash
    php artisan make:controller ApiController --api
    ```
- **ใช้ Resource Controller:**  
  - **ตัวอย่าง:**  
    ```php
    Route::apiResource('products', ProductController::class);
    ```

---

**4.7 การทดสอบระบบ (Testing)**  
- **การรันการทดสอบ:**  
  ```bash
  php artisan test
  ```
- **Unit Testing ด้วย PHPUnit:**  
  - **ตัวอย่าง:**  
    ```php
    <?php
    use PHPUnit\Framework\TestCase;

    class UserTest extends TestCase {
        public function testUserCreation() {
            $user = new User(['name' => 'Test']);
            $this->assertEquals('Test', $user->name);
        }
    }
    ?>
    ```

---

**4.8 Deployment และ Security**  
- **การตั้งค่า .env และ Security:**  
  - กำหนดค่าในไฟล์ `.env` เช่น APP_DEBUG, APP_KEY, SESSION_DRIVER  
  - **ตัวอย่าง:**
    ```env
    APP_DEBUG=false
    APP_KEY=base64:xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    SESSION_DRIVER=redis
    CACHE_DRIVER=redis
    QUEUE_CONNECTION=redis
    ```
- **CSRF Protection, SQL Injection Prevention, Sanitization:**  
  - Laravel มีระบบป้องกัน CSRF โดยอัตโนมัติใน Blade ผ่าน `@csrf`

---

#### 📚 สรุปลำดับการเรียนรู้

**🔰 ระดับมือใหม่ (Beginner):**  
- พื้นฐาน PHP (Syntax, Variables, Arrays, Functions)  
- คำสั่งควบคุม (If-Else, Loops, Switch-Case)  
- พื้นฐาน MySQL (CRUD)  
- Superglobals ($_GET, $_POST, $_SESSION)

**⚡ ระดับกลาง (Intermediate):**  
- การเขียน OOP (Class, Object, Inheritance, Encapsulation)  
- PDO และ Eloquent ORM  
- ติดตั้ง Laravel และเข้าใจโครงสร้างโปรเจ็กต์

**🔥 ระดับสูง (Advanced):**  
- REST API Development  
- Authentication & Middleware  
- Security & Performance Optimization  
- Unit Testing และ Deployment

---


