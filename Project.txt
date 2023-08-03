; Name : Yasir Hussain
; ID : 19K-0223
; Section : A

; Project : Parking Management System 

INCLUDE Irvine32.inc

.data

;---------------- For Filling -----------------------

BUFFER_SIZE = 250
buffer BYTE BUFFER_SIZE DUP(?) 
filename BYTE "myFile.txt",0
fileHandle HANDLE ?

;---------------- For Color -----------------------

fore DWORD 11   ; 11 = LightCyan (Foreground)
back DWORD 0  ;  0 = Black (Background)

;---------------- Printing Statements -----------------------

menu BYTE "***************** MENU *********************",0ah,0ah

menu0 BYTE ' Press ( 0 / Enter ) to Clear Screen ',0ah,0ah
menu1 BYTE ' Press 1 for Rikshw ',0ah
menu2 BYTE ' Press 2 for Cars ',0ah
menu3 BYTE ' Press 3 for Bus ',0ah
menu4 BYTE ' Press 4 to Show the Record ',0ah
menu5 BYTE ' Press 5 to Clear the Records ',0ah
m3 BYTE " Press 6 to Remove Vehicle ",0ah
menu6 BYTE ' Press 7 to Exit ',0


my0 BYTE " (1) Remove a Rikshaw",0ah
my1 BYTE " (2) Remove a Car ",0ah
my2 BYTE " (3) Remove a Bus ",0ah
ml BYTE " (4) Return to Menu ",0

str1 BYTE " ERROR in File ",0
str2 BYTE "	 --- Enter User Data --- ",0ah,0ah
str3 BYTE " --> Your Name : ",0
str4 BYTE " Welcome ,  ",0

msg0 BYTE ' --> Parking Is Full',0
msg1 BYTE ' --> Wrong input',0

m1 BYTE "*** Clear Screen ***",0
m2 BYTE "Press OK to Clear Screen ",0
my3 BYTE "--> Vehicle Removed Successfully ",0
my4 BYTE "--> Vehicle isn't Parked ",0

msg2 BYTE ' Rikshaw	',0
msg3 BYTE ' Car	',0
msg4 BYTE ' Bus	',0
msg5 BYTE '	--- Record --- ',0

p1 BYTE 'Parking Fee : ',0
p2 BYTE 'Vehicle : ',0
p3 BYTE 'COUNT : ',0
p4 BYTE ' ---> Total Capacity : 10 Vehicles ',0ah,0

msg6 BYTE ' The Total Amount is : ',0
msg7 BYTE ' The Total Numbers of Vehicles Parked : ',0
msg8 BYTE ' The Total Number of Rikshws Parked : ',0
msg9 BYTE ' The Total Number of Cars Parked : ',0
msg10 BYTE ' The Total Number of Buses Parked : ',0

Choose BYTE "Enter Choice : ",0
msg12 BYTE ' *** Records Deleted Successfully *** ',0
final BYTE " --> Thanks For Using My Application ",0

;---------------- Variables -----------------------

amount WORD 0
count WORD 0
strL DWORD ?
TOTAL DWORD ?

am1 WORD ?
am2 WORD ?
am3 WORD ?

x WORD 0 ; rikshaw
y WORD 0 ; car
z WORD 0 ; bus

;-------------------- MAIN Function ------------------------

.code

main PROC
	
	call setcolor
	call filling
	call ShowMenu

	call crlf
	mov  edx,OFFSET final
	call WriteString


call crlf
exit
main ENDP

;------------------------------------------------------------

filling proc

; CREATE FILE

mov edx,OFFSET filename
call CreateOutputFile
mov fileHandle,eax

; Check Error

cmp eax, INVALID_HANDLE_VALUE
jne file_ok
mov edx,OFFSET str1
call WriteString
jmp quit

file_ok:

mov edx,offset str2
call WriteString
mov edx,0
clc
mov edx,OFFSET buffer
mov ecx,BUFFER_SIZE
call ReadString
mov strL,eax

; WRITE FILE

mov eax,fileHandle
mov edx,OFFSET buffer
mov ecx,strL
call WriteToFile

; CLOSE FILE

call CloseFile	

; Print Text on Console

call crlf
mov edx,OFFSET str4
call WriteString
mov edx,OFFSET buffer
call WriteString
call crlf
call crlf
call WaitMsg
call clrscr

quit:
ret 8
filling endp

;------------------------------------------------------------

setcolor proc

mov eax,0
mov ebx,0
clc
mov edx,0

mov eax,back
mov ebx,16

mul ebx

mov ebx,fore
add eax,ebx

call SetTextColor

ret 
setcolor endp

;------------------------------------------------------------

ShowMenu PROC
	
	call crlf
	mov edx,offset p4
	call writestring
	
	call crlf
	mov  edx,OFFSET menu ; Display Menu
	call WriteString
	
	call crlf
	call crlf
	mov edx,offset Choose
	call writestring	; CHOICE :
	call ReadInt

	call select
	ret 8

ShowMenu endp

;-----------------------------------------------------------------------

select proc

	cmp eax,0
	je clear
	jmp start

clear:
	mov ebx,offset m1
	mov edx,offset m2
	
	call MsgBox
	call crlf
	call clrscr
	call ShowMenu

start:
	cmp  eax,1
	jne  L1
	
	call crlf
	call rikshw
L1:
	cmp  eax,2	
	jne  L2
	
	call crlf
	call car
L2:
	cmp  eax,3	
	jne   L3
	
	call crlf
	call bus	

L3:
	cmp  eax,4	
	jne   L4
	
	call crlf
	call rec

