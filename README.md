# Temp

Below are complete C programs for each topic, all with user input. Each is standalone.


---

1. Stack Implementation Using Array

#include <stdio.h>
#define MAX 100

int stack[MAX], top = -1;

void push(int val) {
    if (top == MAX - 1) printf("Stack Overflow\n");
    else stack[++top] = val;
}

void pop() {
    if (top == -1) printf("Stack Underflow\n");
    else printf("Popped: %d\n", stack[top--]);
}

void display() {
    if (top == -1) printf("Stack Empty\n");
    else {
        for (int i = top; i >= 0; i--)
            printf("%d ", stack[i]);
        printf("\n");
    }
}

int main() {
    int ch, val;
    while (1) {
        printf("1.Push 2.Pop 3.Display 4.Exit: ");
        scanf("%d", &ch);
        if (ch == 1) { printf("Enter value: "); scanf("%d", &val); push(val); }
        else if (ch == 2) pop();
        else if (ch == 3) display();
        else break;
    }
}


---

2. Infix to Postfix Conversion

#include <stdio.h>
#include <ctype.h>

char stack[100];
int top = -1;

void push(char c) { stack[++top] = c; }
char pop() { return stack[top--]; }
int precedence(char c) {
    if (c == '^') return 3;
    if (c == '*' || c == '/') return 2;
    if (c == '+' || c == '-') return 1;
    return 0;
}

int main() {
    char infix[100], postfix[100];
    printf("Enter infix: ");
    scanf("%s", infix);
    int j = 0;
    for (int i = 0; infix[i]; i++) {
        char c = infix[i];
        if (isalnum(c)) postfix[j++] = c;
        else if (c == '(') push(c);
        else if (c == ')') {
            while (top != -1 && stack[top] != '(') postfix[j++] = pop();
            pop();
        } else {
            while (top != -1 && precedence(stack[top]) >= precedence(c))
                postfix[j++] = pop();
            push(c);
        }
    }
    while (top != -1) postfix[j++] = pop();
    postfix[j] = '\0';
    printf("Postfix: %s\n", postfix);
}


---

3. Binary Search and Linear Search

#include <stdio.h>

int linear(int arr[], int n, int key) {
    for (int i = 0; i < n; i++)
        if (arr[i] == key) return i;
    return -1;
}

int binary(int arr[], int n, int key) {
    int l = 0, r = n - 1;
    while (l <= r) {
        int mid = (l + r) / 2;
        if (arr[mid] == key) return mid;
        else if (arr[mid] < key) l = mid + 1;
        else r = mid - 1;
    }
    return -1;
}

int main() {
    int n, key, choice;
    printf("Enter size: "); scanf("%d", &n);
    int arr[n];
    printf("Enter sorted array: ");
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);
    printf("Enter key: "); scanf("%d", &key);
    printf("1.Linear 2.Binary: "); scanf("%d", &choice);
    int res = (choice == 1) ? linear(arr, n, key) : binary(arr, n, key);
    if (res != -1) printf("Found at %d\n", res);
    else printf("Not found\n");
}


---

4. Queue Using Array

#include <stdio.h>
#define MAX 100

int queue[MAX], front = -1, rear = -1;

void enqueue(int val) {
    if (rear == MAX - 1) printf("Overflow\n");
    else {
        if (front == -1) front = 0;
        queue[++rear] = val;
    }
}

void dequeue() {
    if (front == -1 || front > rear) printf("Underflow\n");
    else printf("Dequeued: %d\n", queue[front++]);
}

void display() {
    if (front == -1 || front > rear) printf("Empty\n");
    else for (int i = front; i <= rear; i++) printf("%d ", queue[i]);
    printf("\n");
}

int main() {
    int ch, val;
    while (1) {
        printf("1.Enqueue 2.Dequeue 3.Display 4.Exit: ");
        scanf("%d", &ch);
        if (ch == 1) { printf("Enter value: "); scanf("%d", &val); enqueue(val); }
        else if (ch == 2) dequeue();
        else if (ch == 3) display();
        else break;
    }
}


---

5. Stack Using Linked List

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
} *top = NULL;

