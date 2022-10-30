INTEGROVANÉ VÝVOJOVÉ PROSTŘEDÍ PRO PL/SQL
Aplikace pro vývoj jednoduchých konzolových programů
v ořezané verzi jazyka PL/SQL. Aplikace umožňuje vytvářet
a načíst uložené projekty, rozdělit kód na hlavní blok
a funkce, které mohou být uloženy odděleně do jednotlivých
souborů. Uživatel má možnost přepínat mezi souboy projektu
a odstraňovat či přejmenovat jednotlivé soubory pomocí
vestavěného průzkumníka souborů. Při nastání chyby v programu
je uživatel upozorněn na chybu a při syntaktické chybě i na 
pozici tokenu, na které se chyba vyskytla.

TECHNOLOGIE
Aplikace je napsaná v jazyce C-Sharp .NET Core 3.1

GRAMATIKA JAZYKA
program = {function} {input} block {function} ;
input = "ACCEPT" identifier ( "CHAR" | "NUMBER" ) "PROMPT" varchar2 ";" ;
statement = [ ( define | if | while | for | functionCall | begin | block | return ) ";" ] ;
begin = "BEGIN" { statement } "END" ;
block = [ "DECLARE" { declare } ] begin ";" ;
return = "RETURN" [ expression ] ;
define = identifier ":=" ( expression ) ;
if = "IF" condition "THEN" { statement } { "ELSIF" condition "THEN" { statement } } [ "ELSE" { statement } ] "END IF" ;
while = "WHILE" condition "LOOP" { statement } "END LOOP" ;
for = "FOR" identifier "IN" number ".." number "LOOP" { statement } "END LOOP" ;
declare = (identifier "NUMBER" [ ":=" expression ] ";") | (identifier "VARCHAR2" "(" number ")" [ ":=" varchar2 ] ";") ;
condition = [ "NOT" ] expression ( "=" | "<>" | "!=" | "<=" | ">=" | "<" | ">" ) expression ;
functionCall = identifier "(" [ ( expression ) { "," ( expression ) } ] ")" ;
expression = [ "+" | "-" ] term {( "+" | "-" | "||" ) term} ;
term = factor {( "*" | "/" ) factor} ;
factor = functionCall | identifier | number | varchar2 | "(" expression ")" ;
identifier = /([&a-zA-Z]{1})[a-zA-Z0-9_]*/ ; 
digit = /[0-9]{1}/ ;
number = digit { digit } [ "." { digit } ] ;
varchar2 = /[']{1}[^']*[']{1}/ ;
function = "CREATE" [ "OR" "REPLACE" ] "FUNCTION" identifier [ "(" identifier ( "NUMBER" | "VARCHAR2" ) { "," identifier ( "NUMBER" | "VARCHAR2" ) } ")" ] "RETURN" ( "NUMBER" | "VARCHAR2" ) "IS" { declare } begin ";" ;


PŘÍKLAD

DECLARE
   a NUMBER := 10.15;
   b NUMBER := 0.05;
   c VARCHAR2(10) := 'print';
   d NUMBER := 1;
   e NUMBER := 2;

BEGIN
   IF NOT d > e THEN
      put_line(d);
   END IF;

   WHILE a < 15.3 
   LOOP
      a := a + b;
      put_line(concat(concat(c, ' '), 'string'));
   END LOOP;
END;

