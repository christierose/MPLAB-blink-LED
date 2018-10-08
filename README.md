;Blink LED with Loop Timer Delay
;Christie Carranza
; PIC16F1829 Configuration Bit Settings

; Assembly source line config statements

#include "p16f1829.inc"

; CONFIG1
; __config 0x9E4
 __CONFIG _CONFIG1, _FOSC_INTOSC & _WDTE_OFF & _PWRTE_OFF & _MCLRE_ON & _CP_OFF & _CPD_OFF & _BOREN_OFF & _CLKOUTEN_OFF & _IESO_OFF & _FCMEN_OFF
; CONFIG2
; __config 0x1EFF
 __CONFIG _CONFIG2, _WRT_OFF & _PLLEN_OFF & _STVREN_ON & _BORV_LO & _LVP_OFF

    list p=16F1829, R=DEC
    CBLOCK 0x30
    
    DLAY
    LOOPcount
    VarA
    VarB
   
    
    
    
	;declare extra variables here
	ENDC
	
	
	
	;start setup
	ORG 0
	goto Start
	
	ORG 4
	RETFIE
Start
	
	;Clock setup
	BANKSEL OSCCON
	movlw 0x6A
	movwf OSCCON
	;port setup
	BANKSEL TRISA
	Clrf TRISA
	
	BANKSEL LATA
	Clrf LATA
	
	;Challenge loop
	Loop
	
	BANKSEL LATA
	BSF LATA,5
	CALL DELAY
	BANKSEL LATA
	BCF LATA,5
	CALL DELAY	
	
	goto Loop
	
	;delay
    DELAY
    BANKSEL VarA
    movlw 0xFF
    movwf VarA
    Outside
    decfsz VarA
    goto Goon
    return 
    Goon
    movlw 0xFF
    movwf VarB    
    Inside
    decfsz VarB
    goto Inside
    goto Outside
    End

