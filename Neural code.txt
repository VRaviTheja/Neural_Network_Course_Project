#include <iostream>
#include <string.h>
#include <fstream>
#include<vector>
#include<iomanip>

using namespace std;

float testbinary[50][6];
char res[27]={'A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z',' '};

void binary(int num,int index,int i)
{
    int rem;
    if (i == -1)
        return;
    rem = num % 2;
    binary(num / 2,index,i-1);
    testbinary[index][i]=rem;
}

int main()
{
    float w[6][27];
    int i=0,j=0,result;
    ifstream fin;
    fin.open("TRAINING.txt", ios::in);
    char my_character ;
    cout<<"Training data The alphabets in 6 digit binary Form"<<endl;
	while (!fin.eof() )
    {
        fin.get(my_character);
        cout << my_character;
        if(my_character == '0')
            w[i][j] = -0.5;
         else
            w[i][j] = 0.5;
        i++;
        if(i==6)
        {
            j++;
            i=0;
            cout<<endl;
        }
    }
    cout<<"\r "<<endl;
    cout <<"Weight Matrix 6x28:\n";
    for (int i=0; i < 6; i++)
    {
            for(j=0; j < 26; j++)
            {
                std::cout << std::setprecision(1);
                std::cout << std::setw(6);
                cout << w[i][j];
            }
            cout<<endl;
    }
    cout<<endl;
    cout<<"Testing data to find the alphabet\n";
    std::fstream myfile("TESTING.txt", std::ios_base::in);
    int test1[50];
    int a;
    i=0;
    while (myfile >> a)
    {
       cout<<a<<"\t";
       test1[i]=a;
       i++;
    }
    cout<<endl;
    cout<<"In binary that is in Braille"<<endl;
   for(int k=0;k<50;k++)
   {
       binary(test1[k],k,5);
   }
   for(int k=0;k<50;k++)
   {
        for(j=0;j<6;j++)
        {
            cout<<testbinary[k][j];
        }
        cout<<"\t";
    }
    for(int k=0;k<50;k++)
    {
        for(i=0;i<6;i++)
        {
            if(testbinary[k][i]==0)
                testbinary[k][i]=-1;
        }
    }
    float max1;
    cout<<"\n\nInput\t"<<"Hamming distance\t"<<"Output\t"<<endl;
    for(int k=0;k<50;k++)
    {
        float mid[26]={0};
    for(i=0;i<26;i++)
    {
        mid[i]=mid[i]+(float)3;        //bias adding
        for(j=0;j<6;j++)
        {
            mid[i]=mid[i]+(float)((float)w[j][i]*(float)testbinary[k][j]);
        }
    }
    max1=-1;
    for(i=0;i<26;i++)
    {
        if(mid[i]>max1)
        {
            max1=mid[i];
            result=i;
        }
    }
    cout<<test1[k]<<"\t";
    cout<<max1<<"               \t";
    cout<<res[result]<<endl;
    }
    return 0;
}
