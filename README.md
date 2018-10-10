# Sets-of-function-for-matrix-manipulation.
// Course:  CS213 - Programming II  - 2018
// Title:   Assignment I - Task 1 - Problem 1
// Program: CS213-2018-A1-T1-P1
// Purpose: Skeleton code for the student to start working
// Author:  Seif Mostafa and Saeed Mohamed
// Date:    10 August 2018
// Version: 1.0

#include <iostream>
#include <iomanip>
//#include <cassert>

using namespace std;

// A structure to store a matrix
struct matrix
{
  int* data;       // Pointer to 1-D array that will simulate matrix
  int row, col;
};

// Already implemented
void createMatrix (int row, int col, int num[], matrix& mat);

// Student #1 with the smallest ID (e.g., 20170080)
// All these operations return a new matrix with the calculation result
matrix operator+  (matrix mat1, matrix mat2); // Add if same dimensions
matrix operator-  (matrix mat1, matrix mat2); // Sub if same dimensions
matrix operator*  (matrix mat1, matrix mat2); // Multi if col1 == row2
matrix operator+  (matrix mat1, int scalar);  // Add a scalar
matrix operator-  (matrix mat1, int scalar);  // Subtract a scalar
matrix operator*  (matrix mat1, int scalar);  // Multiple by scalar

// Student #2 with the middle ID (e.g., 20170082)
// The last operator >> takes an istream and a matrix and return the
// the same istream so it is possible to cascade input like
// cin >> matrix1 >> matrix2 << endl;
matrix operator+= (matrix& mat1, matrix mat2); // mat1 changes & return
					    // new matrix with the sum
matrix operator-= (matrix& mat1, matrix mat2); // mat1 changes + return new
					     // matrix with difference
matrix operator+= (matrix& mat, int scalar);   // change mat & return new matrix
matrix operator-= (matrix& mat, int scalar);   // change mat & return new matrix
void   operator++ (matrix& mat);   	// Add 1 to each element ++mat
void   operator-- (matrix& mat);    	// Sub 1 from each element --mat
istream& operator>> (istream& in, matrix& mat);
       	// Input matrix like this (dim 2 x 3) cin >> 2 3 4 6 8 9 12 123
       // and return istream to allow cascading input

//Student #3 with the biggest ID (e.g., 20170089)
ostream& operator<< (ostream& out, matrix mat);
       	// Print matrix  as follows (2 x 3)			4	 6 	  8
	       // and return ostream to cascade printing	9	12  	123
bool   operator== (matrix mat1, matrix mat2);	// True if identical
bool   operator!= (matrix mat1, matrix mat2); 	// True if not same
bool   isSquare   (matrix mat);  // True if square matrix
bool isSymetric (matrix mat);  // True if square and symmetric
bool   isIdentity (matrix mat);  // True if square and identity
matrix transpose(matrix mat);    // Return new matrix with the transpose

//__________________________________________

int main()
{
  int data1 [] = {1,2,3,4,5,6,7,8};
  int data2 [] = {1,2,3,4,5,6,7,8,8};
  int data3 [] = {1,0,0,0,1,0,0,0,1};


  matrix mat1, mat2, mat3;
  createMatrix (4, 2, data1, mat1);
  createMatrix (3, 3, data2, mat2);
  createMatrix (3, 3, data3, mat3);





/* The next code will not work until you write the functions
  cout << mat1 << endl;
  cout << mat2 << endl;
  cout << mat3 << endl;

  cout << (mat1 + mat3) << endl << endl;
  cout << (mat3 + mat3) << endl << endl;

  ++mat1;
  cout << mat1 << endl;

  mat1+= mat3 += mat3;
  cout << mat1 << endl;
  cout << mat2 << endl;
  cout << mat3 << endl;
  // Add more examples of using matrix
  // .......
*/

  return 0;
}

//__________________________________________
// Takes an array of data and stores in matrix according
// to rows and columns
void createMatrix (int row, int col, int num[], matrix& mat) {
  mat.row = row;
  mat.col = col;
  mat.data = new int [row * col];
  for (int i = 0; i < row * col; i++)
    mat.data [i] = num [i];
}
ostream& operator<< (ostream& out, matrix mat){
int v= 0 ;
    for(int i=0;i<mat.row ;i++){
    for(int x=0;x<mat.col ;x++){
    out << mat.data[v]<<" ";
     v++;
      }
     cout<<endl;
      }
return out;
}


