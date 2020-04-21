# รายงานวิชา CN210
## สรุปเนื้อหาวิชา

#### ส่วนประกอบคอมพิวเตอร์
* คอมพิวเตอร์ ประกอบด้วย 1. CPU(Central Processing Unit) 2. I/O (Input, Output) 3. Main Memory
#### MIPS Instruction Format
* มีทั้งหมด 3 รูปแบบ
  1. R-Format : เป็นคำสั่งประเภทคำนวณทางคณิตศาสตร์
  * ![image](http://drive.google.com/uc?export=view&id=16E1EZPLX0AB3rCJKctrxZLzTX8d4JAel)
  
  2. I-Format : เป็นคำสั่งที่จัดการเกี่ยวกับข้อมูล
  * ![image](http://drive.google.com/uc?export=view&id=1RKG_OyWCl5vUHJDnQWbdwhqpN-zbOlDG)
  
  3. J-Format : เป็นคำสั่งที่ให้กระโดดไปทั้งงานที่ตำแหน่งหนึ่งๆ
  * ![image](http://drive.google.com/uc?export=view&id=1ZFX3zuWFomzyou7p-JJMWHfKyQWX-8jd)
  
#### Von Neuman & Harvard Architectures
* Von Neuman : เก็บทั้ง Data และ Instruction อยู่ใน Memory เดียวกัน
* Harvard Architectures : เก็บ Data และ Instruction ไว้คนละ Memory

#### Single-Cycle, Multi-Cycle and Pipeline
* Single Cycle : ทำทุกคำสั่งจบใน 1 Cycle และทุก Cycle ใช้เวลาเท่ากันหมด
* Multi-Cycle : ทุกคำสั่งไม่สามารถจบใน Cycle เดียวได้ แต่ละคำสั่ง ใช่เวลาการทำงานไม่เท่ากัน
* Pipeline : 1 คำสั่งมีหลาย Cycle แต่สามารถทำหลายๆคำสั่งพร้อมกันได้

### ส่งการบ้านครั้งที่ 1
* [CLIP1](https://youtu.be/ny0FBS_-dvw) : อธิบายคำสั่ง ADD

#### อธิบายการบ้านครั้งที่ 1
* คำสั่ง ADD เป็นคำสั่งประเภท R-Format โดยจะมีรูปแบบการเขียนดังนี้ 
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

  ##### ตัวอย่างโค้ดภาษา Java
  
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
  00000000:		08400000		// j 01000000
  00000004:		1A000000		// data
  …
  01000000:		8C090004		// lw $9, $0(4)
  01000004:		8D210000		// lw $1, $9(0)
  01000008:		8D220004		// lw $2, $9(4)
  0100000C:		00221820		// add $3, $1, $2
  01000010:		AD230008		// sw $3, $9(8)
  …
  1A000000:		0000000A		// a = 10
  1A000004:		00000014		// b = 20
  1A000008:		0000001E		// c = a + b = 30
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
    1. แต่ละคำสั่ง ใช้เวลาทำงานไม่เท่ากัน และไม่สามารถจบได้ใน Cycle เดียว
    2. มี ALU 1 ตัว
    3. มี Memory 1 ตัว เก็บ Data กับ Instruction ไว้ใน Memory เดียวกัน

### ส่งการบ้านครั้งที่ 4
* [CLIP4](https://youtu.be/V6D0ssIwwcU) : อธิบายคำสั่ง load word (LW)

#### อธิบายการบ้านครั้งที่ 4
* LW เป็นคำสั่ง I-Format โดยมีการทำงาน 5 ขั้นตอน (T1 - T5)
  1. (T1) อ่านคำสั่งจาก Memory มาเก็บไว้ใน Instruction Register (R = Memory[PC])
     แล้วนำค่า PC ไปบวกกับ 4 แล้วนำมาเก็บไว้ใน PC (PC = PC + 4)
  2. (T2) อ่านค่าจาก Register Rs และ Rt มาพักไว้ที่ A กับ B (A = Reg[IR[25-21]], B = Reg[IR[20-16]])
     จากนั้น นำค่า offset (IR[15-0])
     มา sign extend เป็น 32 bits, shift left ไป 2 แล้วนำค่าที่ได้มาบวกกับ PC หลังจากนั้น นำค่าที่คำนวณได้มาเก็บไว้ใน ALUOut
     (ALUout = PC + (signext(IR[15-0])<<2))
  3. (T3) นำค่า A มาบวกกับ offset ที่ผ่านการ sign extend แล้วนำค่าที่คำนวณได้ไปเก็บไว้ที่ ALUOut (ALUOut = A + signext(IR[15-0]))
  4. (T4) นำค่าที่เก็บอยู่ใน ALUOut มาเก็บใน MDR (MDR = Memory[ALUout])
  5. (T5) นำค่าที่ได้ไปเก็บไว้ใน Register Rt (Reg[IR[20-16]] = MDR)

### ส่งการบ้านครั้งที่ 5
* [CLIP5](https://youtu.be/tBfjp4cu408) : อธิบายคำสั่ง beq

#### อธิบายการบ้านครั้งที่ 5
* beq เป็นคำสั่ง I-Format โดยมีการทำงาน 3 ขั้นตอน (T1 - T3)
  1. (T1) อ่านคำสั่งจาก Memory มาเก็บไว้ใน Instruction Register (R = Memory[PC])
     แล้วนำค่า PC ไปบวกกับ 4 แล้วนำมาเก็บไว้ใน PC (PC = PC + 4)
  2. (T2) อ่านค่าจาก Register Rs และ Rt มาพักไว้ที่ A กับ B (A = Reg[IR[25-21]], B = Reg[IR[20-16]])
     จากนั้น นำค่า offset (IR[15-0])
     มา sign extend เป็น 32 bits, shift left ไป 2 แล้วนำค่าที่ได้มาบวกกับ PC นำค่าที่คำนวณได้มาเก็บไว้ใน ALUOut
     (ALUout = PC + (signext(IR[15-0])<<2))
  3. (T3) นำค่า A มาเปรียบเทียบกับ B โดยถ้าหาก A เท่ากับ B (A == B) จะทำการ jump ไปที่ address ใหม่ (PC = ALUOut)

### ส่งการบ้านครั้งที่ 6
* [CLIP6](https://youtu.be/CDL71mYIqpk) : อธิบาย State Machine ของคำสั่ง R-Format

#### อธิบายการบ้านครั้งที่ 6
* คำสั่ง R-Format ที่ยกตัวอย่าง มีการทำงาน 4 ขั้นตอน (T1 - T4)

  ##### T1
  
  ```
  MemRead = 1                 ส่งไปที่ Memory
  lorD = 0                    (MemAddr <- PC) อ่านค่าจาก PC มาเก็บไว้ใน Memory
  IRWrite = 1                 (IR <- Mem[PC]) อ่านน่าจาก Memory มาเก็บใน Instruction Register
  ALUSrcA = 0                 (= PC) นำค่า PC ผ่าน MUX ไปที่ ALU เพื่อนำไปคำนวณต่อไป
  ALUSrcB = 1                 (= 4) นำค่า 4 ผ่าน MUX ไปที่ ALU เพื่อนำไปคำนวณต่อไป
  ALUOP = ADD                 (PC <- PC + 4) นำค่า PC มาบวก 4
  PCWrite = 1, PCSource = 0   (นำค่าที่คำนวณได้ ส่งไปเก็บไว้ใน PC)
  ```
  
  ##### T2
  
  ```
  ALUSrcA = 0                 (= PC) นำค่า PC ผ่าน MUX ไปที่ ALU เพื่อนำไปคำนวณต่อไป
  ALUSrcB = 3                 (= signext(IR<<2)) นำค่า offset มา sign extend, shift left 2 ผ่าน MUX ไปที่ ALU  
  ALUOP = 0                   (= add) นำค่ามาบวกกันแล้วนำไปเก็บไว้ใน ALUOut
  ```
  
  ##### T3
  
  ```
  ALUSrcA = 1                 (= A = Reg[$rs]) นำค่าจาก Rs มาเก็บใน A จากนั้น นำค่า A ผ่าน MUX ไปที่ ALU 
  ALUSrcB = 0                 (= A = Reg[$rt]) นำค่าจาก Rt มาเก็บใน B จากนั้น นำค่า A ผ่าน MUX ไปที่ ALU 
  ALUOP = 2                   (= IR[28-26]) นำค่ามาบวกกันแล้วนำไปเก็บไว้ใน ALUOut
  ```
  
  ##### T4
  
  ```
  RegWrite = 1                (Reg[$rd] <- ALUOut) 
  MemtoReg = 0                (= ALUOut) ส่งค่า ALUOut
  RegDst = 1                  (= $rd) มาเก็บที่ Register Rd
  ```

### ส่งการบ้านครั้งที่ 7
* [CLIP7](https://youtu.be/B_lLvlft4Kg) : Pipelining

#### อธิบายการบ้านครั้งที่ 7
* Pipelining จะสามารถทำงานหลายคำสั่งพร้อมกันได้ต่างจาก Single Cycle และ Multi-Cycle ที่ต้องทำงานให้จบที่ละคำสั่ง
  ##### ตัวอย่าง การทำงานของ Pipelining เปรียนเทียบกับ Single & Multiple Cycle
  
  ![image](http://drive.google.com/uc?export=view&id=1swZdQRgtWe_mqvAO8xVMxohDTeSfHDla)
  
  จากตัวอย่าง ใน Single และ Multiple Cycle จำเป็นต้องทำคำสั่งหนึ่งๆให้จบก่อน ถึงจะทำคำสั่งต่อๆไปได้
  แต่การทำงานแบบ Pipelining หลังจากทำาน IFetch ของคำสั่ง Load เสร็จก็สามารถทำงานทั้ง Reg ที่เป็นขั้นตอนต่อไปของคำสั่ง Load 
  และ IFetch ของคำสั่ง Store ที่เป็นคำสั่งต่อไปได้พร้อมๆกัน
