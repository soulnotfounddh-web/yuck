Ex-1

#include <stdio.h>
#include <stdlib.h>

struct node {
    int value;
    struct node *next;
};

void printLinkedlist(struct node* p) {
    while (p != NULL) {
        printf("%d ", p->value);
        p = p->next;
    }
}

int main() {
    struct node* head;
    struct node* one = NULL;
    struct node* two = NULL;
    struct node* three = NULL;
    one = malloc(sizeof(struct node));
    two = malloc(sizeof(struct node));
    three = malloc(sizeof(struct node));
    one->value = 1;
    two->value = 2;
    three->value = 3;
    one->next = two;
    two->next = three;
    three->next = NULL;
    head = one;
    printLinkedlist(head);
    return 0;
}



Ex-2

#include <stdlib.h>
#include <stdio.h>

struct node {
    int data;
    struct node *left;
    struct node *right;
};

struct node *root = NULL;

void insert(int data) {
    struct node *tempnode = (struct node*) malloc(sizeof(struct node));
    struct node *current;
    struct node *parent;
    tempnode->data = data;
    tempnode->left = NULL;
    tempnode->right = NULL;
    if (root == NULL) {
        root = tempnode;
        return;
    } else {
        current = root;
        parent = NULL;
        while (1) {
            parent = current;
            if (data < parent->data) {
                current = current->left;
                if (current == NULL) {
                    parent->left = tempnode;
                    return;
                }
            } else {
                current = current->right;
                if (current == NULL) {
                    parent->right = tempnode;
                    return;
                }
            }
        }
    }
}

struct node* search(int data) {
    struct node *current = root;
    printf("Visiting elements: ");
    while (current != NULL && current->data != data) {
        printf("%d ", current->data);
        if (data < current->data)
            current = current->left;
        else
            current = current->right;
    }
    return current;
}

int main() {
    int arr[7] = {27, 14, 35, 10, 19, 31, 42};
    int i;
    for (i = 0; i < 7; i++)
        insert(arr[i]);
    i = 31;
    struct node *temp = search(i);
    if (temp != NULL) {
        printf("\n[%d] Element found\n", temp->data);
    } else {
        printf("\n%d Element not found\n", i);
    }
    i = 15;
    temp = search(i);
    if (temp != NULL) {
        printf("\n[%d] Element found\n", temp->data);
    } else {
        printf("\n%d Element not found\n", i);
    }
    return 0;
}


Ex-3


#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
};

struct node *head = NULL, *tail = NULL;

void addnode(int data) {
    struct node* new_node = (struct node*) malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    if (head == NULL) {
        head = new_node;
        tail = new_node;
    } else {
        tail->next = new_node;
        tail = new_node;   // FIXED missing semicolon
    }
}

void sortlist() {
    struct node* current = head;
    struct node* index = NULL;
    int temp;
    if (head == NULL) {
        return;
    } else {
        while (current != NULL) {
            index = current->next;
            while (index != NULL) {
                if (current->data > index->data) {
                    temp = current->data;
                    current->data = index->data;
                    index->data = temp;
                }
                index = index->next;
            }
            current = current->next;
        }
    }
}

void display() {
    struct node* current = head;
    if (head == NULL) {
        printf("List is empty\n");
        return;
    }
    while (current != NULL) {
        printf("%d ", current->data);
        current = current->next;
    }
    printf("\n");
}

int main() {
    addnode(9);
    addnode(7);
    addnode(11);
    addnode(15);
    addnode(2);
    printf("Original List:\n");
    display();
    sortlist();
    printf("Sorted List:\n");
    display();
    return 0;
}

Ex-4

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

struct node {
    int key;
    struct node* next;
};

void push(struct node** head_ref, int new_key) {
    struct node* new_node = (struct node*) malloc(sizeof(struct node));
    new_node->key = new_key;
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}

bool search(struct node* head, int x) {
    struct node* current = head;
    while (current != NULL) {
        if (current->key == x)
            return true;
        current = current->next;
    }
    return false;
}

