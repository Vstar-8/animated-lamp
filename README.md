# vstar
week_1_homework
#include<iostream>
#include<vector>
#include<fstream>
#include<algorithm>
#include <iomanip>
using namespace std;
void shanchu();
void xiugai();
void chaxun();
void xianshi(); 
void xiehui();
void tianjia(); 
void duqu_stu();
void out();
void choice();
void show();
class Stu{
	public:
		string name;
		int num;
		int score;
};
bool cmp1(Stu s1,Stu s2){
	return s1.num<s2.num;
}
bool cmp2(Stu s1,Stu s2){
	return s1.score>s2.score;
}
vector<Stu> list;
//删除学生信息
void shanchu(){
	system("cls");
	duqu_stu();
	cout<<"<删除学生信息>"<<endl;
	cout<<"请输入你要删除的学号"<<endl;
	bool fg=false;
	int n;cin>>n;
	system("cls");
	for(int i=0;i<list.size();i++){
		if(list[i].num==n){
			fg=true; 
			list.erase(list.begin()+i); 
			xiehui();
			system("cls");
			cout<<"删除成功！"<<endl;
		}
	}
	if(fg==false){
		cout<<"没有找到该学号的信息"<<endl;
	}
	system("pause");
	list.clear();
} 
//修改学生信息
void xiugai(){
	system("cls");
	duqu_stu();
	cout<<"<修改学生信息>"<<endl;
	cout<<"请输入你要修改的学号"<<endl;
	bool fg=false;
	int n;cin>>n;
	system("cls");
	for(int i=0;i<list.size();i++){
		if(list[i].num==n){
			fg=true;
			if(fg==true){
			system("cls");
		    cout<<"请输入你要修改的信息"<<endl;
		    cout<<"1.姓名"<<endl;
		    cout<<"2.学号"<<endl;
		    cout<<"3.成绩" <<endl;
		    int m;cin>>m;
		    if(m==1){
		    	system("cls");
		    	cout<<"请输入新的姓名:"<<endl;
		    	cin>>list[i].name;
		    }
		    if(m==2){
		    	system("cls");
		    	cout<<"请输入新的学号:"<<endl;
		    	cin>>list[i].num;
			}
			if(m==3){
				system("cls");
				cout<<"请输入新的成绩"<<endl;
				cin>>list[i].score;
			}
			xiehui();
			system("cls");
			cout<<"修改成功！"<<endl;
	      }
		}
	} 
	if(fg==false) cout<<"没有找到该学号的信息"<<endl;
	system("pause");
	list.clear();
} 
//查询学生信息
void chaxun(){
	system("cls");
	duqu_stu();
	cout<<"<查询学生信息>"<<endl;
	cout<<"请输入你要查询的内容"<<endl;
	cout<<"1.学号"<<endl;
	cout<<"2.姓名"<<endl;
	int n;cin>>n;
	bool fg=false;
	system("cls");
	if(n==1){
		cout<<"请输入你要查询的学号"<<endl; 
		int num=0;cin>>num;
		system("cls");
		for(int i=0;i<list.size();i++){
			if(num==list[i].num){
				fg=true;
				cout<<setw(10) <<left<<"姓名"<<setw(10) <<left<<"学号"<<setw(10) <<left<<"成绩"<<endl;
				cout<<setw(10) <<left<<list[i].name<<setw(10) <<left<<list[i].num<<setw(10) <<left<<list[i].score<<endl;
			}
		}
		if(fg==false) cout<<"没有查到该学号的信息"<<endl; 
	}
	if(n==2){
		cout<<"请输入你要查询的姓名"<<endl; 
		string name;cin>>name;
		system("cls");
		for(int i=0;i<list.size();i++){
			if(name==list[i].name){
				fg=true;
				cout<<setw(10) <<left<<"姓名"<<setw(10) <<left<<"学号"<<setw(10) <<left<<"成绩"<<endl;
				cout<<setw(10) <<left<<list[i].name<<setw(10) <<left<<list[i].num<<setw(10) <<left<<list[i].score<<endl;
			}
		}
		if(fg==false) cout<<"没有查到该姓名的信息"<<endl; 
	}
	system("pause");
	list.clear();
}
//求平均分 
double av(){
	int sum=0;int n=list.size();
	for(int i=0;i<list.size();i++){
		sum+=list[i].score;
	} 
	double avg=sum/n;
	return avg;
}
//求最高分
int h(){
	sort(list.begin(),list.end(),cmp2);
	return list[0].score;
} 
//求最低分
int l(){
	sort(list.begin(),list.end(),cmp2);
	int i=list.size();
	return list[i-1].score;
} 
//显示学生信息
void xianshi(){
	system("cls");
	cout<<"<显示学生信息>"<<endl; 
	duqu_stu();
	cout<<"1.按学号排序"<<endl;
	cout<<"2.按成绩排序"<<endl; 
	int n;cin>>n;
	system("cls");
	if(n==1){
		sort(list.begin(),list.end(),cmp1);
		cout<<setw(10) <<left<<"姓名"<<setw(10) <<left<<"学号"<<setw(10) <<left<<"成绩"<<endl;
		for(int i=0;i<list.size();i++){
			cout<<setw(10) <<left<<list[i].name<<setw(10) <<left<<list[i].num<<setw(10) <<left<<list[i].score<<endl;
		}
	}
	if(n==2){
		sort(list.begin(),list.end(),cmp2);
		cout<<setw(10) <<left<<"姓名"<<setw(10) <<left<<"学号"<<setw(10) <<left<<"成绩"<<endl;
		for(int i=0;i<list.size();i++){
			cout<<setw(10) <<left<<list[i].name<<setw(10) <<left<<list[i].num<<setw(10) <<left<<list[i].score<<endl;
		}
	}
	cout<<".................."<<endl;
	cout<<"平均分:"<<av()<<endl;
	cout<<"最高分:"<<h()<<endl;
	cout<<"最低分:"<<l()<<endl; 
	system("pause");
	list.clear();
} 
//写回函数
void xiehui(){
	ofstream fout("student.txt",ios::out);
	for(int i=0;i<list.size();i++){
		fout<<list[i].name<<" "
		    <<list[i].num<<" "
		    <<list[i].score<<" "
		    <<endl;
	}
	fout.close();
} 
//添加学生信息
void tianjia(){
	duqu_stu();
	system("cls");
	Stu t;
	cout<<"<<添加学生信息>>"<<endl;
	cout<<"请输入学生姓名"<<endl; cin>>t.name;
	cout<<"请输入学生学号"<<endl; cin>>t.num;
	cout<<"请输入学生成绩"<<endl; cin>>t.score;
	list.push_back(t);
	cout<<"添加成功"<<endl;
	system("pause"); 
	xiehui();
	list.clear();
	
} 
//读取文件 
void duqu_stu(){
	ifstream fin("student.txt",ios::in);
	if(!fin){
		cout<<"文件打开失败！"<<endl;
		exit(1); 
	}
	Stu t;
	while(fin>>t.name>>t.num>>t.score){
		list.push_back(t);
	}
	fin.close();
}
//主界面 
void show(){
	while(1){
	cout<<"1.添加学生信息"<<endl;
	cout<<"2.查询学生信息"<<endl;
	cout<<"3.修改学生信息"<<endl;
	cout<<"4.删除学生信息"<<endl;
	cout<<"5.显示所有学生信息"<<endl; 
	cout<<"0.一键退出"<<endl; 
	while(1){
		int n;cin>>n;
		if(n==1){
			tianjia();
			system("cls");
			break;
		}
		if(n==2){
			chaxun();
			system("cls");
			break;
		} 
		if(n==3){
			xiugai();
			system("cls");
			break;
		}
		if(n==4){
			shanchu();
			system("cls");
			break;
		}
		if(n==5){
			 xianshi();
			 system("cls");
			break;
		}
		if(n==0){
			out();
		}
		
	}
    }
}
//一键退出函数 
void out(){
	system("cls");
	cout << "走好不送喵~" << endl;
	exit(0);
	system("pause");
}
int main(){
	show();
}
