
# 官方

`header <fstream>` http://www.cplusplus.com/reference/fstream/
- **Classes**
  * std::ifstream http://www.cplusplus.com/reference/fstream/ifstream/
  * std::ofstream http://www.cplusplus.com/reference/fstream/ofstream/
  * std::fstream http://www.cplusplus.com/reference/fstream/fstream/

std::ifstream http://www.cplusplus.com/reference/fstream/ifstream/
- **Public member functions**
  * std::ifstream::open http://www.cplusplus.com/reference/fstream/ifstream/open/
- **Public member functions inherited from `istream`**
  * std::istream::getline http://www.cplusplus.com/reference/istream/istream/getline/

std::fstream http://www.cplusplus.com/reference/fstream/fstream/
- **Public member functions**
  * std::fstream::open http://www.cplusplus.com/reference/fstream/fstream/open/
- **Public member functions inherited from `ostream`**
  * std::ostream::flush https://www.cplusplus.com/reference/ostream/ostream/flush/

# `.open()`

std::fstream::open https://www.cplusplus.com/reference/fstream/fstream/open/
```cpp
// fstream::open / fstream::close
#include <fstream>      // std::fstream

int main () {
  std::fstream fs;
  fs.open ("test.txt", std::fstream::in | std::fstream::out | std::fstream::app);
  fs << " more lorem ipsum";
  fs.close();
  return 0;
}
```

# `.flush()`

std::ostream::flush https://www.cplusplus.com/reference/ostream/ostream/flush/
```cpp
// Flushing files
#include <fstream>      // std::ofstream

int main () {
  std::ofstream outfile ("test.txt");
  for (int n=0; n<100; ++n)
  {
    outfile << n;
    outfile.flush();
  }
  outfile.close();
  return 0;
}
```

# 其他

C++ 文件和流 https://www.runoob.com/cplusplus/cpp-files-streams.html

C++ 文件和流 https://www.cnblogs.com/linuxAndMcu/p/10396531.html

C++文件读写详解（ofstream,ifstream,fstream) https://www.cnblogs.com/codingmengmeng/p/5545042.html

# 个人实战

## 读csv

C++ 读取.csv文件 https://www.jianshu.com/p/1172e2de7a7a
- 文章原版，甚至都有错误（没有包含`<vector>`）——而更大的问题在于这个版本分隔符只能处理逗号，csv里的数据一旦复杂点就读不完全了。。。
```cpp
#include <fstream>
#include <string>
#include <sstream>

int main(){
    vector<vector<int>> user_arr;
    ifstream fp("xxx/user_data.csv"); //定义声明一个ifstream对象，指定文件路径
    string line;
    getline(fp,line); //跳过列名，第一行不做处理
    while (getline(fp,line)){ //循环读取每行数据
        vector<int> data_line;
        string number;
        istringstream readstr(line); //string数据流化
        //将一行数据按'，'分割
        for(int j = 0;j < 11;j++){ //可根据数据的实际情况取循环获取
            getline(readstr,number,','); //循环读取数据
            data_line.push_back(atoi(number.c_str())); //字符串传int
        }
        user_arr.push_back(data_line); //插入到vector中
    }
    return 0;
}
```
- 个人修改后的版本（参考了这个链接：https://stackoverflow.com/questions/236129/how-do-i-iterate-over-the-words-of-a-string 核心思想就是自己不处理分隔符了，完全让 `istringstream` 来处理）
```cpp
#include <fstream>
#include <string>
#include <sstream>
#include <vector>
#include <iostream>
using namespace std;

int main(){
    vector<vector<float>> user_arr;
    ifstream fp("YYY.csv"); //定义声明一个ifstream对象，指定文件路径
	  std::cout << "Using YYY.csv" << std::endl;
    string line;
    ////getline(fp,line); //跳过列名，第一行不做处理
    while (getline(fp,line)){ //循环读取每行数据
        vector<float> data_line;
        string number;
        istringstream readstr(line); //string数据流化
        //将一行数据按'，'分割
        // for(int j = 0;j < 3;j++){ //可根据数据的实际情况取循环获取
        //     getline(readstr,number); //循环读取数据
        //     data_line.push_back(atoi(number.c_str())); //字符串传int
        // }

		    while (!readstr.eof()) {
			      readstr >> number;
			      data_line.push_back(atof(number.c_str()));
		    }
        user_arr.push_back(data_line); //插入到vector中
    }
	  for (auto vec : user_arr) {
		    for (auto elem : vec) {
			      std::cout << "The elem is: " << elem << std::endl;
		    }
	  }
    return 0;
}
//////////////////////////////////////////////////
$ g++ -g -o main main.cpp
$ ./main
Using YYY.csv
The elem is: 1.5
The elem is: 2
The elem is: 3.66
The elem is: 4
The elem is: 5
The elem is: 66.666
The elem is: 77
The elem is: 8
The elem is: 9999
$
```
//notes：注意，需要在程序当前目录下放一个 `YYY.csv`，里面随便写点数字如下：
```csv
1.5 2   3.66
4 5 66.666
77.0 8           9999
```
>> //notes：其实核心的点就是两重循环，并且还可以在这两重循环里加个变量分别统计行数和列数，其他类似的实现包括：
- Getting the number of columns and rows of a .csv file in C++ https://stackoverflow.com/questions/23042707/getting-the-number-of-columns-and-rows-of-a-csv-file-in-c || 在C++中获取.csv文件的列数和行数 https://www.coder.work/article/3224093
- C++从txt文件读取数据保存为二维数组 https://blog.csdn.net/qq_22080999/article/details/82532157

## 写csv

C/C++读写csv文件 https://blog.csdn.net/u012234115/article/details/64465398
```cpp
#include <string>
#include <vector>
#include <fstream>
using namespace std;

void persistent_2dvector(vector<vector<float>>& test_data) {
	std::string file_path = "./persist-result.csv";
	ofstream outFile;
	outFile.open(file_path, ios::out);
	for (int i = 0; i < test_data.size(); ++i) {
		for (int j = 0; j < test_data[0].size(); ++j) {
			if (j != test_data[0].size() - 1) {
				outFile << test_data[i][j] << ',';
			} else {
				outFile << test_data[i][j];
			}
		}
		outFile << std::endl;
	}
  outFile.close();
}

int main()
{
	vector<vector<float>> test_data(3, vector<float>(2, 6.66));
	persistent_2dvector(test_data);
	return 0;
}
//////////////////////////////////////////////////
$ g++ write_to_csv.cpp -o write_to_csv
$ ./write_to_csv
$ cat persist-result.csv
6.66,6.66
6.66,6.66
6.66,6.66
```
