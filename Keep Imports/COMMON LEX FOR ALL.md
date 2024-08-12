[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

%{
[[include]] "calc.tab.h"
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

