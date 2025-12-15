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







8.  Count of Occurrence of Data Byte 





C000 XRA A ;Clear accumulator 
 C001 MVI B , 00H ;Set Count of Occurrence as 00H in Reg.B 
 C002 00
 C003 LXI H,C04FH ;Initialize memory pointer where block length is stored 
 C004 4F
 C005 C0
 C006 MOV C , M ;Copy block length into Reg.C
 C007 LOOP: INX H ;Point towards next memory location 
 C008 MOV A , M ;Copy Data Byte into Reg.A 
 C009 CPI ABH ;Compare contents of Reg.A with Data Byte ABH
 C00A AB
 C00B JNZ NEXT ;If Z = 0, GO TO Label NEXT
 C00C 0F
 C00D C0
 C00E INR B ;If Z = 1,Increment Count of Occurrence by 1
 C00F NEXT: DCR C ;Decrement Counter by 1
 C010 JNZ LOOP ;If Z = 0 , GO TO Label LOOP
 C011 07
 C012 C0
 C013 LXI H , C100H ; If Z = 1, Initialize memory pointer at C100H
 C014 00
 C015 C1
 C016 MOV M , B ; Copy Count of Occurrence at C100H
 C017 CF RST 1 ;Stop Program Execution







 9. First Occurrence of Data Byte





C000 XRA A ;Clear accumulator 
 C001 LXI H,C07FH ;Point towards memory location where block length is 
stored.
 C002 7F
 C003 C0
 C004 MOV C , M ;Copy Block length into Reg.C
 C005 MVI A , DBH ;Copy Data Byte DBH into Reg.A
 C006 DB
 C007 NEXT: INX H ;Point towards next memory location
 C008 CMP M ;Compare Contents of memory location with Data Byte 
DBH
 C009 JZ STOP ;If Z = 1 , GO TO Label STOP
 C00A 13
 C00B C0
 C00C DCR C ;Decrement Counter By 1
 C00D JNZ NEXT ;If Z = 0 , GO TO Label NEXT
 C00E 07
 C00F C0
 C010 LXI H, ABABH ;Load HL Reg.Pair with ABABH
 C011 AB
 C012 AB
 C013 CF STOP: RST 1 ;Stop Program Execution







 10.   Count of odd as even no.






C000 XRA A ;Clear accumulator
 C001 MVI C , 05H ;Set Counter as Reg.C with 05H.
 C002 05
 C003 MVI D , 00H ;Set Odd Counter as Reg.D as 00H
 C004 00
 C005 MVI E , 00H ;Set Even Counter as Reg.E as 00H
 C006 00
 C007 LXI H, C040H ;Initialize memory pointer at C040H 
 C008 40
 C009 C0
 C00A UP: MOV A , M ;Copy Data Byte in Reg.A
 C00B RRC ;Rotate contents of Reg.A towards Right
 C00C JC ODD ;If CY = 1 , GO TO Label ODD
 C00D 13
 C00E C0
 C00F INR E ;Increment Even Counter
 C010 JMP NEXT ;GO TO Label NEXT
 C011 14
 C012 C0
 C013 ODD: INR D ;Increment ODD Counter
 C014 NEXT: INX H ;Point towards next memory location
 C015 DCR C ;Decrement contents of Reg.C
 C016 JNZ UP ;If Z = 0 , GO TO Label UP
 C017 0A
 C018 C0
 C019 MOV M , D ;If Z = 1,Copy ODD count in next memory location 
 C01A INX H ;Point towards next memory location
 C01B MOV M , E ;Copy EVEN count in current memory location
 C01C RST 1 ;Stop Program Execution









 11. Smallest as well as greatest no.





C000 XRA A ;Clear accumulator
 C001 MVI C , 0BH ;Set Counter as Reg.C with 0BH.
 C002 0B
 C003 LXI H, C030H ;Initialize memory pointer at C030H
 C004 30
 C005 C0
 C006 MOV D , M ;Assume D contents are greatest
 C007 MOV E , M ;Assume E contents are smallest
 C008 DCR C ;Decrement length by one
 C009 UP: INX H ; Point towards next memory location
 C00A MOV A,M ;Store next memory contents in A
 C00B CMP D ;Compare D contents are greater than A 
 C00C JC SMALL ;If D > A, then go to Label SMALL 
 C00D 10
 C00E C0
 C00F MOV D , A ;Copy Greatest in Reg. D 
 C010 SMALL: CMP E ;Compare E contents are smaller than A
 C011 JNC NEXT ;If E < A , then go to Label NEXT
 C012 15
 C013 C0
 C014 MOV E , A ;Copy smallest in Reg.E
 C015 NEXT : DCR C ;Decrement counter by 1
 C016 JNZ UP ;If Z = 0 , GO TO Label UP
 C017 09
 C018 C0
 C019 INX H ;Increment HL Pointer by 1
 C01A MOV M , D ;Copy greatest in memory
 C01B INX H ;Increment HL Pointer by 1
 C01C MOV M , E ;Copy smallest in memory
 C01D RST 1 ;Stop Program Execution







 12. Ascending or descending order






