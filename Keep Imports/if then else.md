[[Keep/Colour/DEFAULT]] 

%{
[[include]] "y.tab.h"
%}

%%

if      { return IF; }
then    { return THEN; }
else    { return ELSE; }
.|\n    { /* ignore other characters */ }

%%

int yywrap() {
    return 1;
}





%{
[[include]] <stdio.h>
[[include]] "y.tab.h"
%}

%token IF THEN ELSE

%%

stmt : IF THEN stmt ELSE stmt
     | IF THEN stmt
     ;

%%

int main() {
    yyparse();
    return 0;
}

void yyerror(const char* msg) {
    printf(stderr, "Error: %s\n", msg);l 
}

