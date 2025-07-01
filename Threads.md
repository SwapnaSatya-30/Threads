# Threading Programs in C 

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
