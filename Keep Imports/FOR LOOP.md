[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

%{
[[include]] <stdio.h>
[[include]] <stdlib.h>
[[include]] "y.tab.h"
%}

%%
"for"           { return FOR; }
";"             { return SEMICOLON; }
[0-9]+          { yylval = atoi(yytext); return NUM; }
[ \t\n]         /* Ignore whitespace */
.               return yytext[0];
%%

int yywrap(void) {
    return 1;
}


%{
[[include]] <stdio.h>
%}

%token FOR LPAREN RPAREN SEMICOLON NUM

%%

stmt_list: stmt_list stmt
         | /* empty */
         ;

stmt: for_stmt
    | /* other statements */
    ;

for_stmt: FOR LPAREN start=NUM SEMICOLON end=NUM SEMICOLON step=NUM RPAREN stmt
        {
            int i;
            for (i = $1; i <= $2; i += $3) {
                // Execute the statements in the loop
                // Note: the yyparse() function will call the `stmt_list` rule recursively
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