int main() {
    struct node* head = NULL;
    push(&head, 10);
    push(&head, 15);
    push(&head, 20);
    push(&head, 48);
    if (search(head, 48))
        printf("Yes");
    else
        printf("No");
    return 0;
}

Ex-5

#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
};

struct node* head = NULL;

void push(int val) {
    struct node* newnode = (struct node*) malloc(sizeof(struct node));
    newnode->data = val;
    newnode->next = head;
    head = newnode;
}

void pop() {
    struct node* temp;
    if (head == NULL)
        printf("Stack is empty \n");
    else {
        printf("Poped element %d\n", head->data);
        temp = head;
        head = head->next;
        free(temp);
    }
}

void printlist() {
    struct node* temp = head;
    while (temp != NULL) {
        printf("\t %d", temp->data);
        temp = temp->next;
    }
    printf("\t NULL\n");
}

int main() {
    push(20);
    push(30);
    push(40);
    printlist();
    pop();
    printlist();
    return 0;
}


Ex-6

#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
};

struct node* front = NULL;
struct node* rear = NULL;

void enqueue(int value) {
    struct node* ptr = (struct node*) malloc(sizeof(struct node));
    ptr->data = value;
    ptr->next = NULL;
    if (front == NULL && rear == NULL) {
        front = rear = ptr;
    } else {
        rear->next = ptr;
        rear = ptr;
    }
    printf("Node is inserted\n\n");
}

int dequeue() {
    if (front == NULL) {
        printf("\nUnderflow\n");
        return -1;
    } else {
        struct node* temp = front;
        int temp_data = front->data;
        front = front->next;
        free(temp);
        return temp_data;
    }
}

void display() {
    struct node* temp;
    if (front == NULL && rear == NULL) {
        printf("\nQueue is empty\n");
    } else {
        printf("The queue is:\n");
        temp = front;
        while (temp) {
            printf("%d ---> ", temp->data);
            temp = temp->next;
        }
        printf("NULL\n\n");
    }
}

int main() {
    int choice = 0, value;
    printf("Implementation of queue using linked list\n");
    while (choice != 4) {
        printf("1. Enqueue\n2. Dequeue\n3. Display\n4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        switch (choice) {
            case 1:
                printf("\nEnter the value to insert: ");
                scanf("%d", &value);
                enqueue(value);
                break;
            case 2:
                printf("Popped Element is: %d\n", dequeue());
                break;
            case 3:
                display();
                break;
            case 4:
                printf("Exiting...\n");
                return 0;
            default:
                printf("\nWrong choice\n");
        }
    }
    return 0;
}


Ex-7


#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
    struct Node* prev;
};

void insertFront(struct Node** head, int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = (*head);
    newNode->prev = NULL;
    if((*head) != NULL)
        (*head)->prev = newNode;
    (*head) = newNode;
}

void insertAfter(struct Node* prev_node, int data) {
    if(prev_node == NULL) {
        printf("Previous node cannot be null");
        return;
    }
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = prev_node->next;
    prev_node->next = newNode;
    newNode->prev = prev_node;
    if(newNode->next != NULL)
        newNode->next->prev = newNode;
}

void insertEnd(struct Node** head, int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;
    struct Node* temp = *head;
    if(*head == NULL) {
        newNode->prev = NULL;
        *head = newNode;
        return;
    }
    while(temp->next != NULL)
        temp = temp->next;
    temp->next = newNode;
    newNode->prev = temp;
}

void deleteNode(struct Node** head, struct Node* del_node) {
    if(*head == NULL || del_node == NULL)
        return;
    if(*head == del_node)
        *head = del_node->next;
    if(del_node->next != NULL)
        del_node->next->prev = del_node->prev;
    if(del_node->prev != NULL)
        del_node->prev->next = del_node->next;
    free(del_node);
}

