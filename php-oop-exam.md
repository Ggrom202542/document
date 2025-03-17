## คำศัพท์และแนวคิดหลักใน OOP

- **Class (คลาส):**  
  แม่แบบหรือแบบแผนสำหรับสร้างวัตถุ (object) ที่ระบุคุณสมบัติ (properties) และพฤติกรรม (methods)  
  *ตัวอย่าง:* คลาส `Book` สำหรับเก็บข้อมูลหนังสือในห้องสมุด

- **Object (ออบเจ็กต์):**  
  สิ่งที่ถูกสร้างจากคลาส เป็นตัวแทนของข้อมูลจริงในโปรแกรม  
  *ตัวอย่าง:* หนังสือเล่มหนึ่งที่มีชื่อ "PHP for Beginners" ซึ่งเป็นออบเจ็กต์จากคลาส `Book`

- **Property (คุณสมบัติ):**  
  ตัวแปรที่อยู่ภายในคลาส ใช้เก็บข้อมูลของออบเจ็กต์  
  *ตัวอย่าง:* ในคลาส `Book` อาจมี property เช่น `$title`, `$author`

- **Method (เมธอด):**  
  ฟังก์ชันที่อยู่ภายในคลาส ใช้บ่งบอกพฤติกรรมของออบเจ็กต์  
  *ตัวอย่าง:* เมธอด `displayInfo()` ในคลาส `Book` เพื่อแสดงข้อมูลหนังสือ

- **Constructor:**  
  เมธอดพิเศษที่ถูกเรียกใช้ทันทีเมื่อสร้างออบเจ็กต์ ใช้สำหรับกำหนดค่าเริ่มต้นให้กับ property  
  *ตัวอย่าง:* เมธอด `__construct($title, $author)` ในคลาส `Book`

- **Destructor:**  
  เมธอดที่ถูกเรียกใช้เมื่อออบเจ็กต์ถูกทำลายหรือหมดขอบเขต ใช้สำหรับทำความสะอาดหรือบันทึกข้อมูลก่อนออบเจ็กต์จะหายไป

- **Encapsulation (การห่อหุ้ม):**  
  แนวคิดในการซ่อนข้อมูลภายในออบเจ็กต์และเข้าถึงผ่านเมธอดที่กำหนดไว้เท่านั้น โดยใช้ access modifiers เช่น `private`, `protected`, และ `public`  
  *ตัวอย่าง:* กำหนด property `$title` เป็น `private` และเข้าถึงผ่านเมธอด `getTitle()`

- **Inheritance (การสืบทอด):**  
  ความสามารถที่คลาสลูกสามารถรับคุณสมบัติและพฤติกรรมจากคลาสแม่ได้  
  *ตัวอย่าง:* คลาส `Book` สืบทอดจากคลาสแม่ `Item` ซึ่งมีคุณสมบัติพื้นฐานที่ใช้ร่วมกันในระบบห้องสมุด

- **Polymorphism (พหุรูป):**  
  แนวคิดที่ให้คลาสลูกสามารถมีการทำงานของเมธอดที่ชื่อเดียวกันแต่มีพฤติกรรมที่แตกต่างกัน  
  *ตัวอย่าง:* เมธอด `displayInfo()` ของคลาส `Book` และ `DVD` อาจมีการแสดงผลข้อมูลที่แตกต่างกันแต่เรียกใช้งานแบบเดียวกัน

- **Trait:**  
  ชุดของเมธอดที่สามารถนำไปใช้ร่วมกันในหลายคลาสโดยไม่ต้องใช้ inheritance  
  *ตัวอย่าง:* Trait `Logger` สำหรับบันทึกการทำงานในระบบ ซึ่งสามารถนำมาใช้ในคลาส `Book`, `DVD` หรือคลาสอื่นๆ

---

## ตัวอย่างโปรเจค: ระบบจัดการห้องสมุด (Library Management System)

