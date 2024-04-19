# Quick Common Lisp - Cheatsheet
"$>" o "==>" significará "resultado de la evaluación en el interprete.

# TEMA 1: operaciones
## Operaciones Aritmeticas
- `(+ 1 2) ; suma `
- `(- 2 3) ; resta `
- `(* 4 4) ; producto `
- `(/ 4 4) ; division `

## Funciones Matemáticas.
- `(truncate 5.15) ;` $> 5 ; 0.1500001 
- `(round 5.95) ;` $> 5
- `(float 8) ; ` $> 8.0
- `(rational 2.5) `; $> 5/2
- `(rem 7 2) (mod 7 2); $> 1 `; remanente de la división
- `(abs -8) `; $> 8 `; valor absoluto
- `(signum -8) `; $> -1 `; es equivalente a: (/ NUMBER (ABS NUMBER)).
- `(SQRT 16) ; $> 4.0` ; raiz cuadrada
- `(EXPT 2 3) `; ==> 8 ; exponencial
- `(INCF C 10) `; => 10; incrementa variable C en 10
- `(DECF C 10) `; ==> -5; Decrementa variable C en 10
- `(DECF (SETF C 5) 10) `; ==> -5

## COMPARACIONES DE NUMEROS
- `(= 3 3.0) `; ==> T
- `(< 3 5 8) `; ==> T
- `(< 3 5 4) `; ==> NIL
- `(> 8 5 3) `; ==> T 
- `(< 8 3 5) `; ==> NIL
- `(>= 9 7 7) `; ==> T
- `(>= 8 9 8) `; ==> NIL


## PREDICADOS NUMERICOS
- `(NUMBERP 7) `; ==> T ; es numero
- `(NUMBERP 'NOMBRE) `; ==> NIL
- `(ODDP -7) `; ==> T ; es par
- `(ODDP 4) `; ==> NIL
- `(ODDP 5.8) `; ==> Error: 5.8 is not an integer
- `(INTEGERP 7) `; ==> T
- `(INTEGERP ‘NOMBRE) `; ==> NIL
- `(ZEROP 0.0) `; ==> T
- `(ZEROP 'NOMBRE) `; ==> ERROR


## Funciones utiles sobre listas
- `(MAX 2 5 3 1) `; ==> 5
- `(MIN 2 5 3 1) `; ==> 1
- `(GCD 12 34 56) `; ==> 2 ; Máximo Común Divisor

# EJEMPLOS
## ATOMOS
- `(+ 1 -2 3.5) `; ==> 2.5
- `(- 1 '-2 3.5) `; ==> -0.5
- `(* 1 '-2 3.5) `; ==> -7.0
- `(/ 1 -2 3.5) `; ==> -0.14285714285714285

## Listas de IGUAL LONGITUD en el 1er. nivel
- `((+ '(1 -2 3.5) '(4 5 6)) `; ==>  (5 3 9.5)
- `((+ '(1 -2 3.5) '(4 5 6) '((2 4) (3) (((5)2)))) `; ==> ((7 9) (6) (((14.5) 11.5)))
- `((- '(1 -2 3.5) '(4 5 6)) `; ==> (-3 -7 -2.5)
- `((- '(1 2 3.5) '(4 5 6) '((2 4) (3) (((5)2)))) `; ==> ((-5 -7) (-10) (((-7.5) -4.5)))
- `((* '(1 -2 3.5) '(4 5 6)) `; ==> (4 -10 21.0)
- `((* '(1 2 3.5) '(4 5 6) '((2 4) (3) (((5)2)))) `; ==> ((8 16) (30) (((105.0) 42.0)))

## Listas de DISTITNA longitud  en el 1er. nivel
- `((/ '(1 -2 3.5) '(4 5 6)) `; ==> (0.25 -0.4 0.583)
- `((+ '(1 2 3) '(4 5) )) `; ==> Error: arguments not all the same length


