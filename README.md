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

```
#include <iostream>
#include <string.h>
using namespace std;

class Point {
private:
	double xval, yval;
public:
	Point(double x = 0.0, double y = 0.0) {
		xval = x;
		yval = y;
	}
	double getX() { return xval; } // xval 접근자
	double getY() { return yval; } // yval 접근자
	void swap(Point &p1, Point &p2);
	void print() {
		cout << "(" << xval << "," << yval << ")" << endl;
	}
};

// 두 개의 Point 객체를 교환하는 swap() 함수
void Point::swap(Point& p1, Point& p2) {
	Point temp;
	temp = p1;
	p1= p2;
	p2= temp;
}

int main()
{
	Point p1(1.2, -2.8); // Point 객체 p1 생성
	Point p2(3.4, 5.6); // Point 객체 p2 생성
	swap(p1, p2); // Point p1와 p2를 서로 교환
	p1.print(); // p1의 내용 출력 p1(3.4, 5.6)
	p2.print(); // p2의 내용 출력 p2(1.2, -2.8)
	return 0;
}
```

```
#include <iostream>
#include <string.h>
using namespace std;

class Box {
private:
	double length;
	double width;
	double height;
public:
	static int count; // 정적 변수 count 선언
	Box(double l = 2.0, double w = 2.0, double h = 2.0) {
		length = l;
		width = w;
		height = h;
		count++; // 객체가 생성될 때마다 count를 1증가
	}
	double Volume() {
		return length * width * height;
	}
};

int Box::count = 0;

int main()
{
	Box box1(10, 20, 30); // box 객체 box1 생성
	Box box2(40, 50, 60); // box 객체 box2 생성

	cout << "전체 객체 수: " << Box::count << endl; // 생성된 객체 수를 출력

	return 0;
}
```
```
#include <iostream>
#include <string>
using namespace std;

class Box {
private:
	double length;
	double width;
	double height;
public:
	Box(int l = 0, int w = 0, int h = 0) : length(l), width(w), height(h) { }
	double getVolume(void)
	{
		return length * width * height;
	}
	// + 연산자에 대한 중복 정의
	Box operator+(const Box& b2);
	void print() {
		cout << "상자의 길이: " << length << endl;
		cout << "상자의 너비: " << width << endl;
		cout << "상자의 높이: " << height << endl;
		cout << "상자의 부피: " << getVolume() << endl;
	}
};

Box Box::operator+(const Box& b2) {
	Box b;
	b.length = this->length + b2.length;
	b.width = this->width + b2.width;
	b.height = this->height + b2.height;
	return b;
}

int main()
{
	Box a(10, 10, 10), b(20, 20, 20), c;

	c = a + b;

	cout << "상자 #1" << endl;
	a.print();
	cout << endl;

	cout << "상자 #2" << endl;
	b.print();
	cout << endl;

	cout << "상자 #3" << endl;
	c.print();

	return 0;
}
```
```
#include <iostream>
#include <string>
using namespace std;

class Box {
private:
	double length;
	double width;
	double height;
	double volume = length * width * height;
public:
	Box(int l = 0, int w = 0, int h = 0) : length(l), width(w), height(h) { }
	// + 연산자에 대한 중복 정의
	Box operator+(const Box& b2);
	// == 연산자에 대한 중복 정의
	bool operator==(Box& b2) {
		return this->volume == b2.volume;
	};
	// < 연산자에 대한 중복 정의
	bool operator<(Box& b2) {
		return this->volume < b2.volume;
	}
	friend void printBox(Box box);
};

void printBox(Box box) {
	cout << "상자의 길이: " << box.length << endl;
	cout << "상자의 너비: " << box.width << endl;
	cout << "상자의 높이: " << box.height << endl;
	cout << "상자의 부피: " << box.volume << endl;
}

Box Box::operator+(const Box& b2) {
	Box b;
	b.length = this->length + b2.length;
	b.width = this->width + b2.width;
	b.height = this->height + b2.height;
	return b;
}


int main()
{
	Box a(10, 10, 10), b(20, 20, 20), c;

	c = a + b;

	cout << "상자 #1" << endl;
	printBox(a);
	cout << endl;

	cout << "상자 #2" << endl;
	printBox(b);
	cout << endl;

	cout << boolalpha;
	cout << (a < b);


	return 0;
}

프렌드 함수는 클래스 안에 있지만 안에있는게아닌 그니까 밖에다가 정의해야되고 정의할때도 클래스:: 안써줘도됌
```

