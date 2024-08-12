[[Keep/Colour/DEFAULT]] 

%{
[[include]] <stdio.h>
[[include]] "y.tab.h"
%}

%%

[0-9]+ { yylval = atoi(yytext); return NUMBER; }
[-+=;(){}\n] { return yytext[0]; }
[ \t] ; /* skip whitespace */
. { printf("Unknown character: %s\n", yytext); }

%%

int yywrap(void) {
  return 1;
}






%{
[[include]] <stdio.h>
%}

%token WHILE DO DONE NUMBER

%%

statement:
    WHILE expr DO statement DONE { while ($2) $4; }
  | expr
  ;

expr:
    NUMBER
  | '(' expr ')'
  | expr '+' expr
  | expr '-' expr
  | expr '*' expr
  | expr '/' expr
  ;

%%

int main(void) {
    yyparse();
    return 0;
}

void yyerror(const char *msg) {
    fprintf(stderr, "Error: %s\n", msg);
}

