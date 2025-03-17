## 3. การเชื่อมต่อฐานข้อมูล (MySQL + PDO + Eloquent ORM) (สำหรับมือใหม่ถึงระดับกลาง)

### 3.1 พื้นฐาน MySQL และการออกแบบฐานข้อมูล
- **คำสั่ง CREATE TABLE, INSERT, SELECT, UPDATE, DELETE**  
  SQL คือภาษาที่ใช้สื่อสารกับฐานข้อมูล  
  **ตัวอย่าง CREATE TABLE:**  
  ```sql
  CREATE TABLE users (
      id INT AUTO_INCREMENT PRIMARY KEY,
      name VARCHAR(100),
      email VARCHAR(100)
  );
  ```
  **ตัวอย่าง INSERT:**  
  ```sql
  INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');
  ```
  **เหตุผล:** การเข้าใจคำสั่ง SQL เป็นพื้นฐานสำหรับการจัดการและเข้าถึงข้อมูลในฐานข้อมูล

- **การใช้ JOIN, GROUP BY, HAVING, INDEX**  
  ช่วยให้การดึงข้อมูลจากหลายตารางเป็นไปอย่างมีประสิทธิภาพ  
  **ตัวอย่าง JOIN:**  
  ```sql
  SELECT orders.id, users.name 
  FROM orders 
  JOIN users ON orders.user_id = users.id;
  ```
  **เหตุผล:** การใช้ JOIN และคำสั่งอื่น ๆ ช่วยให้สามารถสร้างรายงานหรือวิเคราะห์ข้อมูลได้จากหลายแหล่งที่มาในฐานข้อมูลเดียวกัน

### 3.2 การเชื่อมต่อฐานข้อมูลด้วย PDO
- **PDO คืออะไร? ทำไมควรใช้แทน MySQLi?**  
  PDO (PHP Data Objects) เป็นอินเตอร์เฟซที่ให้คุณเขียนโค้ดเชื่อมต่อฐานข้อมูลได้อย่างเป็นกลางต่อประเภทของฐานข้อมูล ทำให้โค้ดมีความปลอดภัยและสามารถย้ายไปใช้กับฐานข้อมูลอื่นได้ง่าย  
  **ตัวอย่างการเชื่อมต่อ:**  
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
  **เหตุผล:** การใช้ PDO ช่วยป้องกัน SQL Injection ด้วยการใช้ prepared statements และทำให้การจัดการข้อผิดพลาดทำได้ดีกว่า

- **try-catch และ prepared statements**  
  - **try-catch:** ใช้จัดการข้อผิดพลาดที่อาจเกิดขึ้นระหว่างการเชื่อมต่อหรือการประมวลผล SQL  
  - **Prepared Statements:** ป้องกัน SQL Injection และทำให้โค้ดปลอดภัย  
  **ตัวอย่างการใช้ prepared statement:**  
  ```php
  <?php
    $stmt = $pdo->prepare("SELECT * FROM users WHERE email = :email");
    $stmt->execute(['email' => 'alice@example.com']);
    $user = $stmt->fetch();
    print_r($user);
  ?>
  ```
  **เหตุผล:** การใช้ try-catch ช่วยให้โปรแกรมไม่หยุดทำงานเมื่อเกิดข้อผิดพลาด ในขณะที่ prepared statements เพิ่มความปลอดภัยให้กับฐานข้อมูล

### 3.3 Eloquent ORM (ใช้ใน Laravel 10)
- **การสร้าง Model**  
  Laravel ใช้ Eloquent ORM เพื่อเป็นตัวกลางในการเชื่อมต่อกับฐานข้อมูลในรูปแบบของออบเจ็กต์  
  **ตัวอย่างคำสั่งสร้าง Model:**  
  ```bash
  php artisan make:model User
  ```
  **เหตุผล:** Eloquent ทำให้การทำงานกับฐานข้อมูลใน Laravel ง่ายขึ้นโดยไม่ต้องเขียน SQL ทุกครั้ง

- **Query Builder**  
  ใช้สำหรับดึงข้อมูลจากฐานข้อมูลในรูปแบบที่อ่านง่าย  
  **ตัวอย่าง:**  
  ```php
  <?php
    $users = User::where('name', 'John')->get();
    foreach ($users as $user) {
        echo $user->email;
    }
  ?>
  ```
  **เหตุผล:** การใช้ Query Builder ช่วยให้โค้ดมีความกระชับและเป็นมิตรกับผู้พัฒนาที่ไม่คุ้นเคยกับ SQL ที่ซับซ้อน

---