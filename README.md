//实现以逗号分隔数字的字符串向数字转换功能
#include <iostream>
#include <sstream>
#include <string>
#include <vector>
#include <istream>

using namespace std;
//space函数把所有逗号变成' '空格符
string space(string &s){
    for(auto &c : s){
        if(c == ','){
            c = ' ';
        }
    }
    return s;
}

//tran函数把字符串s中的数字逐个导入到向量vec中
void tran(string &s, vector<double> &vec){
    space(s);//space函数把所有逗号变成' '空格符
    stringstream ss;
    double num = 0;
    double temp = 0;
    int flag = 1;
    for(auto c : s){
        if(flag == 1){
            if(c != ' '){
                ss << c;
                ss >> temp;
                ss.clear();
                num = (num*10)+temp; 
            }
            if(c == ' '){
                flag = 0;
            }
        }

        if(flag == 0){//把num输出到向量，并重新置零
            flag = 1;
            vec.push_back(num);
            num = 0;
        }
    }
    vec.push_back(num);
}
//测试用的主函数
int main(){
    vector<double> vec;
    string s("11,22,33,44,55");
    tran(s, vec);
    vector<double>::size_type size = vec.size();
    int i = 0;
    while(i < size){
        cout << vec[i] << endl;
        i++;
    }
    system("pause");
}
