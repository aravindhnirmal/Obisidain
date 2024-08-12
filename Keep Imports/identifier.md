[[Keep/Colour/DEFAULT]] 

%{
[[include]] <stdio.h>
%}

%option noyywrap

%%
if|else|while|int|float|char { printf("Keyword: %s\n", yytext); }
[a-zA-Z_][a-zA-Z0-9_]*      { printf("Identifier: %s\n", yytext); }
[0-9]+                      { printf("Numeric: %s\n", yytext); }
[+-/*=()]                   { printf("Operator: %s\n", yytext); }
[ \t\n]                     { /* ignore whitespace */ }
.                           { printf("Invalid token: %s\n", yytext); }
%%

int main()
{
    yylex();
    return 0;
}

int yywrap() {
    return 1;
}

