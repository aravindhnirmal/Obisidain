[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

%{
[[include]] "y.tab.h"
%}

%%
[0-9]+      { yylval = atoi(yytext); return NUMBER; }
[+\-*/\(\)] { return yytext[0]; }
[ \t\n]     { /* ignore whitespace */ }
.           { printf("Invalid character %c\n", yytext[0]); }
%%

int yywrap() {
    return 1;
}



%{
[[include]] <stdio.h>
%}

%token NUMBER
%left '+' '-'
%left '*' '/'
%left UMINUS

%%

program:   /* empty */
         | program statement '\n'
         ;

statement: expression      { printf("%d\n", $1); }
         | error '\n'      { yyerrok; }
         ;

expression: NUMBER          { $$ = $1; }
          | expression '+' expression  { $$ = $1 + $3; }
          | expression '-' expression  { $$ = $1 - $3; }
          | expression '*' expression  { $$ = $1 * $3; }
          | expression '/' expression  { $$ = $1 / $3; }
          | '(' expression ')'        { $$ = $2; }
          | '-' expression %prec UMINUS { $$ = -$2; }
          ;

%%

int main() {
    yyparse();
    return 0;
}

int yyerror(const char* msg) {
    fprintf(stderr, "Error: %s\n", msg);
    return 0;
}

