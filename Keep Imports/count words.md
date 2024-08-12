[[Keep/Colour/DEFAULT]] 

%{
[[include]] <stdio.h>
%}

%%
[a-zA-Z]+   { count++; }
.|\n        { }
%%

int count = 0;

int main() {
    printf("Enter a sentence: ");
    yylex();
    printf("Number of words: %d\n", count);
    return 0;
}

