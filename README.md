<div align="center">

## Convert number in to Colum Refrences and vise versa


</div>

### Description

This code was created to properly asign names to columns in a database program I have been writing. an example of how it numbers is as following:

A,B,C...Z,AA,AB...ZZ,AAA,AAB... and so on

This code uses recursion
 
### More Info
 
The name of the column or the number of the column

The code assumes that there is no '0' column and there is no colum greater that the maximum integer value ( around 32,000)

This program was written in Borland Builder under console (with out wich you may not have access to the AnsiString class)

The code returns the Column name as a string or a numbber

The code that makes Names in to numbers is only abel to curently handel up to two letter names ie A-ZZ, I have yet figured out a way to make it work other wise


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Robert 'Bob' Engelhardt](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/robert-bob-engelhardt.md)
**Level**          |Advanced
**User Rating**    |3.0 (6 globes from 2 users)
**Compatibility**  |C\+\+ \(general\)
**Category**       |[Algorithms](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/algorithms__3-29.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/robert-bob-engelhardt-convert-number-in-to-colum-refrences-and-vise-versa__3-466/archive/master.zip)

### API Declarations

```
#include <condefs.h>
#include <conio.h>
#include <iostream.h>
#include <string.h>
#pragma hdrstop
#define AsciiText 64
#define AsciiA 65
#define AsciiZ 90
#define AlphaSize 26
#pragma argsused
```


### Source Code

```
AnsiString MakeCol(int value);  // convert # into column ref A,B,C...AA,AB...
int MakeNum(AnsiString string); // convert column into #
void main()
{
  // A,B,C...Z,AA,AB,..AZ,BA,BC...ZZ,AAA,AAB... and so on
  int col=1; // value must be >1 & <=MAXINT to properly work
  AnsiString string;  // just a string to use
  do
  {
   cout << "Enter value to convert (0 for exit) ";
   cin >> col;
   string = MakeCol(col); // copy the sting to as string for handeling
   cout << MakeNum(string) << "= " << string.c_str() << endl;
  }
  while(col>0);
}
AnsiString MakeCol(int value)
{
  AnsiString Finalstring;
  int overz=0;
  if(value<=AlphaSize) // if it is A-Z
   return( char(value+AsciiText) );
  if(value>AlphaSize)  // if it goes beyond Z
  {
   while(value>AlphaSize)  // calculate how many times it goes beyond Z
   {
     overz++; // add to over singel digit counter
     value-=AlphaSize;
   }
   //_____________Recurse_Call__________________________
   Finalstring+=MakeCol(overz);  // recursively convert
  }
  Finalstring+=char(value+AsciiText); // append letter to back of string
  return(Finalstring);
}
int MakeNum(AnsiString string)
{
  string=string.UpperCase(); // make string uppercase letters
  char *TrueString=string.c_str(); // make into string of characters
  int length=string.Length();  // find length of string
  int value=0; // whole value of string as int
  int lcv=0;  // loop controll variable
  if(!length)  // no size to string
   return(0); // string is empty return with error
  // check to be sure string is of valid character (ONLY LETTERS any case)
  for(lcv=0;lcv<length;lcv++)
   if((TrueString[lcv] < AsciiA) || (TrueString[lcv] > AsciiZ)) // proper ?
     return(0); // return 0 for error with string
  if(length==1) // singel character column number
   value+=int(TrueString[0]-AsciiText);  // give proper value of cahracter
  if(length>1)  // string contains more than one character
  {
   value+=int(TrueString[length-1]-AsciiText); // remove leading value of 64
   for(lcv=2;lcv<=length;lcv++)
   {
     value+=(int(TrueString[length-lcv]-AsciiText) * AlphaSize);
   }
  }
  return(value);
}
```