void displayList(struct Node* node) {
    struct Node* last;
    while(node != NULL) {
        printf("%d->", node->data);
        last = node;
        node = node->next;
    }
    if(node == NULL)
        printf("NULL\n");
}

int main() {
    struct Node* head = NULL;
    insertEnd(&head, 5);
    insertFront(&head, 1);
    insertFront(&head, 6);
    insertEnd(&head, 9);
    insertAfter(head, 11);
    insertAfter(head->next, 15);
    displayList(head);
    deleteNode(&head, head->next->next->next->next->next);
    displayList(head);
    return 0;
}

Ex-8

#include<stdio.h>

int main() {
    int arr[10], no, i, j, c, heap_root, temp;
    printf("Input number of elements:");
    scanf("%d", &no);
    printf("\nInput array values one by one: ");
    for(i = 0; i < no; i++)
        scanf("%d", &arr[i]);
    for(i = 1; i < no; i++) {
        c = i;
        do {
            heap_root = (c - 1) / 2;
            if(arr[heap_root] < arr[c]) {
                temp = arr[heap_root];
                arr[heap_root] = arr[c];
                arr[c] = temp;
            }
            c = heap_root;
        } while(c != 0);
    }
    printf("Heap array: ");
    for(i = 0; i < no; i++)
        printf("%d \t", arr[i]);
    for(j = no - 1; j >= 0; j--) {
        temp = arr[0];
        arr[0] = arr[j];
        arr[j] = temp;
        heap_root = 0;
        do {
            c = 2 * heap_root + 1;
            if((arr[c] < arr[c + 1]) && c < j - 1)
                c++;
            if(arr[heap_root] < arr[c] && c < j) {
                temp = arr[heap_root];
                arr[heap_root] = arr[c];
                arr[c] = temp;
            }
            heap_root = c;
        } while(c < j);
    }
    printf("\nSorted array:");
    for(i = 0; i < no; i++)
        printf("\t%d", arr[i]);
    printf("\n");
}


Ex- 9

#include<stdio.h>
#include<ctype.h>

char stack[20];
int top = -1;

void push(char x) {
    stack[++top] = x;
}

char pop() {
    if(top == -1)
        return -1;
    else
        return stack[top--];
}

int priority(char x) {
    if(x == '(')
        return 0;
    if(x == '+' || x == '-')
        return 1;
    if(x == '*' || x == '/')
        return 2;
}

int main() {
    char exp[20];
    char *e, x;
    printf("Enter the expression:");
    scanf("%s", exp);
    e = exp;
    while(*e != '\0') {
        if(isalnum(*e))
            printf("%c", *e);
        else if(*e == '(')
            push(*e);
        else if(*e == ')') {
            while((x = pop()) != '(')
                printf("%c", x);
        } else {
            while(priority(stack[top]) >= priority(*e))
                printf("%c", pop());
            push(*e);
        }
        e++;
    }
    while(top != -1) {
        printf("%c", pop());
    }
}

Ex-10

#include <stdio.h>

int max(int a, int b) {
    return (a > b) ? a : b;
}

int knapSack(int W, int wt[], int val[], int n) {
    int i, w;
    int K[n + 1][W + 1];
    for(i = 0; i <= n; i++) {
        for(w = 0; w <= W; w++) {
            if(i == 0 || w == 0)
                K[i][w] = 0;
            else if(wt[i - 1] <= w)
                K[i][w] = max(val[i - 1] + K[i - 1][w - wt[i - 1]], K[i - 1][w]);
            else
                K[i][w] = K[i - 1][w];
        }
    }
    return K[n][W];
}

int main() {
    int i, n, val[20], wt[20], W;
    printf("Enter number of items:");
    scanf("%d", &n);
    printf("Enter value and weight of items:\n");
    for(i = 0; i < n; ++i) {
        scanf("%d%d", &val[i], &wt[i]);
    }
    printf("Enter size of knapsack:");
    scanf("%d", &W);
    printf("%d", knapSack(W, wt, val, n));
    return 0;
}


Ex-11


