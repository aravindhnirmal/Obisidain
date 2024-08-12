[[Keep/Colour/DEFAULT]] 

%{
[[include]] "y.tab.h"
%}

%%

"do"        { return DO; }
"while"     { return WHILE; }
"("         { return LPAREN; }
")"         { return RPAREN; }
";"         { return SEMICOLON; }

[ \t\n]     { /* ignore whitespace */ }

.           { printf("Invalid character: %s\n", yytext); }

%%

int yywrap() {
    return 1;
}




%{
[[include]] <stdio.h>
%}

%token DO WHILE LPAREN RPAREN SEMICOLON

%%

program: statement
       | program statement
       ;

statement: do_while_statement SEMICOLON { printf("Valid do-while statement\n"); }
         ;

do_while_statement: DO statement WHILE LPAREN expression RPAREN
                  ;

expression: /* empty */
          ;

%%

int main() {
    yyparse();
    return 0;
}

int yyerror(const char* message) {
    fprintf(stderr, "%s\n", message);
    return 0;
}

%%








