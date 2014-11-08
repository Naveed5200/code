code
====
//matrix.h
#include<iostream>
#include<conio.h>
using namespace std;

class Matrix{
	int *Mat;
	int row;
	int col;
public:
	Matrix(){
	row=0 ;
	col=0;
	Mat=0;
	}
	Matrix(int x , int y)
	{
	row=x;
	col=y;
	Mat=new int [row * col];
     Init();
	}
	void Init()
	{
		for(int c = 0; c < (row * col); c++)
			Mat[c] = 0;
	}
	int & set_Val_at_Cell(int x , int y)
	{ 
		int Cell;
	Cell= (x * col)+y;
	return Mat[Cell];

	}


	void Input()
	{
		int temp=0;
		for(int i = 0 ; i< row;i++)
			{
				for(int j = 0 ;j<col;j++)
				{
					cout<<"location"<<i<<j<<endl;
	      			cin>>temp;
					 set_Val_at_Cell(i , j)=temp;
				}
			}
	}


  void Display()
  {
  for(int i = 0 ; i<row; i++)
	  {for(int j = 0 ; j< col ; j++)
	   {
 	  cout<<set_Val_at_Cell(i , j)<<"  ";
      }cout<<endl;
	   }cout<<endl;

  }

  Matrix operator +(Matrix & rhs)
  {Matrix temp(row , col);
      for(int i = 0 ; i < row; i++ )
      {
          for (int j = 0 ; j < col ; j++ )
          {

            temp.set_Val_at_Cell(i , j ) = set_Val_at_Cell(i , j ) + rhs.set_Val_at_Cell(i , j );



          }

      }
      return temp;
  }

 Matrix operator -(Matrix & rhs )
 {
     Matrix temp(row , col);
     for(int i = 0 ; i < row; i++ )
      {
          for (int j = 0 ; j < col ; j++ )
          {
              temp.set_Val_at_Cell(i , j ) = set_Val_at_Cell(i , j ) - rhs.set_Val_at_Cell(i , j );
          }
      }
      return temp;
 }

Matrix operator *(Matrix &rhs)
{
Matrix temp(row , col);
     for(int i = 0 ; i < row; i++ )
      {
          for (int j = 0 ; j < col ; j++ )
          {
            temp.set_Val_at_Cell(i , j )=0;
              for(int k=0 ; k < col ; k++)
              {
              temp.set_Val_at_Cell(i , j ) =  temp.set_Val_at_Cell(i , j )+( set_Val_at_Cell(i , k ) * rhs.set_Val_at_Cell(k , j ));
              }
          }
      }
      return temp;
	  
}

void Is_Identity ()
{
 int check=1;
	for(int i=0; i<row; i++)
    {     for(int j=0; j<col; j++)
       {	 if(set_Val_at_Cell(i , j) != 1 && set_Val_at_Cell(j ,i) !=0)
                {
					check = 0;	   
	                break;
	            }
	   }
    }
	if(check == 1 )
		cout<<"It is identity matrix"<<endl;
	else	
cout<<"It is not a identity matrix"<<endl;

}


};
//matrix.cpp

#include"matrix.h"
void Menu();
bool Allright(char );
 
 
int main()
{
	char anwser = '?';
	cout << "Choose Matrix Size Plz." << endl;
	cout << "Enter Line: " ; 
	unsigned line = 0;
	cin  >> line;
	cout << "Enter Column: " ;
	unsigned colu = 0;
	cin  >> colu;
	Matrix m1(line, colu);
	Matrix m2(line, colu);
	Matrix m3;
	string signe = ""; 
	bool   first = false;
	do
	{
		if(!first )
		{
			cout << "Enter First Matrix data : " << endl;
			m1.Input();
			cout << "Enter Secoud Matrix data: " << endl;
			m2.Input();
			first = true;
		}
		else
			cout << "Chose Another Operation to perform: " << endl;
		Menu();
		cin >> anwser;
		if(Allright(anwser))
		{
			if(anwser != 'e' && anwser != 'E')
			{
			switch(anwser)
			{
			case 'a': 
			case 'A':signe = " + ";
					m3 = m1 + m2;
				break;
			case 'S':
			case 's': signe = " - ";
					m3 = m1 - m2;
				break;
			case 'M':
			case 'm':
					signe = " * ";
					m3 = m1 * m2;
					
				break;
			case 'I':
			case 'i':
	cout << "Choose Matrix Size Plz." << endl;
	cout << "Enter Line: " ; 
	unsigned line = 0;
	cin  >> line;
	cout << "Enter Column: " ;
	unsigned colu = 0;
	cin  >> colu;
		Matrix obj4(line , colu);
        obj4.Input();
        obj4.Is_Identity();
			break;
			}
				m3.Display();	
			}
		}
		else
		{
			cout << anwser << " not reconized like command, choose correct one plz" << endl;
		}
 
	}
	while(anwser != 'e' && anwser != 'E');
}
 
void Menu()
{
	cout << "Press (A/a) for Addition." << endl;
	cout << "Press (S/s) for Substraction." << endl;
	cout << "Press (M/m) for Multiplication." << endl;
	cout << "Press (E/e) for Exit." << endl;
	cout<< "Enter (I/i) for Identity matrix";
}
 
bool Allright(char x)
{
	if(	x == 'A' || x == 'a' ||
		x == 'S' || x == 's' ||
		x == 'M' || x == 'm' ||
		x == 'E' || x == 'e' || 
		x == 'I' || x == 'i')
		return(true);
	return(false);
}
 
/*
#include"matrix.h"

int main()
{
	
	
    int row , col;
    Matrix obj3 ;

			
	  cout<<"enter row and col of matrix1 "<<endl;
	    cin>>row>>col;
		Matrix obj1(row , col);
		obj1.Input();
	   
      cout<<"\nEnter row and col of matrix2"<<endl;
	    cin>>row>>col;
	  Matrix obj2(row , col);
	  obj2.Input();
	  obj1.Display();
	  obj2.Display(); 

       obj3 = obj1+obj2;
       cout<<"Addition"<<endl;
       obj3.Display();
	
	
       cout<<"Subtraction"<<endl;
       obj3 = obj1-obj2;
       obj3.Display();

      cout<<"Multiplication"<<endl;
      obj3 = obj1*obj2;
      obj3.Display();
	

		 cout<<"\n Enter rows and column"<<endl;
	     cin>>row>>col;
		 Matrix obj4(row , col);
         obj4.Input();
         obj4.Is_Identity();
	
	
}

*/