L4:
	cmp  eax,5	
	jne   L5
	
	call crlf
	call del

L5:	
	cmp eax,6
	jne L6

	call crlf
	call rem
	
L6:
	cmp eax,7
	jne quit

	call crlf
	jmp end_

quit:
	call crlf
	mov edx,offset msg1
	call writestring
	call crlf
	call crlf
	call WaitMsg
	call clrscr
	call ShowMenu
	
call ShowMenu

end_:
ret
select endp

;-----------------------------------------------------------------------

rikshw PROC		

	mov edx,offset p2
	call writeString
	mov edx,OFFSET msg2
	call WriteString

	cmp count,9
	ja L1

	mov ax,200

	call crlf
	mov edx,offset p1
	call writeString
	call writeDec

	add amount,ax
	mov dx,0
	mov bx,10
	mov cx,0

L2:
	div bx
	inc cx
	cmp ax,0
	jne l2

inc count
inc x

call crlf
mov edx,offset p3
call writeString
mov ax,count
call writeDec

call crlf
mov ax,amount
mov am1,ax

call crlf
call waitmsg
call crlf
call clrscr
call ShowMenu
	
jmp end_

L1:

call crlf
call crlf
mov edx,offset msg0
call writeString
call crlf
call crlf
call WaitMsg
call clrscr
call ShowMenu

end_:
ret 8
rikshw endp

;-----------------------------------------------------------------------

car proc

	mov edx,offset p2
	call writeString
	mov edx,OFFSET msg3
	call WriteString

	cmp count,9
	ja L1

	mov ax,400

	call crlf
	mov edx,offset p1
	call writeString
	call writeDec

	add amount,ax
	mov dx,0
	mov bx,10
	mov cx,0

L2:
	div bx
	inc cx
	cmp ax,0
	jne l2

inc count
inc y

call crlf
mov edx,offset p3
call writeString
mov ax,count
call writeDec

call crlf
mov ax,amount
mov am2,ax

call crlf
call waitmsg
call crlf
call clrscr
call ShowMenu

jmp end_

L1:

call crlf
call crlf
mov edx,offset msg0
call writeString
call crlf
call crlf
call WaitMsg
call clrscr
call ShowMenu

end_:
ret 8

car endp

;-----------------------------------------------------------------------

bus proc

	mov edx,offset p2
	call writeString
	mov edx,OFFSET msg4
	call WriteString

	cmp count,9
	ja L1

	mov ax,600

	call crlf
	mov edx,offset p1
	call writeString
	call writeDec

	add amount,ax
	mov dx,0
	mov bx,10
	mov cx,0

L2:
	div bx
	inc cx
	cmp ax,0
	jne l2

inc count
inc z

call crlf
mov edx,offset p3
call writeString
mov ax,count
call writeDec

call crlf
mov ax,amount
mov am3,ax

call crlf
call waitmsg
call crlf
call clrscr
call ShowMenu

jmp end_

L1:

call crlf
call crlf
mov edx,offset msg0
call writeString
call crlf
call crlf
call WaitMsg
call clrscr
call ShowMenu

end_:
ret 8

bus endp

;-----------------------------------------------------------------------

rec proc
	
	mov edx,OFFSET msg5
	call WriteString

	call crlf
	call crlf

	mov edx,offset msg6
	call writeString
	mov ax,amount
	call writeDec

	call crlf
	mov edx,offset msg7
	call writeString
	mov ax,x
	mov bx,y
	add ax,bx
	mov bx,z
	add ax,bx
	mov TOTAL,eax
	call writeDec

	call crlf
	mov edx,offset msg8
	call writeString
	mov ax,x
	call writeDec

	call crlf
	mov edx,offset msg9
	call writeString
	mov ax,y
	call writeDec

	call crlf
	mov edx,offset msg10
	call writeString
	mov ax,z
	call writeDec

	call crlf
	call crlf
	call WaitMsg
	call clrscr
	call ShowMenu

ret 8
rec endp

;-----------------------------------------------------------------------

del proc

	mov eax,0
	mov ebx,0
	clc
	mov edx,0

	mov count,0
	mov amount,0

	mov am1,0
	mov am2,0
	mov am3,0

	mov x,0
	mov y,0
	mov z,0

	call crlf

	mov edx,offset msg12
	call writeString
	call crlf
	call crlf
	call waitmsg
	call clrscr
	call crlf
	call ShowMenu
	ret 8
del endp

;-----------------------------------------------------------------------

rem PROC

call clrscr
call crlf

mov edx,offset my0
call WriteString
mov edx,offset Choose
call crlf
call crlf
call WriteString
call readint

cmp eax,1
jne L1

cmp x,0
je err

dec count
dec TOTAL
dec x
jmp quit

L1:

cmp eax,2
jne L2

cmp y,0
je err

dec count
dec TOTAL
dec y
jmp quit

L2:

cmp eax,3
jne L3

cmp z,0
je err

dec count
dec TOTAL
dec z
jmp quit

L3:

cmp eax,4
je last
jmp uff

uff:

call crlf
mov edx,offset msg1
call writeString
jmp now

err:

call crlf
mov edx,offset my4 ; Vehicle isn't Parked
call writeString
call crlf
call crlf
call waitmsg
call rem

quit:

call crlf
call crlf
mov edx,offset my3 ; REMOVED Vehicle
call WriteString

now:

call crlf
call crlf
call waitmsg
call rem

last:

call crlf
call crlf
call waitmsg
call crlf
call crlf
call clrscr
call ShowMenu
ret
rem ENDP

;-----------------------------------------------------------------------
END main