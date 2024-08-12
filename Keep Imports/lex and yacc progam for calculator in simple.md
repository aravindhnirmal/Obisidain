[[Keep/Colour/DEFAULT]] 

%{
[[include]] <stdio.h>
[[include]] "y.tab.h"
%}

%%

[0-9]+ { yylval = atoi(yytext); return NUMBER; }
[-+*/\n] { return yytext[0]; }
[ \t] ; /* skip whitespace */
. { printf("Unknown character: %s\n", yytext); }

%%

int yywrap(void) {
  return 1;
}



%{
[[include]] <stdio.h>
[[include]] <stdlib.h>
%}

%token NUMBER
%left '+' '-'
%left '*' '/'

%%

calc: expr '\n' { printf("Result: %d\n", $1); }
    ;

expr: expr '+' expr { $$ = $1 + $3; }
    | expr '-' expr { $$ = $1 - $3; }
    | expr '*' expr { $$ = $1 * $3; }
    | expr '/' expr { $$ = $1 / $3; }
    | '(' expr ')'  { $$ = $2; }
    | NUMBER        { $$ = $1; }
    ;

%%

int main(void) {
  yyparse();
  return 0;
}

void yyerror(char *msg) {
  fprintf(stderr, "%s\n", msg);
  exit(1);
}

