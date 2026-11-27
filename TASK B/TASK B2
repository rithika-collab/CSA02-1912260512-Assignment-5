#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define NAME_SIZE 10

int validBloodGroup(const char *group)
{
    const char *groups[] = {
        "A+", "A-", "B+", "B-",
        "AB+", "AB-", "O+", "O-"
    };

    for (int i = 0; i < 8; i++)
    {
        if (strcmp(group, groups[i]) == 0)
            return 1;
    }

    return 0;
}

int main(int argc, char *argv[])
{
    char name[NAME_SIZE];
    FILE *fp;
    char *end;
    long quantity;

    printf("Enter donor name: ");

    if (fgets(name, sizeof(name), stdin) == NULL)
    {
        printf("Input error\n");
        return 1;
    }

    name[strcspn(name, "\n")] = '\0';

    printf("Donor Name: %s\n", name);

    fp = fopen("donors.txt", "r");

    if (fp == NULL)
    {
        perror("File opening failed");
    }
    else
    {
        printf("Donor file opened successfully\n");
        fclose(fp);
    }

    if (argc < 2)
    {
        printf("\nUsage:\n");
        printf("program find O+\n");
        printf("program issue O+ 2\n");
        printf("program stock\n");
        return 1;
    }

    if (strcmp(argv[1], "find") == 0)
    {
        if (argc != 3)
        {
            printf("Usage: program find O+\n");
            return 1;
        }

        if (!validBloodGroup(argv[2]))
        {
            printf("Invalid blood group\n");
            return 1;
        }

        printf("Blood group: %s\n", argv[2]);
        printf("Command accepted\n");
    }

    else if (strcmp(argv[1], "issue") == 0)
    {
        if (argc != 4)
        {
            printf("Usage: program issue O+ 2\n");
            return 1;
        }

        if (!validBloodGroup(argv[2]))
        {
            printf("Invalid blood group\n");
            return 1;
        }

        quantity = strtol(argv[3], &end, 10);

        if (end == argv[3] || *end != '\0' || quantity <= 0)
        {
            printf("Invalid quantity\n");
            return 1;
        }

        printf("Blood group: %s\n", argv[2]);
        printf("Requested units: %ld\n", quantity);
    }

    else if (strcmp(argv[1], "stock") == 0)
    {
        if (argc != 2)
        {
            printf("Usage: program stock\n");
            return 1;
        }

        printf("Available Blood Stock\n");
        printf("A+ : 10\n");
        printf("A- : 8\n");
        printf("B+ : 15\n");
        printf("B- : 6\n");
        printf("AB+ : 12\n");
        printf("AB- : 9\n");
        printf("O+ : 5\n");
        printf("O- : 11\n");
    }

    else
    {
        printf("Unknown command\n");
        return 1;
    }

    return 0;
}
