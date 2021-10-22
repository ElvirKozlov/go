# binar
//
//  Created by Elvira
//

#include "laba2.h"

#include <stdio.h>
#include <stdlib.h>

/* реализовать вывод всех индексов, которые содержат искомое значение */

int *getarray(int n, int x, int *array){ //функция возвращает указатель на заполненный массив

    for (int i = 0; i<(2*n); i++) *(array+i)=rand()%(2*n); //заполнение массива случайными числами диапазона от 0 до 2n


    printf("\nЗаполнение завершено:\n array= ");
    for (int i = 0; i<(2*n); i++) printf("%d ",*(array+i));


    return array;

}


int array_sort(int *array, int n){

    int save;           // необходима для перестановки значений
    int *first;         // хранит первый компонент пары
    int *second;        // хранит второй компонент пары
    int rec_break=1;    // останавливает рекурсию


    for (int i = 0; i<(2*n-1); i++)
        {
            first = array+i;        // первый компонент пары
            second = array +i+1;    // второй компонент пары

            if (*first > *second ) { save = *first; *first = *second; *second = save; }
            else rec_break++;       // если пара не поменялась местами, то +1
        }

    if (rec_break!=2*n) array_sort(array, n); // рекурсия остановится когда пары перестанут менятся местами

    return 0;

}


void get_x(int*array, int x, int left, int right)
{
    int mid  = (left+right)/2;                                                          // серединный элемент области, ограниченной параметрами left и right
    if (left > right)
    printf("\n\nНе найдено\n");                                                         // если нет такого значения серединного элемента, который был бы равен x, на вывод идет "не найдено"
    else if (array[mid]>x)
    get_x(array, x, left, mid-1);                                                       // если элемент по индексу mid больше x, то параметр right(правая граница) становится равен mid-1
    else if (array[mid]<x)
    get_x(array, x, mid+1, right);                                                      // если элемент по индексу mid меньше x, то параметр left(левая граница) становится равен mid+1
                                                                                        // т.е. границы стремятся к искомому элементу
    else if (array[mid]==x ) {                                                          // если значение серединного элемента равно искомому x, то на вывод идет mid как индекс x
    int i = mid;                                                                        // + идет проверка на наличие одинаковых значений слева и справа от найденного элемента
    while(array[i]==x){printf("\n\narray[%d] содержит значение %d\n",i ,x);i--;}
    i=mid+1;
    while(array[i]==x){printf("\n\narray[%d] содержит значение %d\n",i ,x);i++;}

    }
}


int main ()
{
    int n;          // половинная длина массива
    int x;          // число, которое необходимо найти

    printf("Половинная длина массива: ");
    scanf("%d", &n);
    printf("Найти: ");
    scanf("%d", &x);

    int array[2*n];                                         // инициализация массива

    array_sort(getarray(n, x, array), n);                   // в сортировщик передается адрес заполненного массива (из функции getarray)

    printf("\nСортировка завершена:\n array= ");
    for (int i = 0; i<(2*n); i++) printf("%d ",*(array+i)); // вывод отсортированного массива

    get_x(array, x, 0, (2*n-1));                            // в функцию передаётся отсортированный массив, значение, индекс которого надо найти, левая начальная граница, правая начальная граница


    return 0;
}



