# Threading Programs in C 


## 1.Write a C program to create a thread that prints "Hello, World!"? 
```c
#include <stdio.h>
#include <pthread.h>

void* hello(void* arg) {
    printf("Hello, World!\n");
    return NULL;
}

int main() {
    pthread_t t;
    pthread_create(&t, NULL, hello, NULL);
    pthread_join(t, NULL);
    return 0;
}
```

## 2.Modify the above program to create multiple threads, each printing its own message? 

```c
#include <stdio.h>
#include<pthread.h>

void* printHello(void* arg)
{
    for(int i=0;i<5;i++)
    {printf("Hello !\n");}
    return NULL;
}
void* printHi(void* arg)
{
    for(int i=0;i<5;i++)
    {printf("Hi !\n");}
    return NULL;
}

int main()
{
    pthread_t thread1,thread2;
    pthread_create(&thread1, NULL, printHello, NULL);
    pthread_create(&thread2, NULL, printHi, NULL);
    pthread_join(thread1,NULL);
    pthread_join(thread2,NULL);

    return 0;
}
```

## 3.Develop a C program to create two threads that print numbers from 1 to 10 concurrently? 

```c
#include <stdio.h>
#include <pthread.h>

void* print_nums(void* arg) {
    for (int i = 1; i <= 10; i++) {
        printf("Thread %s: %d\n", (char*)arg, i);
    }
    return NULL;
}

int main() {
    pthread_t t1, t2;
    pthread_create(&t1, NULL, print_nums, "A");
    pthread_create(&t2, NULL, print_nums, "B");
    pthread_join(t1, NULL);
    pthread_join(t2, NULL);
    return 0;
}
```

## 4.Implement a C program to create a thread that calculates the factorial of a given number?

```c
#include <stdio.h>
#include <pthread.h>

void* factorial(void* arg) {
    int n = *(int*)arg, fact = 1;
    for (int i = 1; i <= n; i++) fact *= i;
    printf("Factorial of %d is %d\n", n, fact);
    return NULL;
}

int main() {
    pthread_t t;
    int num = 5;
    pthread_create(&t, NULL, factorial, &num);
    pthread_join(t, NULL);
    return 0;
}
```

## 5.Write a C program to create two threads that print their thread IDs? 

```c
#include <stdio.h>
#include <pthread.h>

void* print_id(void* arg) {
    printf("Thread ID: %lu\n", pthread_self());
    return NULL;
}

int main() {
    pthread_t t1, t2;
    pthread_create(&t1, NULL, print_id, NULL);
    pthread_create(&t2, NULL, print_id, NULL);
    pthread_join(t1, NULL);
    pthread_join(t2, NULL);
    return 0;
}
```

## 6. Thread that prints the sum of two numbers
```c
#include <stdio.h>
#include <pthread.h>

struct SumArgs {
    int a, b;
};

void* compute_sum(void* arg) {
    struct SumArgs* args = (struct SumArgs*)arg;
    int sum = args->a + args->b;
    printf("Sum = %d\n", sum);
    return NULL;
}

int main() {
    pthread_t t;
    struct SumArgs args = {5, 7};
    pthread_create(&t, NULL, compute_sum, &args);
    pthread_join(t, NULL);
    return 0;
}
```

## 7. Thread that calculates the square of a number
```c
#include <stdio.h>
#include <pthread.h>

void* square(void* arg) {
    int n = *(int*)arg;
    printf("Square of %d is %d\n", n, n * n);
    return NULL;
}

int main() {
    pthread_t t;
    int num = 6;
    pthread_create(&t, NULL, square, &num);
    pthread_join(t, NULL);
    return 0;
}
```

## 8. Thread that prints the current date and time
```c
#include <stdio.h>
#include <pthread.h>
#include <time.h>

void* show_time(void* arg) {
    time_t now = time(NULL);
    printf("Current Time: %s", ctime(&now));
    return NULL;
}

int main() {
    pthread_t t;
    pthread_create(&t, NULL, show_time, NULL);
    pthread_join(t, NULL);
    return 0;
}
```

## 9. Thread that checks if a number is prime
```c
#include <stdio.h>
#include <pthread.h>

void* check_prime(void* arg) {
    int n = *(int*)arg, is_prime = 1;
    if (n <= 1) is_prime = 0;
    for (int i = 2; i*i <= n; i++) {
        if (n % i == 0) { is_prime = 0; break; }
    }
    printf("%d is %s\n", n, is_prime ? "Prime" : "Not Prime");
    return NULL;
}

int main() {
    pthread_t t;
    int num = 29;
    pthread_create(&t, NULL, check_prime, &num);
    pthread_join(t, NULL);
    return 0;
}
```

## 10. Thread that checks if a string is a palindrome
```c
#include <stdio.h>
#include <string.h>
#include <pthread.h>

void* check_palindrome(void* arg) {
    char* str = (char*)arg;
    int len = strlen(str), is_pal = 1;
    for (int i = 0; i < len / 2; i++) {
        if (str[i] != str[len - i - 1]) {
            is_pal = 0; break;
        }
    }
    printf("\"%s\" is %s\n", str, is_pal ? "a Palindrome" : "not a Palindrome");
    return NULL;
}

int main() {
    pthread_t t;
    char str[] = "madam";
    pthread_create(&t, NULL, check_palindrome, str);
    pthread_join(t, NULL);
    return 0;
}
```
