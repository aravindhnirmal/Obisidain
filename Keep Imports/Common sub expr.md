[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

[[include]] <iostream>
[[include]]<string.h>
using namespace std;

int main()
{
    int in[10],p[10],n,i,j,k;
    string ins[10];
    string state;
    cout<<"Enter the number of instructions :";
    cin>>n;
    for(i=0;i<=n;i++)
    {
        getline (cin, state);
        ins[i]=state;
    }
    
    cout<<"\nEnter the priority of each instruction : ";
    for(i=1;i<=n;i++)
    {
        in[i]=i;
        cin>>p[i];
    }
    int temp;
    for(i=0;i<=n;i++)
    {
        for(j=1;j<=n;j++)
        {
            if(p[j]<p[i])
            {
                temp=in[i];
                in[i]=in[j];
                in[j]=temp;
                temp=p[j];
                p[j]=p[i];
                p[i]=temp;
                
            }
        }
    }
    cout<<"\nThe scheduled instructions are :\n";
    for(i=1;i<=n;i++)
    {
        cout<<ins[in[i]]<<"\t\t----"<<p[i]<<"\n";
    }
    return 0;
}
