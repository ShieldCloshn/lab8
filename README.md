#include <stdio.h>
#include <locale.h>
#include <iostream>
#include <vector>
using namespace std;

struct data {
	int d;
	int m;
	int y;
};
struct detal {
	int num;
	int ves;
	float price;
	struct data date;
	bool status;
	int ob;
};


int menu(detal *record);
int add(detal *record);
int read(detal *record);
int nev(detal *record);
int lob(detal *record);
int dop(detal *record);

int main(void)
{
	struct detal record [1000];
	setlocale (0,"RUS");
	menu(record);
}

int menu(detal *record)
{
	int ch;
	cout<<"Меню\n";
	cout<<"просмотр данных - 1\n";
	cout<<"Создать новые данные -2 \n";
	cout<<"Добавить сведенья -3\n";
	cout<<"Доп.сведенья - 4\n";
	cout<<"выход - 5\n";
	cout<<"введите значение: \n";
	cin>>ch;
	switch (ch) {
	case 1 :{ read(record); return 0;};
	case 2 :{ nev(record); return 0;};
	case 3 :{ add(record); return 0;};
	case 4 :{ dop(record);return 0;};
	case 5 :{ system ("pause"); return 0;};
	}
	return 0;
}

int lob(detal *record)
{
	int ch;
	cout<<"в меню - 6\n";
	cout<<"выход - 5\n";
	cout<<"введите значение: \n";
	cin>>ch;
	switch (ch) {
	case 6 :{ menu(record); return 0;};
	case 5 :{ system ("pause");return 0;};
    }
	return 0;
}

int nev(detal *record)
{
  int i,a,kv;
  FILE *f;
  if ((f=fopen("lab8.heh", "w"))==NULL)
  {
	  cout<<"Ошибка при открытии файла\n";
	  lob(record);
	  return 0;
  }
  cout<<"Введите количество деталей"<<endl;
  cin>>kv;
  cout<<"ввод сведений о деталях"<<endl;
 for (i=0; i<kv;i++)
 {
	 cout<<"Сведенья № "<<i+1<<"\n"<<endl;
     cout<<"инвентаный номер\n";
	 cin>>record[i].num;
	 cout<<"вес\n";
	 cin>>record[i].ves;
	 cout<<"цена\n";
	 cin>>record[i].price;
	 cout<<"Дата проиводства - день\n";
	 cin>>record[i].date.d;
	 cout<<"Дата проиводства - месяц\n";
	 cin>>record[i].date.m;
	 cout<<"Дата проиводства - год\n";
	 cin>>record[i].date.y;
	 cout<<"Знак качества, 1 если имеет\n";
	 cin>>a;
	 if (a==1)
	 { record[i].status=true;}
	 else {record[i].status=false;}
	 cout<<"объём производства\n";
	 cin>>record[i].ob;
 }
for(i=0; i<kv; i++)
	if(record[i].num)
		if(fwrite(&record[i],sizeof(struct detal), 1, f)!=1)  
			cout<<"Произошла ошибка, данные не сохранены"<<endl; 
 fclose(f);
  cout<<"Данные сохранены в файл\n";
  system("pause");
  lob(record);
  return 0;
}

int read(detal *record)
{
	int i,kv=-1;
	FILE *f;
	if ((f=fopen("lab8.heh","r"))==NULL)
	{
	 cout<<"Ошибка при открытии файла\n";
	 lob(record);	
	 return 0;
	}
	while(true)
		if(fread(&record[++kv],sizeof(struct detal), 1, f)!=1) 
		{
			if (feof(f)) break;
			cout<<"Произошла ошибка"<<endl; 
			fclose(f);
			lob(record);
			return 0;
		}
 cout<<"Сведенья о деталях\n";
 for (i=0;i<kv;i++)
 {
	 cout<<"Сведенья № "<<i<<"\n"<<endl;
	 cout<<"Инвентарный номер "<<record[i].num<<endl;
	 cout<<"Вес "<<record[i].ves<<endl;
	 cout<<"цена "<<record[i].price<<endl;
	 cout<<"дата производства "<<record[i].date.d<<"."<<record[i].date.m<<"."<<record[i].date.y<<endl;
	 cout<<"Знак качества "<<record[i].status<<endl;
	 cout<<"Объём производства "<<record[i].ob<<endl;
 }
 cout<<"конец файла"<<endl;
 fclose(f);
 system("pause");
 lob(record);
 return 0;
}

