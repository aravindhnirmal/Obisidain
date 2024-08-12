[[Keep/Colour/RED]] [[Keep/Attachments]] [[Keep/Archived]] 

Open
matrixchain.cpp x
[[include]]<iostream>
using namespace std;
int main()
int n=5;
int p[]=(5,4,6,2,7);
int m[5][5]={0};
int s[5][5]={0};
int j,min,q,d;
cout<<"Input\n";
for(int g=0;g<5;g++)
for(d=1;d<n-1;d++)
op
me
loa
es
S
Ve
Vol
BV
70
Dub
Save
cout<<p[g]<<"\t";
for(int i=1;i<n-d;i++)
j=i+d;
min=32767;
for(int k=i;k<=j-1;k++)
q=m[i][k]+m[k+1][j]+p[i-1]*p[k]*p[j];
if(q<min)
min=q;
s[i][j]=k;
m[i][j]=min;
cout<<" \nTotal Multiplication = "<<m[1][n-1]:
C++ Y Tab Width: 8-
selected (481 bytes)
Ln 4, Col 2
INS


![[1654566771941.1953140150.png]]