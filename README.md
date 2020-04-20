# รายงานวิชา CN210
## สรุปเนื้อหาวิชา

### ส่งการบ้านครั้งที่ 1
* [CLIP1](https://youtu.be/ny0FBS_-dvw) : อธิบายคำสั่ง ADD

#### อธิบายการบ้านครั้งที่ 1
* คำสั่ง ADD เป็นคำสั่งประเภท R-Format โดยจะมีรู้แบบการเขียนดังนี้ 
  ```
  ADD $3, $1, $2 
  โดยที่ Rs = $1
       Rt = $2
       Rd = $3
  ```
  จากคำสั่งข้างต้น ADD จะทำการนำค่าที่เก็บอยู่ใน Register Rs มาบวกกับ Rt 
  แล้วนำค่าที่คำนวณได้ไปเก็บไว้ใน Register Rd
  
### ส่งการบ้านครั้งที่ 2
* [CLIP2](https://youtu.be/JuLSpSP8_eA) : Machine Language

#### อธิบายการบ้านครั้งที่ 2
* คอมพิวเตอร์ จะทำการนำคำสั่งที่เขียนเป็นโค้ด ไปแปลงเป็นภาษาที่เครื่องเข้าใจ

  ###### ตัวอย่างโค้ดภาษา Java
  ```
  class Test {
     public static void main(String[] args) {
        int a = 10;
        int b = 20;
        int c = a + b;
     }
  }
  ```
  ##### คำสั่งที่คอมพิวเตอร์เข้าใจ
  ```
  00000000:			08400000		// j 01000000
  00000004:			1A000000		// data
  …
  01000000:			8C090004		// lw $9, $0(4)
  01000004:			8D210000		// lw $1, $9(0)
  01000008:			8D220004		// lw $2, $9(4)
  0100000C:			00221820		// add $3, $1, $2
  01000010:			AD230008		// sw $3, $9(8)
  …
  1A000000:			0000000A		// a = 10
  1A000004:			00000014		// b = 20
  1A000008:			0000001E		// c = a + b = 30
  ```
  
### ส่งการบ้านครั้งที่ 3
* [CLIP3](https://youtu.be/RY3B8YMdZro) : Single Cycle vs Multi-Cycle

#### อธิบายการบ้านครั้งที่ 3
* ความแตกต่างของ Single Cycle กับ Multi-Cycle มีดังนี้

  ##### Single Cycle
  ![image](http://drive.google.com/uc?export=view&id=1VMr1lnfyKohBFLkmBLg08NJvhMphnbMJ)
    1. 1 คำสั่งจบใน Cycle เดียว ไม่มีจะเป็นคำสั่งอะไรก็ตาม
    2. มี ALU 3 ตัว
    3. มี Memory 2 ตัว แยกเก็บ Data กับ Instruction
    
  ##### Multi-Cycle
  ![image](http://drive.google.com/uc?export=view&id=1gw36aznG7a9HcBrN91cA51OqS0qHT313)
    1. แต่ละคำสั่ง ใช้เวลาทำงานไม่เท่ากัน
    2. มี ALU 1 ตัว
    3. มี Memory 1 ตัว เก็บ Data กับ Instruction ไว้ใน Memory เดียวกัน
