[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

%{
[[include]] "y.tab.h"
%}

%%

"for"               { return FOR; }
[a-zA-Z]+           { return IDENTIFIER; }
[0-9]+              { return NUMBER; }
"<"                 { return LESS; }
";"                 { return SEMICOLON; }
"{"                 { return LBRACE; }
"}"                 { return RBRACE; }
"++"                { return PLUSPLUS; }
"="                 { return ASSIGN; }
[ \t\n]             ; /* ignore whitespace */
.                   { return yytext[0]; }

%%

int yywrap() {
    return 1;
}





%{
[[include]] <stdio.h>
%}

%token FOR IDENTIFIER NUMBER LESS SEMICOLON LBRACE RBRACE PLUSPLUS ASSIGN

%%

statement: FOR '(' IDENTIFIER ASSIGN NUMBER SEMICOLON IDENTIFIER LESS NUMBER SEMICOLON IDENTIFIER PLUSPLUS PLUSPLUS ')' LBRACE '}' RBRACE
          { printf("Valid for loop\n"); }
          | error
          { printf("Invalid for loop\n"); }

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
int yywrap() {
    return 1;
}

