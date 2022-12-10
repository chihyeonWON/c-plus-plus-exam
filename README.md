# c-plus-plus-exam
시험범위 코드 정리

```
#include <iostream>

using namespace std;

int main()
{
	int number;

	cout << "몇 개의 정수를 입력합니까? ";
	cin >> number;

	int* p = new int[number];

	for (int i = 0; i < number; i++) {
		cout << "정수를 입력하시오 : ";
		cin >> p[i];
	}

	cout << "입력된 정수는: ";
	for (int i = 0; i < number; i++)
		cout << p[i] << ", ";
	cout << endl;

	delete[] p;

	return 0;
}
```

```
#include <iostream>
#include <string>

using namespace std;

class Student {
private:
	string name; // 학생 이름
public:
	Student(string name = "") :name{ name } {}
	string getName() { return name; }
	void setName(string name) { this->name = name; }
};

class MyClass {
private:
	string className;
	Student* p;
	int size;
public:
	// 이름 설정자
	void setName(string name) { className = name; }
	// 이름 접근자
	string getName() { return className; }
	// 학생 설정자
	void setStudent() { p = new Student[size]; }
	// 학생 접근자
	Student* getStudent() { return p; }
	// 학생 수 설정자
	void setSize(int size) { this->size = size; }
	// 학생 수 접근자
	int getSize() { return size; }
};

int main()
{
	MyClass* special = new MyClass[3]; // 학생 수가 3명인 학급 "special"을 생성

	special->setName("special");
	special->setSize(3);
	special->setStudent();

	special->getStudent()[0].setName("홍길동"); // =(*p).setName("홍길동");
	special->getStudent()[1].setName("김철수"); // =(*p).setName("김철수");
	special->getStudent()[2].setName("최자영"); // =(*p).setName("최자영");

	cout << "학급 " << special->getName() << "의 학생들은 다음과 같다." << endl;
	for (int i = 0; i < special->getSize(); i++)
		cout << "학생 #" << i + 1 << ": " << special->getStudent()[i].getName() << endl;

	delete[] special->getStudent();
	delete[] special;

	return 0;
}
```
