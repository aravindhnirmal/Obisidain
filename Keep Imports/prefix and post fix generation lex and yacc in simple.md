[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

%{
[[include]] "y.tab.h"
%}

%%
[0-9]+ { yylval = atoi(yytext); return INTEGER; }
[ \t\n] ; /* ignore whitespace */
[+-*/()] { return yytext[0]; }
. { fprintf(stderr, "error: unexpected character '%c'\n", yytext[0]); }
%%

int yywrap() {
    return 1;
}


%{
[[include]] <stdio.h>
[[include]] <stdlib.h>
[[include]] <string.h>
%}

%token INTEGER

%left '+' '-'
%left '*' '/'

%%

program:
    expr { printf("Prefix: "); print_prefix($1); printf("\nPostfix: "); print_postfix($1); printf("\n"); }
;

expr:
    INTEGER { $$ = create_node($1); }
    | '(' expr '+' expr ')' { $$ = create_node('+', $2, $4); }
    | '(' expr '-' expr ')' { $$ = create_node('-', $2, $4); }
    | '(' expr '*' expr ')' { $$ = create_node('*', $2, $4); }
    | '(' expr '/' expr ')' { $$ = create_node('/', $2, $4); }
;

%%

struct node {
    char op;
    int val;
    struct node *left, *right;
};

struct node* create_node(int val) {
    struct node* new_node = (struct node*) malloc(sizeof(struct node));
    new_node->op = '\0';
    new_node->val = val;
    new_node->left = NULL;
    new_node->right = NULL;
    return new_node;
}

struct node* create_node(char op, struct node* left, struct node* right) {
    struct node* new_node = (struct node*) malloc(sizeof(struct node));
    new_node->op = op;
    new_node->val = 0;
    new_node->left = left;
    new_node->right = right;
    return new_node;
}

void print_prefix(struct node* root) {
    if (root) {
        printf("%c", root->op);
        if (root->left) print_prefix(root->left);
        if (root->right) print_prefix(root->right);
        if (root->val) printf("%d", root->val);
    }
}

void print_postfix(struct node* root) {
    if (root) {
        if (root->left) print_postfix(root->left);
        if (root->right) print_postfix(root->right);
        printf("%c", root->op);
        if (root->val) printf("%d", root->val);
    }
}

