[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

%{
[[include]] <stdio.h>
[[include]] <stdlib.h>
[[include]] "y.tab.h"
%}

%%
"if"            { return IF; }
"else"          { return ELSE; }
"=="            { return EQUAL; }
[0-9]+          { yylval = atoi(yytext); return NUM; }
[ \t\n]         /* Ignore whitespace */
.               return yytext[0];
%%

int yywrap(void) {
    return 1;
}

