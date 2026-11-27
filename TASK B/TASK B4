#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct
{
    int id;
    char name[50];
    char bloodGroup[5];
    int age;
} Donor;

typedef struct
{
    Donor *data;
    int count;
    int capacity;
} DonorList;

int add_donor(DonorList *list, Donor newDonor)
{
    if (list->count == list->capacity)
    {
        int newCapacity;

        if (list->capacity == 0)
            newCapacity = 2;
        else
            newCapacity = list->capacity * 2;

        Donor *p = realloc(
            list->data,
            newCapacity * sizeof(Donor)
        );

        if (p == NULL)
        {
            printf("Memory allocation failed\n");
            return 0;
        }

        list->data = p;
        list->capacity = newCapacity;
    }

    list->data[list->count] = newDonor;
    list->count++;

    return 1;
}

void display_donors(const DonorList *list)
{
    printf("\nDONOR RECORDS\n");

    for (int i = 0; i < list->count; i++)
    {
        printf("\nID: %d", list->data[i].id);
        printf("\nName: %s", list->data[i].name);
        printf("\nBlood Group: %s",
               list->data[i].bloodGroup);
        printf("\nAge: %d\n", list->data[i].age);
    }
}

int main()
{
    DonorList list = {NULL, 0, 0};

    Donor d;
    int n;

    printf("DISTRICT BLOOD BANK NETWORK\n");

    printf("Enter number of donors: ");
    scanf("%d", &n);

    if (n < 0)
    {
        printf("Invalid number of donors\n");
        return 1;
    }

    for (int i = 0; i < n; i++)
    {
        printf("\nEnter Donor ID: ");
        scanf("%d", &d.id);

        printf("Enter Donor Name: ");
        scanf(" %49[^\n]", d.name);

        printf("Enter Blood Group: ");
        scanf("%4s", d.bloodGroup);

        printf("Enter Age: ");
        scanf("%d", &d.age);

        if (!add_donor(&list, d))
        {
            free(list.data);
            return 1;
        }

        printf("Donor added successfully\n");
        printf("Current Capacity: %d\n",
               list.capacity);
    }

    display_donors(&list);

    printf("\nTotal Donors: %d\n", list.count);
    printf("Final Capacity: %d\n", list.capacity);

    free(list.data);
    list.data = NULL;

    printf("\nMemory released successfully\n");

    return 0;
}