ในโปรเจคนี้ เราจะสร้างคลาสพื้นฐานเพื่อจำลองการจัดการวัตถุในห้องสมุด ซึ่งรวมไปถึงหนังสือ (Book) และสื่ออื่น ๆ ที่อาจมีอยู่ในห้องสมุด (เช่น DVD) เราจะใช้แนวคิด OOP ดังนี้:

1. **คลาสแม่ (Item):**  
   รวบรวมคุณสมบัติพื้นฐานที่ใช้ร่วมกันในทุกสื่อในห้องสมุด เช่น รหัส, ชื่อ, สถานะการให้ยืม

2. **คลาสลูก (Book, DVD):**  
   สืบทอดจากคลาส `Item` และปรับแต่งพฤติกรรมเฉพาะสำหรับแต่ละประเภท

3. **Trait (Logger):**  
   ใช้สำหรับบันทึก log การทำงานของระบบ เช่น เมื่อมีการยืมหรือคืนสื่อ

4. **Constructor และ Encapsulation:**  
   ใช้กำหนดค่าเริ่มต้นให้กับแต่ละออบเจ็กต์และซ่อนข้อมูลที่ไม่ควรเข้าถึงโดยตรง

5. **Polymorphism:**  
   ใช้เมธอด `displayInfo()` ในแต่ละคลาสเพื่อแสดงข้อมูลสื่อที่แตกต่างกันโดยเรียกใช้เมธอดชื่อเดียวกัน

---

### โค้ดตัวอย่างโปรเจค PHP OOP: ระบบจัดการห้องสมุด

```php
<?php
// Trait สำหรับบันทึก log ในระบบ
trait Logger {
    public function log($message) {
        // ในการใช้งานจริงอาจบันทึกลงไฟล์หรือฐานข้อมูล
        echo "[LOG] " . $message . "<br>";
    }
}

// คลาสแม่สำหรับสื่อในห้องสมุด (Item)
abstract class Item {
    // Encapsulation: กำหนด property เป็น private เพื่อซ่อนข้อมูล
    private $id;
    private $title;
    private $isAvailable;

    // Constructor สำหรับกำหนดค่าเริ่มต้น
    public function __construct($id, $title) {
        $this->id = $id;
        $this->title = $title;
        $this->isAvailable = true; // สื่อใหม่จะพร้อมให้ยืม
    }

    // เมธอด getter สำหรับ property title
    public function getTitle() {
        return $this->title;
    }

    // เมธอดสำหรับเปลี่ยนสถานะการให้ยืม
    public function setAvailability($status) {
        $this->isAvailable = $status;
    }

    // เมธอดสำหรับตรวจสอบสถานะการให้ยืม
    public function isAvailable() {
        return $this->isAvailable;
    }

    // เมธอด abstract สำหรับแสดงข้อมูลสื่อ (Polymorphism)
    abstract public function displayInfo();
}

// คลาส Book สืบทอดจาก Item
class Book extends Item {
    use Logger; // ใช้ trait Logger เพื่อบันทึก log

    // Property เฉพาะสำหรับหนังสือ
    private $author;

    // Constructor สำหรับ Book เรียกใช้ constructor ของคลาสแม่ด้วย parent::__construct()
    public function __construct($id, $title, $author) {
        parent::__construct($id, $title);
        $this->author = $author;
        $this->log("สร้างหนังสือ: " . $title);
    }

    // เมธอดแสดงข้อมูลหนังสือ
    public function displayInfo() {
        echo "หนังสือ: " . $this->getTitle() . "<br>";
        echo "ผู้แต่ง: " . $this->author . "<br>";
        echo "สถานะ: " . ($this->isAvailable() ? "พร้อมให้ยืม" : "ไม่พร้อมให้ยืม") . "<br>";
    }
}

// คลาส DVD สืบทอดจาก Item
class DVD extends Item {
    use Logger; // ใช้ trait Logger ด้วยเช่นกัน

    // Property เฉพาะสำหรับ DVD
    private $duration; // ระยะเวลาของภาพยนตร์ (นาที)

    public function __construct($id, $title, $duration) {
        parent::__construct($id, $title);
        $this->duration = $duration;
        $this->log("สร้าง DVD: " . $title);
    }

    // เมธอดแสดงข้อมูล DVD
    public function displayInfo() {
        echo "DVD: " . $this->getTitle() . "<br>";
        echo "ระยะเวลา: " . $this->duration . " นาที<br>";
        echo "สถานะ: " . ($this->isAvailable() ? "พร้อมให้ยืม" : "ไม่พร้อมให้ยืม") . "<br>";
    }
}

// สร้างออบเจ็กต์ตัวอย่างในระบบห้องสมุด
$book1 = new Book(1, "PHP for Beginners", "John Doe");
$dvd1  = new DVD(2, "Learn PHP OOP", 120);

// แสดงข้อมูลสื่อทั้งสองโดยใช้เมธอด displayInfo() ซึ่งเป็นตัวอย่างของ Polymorphism
echo "<h3>ข้อมูลสื่อในห้องสมุด:</h3>";
$book1->displayInfo();
echo "<hr>";
$dvd1->displayInfo();

// สถานการณ์การยืมสื่อ: สมมุติว่าผู้ใช้ยืมหนังสือ $book1
echo "<h3>การยืมสื่อ:</h3>";
if ($book1->isAvailable()) {
    $book1->setAvailability(false); // เปลี่ยนสถานะให้ไม่พร้อมให้ยืม
    $book1->log("หนังสือ '" . $book1->getTitle() . "' ถูกยืมไปแล้ว");
} else {
    echo "หนังสือไม่พร้อมให้ยืม";
}

// แสดงสถานะหนังสือหลังการยืม
echo "<h3>ข้อมูลหนังสือหลังการยืม:</h3>";
$book1->displayInfo();
?>
```

