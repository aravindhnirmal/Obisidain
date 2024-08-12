[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

%{
[[include]] "y.tab.h"
%}

%%

"+"         { return ADD; }
"-"         { return SUB; }
"*"         { return MUL; }
"/"         { return DIV; }
"("         { return LPAREN; }
")"         { return RPAREN; }
[0-9]+      { yylval = atoi(yytext); return NUMBER; }

[ \t\n]     { /* ignore whitespace */ }

.           { printf("Invalid character: %s\n", yytext); }

%%

int yywrap() {
    return 1;
}





%{
[[include]] <stdio.h>
%}

%token ADD SUB MUL DIV LPAREN RPAREN NUMBER

%%

program: expression { printf("Result: %d\n", $1); }
       ;

expression: NUMBER { $$ = $1; }
          | expression ADD expression { $$ = $1 + $3; }
          | expression SUB expression { $$ = $1 - $3; }
          | expression MUL expression { $$ = $1 * $3; }
          | expression DIV expression { $$ = $1 / $3; }
          | LPAREN expression RPAREN { $$ = $2; }
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