#include <stdio.h>
#include <limits.h>

#define V 5

int minKey(int key[], int mstSet[]) {
    int min = INT_MAX, min_index;
    int v;
    for(v = 0; v < V; v++)
        if(mstSet[v] == 0 && key[v] < min)
            min = key[v], min_index = v;
    return min_index;
}

int printMST(int parent[], int n, int graph[V][V]) {
    int i;
    printf("Edge   Weight\n");
    for(i = 1; i < V; i++)
        printf("%d - %d    %d\n", parent[i], i, graph[i][parent[i]]);
}

void primMST(int graph[V][V]) {
    int parent[V];
    int key[V], mstSet[V];
    int i, v, count;
    for(i = 0; i < V; i++)
        key[i] = INT_MAX, mstSet[i] = 0;
    key[0] = 0;
    parent[0] = -1;
    for(count = 0; count < V - 1; count++) {
        int u = minKey(key, mstSet);
        mstSet[u] = 1;
        for(v = 0; v < V; v++)
            if(graph[u][v] && mstSet[v] == 0 && graph[u][v] < key[v])
                parent[v] = u, key[v] = graph[u][v];
    }
    printMST(parent, V, graph);
}

int main() {
    int graph[V][V] = {
        {0, 2, 0, 6, 0},
        {2, 0, 3, 8, 5},
        {0, 3, 0, 0, 7},
        {6, 8, 0, 0, 9},
        {0, 5, 7, 9, 0}
    };
    primMST(graph);
    return 0;
}



Ex-12

#include <stdio.h>
#include <math.h>

int board[20], count;

void queen(int row, int n);
void print(int n);
int place(int row, int column);

int main() {
    int n;
    printf("- N Queens Problem Using Backtracking -");
    printf("\n\nEnter number of Queens:");
    scanf("%d", &n);
    queen(1, n);
    return 0;
}

void print(int n) {
    int i, j;
    printf("\n\nSolution %d:\n\n", ++count);
    for(i = 1; i <= n; ++i)
        printf(" %d", i);
    for(i = 1; i <= n; ++i) {
        printf("\n\n%d", i);
        for(j = 1; j <= n; ++j) {
            if(board[i] == j)
                printf("\tQ");
            else
                printf("\t-");
        }
    }
}

int place(int row, int column) {
    int i;
    for(i = 1; i <= row - 1; ++i) {
        if(board[i] == column)
            return 0;
        else if(abs(board[i] - column) == abs(i - row))
            return 0;
    }
    return 1;
}

void queen(int row, int n) {
    int column;
    for(column = 1; column <= n; ++column) {
        if(place(row, column)) {
            board[row] = column;
            if(row == n)
                print(n);
            else
                queen(row + 1, n);
        }
    }
}


Ex-14


#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* left;
    struct node* right;
};

void inorder(struct node* root) {
    if(root == NULL)
        return;
    inorder(root->left);
    printf("%d->", root->data);
    inorder(root->right);
}

void preorder(struct node* root) {
    if(root == NULL)
        return;
    printf("%d->", root->data);
    preorder(root->left);
    preorder(root->right);
}

void postorder(struct node* root) {
    if(root == NULL)
        return;
    postorder(root->left);
    postorder(root->right);
    printf("%d->", root->data);
}

struct node* createNode(int value) {
    struct node* newNode = (struct node*)malloc(sizeof(struct node));
    newNode->data = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

struct node* insertleft(struct node* root, int value) {
    root->left = createNode(value);
    return root->left;
}

struct node* insertright(struct node* root, int value) {
    root->right = createNode(value);
    return root->right;
}

int main() {
    struct node* root = createNode(1);
    insertleft(root, 12);
    insertright(root, 9);
    insertleft(root->left, 5);
    insertright(root->left, 6);
    printf("inorder traversal\n");
    inorder(root);
    printf("\n preorder traversal\n");
    preorder(root);
    printf("\n postorder traversal\n");
    postorder(root);
    return 0;
}


