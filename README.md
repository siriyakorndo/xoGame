## xoGame
XO Game with any size

### วิธีการ Run โปรแกรม
วิธีการ Run โปรแกรม
-	ดาวน์โหลด XAMPP และโฟลเดอร์ xo_Game และไฟล์ฐานข้อมูล xo.sql
-	วางโฟลเดอร์ xo_Game ไว้ที่ C:\xampp\htdocs
-	เปิด XAMPP Control คลิก Start Apache และ Start MySQL จากนั้นคลิก Admin ของ MySQL
-	สร้างฐานข้อมูลชื่อ xo_game แล้ว Import ไฟล์ฐานข้อมูล xo.sql
-	เปิดใช้งานเว็บ http://localhost/xo_Game/ 

### วิธีการออกแบบโปรแกรม
- สร้างตารางฐานข้อมูล <br>
![image](https://user-images.githubusercontent.com/76682951/212619036-df6f9181-f00d-4666-95ca-91ce79bc7a44.png)
- ผู้เล่นสามารถเล่นตารางขนาดใด ๆ ก็ได้ <br>
  - สร้าง Input เก็บตัวเลขที่ผู้ใช้งานต้องการจะเล่นซึ่งต้องเริ่มจาก 3*3 หรือ อื่น ๆ โดยต้องเป็นเลขคี่เท่านั้นจึงจะสามารถหาผู้ชนะได้
  - ใช้ JavaScript สร้างตารางขนาด Input* Input และใส่ id ของช่องนั้น ๆ เป็นตัวเลขเช่น 0_0, 0_1, 0_2 พร้อมใส่ฟังก์ชันไว้ในแต่ละช่องด้วย
- การเริ่มเกม
  -	กำหนดข้อความบนตารางแสดงข้อความว่าเป็นรอบของ X หรือ O และเมื่อคลิกที่ช่องจะทำการส่งค่า id ของช่องไปเก็บไว้ใน Array และแสดง X หรือ O บนช่องที่คลิก
- การหาผู้ชนะ <br>
![image](https://user-images.githubusercontent.com/76682951/212620050-b602d34b-a89b-4d15-b5dd-79202641d8bf.png)
  -	สร้าง Array มาเก็บค่าคะแนนของ X และ O โดยแบ่งเป็นคะแนนแนวนอน แนวตั้ง และแนวทแยงทั้ง 2 ด้าน เช่น การเก็บคะแนน ของ X จะมีทั้งหมด 3 Array คือ pointXtr (เก็บคะแนนของ X จากแนวนอน), pointXtd (เก็บคะแนนของ X จากแนวตั้ง), diaX (เก็บคะแนนของ X จากแนวทแยง) โดยค่าเริ่มต้นของ pointXtr และ pointXtd จะมีค่าเริ่มต้นเป็น 0 และมีขนาดเท่ากับ Input แต่ diaX จะมีค่าเริ่มต้นเป็น [0,0] คือทแยงมุมซ้าย(เริ่มจาก0,0)และทแยงมุมขวาตามลำดับ
  -	เมื่อมีการคลิกบนช่อง จะมีการตรวจสอบว่าตรงกับช่องใดๆ และทำการเพิ่มคะแนนให้ช่องนั้นๆ โดยการให้คะแนนจะคิดจากหมายเลขช่องที่คลิก พิจารณาจาก id ของช่องๆนั้น เปรียบเทียบกัน id = a_b  โดยการเก็บคะแนนแนวนอนจะพิจารณาจากค่า a เมื่อค่า a ตรงกับค่าใด จะเพิ่มคะแนนให้ คะแนนแนวนอน[a] = +1 กรณีแนวตั้งก็เช่นกัน แต่เปลี่ยนเป็นการพิจารณาจากค่า b โดยเมื่อค่า b ตรงกับค่าใด จะเพิ่มคะแนนให้ คะแนนแนวตั้ง[b] = +1 ในส่วนของค่าทแยงมุมซ้ายจะพิจารณาว่าค่า a=b หรือไม่ หากเท่ากันจะเพิ่มคะแนนให้ แต่ค่าทแยงมุมขวาจะพิจารณาจาก a+b ว่าเท่ากับค่า input – 1 หรือไม่แล้วเพิ่มคะแนน จากนั้นจะพิจารณาคะแนนว่าฝั่งใดมีคะแนนเท่ากับ input เป็นฝั่งชนะ
  -	ตัวอย่าง เมื่อทำการคลิก X ที่ 0,0 จะมีการเพิ่มคะแนนของ X จะได้เป็น pointXtr = [1,0,0] pointXtr = [1,0,0] diaX=[1,0] 
- การแสดง replay
  - เมื่อคลิกเลือกให้ Replay เกมใด ๆ จะทำการส่งค่า table_size และ game ไปยังฟังก์ชัน แล้วจึงสร้างตารางขนาด table_size * table_size และนำค่า game มาเปลี่ยนให้อยู่ในรูป Array แล้วกำหนดให้อยู่ในรูป X หรือ O ตามลำดับ โดยกำหนดเวลาแสดงห่างกัน 1 วินาที
 