## Átomos y Listas
- `((+ 1 '(2 -3 4) 5) `; ==> (8 3 10)
- `((+ 1 '(2 -3 4) 5 '(4 7) ) `; ==> Error: arguments not all the same length
- `((+ 1 '(2 -3 4) 5 '(4 (7) ((2)))) `; ==> (12 (10) ((12)))
- `((- 1 '(2 -3 4) 5) `; ==> (-6 -1 -8)
- `((- 1 '(2 -3 4) 5 '(4 (7) ((2)))) `; ==> (-10 (-8) ((-10)))
- `((* 1 '(2 -3 4) 5) `; ==> (10 -15 20)
- `((* 1 '(2 -3 4) 5 '(4 (7) ((2)))) `; ==> (40 (-105) ((40)))
- `((/ 1 '(2 -3 4) 5) `; ==> (0.1 -0.066 0.05)


# TEMA 3: MANEJO DE LISTAS Y ARREGLOS
# FUNCIONES PARA OPERAR SOBRE LISTAS
Existen tres tipos importantes de funciones de selección de elementos:
 - CAR - devuelve el primer elemento de la lista.
 - CDR - devuelve toda la LISTA menos el primer elemento. (pronounced “could-er”)
 - C*R - permite la combinacion de funciones CAR Y CDR. Es decir, CADR, CDDR, CADADR, etc.

### DATO CURIOSO
Los 3 acronimos vienen de la computora IBM 704 donde se desarrollo originalmente Lisp. Dada la importancia historica de esa maquina se conservan tradicionalmente estos nombre.
- car is an acronym from the phrase "Contents of the Address part of Register number", basically meaning following the pointer in that register.
- cdr (pronounced “could-er”) is an acronym from the phrase "Contents of the Decrement part of Register number",
- cpr is an acronym from the phrase "Contents of the Prefix part of Register number",

## CAR
Primer Elemento de una Función.
- `(CAR '(A B C) ) `; ==>  A
- `(CAR '((A B) C) ) `; ==> (A B)

## CDR
Devuelve el RESTO la LISTA sin el primer elemento.
- `(CDR '(A B C) ) `; ==> (B C)
- `(CDR '((A B) C) ) `; ==> (C)
- `(CDR '(A . B) ) `; ==> B

## C****R
es la abreviación de la combinacion de las formas CAR y CDR. Siempre empiezan con C y terminan con una R. CLisp solo soporta hasta 5 combinanciones: CDDDDR o CAAAAR. 
- `(CADR '(A B C) ) `; ===> B
- `(CAR (CDR '(A B C) ) ) `; ===> B
- `(CDAR '((A B C) D E) ) `; ===> (B C)
- `(CDR (CAR '((A B C) D E ) )) `; ===> (B C)
- `(CADDR '(A B C D E) ) `; ===> C
- `(CAR (CDDDDR '(A B C D E) ) ) `; ===> E

## LAST
Devolverá una LISTA de la última estructura CONS de la lista
- `(LAST '(A B C)) `; ==> (C)
- `(LAST '(A (B C))) `; ==> ((B C))
- `(LAST '(1 2 3.5)) `; ==> (3.5)
- `(LAST '((A B C)) `; ==> ((A B C))

## ELT (/element/)
Devolverá el ELEMENTO de una SECUENCIA que este en la posición del índice, empezando en la posición 0. Funciona con varios tipos de secuencias como listas, vectores, cadenas.
- `(ELT "hola" 0) `; => #\h
- `(ELT '(A (B C)) 1) `; ==> (B C)
- `(ELT '(A B) 3) `;  ==> ERROR index 3 too large
- `(ELT '(A B C D E) 2) `; ==> C ; base 0, por eso devuelve C


# FUNCION DE ASIGNACION 

# SETQ
;; La función SETQ asigna un valor a una variable. 
;; Su sintaxis es: (SETQ {VAR FORM}+).
;; La Q de SETQ es un mnemotécnico de la función Quote. Las llaves y el signo mas, representan repetición del par VAR FORM.
;; (SETQ VAR FORM VAR FORM VAR FORM ...)
;; DEBE haber un número par de argumentos. Los argumentos impares de la función no son evaluados.
(setq x 4 y 6 z 9) ; ==> 9