int add(detal *record)
{
	int i, kv,a;
	FILE *f;
	if ((f=fopen("lab8.heh","a"))==NULL)
	{
	 cout<<"Ошибка при открытии файла\n";
	 lob(record);	
	 return 0;
	}
  cout<<"Введите количество деталей"<<endl;
  cin>>kv;
  cout<<"ввод сведений о деталях"<<endl;
 for (i=0; i<kv;i++)
 {
	 cout<<"Сведенья № "<<i+1<<"\n"<<endl;
     cout<<"инвентаный номер\n";
	 cin>>record[i].num;
	 cout<<"вес\n";
	 cin>>record[i].ves;
	 cout<<"цена\n";
	 cin>>record[i].price;
	 cout<<"Дата проиводства - день\n";
	 cin>>record[i].date.d;
	 cout<<"Дата проиводства - месяц\n";
	 cin>>record[i].date.m;
	 cout<<"Дата проиводства - год\n";
	 cin>>record[i].date.y;
	 cout<<"Знак качества, 1 если имеет\n";
	 cin>>a;
	 if (a==1)
	 { record[i].status=true;}
	 else {record[i].status=false;}
	 cout<<"объём производства\n";
	 cin>>record[i].ob;
	 for(i=0; i<kv; i++)
	if(record[i].num)
		if(fwrite(&record[i],sizeof(struct detal), 1, f)!=1)  
			cout<<"Произошла ошибка, данные не сохранены"<<endl; 
  fclose(f);
  cout<<"Данные сохранены в файл\n";
  system("pause");
  lob(record);
  return 0;
}
}

int dop(detal *record)
{
	struct detal temp;
	int i,j,kv=-1;
	FILE *f;
	if ((f=fopen("lab8.heh","r"))==NULL)
	{
	 cout<<"Ошибка при открытии файла\n";
	 lob(record);	
	}
	while(true)
		if(fread(&record[++kv],sizeof(struct detal), 1, f)!=1) 
		{
			if (feof(f)) break;
			cout<<"Произошла ошибка"<<endl; 
			fclose(f);
			lob(record);
			return 0;
		}
	for (i=0;i<kv;i++)
		if (fread(&record[i],sizeof(struct detal), 1, f)!=1)
		{
			if (feof(f)) break;
			cout<<"Ошибка при открытии файла\n";
				lob(record);
		}
cout<<"ввод сведений о деталях c знаком качества"<<endl;
 for (i=0; i<kv;i++)
 {
	 if (record[i].status==true)
	{ cout<<"Сведенья № "<<i+1<<"\n"<<endl;
	 cout<<"Инвентарный номер "<<record[i].num<<endl;
	 cout<<"цена "<<record[i].price<<endl;
	 cout<<"Объём производства "<<record[i].ob<<endl;}
 } 

 cout<<"вывод деталей по дате"<<endl;
  cout<<"____________________"<<endl;
 for (i=0;i<kv;i++) 
 {
	 for (j=i+1;j<kv;j++){
		 if (((record[i].date.y<record[j].date.y) || (record[i].date.y==record[j].date.y && record[i].date.m<record[j].date.m)) || (record[i].date.y==record[j].date.y && record[i].date.m==record[j].date.m && record[i].date.d<record[j].date.d))
			 temp=record[i];
             record[i]=record[j];
			 record[j]=temp;}
cout<<"Сведенья № "<<i+1<<"\n"<<endl;
	 cout<<"Инвентарный номер "<<record[i].num<<endl;
	 cout<<"Вес "<<record[i].ves<<endl;
	 cout<<"цена "<<record[i].price<<endl;
	 cout<<"дата производства "<<record[i].date.d<<"."<<record[i].date.m<<"."<<record[i].date.y<<endl;
	 cout<<"Знак качества "<<record[i].status<<endl;
	 cout<<"Объём производства "<<record[i].ob<<endl;
}
 cout<<"конец файла"<<endl;
 fclose(f);
 system("pause");
 lob(record);
 return 0;}

/*Деталь автомобиля описывается инвентарным номером (положительное целое число),
весом (в килограммах), ценой и стоимостью (в рублях), датой начала производства (год, 
месяц, день), статусом (имеет или не имеет знак качества) и объемом производства (в 
штуках за смену). В заданной последовательности сведений о деталях найти инвентарные 
номера деталей с наибольшей датой начала производства среди всех заданных деталей. 
Вывести на экран инвентарный номер, объем производства, цену и стоимость деталей со 
знаком качества.*/
