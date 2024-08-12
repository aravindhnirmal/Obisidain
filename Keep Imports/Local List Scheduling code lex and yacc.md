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

%%

program:
    expr { printf("%d\n", $1); }
;

expr:
    INTEGER
    | '(' expr '+' expr ')' { $$ = $2 + $4; }
    | '(' expr '-' expr ')' { $$ = $2 - $4; }
    | '(' expr '*' expr ')' { $$ = $2 * $4; }
    | '(' expr '/' expr ')' { $$ = $2 / $4; }
;

%%

int main() {
    yyparse();
    return 0;
}

void yyerror(const char *s) {
    fprintf(stderr, "error: %s\n", s);
}

