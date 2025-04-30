#include <stdio.h>
#include <stdlib.h>
#include<locale.h>
struct stack
{
    int size;//размер стека
    char* st;//добавляю эл в стек
};
struct stack s;
void push(char hell)
{
    if (s.size == 0 && s.st == NULL)
    {
        s.size++;
        s.st = (char*)malloc(sizeof(char) * s.size);
        s.st[s.size - 1] = hell;//добавляю в стек один элемент
    }
    else
    {
        char* tmp = s.st;
        s.size++;
        s.st = (char*)malloc(sizeof(char) * s.size);
        int i;
        for (i = 0; i < s.size - 1; i++)
        {
            s.st[i] = tmp[i];
        }
        free(tmp);
        s.st[s.size - 1] = hell;
    }
}
char pop() {
    char ch = s.st[s.size - 1];//сохраняю верхний элемнт стека
    s.st[s.size - 1] = '\0';
    s.size--;
    return ch;
}
int main()
{

    setlocale(LC_ALL, "RUS");
    char* m = (char*)malloc(sizeof(char*) * 10);// малок выделяет память в 10 символов,сайзоф возвращает число байтов для чара это 1 байт
    char* temp;
    char c = 0;//переменая для ввода символов (с это один символ)
    int i = -1, n = 0, t = 0;//n- испульзуем для выделения памяти,i-значение массива(i может быть от 0 до 9,а кол-во значениий 10)
    //t- проходит по старому массиву и вставляет его в новый
    printf("Введите значение:\n");
    while (c != '\n')
    {
        i++;
        c = getchar();//считываю один символ из потока ввода
        m[i + n] = c;
        if (i == 9)//если строка превышает 10 симв
        {
            n = n + i + 1;//предыдущщее кол-во элементов массива
            i = -1;//т.к массив начинается с нуля
            temp = m;//новый массив
            char* m = (char*)malloc(sizeof(char*) * (n + 10));//увеличиваем рахмер на 10
            for (t = 0; t < n + 1; t++)
                m[t] = temp[t];//t- проходит по старому массиву и вставляет его в новый
        }
    }
    m[i + n] = '\0';
    int j, ok = 1, k;//Переменная OK  чтобы выйти из внешнего цикла,=0, если в стеке  скобка другого типа или стек  пуст.
    char z;
    char br1[3] = { '(', '[', '{' };
    char br2[3] = { ')', ']', '}' };
    for (j = 0; ok && (*m != '\0'); j++)
        for (k = 0; k < 3; k++)
        {
            if (*m == br1[k])
            {
                push(*m);
                m++;
                break;
            }
            if (ok && (*m == 0))
                printf("\nВыpажение пpавильное\n");
            else printf("\nВыpажение непpавильное \n");
            free(m);
            free(s.st);
            return 0;
        }