istream& operator>> (istream& in, matrix& mat){
int r,c;
in>>r>>c;
mat.row = r;
mat.col = c;
mat.data = new int [r * c];
for(int i=0;i<r*c;i++){
in>>mat.data[i];
}

}
matrix operator+  (matrix mat1, matrix mat3){
    if ((mat1.row==mat3.row)&&(mat1.col==mat3.col)){
    matrix matt;
matt.row=mat1.row;
matt.col=mat1.col;
matt.data = new int [mat1.row*mat1.col];
for(int i=0;i<mat1.row*mat1.col ;i++){
    matt.data[i]= mat1.data[i]+mat3.data[i];
    }

return matt;
}
else {
    cout<<"not same dimensions";
}
}
matrix operator-  (matrix mat1, matrix mat3){
if ((mat1.row==mat3.row)&&(mat1.col==mat3.col)){
    matrix matt;
matt.row=mat1.row;
matt.col=mat1.col;
matt.data = new int [mat1.row*mat1.col];
for(int i=0;i<mat1.row*mat1.col ;i++){
    matt.data[i]= mat1.data[i]-mat3.data[i];
    }
createMatrix (matt.row, matt.col , matt.data, matt);
return matt;
}
else {
    cout<<"not same dimensions";
}
}
matrix operator*  (matrix mat1, matrix mat2){
matrix matt;
matt.row=mat1.row;
matt.col=mat2.col;
matt.data = new int [mat1.row*mat2.col];
int v=0;
if(mat1.col==mat2.row){
for(int i=0;i<mat1.row;i++){
    for(int j=0;j<mat2.col;j++){
        int sum=0;
        for(int k=0;k<mat2.row;k++){
            sum=sum+mat1.data[i*mat1.col+k]*mat2.data[k*mat2.col+j];
        matt.data[v]=sum;
        v++;

    }
  }
 }
return matt;
}

}
matrix operator+  (matrix mat1, int scalar){
matrix matt;
matt.row=mat1.row;
matt.col=mat1.col;
matt.data = new int [mat1.row*mat1.col];
for(int i=0;i<mat1.row*mat1.col ;i++){
    matt.data[i]= mat1.data[i]+scalar;
    }
createMatrix (matt.row, matt.col , matt.data, matt);
return matt;
}
matrix operator-  (matrix mat1, int scalar){
matrix matt;
matt.row=mat1.row;
matt.col=mat1.col;
matt.data = new int [mat1.row*mat1.col];
for(int i=0;i<mat1.row*mat1.col ;i++){
    matt.data[i]= mat1.data[i]-scalar;
    }
createMatrix (matt.row, matt.col , matt.data, matt);
return matt;
}
matrix operator*  (matrix mat1, int scalar){
matrix matt;
matt.row=mat1.row;
matt.col=mat1.col;
matt.data = new int [mat1.row*mat1.col];
for(int i=0;i<mat1.row*mat1.col ;i++){
    matt.data[i]= mat1.data[i]*scalar;
    }
createMatrix (matt.row, matt.col , matt.data, matt);
return matt;


}
matrix operator+= (matrix& mat1, matrix mat2){
for(int i=0;i<mat1.row*mat1.col ;i++){
    mat1.data[i]= mat1.data[i]+mat2.data[i];
}
return mat1;
}
matrix operator-= (matrix& mat1, matrix mat2){
for(int i=0;i<mat1.row*mat1.col ;i++){
    mat1.data[i]= mat1.data[i]-mat2.data[i];
}
return mat1;
}
matrix operator+= (matrix& mat, int scalar){
for(int i=0;i<mat.row*mat.col ;i++){
    mat.data[i]= mat.data[i]+scalar;
}
return mat;
}
matrix operator-= (matrix& mat, int scalar){
for(int i=0;i<mat.row*mat.col ;i++){
    mat.data[i]= mat.data[i]-scalar;
}
return mat;
}
void   operator++ (matrix& mat){
for(int i=0;i<mat.row*mat.col ;i++){
    mat.data[i]= mat.data[i]+1;
}
}
void   operator-- (matrix& mat){
for(int i=0;i<mat.row*mat.col ;i++){
    mat.data[i]= mat.data[i]-1;
}
}
bool   operator== (matrix mat1, matrix mat2){
if(mat1.row==mat2.row&&mat1.col==mat2.col){
    for(int i=0;i<mat1.row*mat1.col;i++){
        if(mat1.data[i]==mat2.data[i]);
        else if(mat1.data[i]!=mat2.data[i]){
           return 0;
            break;
                }
    }
   return 1;
}
}
bool   operator!= (matrix mat1, matrix mat2){
if(mat1.row==mat2.row&&mat1.col==mat2.col){
    for(int i=0;i<mat1.row*mat1.col;i++){
        if(mat1.data[i]==mat2.data[i]);
        else if(mat1.data[i]!=mat2.data[i]){
           return 1;
            break;
                }
    }
   return 0;
}
else{
    return 1;
}

}
bool   isSquare   (matrix mat){
if(mat.row==mat.col){
    return 1;
}
else{
    return 0;
}

}
bool isSymetric (matrix mat){
int mata[mat.row][mat.col];
if(mat.row==mat.col){
for(int i=0;i<mat.row;i++){
 for (int j =0;j<mat.col;j++){
    mata[i][j]=mat.data[i*mat.row+j];
 }
}
}
int mataTransp[mat.row][mat.col];
   for (int i = 0; i < mat.row; i++){
    for (int j = 0; j < mat.col; j++){
        mataTransp[j][i]=mata[i][j];
    }
}
 for (int i = 0; i < mat.row; i++){
    for (int j = 0; j < mat.col; j++){
       if (mataTransp[i][j]==mata[i][j]);

    else if (mataTransp[i][j]!=mata[i][j]){
        return 0;
        break;
    }
    }

    }
return 1;
}
matrix transpose(matrix mat){
matrix TranspMat;
TranspMat.row=mat.col;
TranspMat.col=mat.row;
TranspMat.data= new int [mat.row*mat.col];
for(int i=0;i<mat.col;i++){
    for(int j=0;j<mat.row;j++)
    TranspMat.data[j+i*mat.row]=mat.data[j+i*3];
}
return TranspMat;

}
bool   isIdentity (matrix mat){
if(mat.row==mat.col){
for(int i=0;i<mat.row*mat.col;i++){
    if(i%(mat.row+1)==0&&mat.data[i]!=1){
        return 0;
        break;
    }
 if(i%(mat.row+1)!=0&&mat.data[i]!=0){
        return 0;
        break;
    }
}
}
return 1;
}
