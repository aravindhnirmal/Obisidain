[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

%{
[[include]] "y.tab.h"
%}

%%
[0-9]+ { yylval = atoi(yytext); return INTEGER; }
[ \t\n] ; /* ignore whitespace */
[+-*/()] { return yytext[0]; }
. { fprintf(stderr, "error: unexpected character '%c'\n", yytext[0]); }
%%

int yywrap() {
    return 1;
}


%{
[[include]] <stdio.h>
[[include]] <stdlib.h>
%}

%token INTEGER

%{
int last_value = 0; /* last computed value */
int last_expr = 0; /* rule number of last expression */
%}

%%

program:
    expr { printf("%d\n", $1); }
;

expr:
    INTEGER { last_value = $1; }
    | '(' expr '+' expr ')' { $$ = $2 + $4; }
    | '(' expr '-' expr ')' { $$ = $2 - $4; }
    | '(' expr '*' expr ')' { $$ = $2 * $4; }
    | '(' expr '/' expr ')' { $$ = $2 / $4; }
    | expr '+' expr { $$ = last_value + $2; last_expr = 1; }
    | expr '-' expr { $$ = last_value - $2; last_expr = 2; }
    | expr '*' expr { $$ = last_value * $2; last_expr = 3; }
    | expr '/' expr { $$ = last_value / $2; last_expr = 4; }
;

%%

int main() {
    yyparse();
    return 0;
}

void yyerror(const char *s) {
    fprintf(stderr, "error: %s\n", s);
}