; Esto asigna 4 a x, 6 a y, 9 a z. Siempre las evaluaciones de expresiones, devuelven el resultado de la ultima evaluación. En este caso, la ultima evaluación fue z 9.

; * Las evaluaciones de las formas y las asignaciones (primero se evalúa y luego se asigna), se realizan secuencialmente.
(SETQ X 5) ; ==> 5
(SETQ NOMBRE "MARIA") ; ==> "MARIA"
(SETQ FRUTA (CAR '(MANZANA PERA ))) ; ==> MANZANA
(SETQ LISTA1 '(A B C)) ; ==> (A B C)
(SETQ X 5 Y 6 Z 7 ; ==> 7
(SETQ X 5 Y 6 Z) ; ==>  Error: too few arguments


;; #########################################
# FUNCIONES DE CONSTRUCCION DE LISTAS
;; Las funciones con las que Lisp permite construir listas son
;; * CONS
;; * LIST
;; * APPEND.

# CONS - construct
;; La función CONS, crea una nueva estructura cons. Sintácticamente podemos expresarlos como:
;; (CONS SEXP SEXP)
;; donde SEXP son expresiones simbólicas, pueden ser átomos o listas.
;; El CAR de la nueva lista será la primera SEXP y el CDR la segunda.
(CONS 'A '(B C D) ) ; ==> (A B C D)
(CONS '(X Y) '(B C D) ) ; ==> ((X Y) B C D)
(CONS '((X Y) (W Z)) '((A B)) ) ; ==> ( ((X Y) (W Z)) (A B))
(CONS 'A NIL ) ; ==> (A)
(CONS NIL '(A) ) ; ==> (NIL A)

; * Obsérvese que si la segunda SEXP corresponde con un átomo entonces se creará una lista punteada ("impropia").
(CONS 'A 'B ) ; ==> (A . B)
(CONS '(A B) 'C ) ; ==> ((A B) . C)
  
# LIST
;; LIST &REST ARGS
; La función LIST devuelve una lista formada con todos los elementos pasados como argumentos. Los argumentos deberán ser expresiones simbólicas válidas.
; La notación &REST ARG implica que se permite cualquier número de argumentos. Es decir, se le puede pasar a la llamada de la función cualquier número de parámetros.
; sintaxis:  (LIST SEXP SEXP ...)
; * LIST se utiliza para crear listas propias. Las listas impropias sólo pueden crearse a partir de la función CONS.
(LIST 'A 'B 'C) ; ==> (A B C)
(LIST '(A) '(B) '(C)) ; ==> ((A) (B) (C))
(LIST 'A '(B C)) ; ==> (A (B C))


# APPEND.
;;  APPEND &REST ARGS
; Permite crear una nueva lista concatenando dos o más listas dadas. Mientras que LIST y CONS aceptan listas y átomos como argumentos, APPEND sólo acepta listas, excepto en el último argumento. También acepta un número indefinido de argumentos.
; La función APPEND concatena los argumentos en una lista. Todos los argumentos, excepto el último deben ser listas. Los argumentos que no sean listas no serán incluidos.
; sintaxis: (APPEND LISTA LISTA ... LISTA SEXP)
(APPEND '(A) '(B) '(C)) ; ==> (A B C)
(APPEND '(A) '(B C)) ; ==> (A B C)
(APPEND '((A)) '((B)) '((C)) ) ; ==> ((A) (B) (C))
(APPEND '(A) NIL) ; ==> (A)
(APPEND NIL '(B C)) ; ==> (B C) ; NIL es una lista y por tanto cumple los requerimientos de la definición de APPEND.
(APPEND 'A '(B C)) ; ==> ERROR
(APPEND '(A) '(B) 'C) ; ==> (A B . C)
    
; #######################
# Otras funciones de listas

# BUTLAST - SIN LOS ÚLTIMOS
; (BUTLAST lista n)
; devuelve una nueva lista con los N-últimos elementos de la lista pasada como parámetro eliminados. No se modifica el contenido de la lista original
(setq b '(3 4 5 6))
(butlast b 2) ; ==> (3 4) 
b ; ==> (3 4 5 6)
; * Si quisiéramos que el resultado se asigne a una nueva lista, haríamos LO SIGUIENTE:
(setq lista (butlast b n))

# NTH - DEVOLVER ORDINAL
; (NTH <n> <list>)
; Permite extraer el elemento “n” de una lista “list”. El primer elemento es N = 0.
(setq b '(4 5 6))
(nth 1 b) ; ==> 5
(nth 0 b) ; ==> 4

# NTHCDR - devolver los ultimos N.
; (NTHCDR <n> <list>)
; Permite extraer el cdr de una lista “list” a partir del elemento “n”. Llama repetidamente a CDR.
(setq b '(4 5 6 7 8)) 
(nthcdr 3 b) ; ==> (7 8)
(nthcdr 1 b) ;  ==> (5 6 7 8)
      
# REVERSE
; (REVERSE <list>)
; Permite obtener el reverso de una lista. No modifica el contenido de la lista original.
(setq b '(4 5 6 7 8))
(reverse b) ; ==> (8 7 6 5 4)
b ; ==> (4 5 6 7 8)
; * Si quisiéramos guardar la lista resultado debemos hacer:
(setq lista1 (reverse b))


;;; #######################################
# FUNCIONES DESTRUCTIVAS de Manipulacion

# RPLACA - REPLACE CA
; (RPLACA lista elem)
; sustituye el car de la lista con elem.
(setq a '(1 2 3))
(rplaca a 7) ; ==> (7 2 3)
a ; ==> (7 2 3)

# RPLACD - REPLACE CDR
; (RPLACD lista elem)
; sustituye el CDR de la lista con elem.
(setq b '(1 2 3))
(rplacd b '(9)) ; ==> (7 2 3)
b ; ==> (7 2 3)

# NCONC
; (NCONC lista1 ... listaN)
; devuelve su valor modificando el símbolo que expresa lista1, y modifica el valor de las sucesivas listas hasta n-1.
(setq a '(1 2) b '(3 4) c '(5 6) d '(7 8))
(nconc a b c d) ; ==> (1 2 3 4 5 6 7 8)
a ; ==> (1 2 3 4 5 6 7 8)
b ; ==> (3 4 5 6 7 8)
c ; ==> (5 6 7 8)
d ; ==> (7 8)

# PUSH - PILAS: Añadir cabecera
; (PUSH item lista)
; añade el elemento item a lista al principio.
; equivalente: (setq lista (cons item lista))  
(setq b '(4 5 6))
(push 9 b) ; ==> (9 4 5 6)
b ; ==> (9 4 5 6)

# POP - PILAS: Eliminar cabecera
; elimina el primer elemento de lista
; sintaxis: (POP lista)
; equivalente: (setq lista (cdr lista))
(setq b '(9 4 5 6))
(pop b) ; ==> 9
b ; ==> (4 5 6)

      
; ##########################################
# OTRAS FUNCIONES

# LENGTH SECUENCIA
; (LENGTH list)
; Devuelve el número de elementos existentes en el nivel superior de la lista (o secuencia).
(LENGTH '(A B C)) ; ==> 3
(LENGTH '(A B . C)) ; ==> 2 (en este caso devuelve 2, porque el segundo elemento es uno solo llamado “Par punteado”).
(LENGTH '()) ; ==> 0

# MEMBER
; MEMBER ITEM LISTA {&KEY {:TEST / :TEST-NOT / :KEY}}
; La función MEMBER busca en el nivel superior de la LISTA un elemento que sea igual, EQL, que el ITEM. Si se encuentra un elemento que cumple esta condición, la función devolverá una lista cuyo CAR es el elemento buscado y el CDR es el resto de la lista.
; La opción :TEST permite realizar comparaciones sucesivas del ITEM con cada uno de los elementos de la lista a través del operador señalado después de :TEST, hasta encontrar el primer elemento que cumple dicha condición, es decir, que de NO-NIL.
; La opción :TEST-NOT es semejante a la anterior, salvo que se detiene al encontrar el primer elemento en cuya evaluación se obtenga NIL. 
; La opción :KEY hace lo mismo que las anteriores pero aplica la función indicada en clave.
(MEMBER 'C '(A B C D E F)) ; ==> (C D E F)
(MEMBER 'Z '(A B C D E F)) ; ==> NIL
(MEMBER 'J '(A B (I J) F)) ; ==> NIL
(MEMBER '(X Y) '(A B C (X Y) D)) ; ==> NIL

; Su valor es NIL por que compara con EQL
(MEMBER '(X Y) '(A B C (X Y) D) :TEST #'EQUAL) ; ==> ((X Y) D)
(MEMBER '7 '(3 5 7 9) :TEST-NOT #'>) ; ==> (7 9)
      
# FMAKUNBOUND - deligar simbolo
; (FMAKUNBOUND <sym>)
; Permite desligar un símbolo de una función.
(fmakunbound mi-suma) ; desliga la función mi-suma
mi-suma ; ==> Error: The variable MI-SUMA is unbound

# MAKUNBOUND
; (MAKUNBOUND <sym>)
; Permite desligar un símbolo de su valor.
(setq a 4) ; liga el símbolo a con 4
a ; ==> 4
(makunbound 'a) ; desliga el símbolo a
A ; ==> Error: The variable A is unbound.

# BOUNDP <sym>
; (BOUNDP <sym>)
; El predicado boundp chequea si el símbolo sym, tiene un valor ligado a el. Retorna T si tiene un valor ligado, o NIL en caso contrario.
(setq a 1) ; liga la variable a con el valor 1
(boundp 'a) ; ==> T ; retorna T – el valor es 1

# FBOUNDP
; (FBOUNDP <sym>)
; El predicado fboundp chequea si el símbolo sym, tiene una definición de función ligada a el. Retorna T si tiene un valor ligado, o NIL en caso contrario.
(defun f1 (x) (print x)) ; set up function F1
(fboundp 'f1) ; ==> T
(fboundp 'car) ; ==> T
(fboundp 'f2) ; ==> Nil


; #########################################
# PREDICADOS Y OPERADORES LOGICOS P/LISTAS
      
## Predicados sobre TIPOS DE DATOS.
; Todos los predicados que se muestran a continuación devuelven T si son ciertos o NIL sino lo son.
; - (ATOM OBJETO) ==> Devuelve true si el objeto NO es una construcción CONS.
; - (CONSP OBJETO)  ==> Devuelve cierto si el objeto es CONS.
; - (LISTP OBJETO) ==> Devuelve cierto si el objeto es CONS o NIL (la lista vacía).
; - (NULL OBJETO) ==> Será cierto si objeto es NIL.
; - (TYPEP OBJETO TIPO-ESPECIFICADO) ==> Es cierto cuando el objeto pertenece al tipo definido en tipo especificado.

## Predicados de IGUALDAD.
; Los objetos Lisp pueden verificarse a diferentes niveles de igualdad:
; - Igualdad numérica: =
; - Identidad referencial: EQ
; - Identidad representacional: EQL (acepta solo dos argumentos)
; - Igualdad estructural EQUAL (acepta solo dos argumentos)
; - Igualdad de valores: EQUALP.

# EQ
; (EQ X Y)
; La función EQ testea si X e Y están referenciados por punteros iguales. Si son objetos identicos.
; Solo se utiliza para caracteres, símbolos y enteros pequeños menores o iguales a 255.
; sintaxis: (EQL SEXPR SEXPR)
(eq 'a 'a) ; ==> T
(eq 1 1) ; ==> T
(eq 256 256) ; ==> Nil
(eq 1 1.0) ; ==> Nil
(eq "a" "a") ; ==> Nil

# EQL - igual valor
; (EQL X Y)
; La función EQL testea si X e Y representan el mismo valor. Esta función puede devolver false aunque el valor imprimible de los objetos sea igual. Esto sucede cuando los objetos apuntados por variables parecen los mismos pero tienen diferentes posiciones en memoria.
; Este predicado no conviene utilizarlo con strings, ya que su respuesta no será fiable. Por el contrario se deberá utilizar con variables y números cuando sea preciso conocer si tienen la misma posición en memoria.
; sintaxis: (EQL SEXPR SEXPR)
(EQL 5 5) ; ==> T
(EQL 5 5.0) ; ==> NIL 

(SETQ A 'WORD)
(SETQ B 'WORD) 
(EQL A B) ; ==> NIL

(SETQ L '(A B C))
(EQL  '(A B C) L) ; ==> NIL

(SETQ M L)
(EQL L M) ; ==> T

(SETQ N  '(A B C)) 
(EQL L N) ; ==> NIL
(EQUAL L A) ; ==> NIL

# EQUAL
; (EQUAL X Y)
; Verifica si los objetos X e Y, son estructuralmente iguales. Es decir, los valores imprimibles de los objetos son iguales. 
; Sintaxis: (EQUAL SEXPR SEXPR).

(EQUAL 5.0 5) ; ==> nil
(EQUAL NIL ()) ; ==> T
      
(SETQ A 'WORD B 'WORD)
(EQUAL A B) ; ==> T
      
(SETQ L '(A B C))
(EQUAL '(A B C) L) ; ==> T

(SETQ M L)
(EQUAL L M) ; ==> T
    
(SETQ N '(A B C))
(EQUAL L N) ; ==> T
(EQUAL L A) ; ==> nil

# EQUALP
; (EQUALP X Y)
; La función EQUALP testea si X e Y representan el mismo valor, pero a diferencia de EQUAL, esta función se denomina Case Insensitive. A diferencia de Eql, puede aplicarse a los string.
(EQUALP 5 5) ; ==> T
(EQUALP 5 5.0) ; ==> T 
(EQUALP "a" "A") ; ==> T

#### Resumen:
; • Eq – Punteros idénticos. Palabras con caracteres, símbolos y pequeños enteros.
; • Eql – Solo números del mismo tipo.
; • Equal – Listas y Strings.
; • Equalp – Caracteres y strings con identificación de mayúsculas, números de diferentes tipos, arreglos.



; #######################
## OPERADORES LOGICOS
; Lisp tiene tres de los operadores lógicos más comunes como primitivas, AND, OR y NOT.      

; AND
; La función AND evalúa sus argumentos en orden. Si cualquiera de los argumentos se evalúa a NIL, se detiene la evaluación y se devuelve el valor NIL. Por el contrario si todos los argumentos son NO-NIL, devolverá el resultado de la ÚLTIMA EVALUCACION.
; Sintácticamente: (AND SEXPR SEXPR ...)
(AND T (< 2 5) (> 7 4) (* 2 5)) ; ==> 10

(SETQ X 3 CONT 0)
(INCF CONT)
(AND (<= CONT 10) (NUMBERP X) (* 2 X)) ; ==> 6
(AND (EVENP X) (/ X 2)) ; ==> NIL

; OR
; La función OR evalúa sus argumentos en orden. Si cualquiera de los argumentos se evalúa a NO-NIL, se detiene la evaluación y se devuelve T. Por el contrario si todos los argumentos son NIL, la función OR devolverá el resultado de la ultima sexp.
; Sintácticamente (OR SEXPR SEXPR ...)
(OR NIL (= 4 5) (NULL '(A B)) (REM 23 13) ) ; ==> 10

(SETQ X 10)
(OR (< 0 X) (DECF X) ) ; ==> T
(OR (> 0 X) (DECF X) ) ; ==> 9
(OR (CONSP X) (EVENP X) (/ X 2)) ; ==> 5
      
; NOT - NEGACION
; (NOT FORM)
; La función NOT evalúa un único argumento. La función NOT devuelve T o NIL. Si los argumentos se evalúan a NIL, entonces devuelve T, en otro caso NIL.
; Sintácticamente (NOT SEXPR), está permitido sólo un argumento.
(NOT NIL) ; ==> T
(NOT T) ; ==> NIL
(NOT (EQUAL  'A  'A) ) ; ==> NIL
(SETQ X  ́(A B C) )
(NOT (ATOM X)) ; ==> T








