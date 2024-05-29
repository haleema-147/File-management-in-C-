# File-management-in-C++
/* File Handling with C++ using ifstream & ofstream class object*/
/* To write the Content in File*/
/* Then to read the content of file*/
#include <iostream>

/* fstream header file for ifstream, ofstream,
fstream classes */
#include <fstream>
#include <string>
#include <stdio.h>
#include <iostream>
#include <filesystem>

using namespace std;

void readFile(string fileName)
{
	string line;
	// Creation of ifstream class object to read the file
	ifstream fin;

	// by default open mode = ios::in mode
	fin.open(fileName);

	// Execute a loop until EOF (End of File)
	while (getline(fin, line))
	{

		// Print line (read from file) in Console
		cout << line << endl;
	}

	// Close the file
	fin.close();
}

void writeFile(string fileName)
{
	// Creation of ofstream class object
	ofstream fout;

	string line;
	// // by default ios::out mode, automatically deletes
	// // the content of file. To append the content, open in ios:app
	// // fout.open("sample.txt", ios::app)
	fout.open(fileName);

	// // Execute a loop If file successfully opened
	while (fout)
	{

		// 	// Read a Line from standard input
		getline(cin, line);

		// Press -1 to exit
		if (line == "-1")
			break;

		// 	// Write line in file
		fout << line << endl;
	}

	// Close the File
	fout.close();
}

void copyFile(string fileName)
{
	ifstream src;
	ofstream dst;

	src.open(fileName, ios::in | ios::binary);
	dst.open("new" + fileName, ios::out | ios::binary);
	dst << src.rdbuf();

	src.close();
	dst.close();
	cout << "file copied successfully...";
}

void moveFile(string fileName)
{
	ifstream src;
	ofstream dst;

	src.open(fileName, ios::in | ios::binary);
	dst.open("new" + fileName, ios::out | ios::binary);
	dst << src.rdbuf();

	src.close();
	dst.close();
	//remove function takes char* so we need to convert string to char*
	const char *fname = fileName.c_str();
	remove(fname);
}

int main()
{
	string fname;
	int op;
	cout << "What would you like to do?" << endl;
	cout << "1. Opening/reading a file " << endl;
	cout << "2. Writing into a file " << endl;
	cout << "3. Copy a file" << endl;
	cout << "4. Move a file" << endl;
	cin >> op;
	cout << "Enter the name of the file you want to open " << endl;
	cin >> fname;
	switch (op)
	{

	case 1:
		readFile(fname);
		break;
	case 2:
		writeFile(fname);
		break;
	case 3:
		copyFile(fname);
		break;
	case 4:
		moveFile(fname);
		break;
	}
	_getwch();
	return 0;
}
