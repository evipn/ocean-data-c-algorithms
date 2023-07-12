#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#include <conio.h>
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

int BinarySearch(OCEAN *oc, int l, int r);
int interpolationSearch(OCEAN *oc, int n);
void insertionSort(OCEAN *oc, int n);
void swap(OCEAN *a, OCEAN *b);
void removeChar(char *str, char charToRemove);
void printInfo(OCEAN *oc, int index);
void checkIndex(OCEAN *oc, int index);

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

    int  choice;

    do
    {
        printf("Select the searching method of your choice (1 or 2):\n");
        printf("1.Binary Search\n2.Interpolation Search\n");
        scanf("%d" ,&choice);
    }while(choice != 1 && choice != 2);

    if(choice == 1)
    {
        printf("Binary Search:\n");
        start = clock();
        int index1 = BinarySearch(oc, 0, n-1);
        end = clock();
        checkIndex(oc, index1);
    }
    else
    {
        printf("Interpolation Search:\n");
        start = clock();
        int index2 = interpolationSearch(oc, n); 
        end = clock();
        checkIndex(oc, index2);
    }

    printf("Clock ticks at starting time: %ld\n", start);
    printf("Clock ticks at end time: %ld\n", end);
    printf("CLOCKS_PER_SEC: %ld\n", CLOCKS_PER_SEC);
    printf("The duration in seconds since the program was launched: %ld\n\n", (end-start)/CLOCKS_PER_SEC);

    free(oc);
    fclose(file);

    return 0;
}

int BinarySearch(OCEAN *oc, int l, int r)
{
    char date[15];
    int x;

    printf("Please give the date that you want to search:\n");
    scanf("%s" ,date);
    removeChar(date, '/');
    x = atoi(date);
    
    while(r >= l)
    {
        int mid = l + (r - l) / 2;

        // If the element is present at the middle
        // itself
        if (oc[mid].date == x)
            return mid;

        // If element is smaller than mid, then
        // it can only be present in left subarray
        else if (oc[mid].date > x)
            r = mid - 1;

        // Else the element can only be present
        // in right subarray
        else
            l = mid + 1;
    }

    // We reach here when element is not
    // present in array
    return -1;
}

int interpolationSearch(OCEAN *oc, int n)
{
    char date[15];
    int x;

    printf("Please give the date that you want to search:\n");
    scanf("%s" ,date);
    removeChar(date, '/');
    x = atoi(date);

    // Find indexes of two corners
    int lo = 0, hi = (n - 1);

    // Since array is sorted, an element present
    // in array must be in range defined by corner
    while (lo <= hi && x >= oc[lo].date && x <= oc[hi].date)
    {
        if (lo == hi)
        {
            if (oc[lo].date == x) return lo;
            return -1;
        }
        // Probing the position with keeping
        // uniform distribution in mind.
        int pos = lo + (((double)(hi - lo) /
            (oc[hi].date - oc[lo].date)) * (x - oc[lo].date));

        // Condition of target found
        if (oc[pos].date == x)
            return pos;

              // If x is larger, x is in upper part
        if (oc[pos].date < x)
            lo = pos + 1;

        // If x is smaller, x is in the lower part
        else
            hi = pos - 1;
    }
    return -1;
}

void insertionSort(OCEAN *oc, int n)
{
    int i, j;
    int key;
    for (i = 1; i < n; i++)
    {
        key = oc[i].date;
        j = i - 1;

        /* Move elements of oc[0..i-1], that are
          greater than key, to one position ahead
          of their current position */
        while (j >= 0 && oc[j].date > key)
        {
            oc[j + 1].date = oc[j].date;
            swap(&oc[j+1], &oc[j]);
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

void checkIndex(OCEAN *oc, int index)
{
    if(index == -1)
    {
        printf("The date does not exist! \n");
    }
    else
    {
        printInfo(oc, index);
    }
}

void printInfo(OCEAN *oc, int index)
{   
    printf("Temp: %.2f, Phosphate: %.2f \n" ,oc[index].temp, oc[index].phosphate);
}