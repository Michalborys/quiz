	#include <iostream>
	#include<fstream>
	#include <string>
	#include<cstdlib>
	#include<time.h>
	#include<stdio.h>

	using namespace std;

    class pytanie /*klasa pytanie*/
    {
            public:
        	string poprawna[47];    /*zmienna przetrzymujaca prawidlowe odpowiedzi do pytania*/
            string udzielona;       /*zmienna przetrzymujaca odpowiedz udzielona przez uzytkownika*/
            string tresc[47];       /*zmienna - tresc pytania*/
            string a[47],b[47],c[47],d[47]; /*odpowiedzi do pytan*/
            int nr_pytania;         /*zmienna pomocnicza numer pytania*/
            const int liczba_pytan = 47;
            int wczytane;           /*pierwsze wczytane pytanie bedzie mialo zerowy indeks*/
            int ile_juz_wylosowano;
            bool losowanie_ok;
            pytanie()
            {
                wczytane = 0;
                ile_juz_wylosowano = 0;
            }
	void  wczytaj() /*funkcja w klasie wczytujaca pytania z pliku tekstowego*/
	{
            fstream plik;
            plik.open("quiz pytania.txt",ios::in);
            if(plik.good() == false)
            {
            cout<<"NIE UDALO SIE ODNALEZC PLIKU ";
            exit(0);
            }
            int nr_linii = (nr_pytania-1)*6+1; /*kazde pytanie zajmuje w pliku tekstowym 6 linii, nr linii od ktorej czytamy kolejne pytania*/
            int aktualnynr = 1;/*zmienna typu calkowitego -pomocnicza, zaczynamy od nr 1 gdyz tak zaczyna sie w pliku tekstowym, taki mozna powiedziec licznik*/
            string linia;
            while ( getline(plik,linia))
            {
                if(aktualnynr == nr_linii)        tresc[wczytane] = linia;/*tresc pytania*/
                if(aktualnynr == nr_linii+1)      a[wczytane] = linia;/*nr linii o 1 wiekszy- odpowiedz a*/
                if(aktualnynr == nr_linii+2)      b[wczytane] = linia;
                if(aktualnynr == nr_linii+3)      c[wczytane] = linia;
                if(aktualnynr == nr_linii+4)      d[wczytane] = linia;
                if(aktualnynr == nr_linii+5)      poprawna[wczytane] = linia;
                ++aktualnynr;
            }
            plik.close();/*zamkniecie pliku tekstowego*/
	}

	void zapytaj()/*funkcja w klasie drukujaca pytanie na ekranie*/
	{
            cout<<endl<<tresc[wczytane]<<endl;
            cout<<a[wczytane]<<endl;
            cout<<b[wczytane]<<endl;
            cout<<c[wczytane]<<endl;
            cout<<d[wczytane]<<endl;
            do/*petla do while odpowiedzialna za to, zby uzytkownik podal odpowiedz: a,b,c lub d*/
                {
                cout<<" Twoja odpowiedz: "<<endl;
                cin>>udzielona;
                }
            while(udzielona != "a"&&udzielona != "b"&&udzielona != "c"&&udzielona != "d");
	}
    void wylosuj1()/*funkcja w klasie odpowiedzialna za losowanie pytan bez powtorzen*/
    {
            srand(time(NULL));
            int *wylosowane = new int[10];/*dynamiczna alokacja pamieci tablicy 10 elementowej*/
            do
                {
                nr_pytania = rand()%liczba_pytan+1;
                losowanie_ok = true;
            for (int q = 1; q <= ile_juz_wylosowano; q++)
                {
            if (nr_pytania = wylosowane[q]) losowanie_ok = false; /*sprawdzam czy pytanie nie zostalo wczesniej wylosowana*/
                }
            if (losowanie_ok == true)      /*mam unikatowe pytanie zapisuje je do tablicy*/
                {
                ile_juz_wylosowano++;
                wylosowane[ile_juz_wylosowano] = nr_pytania;
                }
                } while(losowanie_ok != true);
            delete[]wylosowane; /*zwalnianie pamieci*/
    }
    void wylosuj2()
    {
            srand(time(NULL));
            int *wylosowane = new int[20];
            do
                {
                nr_pytania = rand()%liczba_pytan+1;
                losowanie_ok=true;
            for (int q = 1; q <= ile_juz_wylosowano; q++)
                {
            if (nr_pytania = wylosowane[q]) losowanie_ok = false;
                }
            if (losowanie_ok == true)
                {
                ile_juz_wylosowano++;
                wylosowane[ile_juz_wylosowano] = nr_pytania;
                }
                } while(losowanie_ok != true);

    }
    void wylosuj3()
    {
            srand(time(NULL));
            int *wylosowane = new int[25];
            do
                {
                nr_pytania = rand()%liczba_pytan+1;
                losowanie_ok=true;
			for (int q = 1; q <= ile_juz_wylosowano; q++)
                {
            if (nr_pytania = wylosowane[q]) losowanie_ok = false;
                }
			if (losowanie_ok == true)
                {
				ile_juz_wylosowano++;
				wylosowane[ile_juz_wylosowano] = nr_pytania;
                }
                } while(losowanie_ok != true);
    }
    void wylosuj4()
    {
            srand(time(NULL));
            int *wylosowane = new int[30];
            do
                {
                nr_pytania = rand()%liczba_pytan+1;
                losowanie_ok = true;
			for (int q = 1; q <= ile_juz_wylosowano; q++)
                {
            if (nr_pytania = wylosowane[q]) losowanie_ok = false;
                }
			if (losowanie_ok == true)
                {
				ile_juz_wylosowano++;
				wylosowane[ile_juz_wylosowano] = nr_pytania;
                }
                }while(losowanie_ok != true);
    }
    };
    class sprawdzanie:public pytanie/*klasa sprawdzanie dziedziczaca po klasie pytanie*/
    {
            public:
            int punkt;/*zmienna punkt*/
    void sprawdz()/*funkcja w klasie sprawdzanie*/
	{
            if(udzielona == poprawna[wczytane])
			punkt = 1;
            else
            punkt = 0;
	}
	void wyswietl()
    {
            if(udzielona == poprawna[wczytane])
                {
                cout<<"Brawo, dobra odpowiedz "<<endl;
                cout<<"Nastepne pytanie- wcisnij ENTER "<<endl;
                }
            else
                {
                cout<<"Niestety zla odpowiedz "<<endl;
                cout<<"Nastepne pytanie- wcisnij ENTER "<<endl;
                }
    }
    };