void push(int val) {
    struct Node* newNode = malloc(sizeof(struct Node));
    newNode->data = val;
    newNode->next = top;
    top = newNode;
}

void pop() {
    if (top == NULL) printf("Underflow\n");
    else {
        printf("Popped: %d\n", top->data);
        struct Node* temp = top;
        top = top->next;
        free(temp);
    }
}

void display() {
    struct Node* temp = top;
    while (temp) { printf("%d ", temp->data); temp = temp->next; }
    printf("\n");
}

int main() {
    int ch, val;
    while (1) {
        printf("1.Push 2.Pop 3.Display 4.Exit: ");
        scanf("%d", &ch);
        if (ch == 1) { printf("Enter value: "); scanf("%d", &val); push(val); }
        else if (ch == 2) pop();
        else if (ch == 3) display();
        else break;
    }
}


---

6. Queue Using Linked List

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
} *front = NULL, *rear = NULL;

void enqueue(int val) {
    struct Node* newNode = malloc(sizeof(struct Node));
    newNode->data = val;
    newNode->next = NULL;
    if (rear == NULL) front = rear = newNode;
    else { rear->next = newNode; rear = newNode; }
}

void dequeue() {
    if (front == NULL) printf("Underflow\n");
    else {
        printf("Dequeued: %d\n", front->data);
        struct Node* temp = front;
        front = front->next;
        if (front == NULL) rear = NULL;
        free(temp);
    }
}

void display() {
    struct Node* temp = front;
    while (temp) { printf("%d ", temp->data); temp = temp->next; }
    printf("\n");
}

int main() {
    int ch, val;
    while (1) {
        printf("1.Enqueue 2.Dequeue 3.Display 4.Exit: ");
        scanf("%d", &ch);
        if (ch == 1) { printf("Enter value: "); scanf("%d", &val); enqueue(val); }
        else if (ch == 2) dequeue();
        else if (ch == 3) display();
        else break;
    }
}


---

7. Single Linked List Operations

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
} *head = NULL;

void insert_end(int val) {
    struct Node* newNode = malloc(sizeof(struct Node));
    newNode->data = val;
    newNode->next = NULL;
    if (!head) head = newNode;
    else {
        struct Node* temp = head;
        while (temp->next) temp = temp->next;
        temp->next = newNode;
    }
}

void delete_val(int val) {
    struct Node *temp = head, *prev = NULL;
    while (temp && temp->data != val) { prev = temp; temp = temp->next; }
    if (!temp) return;
    if (!prev) head = temp->next;
    else prev->next = temp->next;
    free(temp);
}

void display() {
    struct Node* temp = head;
    while (temp) { printf("%d ", temp->data); temp = temp->next; }
    printf("\n");
}

int main() {
    int ch, val;
    while (1) {
        printf("1.Insert 2.Delete 3.Display 4.Exit: ");
        scanf("%d", &ch);
        if (ch == 1) { printf("Enter value: "); scanf("%d", &val); insert_end(val); }
        else if (ch == 2) { printf("Enter value: "); scanf("%d", &val); delete_val(val); }
        else if (ch == 3) display();
        else break;
    }
}


---

8. Double Linked List Operations

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *prev, *next;
} *head = NULL;

void insert_end(int val) {
    struct Node* newNode = malloc(sizeof(struct Node));
    newNode->data = val; newNode->next = NULL; newNode->prev = NULL;
    if (!head) head = newNode;
    else {
        struct Node* temp = head;
        while (temp->next) temp = temp->next;
        temp->next = newNode; newNode->prev = temp;
    }
}

void delete_val(int val) {
    struct Node* temp = head;
    while (temp && temp->data != val) temp = temp->next;
    if (!temp) return;
    if (temp->prev) temp->prev->next = temp->next;
    else head = temp->next;
    if (temp->next) temp->next->prev = temp->prev;
    free(temp);
}

void display() {
    struct Node* temp = head;
    while (temp) { printf("%d ", temp->data); temp = temp->next; }
    printf("\n");
}

