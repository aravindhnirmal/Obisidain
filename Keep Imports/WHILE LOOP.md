[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

%{
[[include]] <stdio.h>
[[include]] <stdlib.h>
[[include]] "y.tab.h"
%}

%%
"while"         { return WHILE; }
"{"             { return LBRACE; }
"}"             { return RBRACE; }
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

%token WHILE LBRACE RBRACE NUM

%%

stmt_list: stmt_list stmt
         | /* empty */
         ;

stmt: while_stmt
    | /* other statements */
    ;

while_stmt: WHILE '(' condition=NUM ')' LBRACE stmt_list RBRACE
        {
            while ($3) {
                yylineno++;
                yyparse();
            }
        }
        ;

%%

int main(void) {
    yyparse();
    return 0;
}

void yyerror(const char *msg) {
    fprintf(stderr, "Error: %s at line %d\n", msg, yylineno);
}

