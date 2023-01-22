#ifndef Lol
#define Lol
#include <iostream>
#include <stdlib.h>
using namespace std;
int min(int a, int b);
class Hare;
class Zver;
class Wolf;
class Dinamic
{
protected:
	Zver **v;
	int len, n1, n2;

public:
	Dinamic(int N1, int N2);
	Dinamic(const Dinamic& A);
	~Dinamic();
	int resize(int N1, int N2);
	void insertW(Wolf d);
	void insertH(Hare d);
	Zver* & operator [] (int index);
	Zver* operator [] (int index) const;
	void show();
	friend class Zver;
	friend class Wolf;
	friend class Hare;


	int getlen();
	void eraseW(int n);
	void eraseH(int n);

};
class Zver {
protected:
	int x, y, life, satiety;
public:
	Zver(int a, int b);
	virtual ~Zver();
	virtual void move() = 0;
	virtual void destroy(Dinamic& arr, int& k) = 0;
	virtual char show() = 0;
	int getx();
	int gety();
	virtual void eat(Dinamic& ar) = 0;
	virtual int kto() = 0;
	virtual void born(Dinamic& ar) = 0;
	friend class Dinamic;
};
class Wolf : public Zver {
public:
	Wolf(int a = rand() % 25, int b = rand() % 80);
	virtual	~Wolf() {};
	void move();
	void eat(Dinamic& ar);
	void destroy(Dinamic& arr, int& k);
	char show();
	void born(Dinamic& ar) { life++; };
	int kto();
	friend class Dinamic;
};
class Hare : public Zver {
public:
	Hare(int a = rand() % 25, int b = rand() % 80);
	virtual ~Hare() {};
	void move();
	void destroy(Dinamic& arr, int& k);
	friend class Dinamic;
	void born(Dinamic& arr);
	char show();

	int kto();
	void eat(Dinamic& ar);

};



#endif
#include "Head.h"
int min(int a, int b) {
	if (a > b) return b; else return a;
}
Dinamic::~Dinamic() {
	for (int i = 0; i < len; i++)
		delete v[i];
	delete[] v;

}
void Dinamic::insertW(Wolf d)
{

	resize(n1 + 1, n2);
	*v[n1 - 1] = d;
}
void Dinamic::insertH(Hare d)
{

	resize(n1, n2 + 1);
	*v[n2 - 1] = d;
}
Dinamic::Dinamic(const Dinamic& A)
{
	v = A.v;
	for (int i = 0; i < len; i++)
		v[i] = A.v[i];
	n1 = A.n1;
	n2 = A.n2;
	len = A.len;

}


Zver* & Dinamic::operator [] (int index)
{
	return v[index];
}
Zver* Dinamic::operator [] (int index) const
{
	return v[index];
}

int Dinamic::getlen() { return len; }
void Dinamic::eraseW(int n)
{
	for (int i = n; i < len - 1; i++)
	{
		*v[i] = *v[i + 1];
	}
	resize(n1 - 1, n2);

}
void Dinamic::eraseH(int n)
{
	for (int i = n; i < len - 1; i++)
	{
		*v[i] = *v[i + 1];
	}
	resize(n1, n2 - 1);

}



Zver::Zver(int a = rand() % 25, int b = rand() % 80) : x(a), y(b), life(0), satiety(0) {}

int Zver::getx() { return x; }
int Zver::gety() { return y; }
Zver::~Zver() {  }



Wolf::Wolf(int a, int b) : Zver(a, b) {}
void Wolf::move() {
	int r;
	for (int i = 0; i < 2; i++) {
		r = rand() % 4;
		switch (r) {
		case 0: x++; break;
		case 1: x--; break;
		case 2: y++; break;
		case 3: y--; break;
		}
		if (y == 80) y = 0;
		if (y == -1) y = 79;
		if (x == 25) x = 0;
		if (x == -1) x = 24;
	}

}

void Wolf::eat(Dinamic &ar) {
	for (int i = 0; i < ar.getlen(); i++) {
		if (ar[i]->kto() && (x == ar[i]->getx()) && (y == ar[i]->gety())) {
			satiety++;
			ar.eraseH(i);
			if (satiety == 5) {
				Wolf w;
				w.x = x; w.y = y;
				ar.insertW(w);
				satiety = 0;
			}
		}
	}
}
int Wolf::kto() { return 0; }
void Wolf::destroy(Dinamic& arr, int& k) {

	if (life == 20) {
		arr.eraseW(k);
		k--;
	}
}
char Wolf::show() { return '#'; }





Hare::Hare(int a, int b) : Zver(a, b) {}
void Hare::move() {
	int r;
	for (int i = 0; i < 1; i++) {
		r = rand() % 4;
		switch (r) {
		case 0: x++; break;
		case 1: x--; break;
		case 2: y++; break;
		case 3: y--; break;
		}
	}
	if (y == 80) y = 0;
	if (y == -1) y = 79;
	if (x == 25) x = 0;
	if (x == -1) x = 24;
}
void Hare::destroy(Dinamic& arr, int &k) {

	if (life == 10) {	arr.eraseH(k);
	k--; }
}

void Hare::born(Dinamic& arr) {
	life++;
	if (life % 5 == 0 && life != 0) {
		Hare r;
		r.x = x; r.y = y;
		arr.insertH(r);
	}
}
char Hare::show() { return '*'; }

int Hare::kto() { return 1; }
void Hare::eat(Dinamic& ar) {}

void Dinamic::show()
{
	char screen[25][80];
	for (int i = 0; i<25; i++)
		for (int j = 0; j < 80; j++)
			screen[i][j] = ' ';
	for (int i = 0; i < len; i++)
		screen[(v[i])->getx()][(v[i])->gety()] = (v[i])->show();
	for (int i = 0; i < 25; i++) {
		for (int j = 0; j < 80; j++)
			cout << screen[i][j];
		cout << endl;


	}
	cout << flush;
}
Dinamic::Dinamic(int N1 = 0, int N2 = 0) : v(0), len(0), n1(0), n2(0)  //конструктор
{

	v = new Zver*[N1 + N2];
	for (int i = 0; i < N1; i++)
		v[i] = new Wolf;
	for (int i = 0; i < N2; i++)
		v[i + N1] = new Hare;

	if (v) len = N1 + N2;
	n1 = N1;
	n2 = N2;

}
int Dinamic::resize(int N1, int N2)
{

	Zver **p = new Zver*[N1 + N2];
	for (int i = 0; i < N1; i++)
		p[i] = new Wolf;
	for (int i = 0; i < N2; i++)
		p[i + N1] = new Hare;
	if (!p) return len;

	for (int i = 0; i < min(N1, n1); i++)
	{
		p[i] = v[i];
		v[i] = nullptr;
	}
	for (int i = 0; i < min(N2, n2); i++)
	{
		p[i + N1] = v[i + n1];
		v[i + n1] = nullptr;
	}
	for (int i = 0; i < len; i++)
		delete v[i];
	delete[] v;
	v = 0;
	v = p;
	len = N1 + N2;
	n1 = N1;
	n2 = N2;
	return len;
}
#include "Head.h"

int main()
{
	int k = 0;;

	Dinamic B(10, 10);
	while (1) {
		for (int i = 0; i < B.getlen(); i++)
			B[i]->move();
		for (int i = 0; i < B.getlen(); i++)
		{
			B[i]->born(B);
			B[i]->eat(B);

			B[i]->destroy(B, i);

		}

		B.show();
		k++;
		
	}

	system("pause");
	return 0;

}
