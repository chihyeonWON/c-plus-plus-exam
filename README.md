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
```
#include <iostream>
using namespace std;

class Line {
private:
	int* ptr; // 선의 길이를 저장한다.
public:
	int getLength();
	Line(int len);
	Line(const Line& other); // 복사 생성자
	~Line();
};

// 일반 생성자
Line::Line(int len) {
	cout << "일반 생성자" << endl;
	ptr = new int;
	*ptr = len;
}

// 복사 생성자
Line::Line(const Line& other)
{
	cout << "복사 생성자" << endl;
	this->ptr = new int;
	*ptr = *other.ptr;
}


// default 소멸자
Line::~Line() {
	delete[] ptr;
}

// 선의 길이 접근자 함수 getLength
int Line::getLength() {
	return *ptr;
}

int main()
{
	Line line(10); // 일반 생성자 호출
	Line clone1(line); // 복사 생성자 호출
	Line clone2(clone1); // 복사 생성자 호출
	cout << "선의 길이: " << clone2.getLength() << endl;
	Line clone3(clone2); // 복사 생성자 호출
	cout << "선의 길이: " << clone3.getLength() << endl; 

	return 0;
}
```

```
#include <iostream>
#include <string.h>
using namespace std;

class MyClass {
private:
	char* stored;
public:
	MyClass(const char* str); // 일반 생성자
	MyClass(const MyClass& other); // 복사 생성자
	~MyClass(); // 일반 소멸자
	void print() {
		cout << stored << endl;
	}
};

// 일반 생성자
MyClass::MyClass(const char* str) {
	cout << "일반 생성자 테스트" << endl;
	stored = new char[strlen(str) + 1];
	strcpy(stored, str);
}

// 복사 생성자 정의
MyClass::MyClass(const MyClass& other) {
	cout << "복사 생성자 테스트" << endl;
	this->stored = new char[strlen(other.stored) + 1];
	strcpy(stored, other.stored);
}

// 일반 소멸자
MyClass::~MyClass() {
	delete[] stored;
}

int main()
{
	MyClass myclass("원치현"); // 일반 생성자 호출
	MyClass clone(myclass); // 복사 생성자 호출

	clone.print();


	return 0;
}

```
