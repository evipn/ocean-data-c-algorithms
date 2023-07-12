#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <string.h>
#include <math.h>
#include <time.h>
#define SIZE 50
#define string 1024

struct ocean            //Dhmiourgia struct ocean me melh tis metrhseis
{
    int date;
    float temp;
    float phosphate;
    float silicate;
    float nitrite;
    float nitrate;
    float salinity;
    float oxygen;
}typedef OCEAN;

int BIS(OCEAN *oc,int left,int right);
void insertionSort(OCEAN *oc, int n);
void removeChar(char *str, char charToRemove);
void swap(OCEAN *a, OCEAN *b);
void printInfo(OCEAN *oc, int n);

int main()
{
   FILE* file=fopen("ocean.csv" , "r");

   if(file == NULL)
   {
       printf("File is empty!");
       return 1;
   }

   int n = 1405;
   OCEAN* oc;
   oc = malloc(sizeof(OCEAN) * n);

   if(oc == NULL)
   {
       printf("Memory is not allocated!");
       return 1;
   }

    char buffer[1024];

    int row = 0;
    int column = 0;

    int i=0;
    while (fgets(buffer,1024, file))
    {
        column = 0;
        row++;

        if (row == 1)
            continue;

        char* value = strtok(buffer, ", ");

        while (value)
        {

            if (column == 0)
            {
                removeChar(value, '/');
                oc[i].date = atoi(value);
            }
            else if (column == 1)
            {
                oc[i].temp = atof(value);
            }
            else if (column == 2)
            {
                oc[i].phosphate = atof(value);
            }
            else if (column == 3)
            {
                oc[i].silicate = atof(value);
            }
            else if (column == 4)
            {
                oc[i].nitrate = atof(value);
            }
            else if (column == 5)
            {
                oc[i].nitrite = atof(value);
            }
            else if (column == 6)
            {
                oc[i].salinity = atof(value);
            }
            else if (column == 7)
            {
                oc[i].oxygen = atof(value);
            }

            value = strtok(NULL, ", ");
            column++;
        }
        i++;
    }

    insertionSort(oc, n);
    
    clock_t start, end;

    start = clock();
    int index = BIS(oc, 0, n);
    end = clock();

    if(index == -1)
    {
        printf("The date that you entered does not exist!");
        return 0;
    }
    else
    {
        printInfo(oc, index);

        printf("Clock ticks at starting time: %ld\n", start);
        printf("Clock ticks at end time: %ld\n", end);
        printf("CLOCKS_PER_SEC: %ld\n", CLOCKS_PER_SEC);
        printf("The duration in seconds since the program was launched: %ld\n\n", (end-start)/CLOCKS_PER_SEC);
    }

    free(oc);
    fclose(file);

    return 0;
}

int BIS(OCEAN *oc,int left,int right)
{
    char date[15];
    int size = right - left + 1;

    printf("Please give the date that you want to search:\n");
    scanf("%s" ,date);
    removeChar(date, '/');
    long int x = atoi(date);

    int next = (size) * ((double)((x - oc[left].date) / (oc[right].date - oc[left].date))) + 1;
    while (x != oc[next].date)
    {
        int i=0;
        size = right - left + 1;
        if (size <= 3)
        {
            for (int j= 0; j < size; j++)
            {
                if(x == oc[j].date)
			    {
				    return j;
			    }
            }

        return next;
        }

        if (x >= oc[next].date)
        {
            while( x > oc[next + i * ((int) sqrt(size)) - 1].date)
            {
                i = i + 1;
            }

        right = next + i * (int)sqrt(size);
        left = next + (i-1) * (int)sqrt(size);
        }
        else if(x < oc[next].date)
        {
            while(x < oc[next - i * ((int) sqrt(size)) + 1].date)
            {
                i = i + 1;
            }

        right = next  - (i - 1) * (int)sqrt(size);
        left = next - i * (int)sqrt(size);
        }
    next = left + ((right-left+1) * ((double)(x - oc[left].date) / (oc[right].date - oc[left].date))) - 1;
    }

    if( x == oc[next].date)
    {
        return next;
    }
    else
    {
        return -1;
    }
}

void insertionSort(OCEAN *oc, int n)
{
    int i, j;
    int key;
    for (i = 1; i < n; i++)
    {
        key = oc[i].date;
        j = i - 1;

        while (j >= 0 && oc[j].date > key)
        {
            oc[j + 1].date = oc[j].date;
            swap(&oc[j + 1], &oc[j]);
            j = j - 1;
        }
        oc[j + 1].date = key;
    }
}

void swap(OCEAN *a, OCEAN *b)
{
  OCEAN t = *a;
  *a = *b;
  *b = t;
}

void removeChar(char * str, char charToRemove)
{
    int i, j;
    int len = strlen(str);

    for(i=0; i<len; i++)
    {
        if(str[i] == charToRemove)
        {
            for(j=i; j<len; j++)
            {
                str[j] = str[j+1];
            }
            len--;
            i--;
        }
    }
}

void printInfo(OCEAN *oc, int index)
{
    printf("Temp: %.2f, Phosphate: %.2f \n" ,oc[index].temp, oc[index].phosphate);
}