```
#include <iostream>
#include <string>
using namespace std;

class Shape {
private:
	int x; // x 위치
	int y; // y 위치
	string color; // 색상
public:
	// 생성자 정의
	Shape(int x = 0, int y = 0, string color = "") {
		this->x = x;
		this->y = y;
		this->color = color;
	}
	//x 멤버변수에 대한 접근자
	int getX() { return x; }
	//x 멤버변수에 대한 설정자
	void setX(int x) { this->x = x; }
	//y 멤버변수에 대한 접근자
	int getY() { return y; }
	//y 멤버변수에 대한 설정자
	void setY(int y) { this->y = y; }

	double getArea() {
		return x * y;
	}

};

class Circle : public Shape {
private:
	int radius;
public:
	Circle(int x = 0, int y = 0, string color = "", int radius = 0) : Shape(x, y, color) {
		this->radius = radius;
	}
	double getArea() {
		return 3.14 * radius * radius;
	}
};

int main()
{
	Circle c(3, 4, "yellow", 4);

	cout << "중심점 X가 " << c.getX() << "중심점 Y가 " << c.getY() << "인 원의 면적은" << c.getArea();

	return 0;
}
```
```
#include <iostream>
#include <string>
using namespace std;

class Employee {
private:
	string name; // 이름
	int salary; // 월급
public:
	// 생성자 정의
	Employee(string name = "", int salary = 0) {
		this->name = name;
		this->salary = salary;
	}
	//name 멤버변수에 대한 접근자
	string getName() { return name; }
	//name 멤버변수에 대한 설정자
	void setName(string n) { name = n; }
	//salary 멤버변수에 대한 접근자
	int getSalary() { return salary; }
	//salary 멤버변수에 대한 설정자
	void setSalary(int s) { salary = s; }
	int computeSalary() { // 3-1 월급을 계산하는 멤버함수 computeSalary()
		return salary;
	}

};

class Manager : public Employee {
private:
	int bonus; // 보너스
public:
	// 생성자 정의
	Manager(string name, int salary, int bonus) : Employee(name, salary) {
		this->bonus = bonus;
	}
	// bonus 멤버 변수에 대한 접근자
	int getBonus() { return bonus; }
	// bonus 멤버 변수에 대한 설정자
	void setBonus(int b) { bonus = b; }
	// 3-2 부모 클래스의 computeSalary()를 재정의하여 (salary+bonus) 반환
	int computeSalary() {
		return getSalary() + bonus;
	}
};

int main()
{
	Manager a("김철수", 200, 100);

	cout << "이름: " << a.getName() << endl;
	cout << "월급: " << a.getSalary() << endl;
	cout << "보너스: " << a.getBonus() << endl;
	cout << "전체 급여: " << a.computeSalary() << endl;

	return 0;
}
```
```
#include <iostream>
#include <string>
using namespace std;

class Weapon {
public:
	virtual void load() = 0;
};

class Bomb : public Weapon {
public:
	void load() {
		cout << "나는 밤을 적재" << endl;
	}
};

class Gun : public Weapon {
	void load() {
		cout << "나는 건을적재" << endl;
	}
};

int main()
{
	Weapon* weapon = new Bomb[5];
	weapon->load();
	Weapon* weapon2 = new Gun[2];
	weapon2->load();

	return 0;
}
```
```
정리해보자면 소멸자도 부모에 가상소멸자안해주면 자식클래스소멸자 호출안됨 그래서
부모클래스에 가상 소멸자를 만들어줘야 자식클래스가 소멸함


```
