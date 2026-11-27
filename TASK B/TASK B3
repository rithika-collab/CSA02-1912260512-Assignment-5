#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define MAX_DONORS 100000

typedef struct
{
    int id;
    char name[30];
    char bloodGroup[5];
    int age;
} Donor;

typedef struct
{
    char bloodGroup[5];
    int units;
} Stock;

int saveText(Donor donors[], int n)
{
    FILE *fp = fopen("donors.txt", "w");

    if (fp == NULL)
        return 0;

    for (int i = 0; i < n; i++)
    {
        fprintf(fp, "%d,%s,%s,%d\n",
                donors[i].id,
                donors[i].name,
                donors[i].bloodGroup,
                donors[i].age);
    }

    fclose(fp);
    return 1;
}

int saveBinary(Donor donors[], int n)
{
    FILE *fp = fopen("donors.dat", "wb");

    if (fp == NULL)
        return 0;

    fwrite(donors, sizeof(Donor), n, fp);

    fclose(fp);
    return 1;
}

int readText()
{
    FILE *fp = fopen("donors.txt", "r");
    char line[100];
    int count = 0;

    if (fp == NULL)
        return 0;

    while (fgets(line, sizeof(line), fp) != NULL)
        count++;

    fclose(fp);
    return count;
}

int readBinary()
{
    FILE *fp = fopen("donors.dat", "rb");
    Donor d;
    int count = 0;

    if (fp == NULL)
        return 0;

    while (fread(&d, sizeof(Donor), 1, fp) == 1)
        count++;

    fclose(fp);
    return count;
}

int update_units(const char *filename,
                 int position, int newUnits)
{
    FILE *fp = fopen(filename, "rb+");
    Stock s;

    if (fp == NULL)
        return 0;

    if (position < 0 ||
        fseek(fp, (long)position * sizeof(Stock), SEEK_SET) != 0)
    {
        fclose(fp);
        return 0;
    }

    if (fread(&s, sizeof(Stock), 1, fp) != 1)
    {
        fclose(fp);
        return 0;
    }

    s.units = newUnits;

    if (fseek(fp, -(long)sizeof(Stock), SEEK_CUR) != 0)
    {
        fclose(fp);
        return 0;
    }

    if (fwrite(&s, sizeof(Stock), 1, fp) != 1)
    {
        fclose(fp);
        return 0;
    }

    fclose(fp);
    return 1;
}

int main()
{
    Donor *donors;
    int sizes[] = {1000, 10000, 100000};

    donors = malloc(MAX_DONORS * sizeof(Donor));

    if (donors == NULL)
    {
        printf("Memory allocation failed\n");
        return 1;
    }

    for (int i = 0; i < MAX_DONORS; i++)
    {
        donors[i].id = i + 1;
        snprintf(donors[i].name,
                 sizeof(donors[i].name),
                 "Donor%d", i + 1);

        strcpy(donors[i].bloodGroup, "O+");
        donors[i].age = 20 + (i % 30);
    }

    printf("Records\tFormat\tWrite Time\tRead Time\n");

    for (int j = 0; j < 3; j++)
    {
        int n = sizes[j];
        clock_t start, end;
        double writeTime, readTime;

        start = clock();
        saveText(donors, n);
        end = clock();
        writeTime = (double)(end - start) / CLOCKS_PER_SEC;

        start = clock();
        readText();
        end = clock();
        readTime = (double)(end - start) / CLOCKS_PER_SEC;

        printf("%d\tText\t%.6f\t%.6f\n",
               n, writeTime, readTime);

        start = clock();
        saveBinary(donors, n);
        end = clock();
        writeTime = (double)(end - start) / CLOCKS_PER_SEC;

        start = clock();
        readBinary();
        end = clock();
        readTime = (double)(end - start) / CLOCKS_PER_SEC;

        printf("%d\tBinary\t%.6f\t%.6f\n",
               n, writeTime, readTime);
    }

    {
        Stock stock[] = {
            {"A+", 10}, {"A-", 8},
            {"B+", 15}, {"B-", 6},
            {"AB+", 12}, {"AB-", 9},
            {"O+", 5}, {"O-", 11}
        };

        FILE *fp = fopen("stock.dat", "wb");

        if (fp != NULL)
        {
            fwrite(stock, sizeof(Stock), 8, fp);
            fclose(fp);

            if (update_units("stock.dat", 6, 7))
                printf("\nStock updated successfully\n");
            else
                printf("\nStock update failed\n");
        }
    }

    free(donors);

    return 0;
}
