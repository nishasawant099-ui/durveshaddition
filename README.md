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



 
