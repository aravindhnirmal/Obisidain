[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

%{
[[include]] <stdio.h>
[[include]] "y.tab.h"
%}

%%
[0-9]+          { yylval = atoi(yytext); return NUM; }
[ \t\n]         /* Ignore whitespace */
.               return yytext[0];
%%

int yywrap(void) {
    return 1;
}



%{
[[include]] <stdio.h>
[[include]] <stdlib.h>
%}

%token NUM

%%

stmt: expr '\n'         { printf("= %d\n", $1); }
    ;

expr: NUM               { $$ = $1; }
    | expr '+' expr     { $$ = $1 + $3; }
    | expr '-' expr     { $$ = $1 - $3; }
    | expr '*' expr     { $$ = $1 * $3; }
    | expr '/' expr     { $$ = $1 / $3; }
    | '(' expr ')'      { $$ = $2; }
    ;

%%

int main(void) {
    yyparse();
    return 0;
}

void yyerror(const char *msg) {
    fprintf(stderr, "Error: %s\n", msg);
}

