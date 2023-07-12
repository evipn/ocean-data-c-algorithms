#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#define SIZE 50
#define string 1024
#define RANGE 332

struct ocean            //Dhmiourgia struct ocean me melh tis metrhseis
{
    char date[SIZE];
    float temp;
    float phosphate;
    float silicate;
    float nitrite;
    float nitrate;
    float salinity;
    float oxygen;
}typedef OCEAN;

void swap(OCEAN *a, OCEAN *b); 
void HeapSort(OCEAN *oc, int n);
void heapify(OCEAN *oc, int n, int i);
void countingSort(OCEAN *oc, int n);
void Multiply(OCEAN *oc, int n);
int floatToInt(OCEAN *oc, int k);
void printArray(OCEAN *oc, int n);

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
                strcpy(oc[i].date, value);
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

    clock_t start, end;
    int  choice;

    do
    {
        printf("Select the sorting method of your choice (1 or 2):\n");
        printf("1. Heapsort\n2.Counting Sort\n");
        scanf("%d" ,&choice);
    }while(choice != 1 && choice != 2);

    if(choice == 1)
    {
        printf("Heapsort:\n");
        start = clock();
        printf("Clock ticks at starting time: %ld\n", start);
        HeapSort(oc, n);
        end = clock();
    }
    else
    {
        printf("Counting Sort:\n");
        Multiply(oc, n);
        start = clock();
        printf("Clock ticks at starting time: %ld\n", start);
        countingSort(oc, n);
        end = clock();
    }

    printArray(oc, n);
    printf("Clock ticks at end time: %ld\n", end);
    printf("CLOCKS_PER_SEC: %ld\n", CLOCKS_PER_SEC);
    printf("The duration in seconds since the program was launched: %ld\n\n", (end-start)/CLOCKS_PER_SEC);

    free(oc);
    fclose(file);

    return 0;
}

void swap(OCEAN *a, OCEAN *b)
{
    OCEAN temp = *a;
    *a = *b;
    *b = temp;
}

void HeapSort(OCEAN *oc, int n)
{
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(oc, n, i);

    for (int i = n - 1; i >= 0; i--)
    {
        swap(&oc[0], &oc[i]);

        heapify(oc, i, 0);
    }
}

void heapify(OCEAN *oc, int n, int i)
{
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if(left < n && oc[left].phosphate > oc[largest].phosphate)
        largest = left;

    if(right < n && oc[right].phosphate > oc[largest].phosphate)
        largest = right;

    if (largest != i)
    {
        swap(&oc[i], &oc[largest]);
        heapify(oc, n, largest);
    }
}

void countingSort(OCEAN *oc, int n)
{
    OCEAN *output = malloc(sizeof(OCEAN) * n);

    int max = oc[0].phosphate;

    for(int i = 0; i < n; i++)
    {
        if(oc[i].phosphate > max)
        {
            max = oc[i].phosphate;
        }
    }

    int *count = malloc(sizeof(int) * (RANGE + 1));
    for(int i = 0; i <= max; i++)
    {
        count[i] = 0;
    }

    for (int i = 0; i < n; i++)
    {
        int index1 = floatToInt(oc, i);
        count[index1]++;
    }

    for(int i = 1; i<= max; i++ )
    {
        count[i] += count[i - 1];
    }

    for(int i = n - 1; i >= 0; i--)
    {
        int index2 = floatToInt(oc, i);
        output[count[index2] - 1] = oc[i];
        count[index2]--;
    }
    
    for(int i = 0; i < n; i++)
    {
        oc[i] = output[i];
        oc[i].phosphate /= 100; 
    }

    free(count);
    free(output);
}

void Multiply(OCEAN *oc, int n)
{
    for(int i = 0; i < n; i++)
    {
        oc[i].phosphate = oc[i].phosphate * 100;
    }
}

int floatToInt(OCEAN *oc, int k)
{
    int index = (int)oc[k].phosphate;
    return index;
}

void printArray(OCEAN *oc,int n)
{
    int i;
    for(i=0; i < n; i++)
    {
        printf("Date:%s Pho:%.2f\n" ,oc[i].date, oc[i].phosphate);
    }
}
