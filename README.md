#include <iostream>
#include<fstream>
#include <string>
#include<cstdlib>
#include<time.h>
#include<stdio.h>

using namespace std;
int main()
{
    class pytanie
    {
    	public:
    	string tresc;
    	string a,b,c,d;
    	int nr_pytania;
    	string poprawna;
    	string udzielona;
    	int punkt;

	void  wczytaj()
	{
	fstream plik;
	plik.open("quiz pytania.txt",ios::in);
	if(plik.good()==false)
	{
		cout<<"NIE UDALO SIE ODNALEZC PLIKU ";
		exit(0);
	}
	int nr_linii=(nr_pytania-1)*6+1;
	int aktualnynr=1;
	string linia;
	while ( getline(plik,linia))
	{
		if(aktualnynr==nr_linii)  tresc=linia;
		if(aktualnynr==nr_linii+1)  a=linia;
		if(aktualnynr==nr_linii+2)  b=linia;
		if(aktualnynr==nr_linii+3)  c=linia;
		if(aktualnynr==nr_linii+4)  d=linia;
		if(aktualnynr==nr_linii+5)  poprawna=linia;
		aktualnynr++;
	}
plik.close();
	}

	void zapytaj()
	{
		cout<<endl<<tresc<<endl;
		cout<<a<<endl;
		cout<<b<<endl;
		cout<<c<<endl;
		cout<<d<<endl;