---

## การอธิบายแนวคิดผ่านโปรเจค

1. **การสร้างคลาสและออบเจ็กต์:**  
   - **Item:** เป็นคลาสแม่ที่มีข้อมูลพื้นฐานของสื่อในห้องสมุด เช่น รหัสและชื่อ  
   - **Book และ DVD:** เป็นคลาสลูกที่สืบทอดจาก `Item` โดยเพิ่มคุณสมบัติเฉพาะ เช่น ผู้แต่งของหนังสือหรือระยะเวลาของ DVD  
   - **ออบเจ็กต์:** เมื่อสร้าง `$book1` และ `$dvd1` จะเป็นตัวแทนของหนังสือและ DVD ที่แท้จริงในระบบ

2. **Encapsulation:**  
   - ใช้ `private` ในการกำหนด property เช่น `$title`, `$isAvailable` ทำให้ไม่สามารถเข้าถึงหรือแก้ไขข้อมูลโดยตรงจากภายนอก  
   - มีเมธอด `getTitle()`, `setAvailability()` เพื่อเข้าถึงและปรับเปลี่ยนข้อมูล

3. **Constructor และ Destructor:**  
   - **Constructor:** ในแต่ละคลาสมีการกำหนดค่าเริ่มต้นและใช้ `parent::__construct()` เพื่อสืบทอดค่าเริ่มต้นจากคลาสแม่  
   - (ในตัวอย่างนี้ไม่ได้ใช้ Destructor แต่ในระบบจริงอาจมีการใช้เพื่อบันทึก log หรือทำความสะอาดทรัพยากร)

4. **Inheritance:**  
   - คลาส `Book` และ `DVD` สืบทอดจาก `Item` ทำให้สามารถใช้เมธอดพื้นฐานและเข้าถึง property ของคลาสแม่ได้

5. **Polymorphism:**  
   - เมธอด `displayInfo()` ถูกนิยามในแต่ละคลาสลูกเพื่อแสดงข้อมูลเฉพาะตัว แม้ว่าจะเรียกใช้เมธอดชื่อเดียวกันก็จะแสดงผลที่แตกต่างกันตามประเภทของสื่อ

6. **Trait:**  
   - Trait `Logger` ถูกนำไปใช้ในทั้งคลาส `Book` และ `DVD` เพื่อแชร์ฟังก์ชันการบันทึก log ช่วยลดความซ้ำซ้อนของโค้ด

---