int main() {
    int ch, val;
    while (1) {
        printf("1.Insert 2.Delete 3.Display 4.Exit: ");
        scanf("%d", &ch);
        if (ch == 1) { printf("Enter value: "); scanf("%d", &val); insert_end(val); }
        else if (ch == 2) { printf("Enter value: "); scanf("%d", &val); delete_val(val); }
        else if (ch == 3) display();
        else break;
    }
}


---

9. Polynomial Addition Using Linked List

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int coeff, pow;
    struct Node* next;
};

struct Node* create(int n) {
    struct Node* head = NULL, *temp = NULL;
    for (int i = 0; i < n; i++) {
        struct Node* newNode = malloc(sizeof(struct Node));
        printf("Coeff and power: ");
        scanf("%d%d", &newNode->coeff, &newNode->pow);
        newNode->next = NULL;
        if (!head) head = temp = newNode;
        else { temp->next = newNode; temp = newNode; }
    }
    return head;
}

struct Node* add(struct Node* p1, struct Node* p2) {
    struct Node* res = NULL, **tail = &res;
    while (p1 && p2) {
        struct Node* newNode = malloc(sizeof(struct Node));
        if (p1->pow > p2->pow) { *newNode = *p1; p1 = p1->next; }
        else if (p1->pow < p2->pow) { *newNode = *p2; p2 = p2->next; }
        else { newNode->pow = p1->pow; newNode->coeff = p1->coeff + p2->coeff; p1 = p1->next; p2 = p2->next; }
        newNode->next = NULL; *tail = newNode; tail = &newNode->next;
    }
    while (p1 || p2) {
        struct Node* src = p1 ? p1 : p2;
        struct Node* newNode = malloc(sizeof(struct Node));
        *newNode = *src; newNode->next = NULL;
        *tail = newNode; tail = &newNode->next;
        if (p1) p1 = p1->next; else p2 = p2->next;
    }
    return res;
}

void display(struct Node* p) {
    while (p) { printf("%dx^%d ", p->coeff, p->pow); p = p->next; if (p) printf("+ "); }
    printf("\n");
}

int main() {
    int n1, n2;
    printf("Terms in 1st: "); scanf("%d", &n1);
    struct Node* p1 = create(n1);
    printf("Terms in 2nd: "); scanf("%d", &n2);
    struct Node* p2 = create(n2);
    struct Node* sum = add(p1, p2);
    printf("Result: "); display(sum);
}


---

10. DFS and BFS

#include <stdio.h>

int adj[10][10], visited[10], n;

void dfs(int v) {
    printf("%d ", v);
    visited[v] = 1;
    for (int i = 0; i < n; i++)
        if (adj[v][i] && !visited[i]) dfs(i);
}

void bfs(int start) {
    int q[10], f = 0, r = 0;
    visited[start] = 1;
    q[r++] = start;
    while (f < r) {
        int v = q[f++];
        printf("%d ", v);
        for (int i = 0; i < n; i++)
            if (adj[v][i] && !visited[i]) {
                visited[i] = 1;
                q[r++] = i;
            }
    }
}

int main() {
    int start, ch;
    printf("Enter number of vertices: ");
    scanf("%d", &n);
    printf("Enter adjacency matrix:\n");
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            scanf("%d", &adj[i][j]);
    printf("Start vertex: ");
    scanf("%d", &start);
    printf("1.DFS 2.BFS: ");
    scanf("%d", &ch);
    for (int i = 0; i < n; i++) visited[i] = 0;
    if (ch == 1) dfs(start);
    else bfs(start);
    printf("\n");
}


---

11. Selection Sort

#include <stdio.h>

int main() {
    int n;
    printf("Enter size: ");
    scanf("%d", &n);
    int arr[n];
    printf("Enter elements: ");
    for (int i = 0; i < n; i++) scanf("%d", &arr[i]);

    for (int i = 0; i < n - 1; i++) {
        int min = i;
        for (int j = i + 1; j < n; j++)
            if (arr[j] < arr[min]) min = j;
        int temp = arr[i]; arr[i] = arr[min]; arr[min] = temp;
    }

    printf("Sorted: ");
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
}

