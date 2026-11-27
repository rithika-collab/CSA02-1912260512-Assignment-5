#include <stdio.h>

long long calls = 0;

int sum_digits(int n)
{
    if (n < 10)
        return n;

    return (n % 10) + sum_digits(n / 10);
}

int digital_root(int n)
{
    if (n < 10)
        return n;

    return digital_root(sum_digits(n));
}

long long power_linear(long long base, int exp)
{
    calls++;

    if (exp == 0)
        return 1;

    return base * power_linear(base, exp - 1);
}

long long power_fast(long long base, int exp)
{
    long long half;

    calls++;

    if (exp == 0)
        return 1;

    if (exp == 1)
        return base;

    half = power_fast(base, exp / 2);

    if (exp % 2 == 0)
        return half * half;

    return base * half * half;
}

long long power_iterative(long long base, int exp)
{
    long long result = 1;

    while (exp > 0)
    {
        if (exp % 2 == 1)
            result *= base;

        base *= base;
        exp /= 2;
    }

    return result;
}

int main()
{
    int n;
    int values[] = {10, 100, 1000, 10000};

    printf("Enter number for digital root: ");
    scanf("%d", &n);

    if (n < 0)
    {
        printf("Enter a non-negative number.\n");
        return 1;
    }

    printf("Digital Root = %d\n", digital_root(n));

    printf("\nPower Calculation\n");

    calls = 0;
    printf("Linear Power (2^10) = %lld\n",
           power_linear(2, 10));
    printf("Linear Calls = %lld\n", calls);

    calls = 0;
    printf("Fast Power (2^10) = %lld\n",
           power_fast(2, 10));
    printf("Fast Calls = %lld\n", calls);

    printf("Iterative Power (2^10) = %lld\n",
           power_iterative(2, 10));

    printf("\nRecursive Call Comparison\n");
    printf("Exponent\tLinear\tFast\n");

    for (int i = 0; i < 4; i++)
    {
        int exp = values[i];

        calls = 0;
        power_linear(1, exp);
        long long linearCalls = calls;

        calls = 0;
        power_fast(1, exp);
        long long fastCalls = calls;

        printf("%d\t\t%lld\t%lld\n",
               exp, linearCalls, fastCalls);
    }

    return 0;
}
