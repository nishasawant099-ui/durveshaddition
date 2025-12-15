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
