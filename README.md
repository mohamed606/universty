# universty
#include <iostream>
#include <fstream>
#include<string>
#include <bits/stdc++.h>
using namespace std;
int Union[1000] , intersection[1000] , diffA[1000];
int main()
{
    int a[1000] , b[1000] ;
    int size1=0 , size2=0 , unionSize=0  , intersectionSize=0 , diffASize=0;
    while(true)
    {

        int x ;
        char nameFile1[100] , nameFile2[100];
        cout<<"1- Enter a new data set \n2- Load two data sets\n3- Display data set\n4- Union of A , B\n5- Intersection A , B\n6- A - B\n7- B - A\n8- Cartesian product of A and B\n9- Power set of A or B\n10- Check if A and B are disjoint\n11- Check if A and B are equal\n12- Check if a set is a proper subset of other\n";
        cin>>x;
        if(x==1)
        {
            int data1 , size1 , data2 , size2;
            ofstream file1 , file2;
            cout<<"please enter the first file name : ";
            cin>>nameFile1;
            file1.open(nameFile1);
            cout<<"enter the size of the set \n";
            cin>>size1;
            cout<<"enter the data into the file \n";
            for(int i=0 ; i<size1 ; i++)
            {
                cin>>data1;
                file1<<data1<<endl;
            }
            file1.close();
            cout<<"please enter the second file name : ";
            cin>>nameFile2;
            file2.open(nameFile2);
            cout<<"enter the size of the set \n";
            cin>>size2;
            cout<<"enter the data into the file \n";
            for(int i=0 ; i<size2 ; i++)
            {
                cin>>data2;
                file2<<data2<<endl;
            }
            file2.close();
        }
        else if(x==2)
        {
            ifstream file1 , file2;
            cout<<"enter the name of the two files \n";
            cin>>nameFile1>>nameFile2;
            file1.open(nameFile1);
            if(!file1.fail())
            {
                int i=0;
                while(true)
                {
                    file1>>a[i];
                    i++;
                    size1++;
                    if(file1.eof())
                    {
                        break;
                    }
                }
            }
            file1.close();
            file2.open(nameFile2);
            if(!file2.fail())
            {
                int i=0;
                while(true)
                {
                    file2>>b[i];
                    i++;
                    size2++;
                    if(file2.eof())
                    {
                        break;
                    }
                }
            }
            file2.close();
        }
        else if(x==3)
        {
            cout<<"The data in set A\n";
            cout<<"{ ";
            for(int i=0 ; i<size1-1 ; i++)
            {
                cout<<a[i];
                if(i<size1-2)
                {
                    cout<<",";
                }
            }
            cout<<" }\n";
            cout<<"The data in set B\n";
            cout<<"{ ";
            for(int i=0 ; i<size2-1 ; i++)
            {
                cout<<b[i];
                if(i<size2-2)
                {
                    cout<<",";
                }
            }
            cout<<" }\n";
        }
        else if(x==4)
        {
            for(int i=0 ; i<size1-1 ; i++)
            {
                Union[i]=a[i];
                unionSize++;
            }
            for(int i=0 ; i<size2-1 ; i++)
            {
                for(int s=0 ; s<unionSize ; s++)
                {
                    if(Union[s]==b[i])
                    {
                        break;
                    }
                    if(s==unionSize-1)
                    {
                        Union[s+1]=b[i];
                        unionSize++;
                    }
                }
            }
            cout<<"{ ";
            for(int i=0 ; i <unionSize ; i++)
            {
                cout<<Union[i];
                if(i<unionSize-1)
                {
                    cout<<",";
                }
            }
            cout<<" }\n";

        }
        else if((x==5)||(x==10))
        {
            for(int i=0 ; i<size1-1 ; i++)
            {
                for(int s=0 ; s<size2-1 ; s++)
                {
                    if(a[i]==b[s])
                    {
                        intersection[intersectionSize]=a[i];
                        intersectionSize++;
                    }
                }
            }
            if(x==5)
            {
                cout<<"{ ";
                for(int i=0 ; i<intersectionSize ; i++)
                {
                    cout<<intersection[i];
                    if(i<intersectionSize-1)
                    {
                        cout<<",";
                    }
                }
                cout<<" }\n";
            }
            if(x==10)
            {
                if(intersectionSize==0)
                {
                    cout<<endl<<"A and B are disjoint\n\n";
                }
                else
                {
                    cout<<"\nA and B aren't disjoint\n\n";
                }
            }
        }
        else if((x==6)||(x==7))
        {
            for(int i=0 ; i<size1-1 ; i++)
            {
                for(int s=0 ; s<size2-1 ; s++)
                {
                    if(a[i]==b[s])
                    {
                        break;
                    }
                    if(s==size2-2)
                    {
                        diffA[diffASize]=a[i];
                        diffASize++;
                    }
                }
            }
            if(diffASize!=0)
            {
                cout<<"{ ";
                for(int i=0 ; i<diffASize ; i++)
                {
                    cout<<diffA[i];
                    if(i<diffASize-1)
                    {
                        cout<<",";
                    }
                }
                cout<<" }\n";
            }
            else
            {
                cout<<(char(127))<<endl;
            }

        }
        else if(x==8)
        {
            cout<<"{ ";
            for(int i=0 ; i<size1-1 ; i++)
            {
                for(int s=0 ; s<size2-1 ; s++)
                {
                    cout<<"("<<a[i]<<","<<b[s]<<")";
                    if(s<size2-2)
                    {
                        cout<<" , ";
                    }
                }
                if(i<size1-2)
                {

                    cout<<" , ";
                }
            }
            cout<<" }"<<endl;
        }
        else if(x==9)
        {
            int counter=1;
            char setType ;
            cout<<"choose set A or set B : \n";
            cin>>setType;
            if(setType=='A')
            {
                cout<<"{ ";
                cout<<(char)127<<" , ";
                for(int i=0 ; i<size1-1 ; i++)
                {
                    cout<<"{"<<a[i]<<"}"<<" , ";
                }
                for(int i=0 ; i<size1-2 ; i++)
                {
                    if(i>0)
                    {
                        counter++;
                    }
                    for(int s=counter ; s<size1-1 ; s++)
                    {
                        cout<<"{"<<a[i]<<" , "<<a[s]<<"}"<<" , ";
                    }
                }
                cout<<"{ ";
                for(int i=0 ; i<size1-1 ; i++)
                {
                    cout<<a[i];
                    if(i<size1-2)
                    {
                        cout<<" , ";
                    }
                }
                cout<<" } }\n";

            }
            else if(setType=='B')
            {
                cout<<"{ ";
                cout<<(char)127<<" , ";
                for(int i=0 ; i<size2-1 ; i++)
                {
                    cout<<"{"<<b[i]<<"}"<<" , ";
                }
                for(int i=0 ; i<size2-2 ; i++)
                {
                    if(i>0)
                    {
                        counter++;
                    }
                    for(int s=counter ; s<size2-1 ; s++)
                    {
                        cout<<"{"<<b[i]<<" , "<<b[s]<<"}"<<" , ";
                    }
                }
                cout<<"{ ";
                for(int i=0 ; i<size2-1 ; i++)
                {
                    cout<<b[i];
                    if(i<size2-2)
                    {
                        cout<<" , ";
                    }
                }
                cout<<" } }\n";

            }
        }
        else if(x==11)
        {
            int z=0;
            sort(a , a+(size1-1));
            sort(b , b+(size2-1));
            if(size1>=size2)
            {
                for(int i=0 ; i<size1-1 ; i++)
                {
                    for(int s=0 ; s<size2-1 ; s++)
                    {
                        if(b[i]!=a[i])
                        {
                            z=1;
                            break;
                        }
                    }
                }
                if(z==1)
                {
                    cout<<"\nset A not equal set B\n\n";
                }
                else
                {
                    cout<<"\nset A equal set B\n\n";
                }

            }
            else if(size2>size1)
            {
                for(int i=0 ; i<size2-1 ; i++)
                {
                    for(int s=0 ; s<size1-1 ; s++)
                    {
                        if(b[i]!=a[i])
                        {
                            z=1;
                            break;
                        }
                    }
                }
                if(z==1)
                {
                    cout<<"\nset A not equal set B\n\n";
                }
                else
                {
                    cout<<"\nset A equal set B\n\n";
                }
            }

        }
        else if(x==12)
        {
            int z=0;
            sort(a , a+(size1-1));
            sort(b , b+(size2-1));
            if(size1>=size2)
            {
                for(int i=0 ; i<size1-1 ; i++)
                {
                    for(int s=0 ; s<size2-1 ; s++)
                    {
                        if(a[i]==b[s])
                        {
                            break;
                        }
                        if(s==size2-2)
                        {
                            z=1;
                        }
                    }
                }
                if(z==0)
                {
                    cout<<"\nB is not a proper subset from A\n\n";
                }
                else
                {
                    cout<<"\nB is a proper subset from A\n\n";
                }
            }
            else if(size2>size1)
            {
                for(int i=0 ; i<size2-1 ; i++)
                {
                    for(int s=0 ; s<size1-1 ; s++)
                    {
                        if(b[i]==a[s])
                        {
                            break;
                        }
                        if(s==size1-2)
                        {
                            z=1;
                        }
                    }
                }
                if(z==0)
                {
                    cout<<"\nA is not a proper subset from B\n\n";
                }
                else
                {
                    cout<<"\nA is a proper subset from B\n\n";
                }
            }

        }
        else
        {
            break;
        }


    }
    return 0;
}
