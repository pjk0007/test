Project title
------
This program reads the 'resource.dat' and 'input.dat' files from the library class and processes them according to the order of the input and generates output.
The main function only generated the library and the function that generates the library reads the file and stores and processes the data.
First, read the file 'resource.dat' and save the contents of the data to the Vector declared as resource data type.
Read the 'input.dat' file to store the vector declared as the member data type and process the input order using the information of each vector.

Getting started
-----
###What things you need to install and how to install
Among the files to run the program, we need 'main.cpp', 'library.cpp', 'resource.cpp', 'book.cup' and 'memberc'.
Required data files include 'resource.dat' and 'input.dat'.
###How to compile
You can compile in two ways. The first method is as follows.
```
$ g++ -std=c++11 -o start main.cpp library.cpp resource.cpp book.cpp member.cpp undergraduate.cpp
```
Other methods can be made through 'Makefile'.
```
$ make
```
The above command creates an executable file called 'start'.

Running
-----------
###Explain how to run
When a file named `start` is created through a compilation,
```
$ ./start >output.dat
```
You can obtain a result of 'output.dat' through the command.

API
--------
library
```
class library
{
	private:
		vector<resource*> RESLIST;
		vector<member*> MEMLIST;
	public:
		library();
};
```
rsource
```
class resource
{
	protected:
		string res_Name;
		string mem_Name;
		string Type;
		int B_year;
		int B_month;
		int B_day;
		int R_year;
		int R_month;
		int R_day;
		int exist;	// 0 is already borrowed, 1 is exist in library
	public:
		resource(string rn, string T);
		string getName();
		string getType();
		int getB_year();
		int getB_month();
		int getB_day();
		int getR_year();
		int getR_month();
		int getR_day();
		int borrow(string mn, int B_y, int B_m, int B_d, int R_y, int R_m, int R_d);
		int giveBack(string mn, int N_y, int N_m, int N_d);
};
```
int resource::borrow(string mn, int B_y, int B_m, int B_d, int R_y, int R_m, int R_d)
Return 0 when borrow is success.
Return 1 when you already borrowed this `Type` at B_y/B_m/B_d
Return 2 when other member already borrowed this `Type`

int resource::giveBack(string mn, int N_y, int N_m, int N_d)
Return 0 when return is success.
Return 1 when delayed return.
Return 2 when you did not borrow this `Type`.

member
```
class member
{
	protected:
		string mem_Name;
		string Type;
		int canBorrow;
		int nowBorrow;
		int ban_year;
		int ban_month;
		int ban_day;
		int term;		
	public:
		member(string mn, string T);
		string getName();
		int getBorrow();
		int getYear();
		int getMonth();
		int getDay();
		int getTerm();
		void setBorrow(int b);
		void setYear(int y);
		void setMonth(int m);
		void setDay(int d);
		int borrow(int n_y, int n_m, int n_d);
		void giveBack();
};
```

int member::borrow(int n_y, int n_m, int n_d)
Return 0 when you can borrow something.
Return 1 when you are restricted member until ban_year/ban_month/ban_day
Return 2 when exceeds your possible number of borrow.

void member::giveBack()
this function is called when the giveback something is successful.
`nowBorrow--;`
