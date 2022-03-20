#include<fstream>
#include<string.h>
#include<iostream>
#include<stdlib.h>
using namespace std;

class Student{
public:
	int id;
	string name,branch,location;

	void getdata()
	{
		cout<<"Enter Id: ";
		cin>>id;
		cout<<"Enter name: ";
		cin>>name;
		cout<<"Enter branch: ";
		cin>>branch;
		cout<<"Enter location: ";
		cin>>location;
	}

	void adddata()
	{
		fstream f;
		Student stu;

		f.open("student.dat",ios::app|ios::binary);
		stu.getdata();
		f.write((char*)&stu,sizeof(stu));
		f.close();
	}

	void findbyid(int id){
		fstream f;
		Student stu;
		int flag=0;

		f.open("student.dat",ios::in|ios::binary);

		while(f.read((char*)&stu,sizeof(stu))){
			if(stu.id == id){
				cout<<"ID: "<<stu.id<<endl;
				cout<<"Name: "<<stu.name<<endl;
				cout<<"Branch: "<<stu.branch<<endl;
				cout<<"Location: "<<stu.location<<endl;

				flag=1;
			}
		}

		if(flag==0){
			cout<<"No record found with given id"<<endl;
		}

		f.close();
	}
};

int main(){

	int choice,id;
	Student s;

	while(choice!=3){

		cout<<endl<<"------------Menu-------------"<<endl;
		cout<<"1. Enter student detail"<<endl<<"2. Find Student"<<endl<<"3. Exit"<<endl;

		cout<<"Enter your choice: ";
		cin>>choice;

		try {
			if(choice>3){
				throw choice;
			}
			else{
				switch(choice)
				{
					case 1:
					s.adddata();
					break;
					case 2:
					cout<<"Enter id to find: ";
					cin>>id;
					s.findbyid(id);
					break;
					case 3:
					exit(0);
				}
			}
		}
		catch(int choice)
		{
			cout<<"Exception: choice not matched"<<endl;
		}
	}

	return 0;
}