C000 START : MVI B ,00H ;Set Ptr = 00H initially
 C001 00
 C002 LXI H ,D000H ;Point towards memory location where block length is 
stored
 C003 00
 C004 D0
 C005 MOV C , M ;Copy count in Reg.C
 C006 LOOP : INX H ;Point towards next memory location where actual block
Starts
 C007 MOV A ,M ;Copy First Data Byte in Reg.A
 C008 DCR C ;Decrement counter by 1
 C009 INX H ;Point towards next memory location
 C00A CMP M ;Compare contents of memory with contents of Reg.A
 C00B JC EXIT ;If CY = 1,GO TO Label EXIT
 C00C 15
 C00D C0
 C00E MOV D , M ;If CY = 0,Copy contents of memory location in Reg.D
 C00F MOV M , A ;Copy Contents of Reg.A into memory location
 C010 DCX H ;Point towards previous memory location
 C011 MOV M , D ;Copy contents of Reg.D into memory location
 C012 INX H ;Point towards next memory location
 C013 MVI B , 01H ;Set Ptr = 01H
 C014 01
 C015 EXIT : DCR C ;Decrement counter by 1
 C016 JNZ LOOP ;If Z = 0,GO TO Label LOOP
 C017 06
 C018 C0
 C019 DCR B ;Decrement Pointer by 1
 C01A JZ START ;If ptr = 0 , GO TO Label START
 C01B 00
 C01C C0
 C01D CF RST 1 ;Stop Program Execution








 13. Separation of two nibble and multiplication








C000 LXI H , D000H ;Initialize memory pointer at D000H
 C001 00
 C002 D0
 C003 MOV A , M ;Copy Data Byte in Reg.A 
 C004 ANI 0FH ;Separate Lower Nibble
 C005 0F
 C006 MOV B , A ;Copy Lower Nibble in Reg.B
 C007 MOV A , M ;Copy Original Data Byte in Reg.A
 C008 ANI F0H ;Logically AND Data Byte with F0H
 C009 F0
 C00A RRC ;Rotate contents of Reg.A towards Right
 C00B RRC ;Rotate contents of Reg.A towards Right
 C00C RRC ;Rotate contents of Reg.A towards Right
 C00D RRC ;Rotate contents of Reg.A towards Right
 C00E MOV C , A ;Copy Upper Nibble into Reg.C
 C00F INX H ;Point towards next memory location
 C010 MOV M , B ;Store Lower Nibble into memory location D001H
 C011 INX H ;Point towards next memory location
 C012 MOV M , C ;Copy Upper Nibble into memory location D002H
 C013 SUB A ;Set Initial Product = 00H
 C014 LOOP: ADD B ;Product = Product + Lower Nibble
 C015 DCR C ;Decrement Upper Nibble By 1
 C016 JNZ LOOP ;If Z = 0 , GO TO Label LOOP
 C017 14
 C018 C0
 C019 INX H ;Point towards memry location D003H
 C01A MOV M , A ;Store Product at memory location D003H
 C01B CF RST 1 ;Stop Program Execution








 14. RDKBD routine Program








C000 LXI B , C030H ;Initialize memory pointer at C030H
 C001 30
 C002 C0
 C003 CALL 02E7H ;Call Keyboard subroutine to accept data from keyboard
 C004 E7
 C005 02
 C006 MOV D , A ;Copy user enterd data from accumulator to Reg.D 
 C007 STAX B ;Store user entered number to memory pointed by BC 
Reg.Pair 
 C008 INX B ;Point towards next memory location
 C009 CALL 02E7H ;Call Keyboard subroutine to accept data from keyboard
 C00A E7
 C00B 02
 C00C STAX B ;Store User entered number to memory pointed by BC 
Pair
 C00D RLC ;Rotate contents of Reg.A towards Left
 C00E RLC ;Rotate contents of Reg.A towards Left
 C00F RLC ;Rotate contents of Reg.A towards Left
 C010 RLC ;Rotate contents of Reg.A towards Left
 C011 ADD D ;Add contents of Reg.D into Reg.A
 C012 INX B ;Point towards next memory location
 C013 STAX B ;Store addition result in memory pointed by BC Pair.
 C014 CF RST 1 ;Stop program Execution








 15. simple calculator





C000 UP : CALL 02E7 ;Call keyboard monitor routine called RDKBD
 C001 E7
 C002 02
 C003 MOV D , A ;Store contents of Reg.A to Reg.D
 C004 CALL 02E7 ;Call keyboard monitor routine called RDKBD
 C005 E7
 C006 02
 C007 ADD D ;Add contents of Reg.D to Reg.A
 C008 DAA ;Decimally Adjust the accumulator
 C009 CALL 036E ;Call monitor routine which displays contents of Reg.A
 C00A 6E
 C00B 03
 C00C JMP UP ;GO TO Label UP
 C00D 00
 C00E C0
