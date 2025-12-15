# durveshaddition
1.    Adition.



C000 XRA A ; Clear the accumulator
 C001 MVI C , 00H ; Set Initial carry as Zero.
 C002 00
 C003 LXI H, C040H ; Initialize memory pointer at C040H 
 C004 40
 C005 C0
 C006 MOV A, M ; Copy first Byte into Reg.A
 C007 INX H ; Point towards Next Byte
 C008 ADD M ;Add first byte & Second byte
 C009 JNC NEXT ; If CY= 0 , GO TO Label NEXT
 C00A 0D
 C00B C0
 C00C INR C ; If CY = 1, Increment contents of Reg. C by 1
 C00D NEXT : INX H ;Point towards next memory location
 C00E MOV M , A ; Store Sum at next memory location 
 C00F INX H ; Point towards next memory location
 C010 MOV M , C ; Store Carry in next consecutive memory location
 C011 RST 1 ; Stop Program Execution



2. Subtraction





C000 XRA A ; Clear the accumulator
 C001 LXI H , CO30H ; Initialize memory pointer to subtrahend
 C002 30
 C003 C0
 C004 MOV B , M ;Copy subtrahend to Reg. B
 C005 INX H ;Point towards next memory location
 C006 MOV A , M ; Copy minuend to Reg.A
 C007 SUB B ; Subtract contents of Reg. B from Contents of Reg. A 
 C008 JP DOWN ;If S=0,Transfer Program Control to Label DOWN
 C009 0E
 C00A C0
 C00B CMA ;Find 1’S Compliment of contents of Reg.A
 C00C ADI 01H ;ADD 01H into contents of Reg.A
 C00D 01
 C00E DOWN: INX H ;Point towards next memory location
 C00F MOV M , A ;Store absolute difference into memory location
 C010 CF RST 1 ;Stop Program Execution



3. Multiplication







C000 XRA A ; Clear the accumulator
 C001 MVI D , 00 H ;Store Initial Carry in Reg.D
 C002 00
 C003 LXI H , CO30H ; Initialize memory pointer to multiplicand
 C004 30
 C005 C0
 C006 MOV B , M ;Copy multiplicand into Reg.B
 C007 INX H ;Point towards next memory location
 C008 MOV C , M ;Copy multiplier into Reg.C
 C009 UP: ADD B ;Add multiplicand into contents of Reg.A
 C00A JNC DOWN ;If CY = 0, Transfer Program Control to Label DOWN
 C00B 0E 
 C00C C0
 C00D INR D ; Increment Carry by 1
 C00E DOWN: DCR C ;Decrement contents of Reg.C by 1
 C00F JNZ UP ; If Z = 0 , Transfer Program Control to Label UP
 C010 09
 C011 C0
 C012 INX H ;Point towards next memory location
 C013 MOV M , A ;Copy Product into Memory location C032H
 C014 INX H ;Point towards next memory location
 C015 MOV M , D ;Store Carry into next memory location
 C016 CF RST 1 ;Stop Program Execution




4. Division




C000 XRA A ;Clear accumulator to store initial Remainder 
 C001 MVI C , 00H ;Store initial Quotient as 00H in Reg.C 
 C002 00
 C003 LXI H , C030H ;Point towards Dividend at memory location C030H 
 C004 30
 C005 C0
 C006 MOV A , M ;Copy Dividend into Reg.A
 C007 INX H ;Point towards next memory location
 C008 UP : CMP M ;Compare Dividend with Divisor
 C009 JC DOWN ; If Dividend < Divisor i.e.CY = 1 GO TO Label DOWN
 C00A 11
 C00B C0
 C00C SUB M ;If Dividend > Divisor i.e CY = 0 Subtract Divisor from 
Dividend
 C00D INR C ;Increment Quotient by 1
 C00E JMP UP ; Transfer program control to Label UP
 C00F 08
 C010 C0
 C011 DOWN : INX H ;Point towards next memory location
 C012 MOV M , C ;Store the Quotient in current memory location
 C013 INX H ;Point towards next memory location
 C014 MOV M , A ;Store Remainder in current memory location
 C015 CF RST 1 ;Stop Program Execution



5. Bad addition





C000 XRA A ;Clear accumulator to store initial SUM.
 C001 MOV B , A ;Set initial carry as 00H as contents of Reg.B 
 C002 LXI H,C0FFH ;Point towards memory location C0FFH
 C003 FF
 C004 C0
 C005 MOV C , M ;Set Counter as Reg. C
 C006 UP: INX H ;Point towards next memory location
 C007 ADD M ;Add memory contents with contents of Reg.A
 C008 DAA ;Decimal Adjust Accumulator
 C009 JNC DOWN ;If CY = 0,GO TO Label DOWN
 C00A 0D
 C00B C0
 C00C INR B ;If CY = 1, Increment contents of Reg.B by 1
 C00D DOWN: DCR C ;Decrement counter by 1
 C00E JNZ UP ;if contents of Reg.C ≠ 0 , GO TO Label UP
 C00F 06
 C010 C0 
 C011 STA C060H ;Store the Sum at memory location C060H.
 C012 60
 C013 C0
 C014 MOV A , B ;Store carry in Reg.A 
 C015 ADI 00H ;Add immediate 00H into Reg.A
 C016 00
 C017 DAA ;Decimal Adjust Accumulator
 C018 STA C061H ;Store Carry at memory location C061H 
 C019 61
 C01A C0
 C01B CF RST 1 ;Stop Program Execution






6. Reverse transverse of a block



C000 XRA A ;Clear accumulator 
 C001 MVI C , 05H ;Set Counter as Reg.C with contents 05H 
 C002 05
 C003 LXI H , C054H ;Initialize memory pointer at C054H of Memory Block 1
 C004 54
 C005 C0
 C006 LXI D , C070H ;Initialize memory pointer at C070H of Memory Block 2
 C007 70
 C008 C0
 C009 BACK : MOV A , M ;Copy Last Data Byte of Block 1 into Reg.A
 C00A STAX D ;Transfer contents of Reg.A to Memory Location C070H 
 C00B DCX H ;Decrement memory pointer of Block 1 By 1
 C00C INX D ;Increment memory pointer of Block 2 By 1
 C00D DCR C ;Decrement Counter By 1
 C00E JNZ BACK ;If Z = 0 , GO TO Label BACK
 C00F 09
 C010 C0
 C011 CF RST 1 ;Stop Program Execution







 7.  Exchange of a Block





C000 XRA A ;Clear accumulator
 C001 MVI C , 05H ;Set Counter as Reg.C with contents 05H 
 C002 05
 C003 LXI H , C060H ;Initialize memory pointer at C060H of Memory Block 1
 C004 60
 C005 C0
 C006 LXI D , C100H ;Initialize memory pointer at C100H of Memory Block 2
 C007 00
 C008 C1
 C009 BACK : LDAX D ;Copy First Data Byte of Block 2 into Reg.A
 C00A MOV B , M ;Copy First Data Byte of Block 1 to Reg.B 
 C00B MOV M , A ;Copy First Data Byte of Block 2 into Block 1
 C00C MOV A , B ;Copy First Data Byte of Block 1 into Reg.A 
 C00D STAX D ;Store contents of Reg.A into Block 2
 C00E INX H ;Point towards next memory location of Block 1
 C00F INX D ;Point towards next memory location of Block 2
 C010 DCR C ; Decrement Counter by 1
 C011 JNZ BACK ;If Z = 0 , GO TO Label BACK 
 C012 09
 C013 C0
 C014 CF RST 1 ;Stop Program Execution


