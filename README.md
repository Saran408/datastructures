# Datastructures

## Module 13

Write a C program to display the priority of the operators in the given Infix expression using switch case statements.
"+ * A B - C D" . int priority(char x) receive operators in the expression from the main() and returns the value of the operator precedence from  lowest to highest [ eg., &,| returns 1(lowest priority) ,

*,/ returns 4 (highest priority)]

For example:

Result
+  ----> Second Lowest Priority
*  ----> Second Highest Priority
-  ----> Second Lowest Priority

```c
#include <stdio.h>
#include<string.h>

    
 int main()
{
   int i,j;
   char ch[100]="+ * A B - C D";
   
   for(i=0;i<strlen(ch);i++)
   {
   if(ch[i]=='+'||
   ch[i]=='-'||
   ch[i]=='*'||
   ch[i]=='/'||
   ch[i]=='%'||
   ch[i]=='^'||
   ch[i]=='&'||
   ch[i]=='|')
       {
       j=priority(ch[i]);
       switch(j)
       {
           case 1:
             printf("%c  ----> ",ch[i]);
           printf("Lowest Priority\n");
             break;
            case 2:
             printf("%c  ----> ",ch[i]);
           printf("Second Lowest Priority\n");
             break;
            case 3:
             printf("%c  ----> ",ch[i]);
           printf("Second Highest Priority\n"); 
             break;
            case 4:
             printf("%c  ----> ",ch[i]);
           printf("Highest Priority\n");
             break;
       }
       }
   }
   
    return 0;
}
```

### Day 2

Write C functions to perform push and pop opertion of the stack in the infix to postfix conversion program.

For example:

Input	Result
a+b
 
ab+

```c
char stack[100];
int top = -1;
void push(char x)
{
    stack[++top] = x;
}

char pop()
{
    if(top == -1)
        return -1;
    else
        return stack[top--];
}
```
Write a C function to convert the infix expression into postfix form.

infix expression is "2-3+4-5*6 "

```c
char IntoPost(char *exp)
{
    char *e,x;
    e = exp;
  while(*e != '\0')
    {
        if(isalnum(*e))
            printf("%c",*e);
        else if(*e == '(')
            push(*e);
        else if(*e == ')')
        {
            while((x = pop()) != '(')
                printf("%c", x);
        }
        else
        {
            while(priority(stack[top]) >= priority(*e))
                printf("%c",pop());
            push(*e);
        }
        e++;
    }
    
    while(top != -1)
    {
        printf("%c",pop());
    } 
    return 1;
}
```

Write a C program to convert the infix expression

"a+(b|c-(d/e^f)*g)&h" into postfix form using stack. Follow the operator precedence and associative rule.

For example:

Result
a b c d e f ^ / g * - | + h &

```c
#include<stdio.h>
#include<ctype.h>

char stack[100];
int top = -1;

void push(char x)
{
    stack[++top] = x;
}

char pop()
{
    if(top == -1)
        return -1;
    else
        return stack[top--];
}
int priority(char x)
{
    if(x == '(')
        return 0;
    if(x == '&' || x == '|')
        return 1;
    if(x == '+' || x == '-')
        return 2;
    if(x == '*' || x == '/' || x == '%')
        return 3;
    if(x == '^')
        return 4;
    return 0;
}
char IntoPost(char *exp)
{
    char *e, x;
   
   
    e = exp;
    
    while(*e != '\0')
    {
        if(isalnum(*e))
            printf("%c ",*e);
        else if(*e == '(')
            push(*e);
        else if(*e == ')')
        {
            while((x = pop()) != '(')
                printf("%c ", x);
        }
        else
        {
            while(priority(stack[top]) >= priority(*e))
                printf("%c ",pop());
            push(*e);
        }
        e++;
    }
    
    while(top != -1)
    {
        printf("%c ",pop());
    }return 0;
}


int main()
{
    char exp[100]="a+(b|c-(d/e^f)*g)&h";
    IntoPost(exp);
    return 1;
    
}
```
Write a C function to find the precedence of the operators ( lowest to highest precedence - 1,2,3,4 ) in the given infix to postfix conversion program. Infix expression is "(A+B)&C+(D%H)/F+G"

```c
int priority(char x)
{
    if(x == '(')
        return 0;
    if(x == '&' || x == '|')
        return 1;
    if(x == '+' || x == '-')
        return 2;
    if(x == '*' || x == '/' || x == '%')
        return 3;
    if(x == '^')
        return 4;
    return 0;
}
```

### Day 3
Write a C function to implement tower of hanoi using recursion 
for no of disks "n".
Display all the moves of the disks as output.

For example:

Input	Result
3
A to B
A to C
B to C
A to B
C to A
C to B
A to B

```c
void TOH(int n,char x,char y,char z)
{
if(n>0)
   {
      TOH(n-1,x,z,y);
      printf("%c to %c",x,y);
      printf("\n");
      TOH(n-1,z,y,x);
   }
}
```
Write a C function to evaluate the post fix expression using Stack for 231*+9+  and also print the output of the given post fix expression inside the function. The input of the post fix expression involves only addition and multiplication .
   
   
 ```c
 int stack[20];
int top = -1;

void push(int x)
{
    stack[++top] = x;
}

int pop()
{
    return stack[top--];
}

void evalpostfix(char *e)
{
    int n1,n2,n3,num;
    while(*e != '\0')
    {
        if(isdigit(*e))
        {
            num = *e - 48;
            push(num);
        }
        else
        {
            n1 = pop();
            n2 = pop();
            switch(*e)
            {
            case '+':
            {
                n3 = n1 + n2;
                break;
            }
          
            case '*':
            {
                n3 = n1 * n2;
                break;
            }
            }
            push(n3);
        }
        e++;
    }
    printf("%d",pop());

}
```

Write a C Program for evaluating the given post fix expression 53+82-*  using stack and display the output of the given post fix  expression inside the function . Use push() and pop() function for storing and retrieving the operands.
```c
#include<stdio.h>
#include<ctype.h>
int stack[20];
int top = -1;

void push(int x)
{
    stack[++top] = x;
}

int pop()
{
    return stack[top--];
}

void evalpostfix(char *exp)
{
     int n1,n2,n3,num;
     char *e;
    e = exp;
    while(*e != '\0')
    {
        if(isdigit(*e))
        {
            num = *e - 48;
            push(num);
        }
        else
        {
            n1 = pop();
            n2 = pop();
            switch(*e)
            {
            case '+':
            {
                n3 = n1 + n2;
                break;
            }
            case '-':
            {
                n3 = n2 - n1;
                break;
            }
            case '*':
            {
                n3 = n1 * n2;
                break;
            }
            case '/':
            {
                n3 = n2 / n1;
                break;
            }
            }
            push(n3);
        }
        e++;
    }
    printf("%d",pop());
}

int main()
{
   char exp[20]="53+82-*";
    evalpostfix(exp);
    return 0;
}
```

### Day 4

Write a C function to evaluate the prefix expression 

"+-927"  using stack  and print the output of the given prefix expression from the stack inside the function. The input expression contains only addition and subtraction. 

```c
   int s[50];
int top=0;

void push(int ch)
{
	top++;
	s[top]=ch;
}

int pop()
{
	int ch;
	ch=s[top];
	top=top-1;
	return(ch);
}

void evalprefix(char p[50])
{ int a,b,c,i;
    for(i=strlen(p)-1;i>=0;i--)
	{
		
		if(p[i]=='+')
		{
		a=pop();
		b=pop();
		c=a+b;
		push(c);
		}
		else if(p[i]=='-')
		{
		a=pop();
		b=pop();
		c=a-b;
		push(c);
		}
	   else
		{
			push(p[i]-48);
		}
			
	}
	printf("%d",pop());
}
```

Write a C program for evaluation of prefix expression  

*+69-31*+   using Stack and display the output of the given Prefix  expression inside the function.  Use push() and pop() function for storing and retrieving the operands.

```c
#include<stdio.h>
#include<string.h>
#include<ctype.h>

int s[50];
int top=0;

void push(int ch)
{
	top++;
	s[top]=ch;
}

int pop()
{
	int ch;
	ch=s[top];
	top=top-1;
	return(ch);
}

void evalprefix(char prefix[50])
{
    	int a,b,c,i;
    	for(i=strlen(prefix)-1;i>=0;i--)
	{
		if(prefix[i]=='+')
		{
			c=pop()+pop();
			push(c);
		}
		else if(prefix[i]=='-')
		{
			a=pop();
			b=pop();
			c=a-b;
			push(c);
		}
		else if(prefix[i]=='*')
		{	
		a=pop();
		b=pop();
		c=b*a;
		push(c);
		}
		else if(prefix[i]=='/')
		{
			a=pop();
			b=pop();
			c=a/b;
			push(c);
		}
		else
		{
			push(prefix[i]-48);
		}
	}
	printf("%d",pop());
    
}

int  main()
{
	char prefix[50]="*+69-31";
	evalprefix(prefix);
	return 0;
}
```


## Module 14
### Day 1
Incorporate the full queue check code to insert elements into the circular queue.

```c
int isFull() {
  if ((front == rear + 1) || (front == 0 && rear == SIZE - 1)) return 1;
  return 0;
}
```
Formulate the code within the main function to insert element "8" into the filled circular queue after two dequeue operations.

```c
int main() {
 
  int m,t,k;
  scanf("%d",&m);
  for(k=0;k<m;k++)
  {  scanf("%d",&t);
     enQueue(t);
  }
  display();
  deQueue();
  display();
  deQueue();
  display();
  enQueue(8);
  display();
  return 0;
}
```
Compose the code to insert elements 5,10,15,20,25 into the circular queue.

```c
void enQueue(int element) {
  if (isFull())
    printf("Queue is full!! \n");
  else {
    if (front == -1) front = 0;
    rear = (rear + 1) % SIZE;
    items[rear] = element;
    //printf(" Inserted -> %d \n", element);
  }
}
```

Integrate the code to display the elements of the circular queue.

```c
void display() {
  int i;
  if (isEmpty())
    printf("Empty Queue\n");
  else {
    printf(" Front -> %d ", front);
    printf(" Items -> ");
    for (i = front; i != rear; i = (i + 1) % SIZE) {
      printf("%d ", items[i]);
    }
    printf("%d ", items[i]);
    printf(" Rear -> %d \n", rear);
  }
}
```
Develop the code to delete an element from the circular queue.
```c
int deQueue() {
  int element;
  if (isEmpty()) {
    printf("Queue is empty !! \n");
    return (-1);
  } else {
    element = items[front];
    if (front == rear) {
      front = -1;
      rear = -1;
    } 
    // Q has only one element, so we reset the 
    // queue after dequeing it. 
    else {
      front = (front + 1) % SIZE;
    }
   // printf(" Deleted element -> %d \n", element);
    return (element);
  }
}

```

### Day 2
Compose the code to swap the elements in order to maintain the root element of the tree arranged in the priority queue as the largest.

```c
void swap(int *a, int *b) {
  int temp = *b;
  *b = *a;
  *a = temp;
}
```
Develop the code to heapify the priority queue elements after deletion according to the max-heap property.[If size=1 print "Single element in the heap" else determine the largest among i(root),l(left child),r(right child)and store it in the variable largest. Then, Call the swap procedure passing the reference of the index of the element to be deleted and the last element of the array. Call the heapify procedure passing three parameters (array,size,i)].

```c
void heapify(int array[], int size, int i) {
  if (size == 1) {
    printf("Single element in the heap");
  } else {
    // Find the largest among root, left child and right child
    int largest = i;
    int l = 2 * i + 1;
    int r = 2 * i + 2;
    if (l < size && array[l] > array[largest])
      largest = l;
    if (r < size && array[r] > array[largest])
      largest = r;

    // Swap and continue heapifying if root is not largest
    if (largest != i) {
      swap(&array[i], &array[largest]);
      heapify(array, size, largest);
    }
  }
}
```

Integrate the code to insert element(s) into the priority queue satisfying the max-heap property. Call the heapify procedure passing three parameters (array,size,i) to arrange the elements back according to the max-heap property. 
```c
void insert(int array[], int newNum) {
  if (size == 0) {
    array[0] = newNum;
    size += 1;
  } else {
    array[size] = newNum;
    size += 1;
    for (int i = size / 2 - 1; i >= 0; i--) {
      heapify(array, size, i);
    }
  }
}
```

Incorporate the code to delete an element from the priority queue and arrange the remaining elements according to the max-heap property. [Call the swap procedure passing the reference of the index of the element to be deleted and the last element of the array. Call the heapify procedure passing three parameters (array,size,i)].

```c
void deleteRoot(int array[], int num) {
  int i;
  for (i = 0; i < size; i++) {
    if (num == array[i])
      break;
  }
  swap(&array[i], &array[size - 1]);
  size -= 1;
  for (int i = size / 2 - 1; i >= 0; i--) {
    heapify(array, size, i);
  }
}
```

Formulate the code to display the elements of the tree in the priority queue satisfying the max-heap property.

```c
void printArray(int array[], int size) {
  for (int i = 0; i < size; ++i)
    printf("%d ", array[i]);
  printf("\n");
}
```

### Day 3
Formulate the code to insert elements at the front of the deQueue.

```c
void addFront(int *arr, int item, int *pfront, int *prear) {
  int i, k, c;

  if (*pfront == 0 && *prear == MAX - 1) {
    printf("deQueue is full.\n");
    return;
  }

  if (*pfront == -1) {
    *pfront = *prear = 0;
    arr[*pfront] = item;
    return;
  }

  if (*prear != MAX - 1) {
    c = count(arr);
    k = *prear + 1;
    for (i = 1; i <= c; i++) {
      arr[k] = arr[k - 1];
      k--;
    }
    arr[k] = item;
    *pfront = k;
    (*prear)++;
  } else {
    (*pfront)--;
    arr[*pfront] = item;
  }
}
```
 
Incorporate the code to delete elements from the front of the deQueue when it is not empty.
 
```c
int delFront(int *arr, int *pfront, int *prear) {
  int item;

  if (*pfront == -1) {
    printf("Deque is empty.\n");
    return 0;
  }

  item = arr[*pfront];
  arr[*pfront] = 0;

  if (*pfront == *prear)
    *pfront = *prear = -1;
  else
    (*pfront)++;

  return item;
}
```

The elements present in the deQueue are 6,8,10,12,14,16. Modify the main function to add two elements at the front of the deQueue and remove an element from the rear of the deQueue.

```c
int main() {
  int arr[MAX];
  int front, rear, i, m,j,t;

  front = rear = -1;
  for (i = 0; i < MAX; i++)
    arr[i] = 0;
 
  addRear(arr, 6, &front, &rear);
  addRear(arr, 8, &front, &rear);
  addRear(arr, 10, &front, &rear);
  addRear(arr, 12, &front, &rear);
  addRear(arr, 14, &front, &rear);
  addRear(arr, 16, &front, &rear);
 
  scanf("%d",&m);
  for(j=0;j<m;j++)
  {
   scanf("%d",&t);   
   addFront(arr, t, &front, &rear);
   
  }
  delRear(arr,&front,&rear);
  printf("Elements in the deQueue after insertion and deletion:\n ");
  display(arr);

}
```

Develop the code to delete elements from the rear of the deQueue
```c
int delRear(int *arr, int *pfront, int *prear) {
  int item;

  if (*pfront == -1) {
    printf("deQueue is empty.\n");
    return 0;
  }

  item = arr[*prear];
  arr[*prear] = 0;
  (*prear)--;
  if (*prear == -1)
    *pfront = -1;
  return item;
}
```
Compose the code to insert elements at the rear of the deQueue.
```c
void addRear(int *arr, int item, int *pfront, int *prear) {
  int i, k;

  if (*pfront == 0 && *prear == MAX - 1) {
    printf("deQueue is full.\n");
    return;
  }

  if (*pfront == -1) {
    *prear = *pfront = 0;
    arr[*prear] = item;
    return;
  }

  if (*prear == MAX - 1) {
    k = *pfront - 1;
    for (i = *pfront - 1; i < *prear; i++) {
      k = i;
      if (k == MAX - 1)
        arr[k] = 0;
      else
        arr[k] = arr[i + 1];
    }
    (*prear)--;
    (*pfront)--;
  }
  (*prear)++;
  arr[*prear] = item;
}
```

### Day 4

Formulate the code to calculate the turnaround time of each process given their burst time and waiting time in First Come first Serve scheduling algorithm.

```c
int turnaroundtime( int proc[], int n,int burst_time[], int wait_time[], int tat[]) {
   // calculating turnaround time by adding
   // burst_time[i] + wait_time[i]
   int i;
   for ( i = 0; i < n ; i++)
   tat[i] = burst_time[i] + wait_time[i];
   return 0;
}
```

Incorporate the code to sort the burst times of the processes in Shortest Job First scheduling algorithm.

```c
#include<stdio.h>
 
int main()
{
    int bt[20],p[20],wt[20],tat[20],i,j,n,total=0,pos,temp;
    float avg_wt,avg_tat;
    //printf("Enter number of process:");
    scanf("%d",&n);
 
   // printf("\nEnter Burst Time:\n");
    for(i=0;i<n;i++)
    {
      //  printf("p%d:",i+1);
        scanf("%d",&bt[i]);
        p[i]=i+1;           //contains process number
    }
 
    //sorting burst time in ascending order using selection sort
    for(i=0;i<n;i++)
    {
        pos=i;
        for(j=i+1;j<n;j++)
        {
            if(bt[j]<bt[pos])
                pos=j;
        }
 
        temp=bt[i];
        bt[i]=bt[pos];
        bt[pos]=temp;
 
        temp=p[i];
        p[i]=p[pos];
        p[pos]=temp;
    }
 
    wt[0]=0;            //waiting time for first process will be zero
 
    //calculate waiting time
    for(i=1;i<n;i++)
    {
        wt[i]=0;
        for(j=0;j<i;j++)
            wt[i]+=bt[j];
 
        total+=wt[i];
    }
 
    avg_wt=(float)total/n;      //average waiting time
    total=0;
 
    printf("Process    Burst Time    Waiting Time  Turnaround Time\n");
    for(i=0;i<n;i++)
    {
        tat[i]=bt[i]+wt[i];     //calculate turnaround time
        total+=tat[i];
        //printf("\n");
        printf("p%d          %d               %d             %d\n",p[i],bt[i],wt[i],tat[i]);
    }
 
    avg_tat=(float)total/n;     //average turnaround time
   // printf("\n");
    printf("Average Waiting Time=%f\n",avg_wt);
  //  printf("\n");
    printf("Average Turnaround Time=%f\n",avg_tat);
    return 0;
}
```

Compose the code to calculate the waiting time of each process given their burst time in First Come first Serve Scheduling algorithm.

```c
int waitingtime(int proc[], int n,int burst_time[], int wait_time[]) {
   // waiting time for first process is 0
   wait_time[0] = 0;
   // calculating waiting time
   for (int i = 1; i < n ; i++ )
   wait_time[i] = burst_time[i-1] + wait_time[i-1] ;
   return 0;
}
```

Integrate the code to calculate the Waiting Time and the Turn Around Time for each process in Round Robin scheduling algorithm.

```c
#include<stdio.h>  

int main()  
{  
    // initlialize the variable name  
    int i, NOP, sum=0,count=0, y, quant, wt=0, tat=0, at[10], bt[10], temp[10];  
    float avg_wt, avg_tat;  
   // printf(" Total number of process in the system: ");  
    scanf("%d", &NOP);  
    y = NOP; // Assign the number of process to variable y  
  
// Use for loop to enter the details of the process like Arrival time and the Burst Time  
for(i=0; i<NOP; i++)  
{  
//printf("\n Enter the Arrival and Burst time of the Process[%d]\n", i+1);  
//printf(" Arrival time is: \t");  // Accept arrival time  
scanf("%d", &at[i]);  
//printf(" \nBurst time is: \t"); // Accept the Burst time  
scanf("%d", &bt[i]);  
temp[i] = bt[i]; // store the burst time in temp array  
}  
// Accept the Time quantum  
//printf("Enter the Time Quantum for the process: \t");  
scanf("%d", &quant);  
// Display the process No, burst time, Turn Around Time and the waiting time  
printf("  Process No \t\tBurst Time \t\tTAT \t\tWaiting Time ");  

for(sum=0, i = 0; y!=0; )  
{  
if(temp[i] <= quant && temp[i] > 0) // define the conditions   
{  
    sum = sum + temp[i];  
    temp[i] = 0;  
    count=1;  
    }     
    else if(temp[i] > 0)  
    {  
        temp[i] = temp[i] - quant;  
        sum = sum + quant;    
    }  
    if(temp[i]==0 && count==1)  
    {  
        y--; //decrement the process no.  
        printf("\n  Process No[%d] \t\t %d\t\t\t\t %d\t\t\t %d", i+1, bt[i], sum-at[i], sum-at[i]-bt[i]);  
        wt = wt+sum-at[i]-bt[i];  
        tat = tat+sum-at[i];  
        count =0;     
    }  
    if(i==NOP-1)  
    {  
        i=0;  
    }  
    else if(at[i+1]<=sum)  
    {  
        i++;  
    }  
    else  
    {  
        i=0;  
    }  
}  
// represents the average waiting time and Turn Around time  
avg_wt = wt * 1.0/NOP;  
avg_tat = tat * 1.0/NOP;  
printf("\n Average Turn Around Time: \t%f", avg_wt);  
printf("\n Average Waiting Time: \t%f", avg_tat);  

}  
```
Formulate the code for the bfs function in order to traverse the graph below in the breadth first manner.

```c
void bfs(struct Graph* graph, int startVertex) {
  struct queue* q = createQueue();
 
  graph->visited[startVertex] = 1;
  enqueue(q, startVertex);
 
  while (!isEmpty(q)) {
    printQueue(q);
    int currentVertex = dequeue(q);
    printf("Visited %d\n ", currentVertex);
   
    struct node* temp = graph->adjLists[currentVertex];
 
    while (temp) {
      int adjVertex = temp->vertex;
 
      if (graph->visited[adjVertex] == 0) {
        graph->visited[adjVertex] = 1;
        enqueue(q, adjVertex);
      }
      temp = temp->next;
    }
  }
}
```

## Module 15
### Day 1 
Complete the  function in the editor below. It received  parameter: a pointer to the root of a binary tree. It must print the values in the tree's postorder traversal as a single line of space-separated values.

Input Format

Our test code passes the root node of a binary tree to the  function.

Constraints

 Nodes in the tree  

Output Format

Print the tree's postorder traversal as a single line of space-separated values.

Sample Input

1 2 5 3 6 4
Sample Output

4 3 6 5 2 1 

For example:

Input	Result
6
1 2 5 3 6 4
4 3 6 5 2 1

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};

struct node* insert( struct node* root, int data ) {
		
	if(root == NULL) {
	
        struct node* node = (struct node*)malloc(sizeof(struct node));

        node->data = data;

        node->left = NULL;
        node->right = NULL;
        return node;
	  
	} else {
      
		struct node* cur;
		
		if(data <= root->data) {
            cur = insert(root->left, data);
            root->left = cur;
		} else {
            cur = insert(root->right, data);
            root->right = cur;
		}
	
		return root;
	}
}

/* you only have to complete the function given below.  
node is defined as  

struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};

*/
void postOrder( struct node *root) {
if(root==NULL)
return;
postOrder(root->left);
postOrder(root->right);
printf("%d ",root->data);
}


int main() {
  
    struct node* root = NULL;
    
    int t;
    int data;

    scanf("%d", &t);

    while(t-- > 0) {
        scanf("%d", &data);
        root = insert(root, data);
    }
  
	postOrder(root);
    return 0;
}
```

Complete the  function in the editor below, which has  parameter: a pointer to the root of a binary tree. It must print the values in the tree's preorder traversal as a single line of space-separated values.

Input Format

Our test code passes the root node of a binary tree to the preOrder function.

Constraints

 Nodes in the tree 

Output Format

Print the tree's preorder traversal as a single line of space-separated values.

Sample Input

6

1 2 5 3 6 4

Sample Output
1 2 5 3 4 6 

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};

struct node* insert( struct node* root, int data ) {
		
	if(root == NULL) {
	
        struct node* node = (struct node*)malloc(sizeof(struct node));

        node->data = data;

        node->left = NULL;
        node->right = NULL;
        return node;
	  
	} else {
      
		struct node* cur;
		
		if(data <= root->data) {
            cur = insert(root->left, data);
            root->left = cur;
		} else {
            cur = insert(root->right, data);
            root->right = cur;
		}
	
		return root;
	}
}

/* you only have to complete the function given below.  
node is defined as  

struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};

*/
void preOrder( struct node *root) {
     if (root == NULL)  
        return;  
    printf("%d ", root->data);  
    preOrder(root->left);  
    preOrder(root->right); 
}


int main() {
  
    struct node* root = NULL;
    
    int t;
    int data;

    scanf("%d", &t);

    while(t-- > 0) {
        scanf("%d", &data);
        root = insert(root, data);
    }
  
	preOrder(root);
    return 0;
}
```

Write a C program to search a node in a binary tree.



For example:

Input	Result
7
26 76 45 33 23 31 14
45
45 Element is found
```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};

struct node* insert( struct node* root, int data ) {
		
	if(root == NULL) {
	
        struct node* node = (struct node*)malloc(sizeof(struct node));

        node->data = data;

        node->left = NULL;
        node->right = NULL;
        return node;
	  
	} else {
      
		struct node* cur;
		
		if(data <= root->data) {
            cur = insert(root->left, data);
            root->left = cur;
		} else {
            cur = insert(root->right, data);
            root->right = cur;
		}
	
		return root;
	}
}

/* you only have to complete the function given below.  
node is defined as  

struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};

*/
void display(struct node *root) {
     if (root == NULL)  
        return;  
    display(root->left);
    printf("%d ", root->data);
    display(root->right); 
}
struct node* search(struct node *root, int value) {
    if(!(root)) {
    return NULL;
    }
    if(value==root->data) {
    printf("%d Element is found",value);
   
    } else if(value<root->data) {
    search(root->left,value);
    } else if(value>root->data){
    search(root->right,value);
    }
     return root;
}
int main() 
{
    struct node* root = NULL;
    //struct node* y;
    
    int t,x;
    int data,choice=2;

    scanf("%d", &t);

    while(t-- > 0) 
    {
        scanf("%d", &data);
        root = insert(root, data);
    }
//    printf("\n Enter choice:1-display 2-delete\n");
    scanf("%d",&x);
    switch(choice)
    {
    case 1:
	display(root);
	break;
	case 2:
	search(root,x);
	break;
    }
    return 0;
}
```

Write a C program to delete a binary tree in C
```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};

struct node* insert( struct node* root, int data ) {
		
	if(root == NULL) {
	
        struct node* node = (struct node*)malloc(sizeof(struct node));

        node->data = data;

        node->left = NULL;
        node->right = NULL;
        return node;
	  
	} else {
      
		struct node* cur;
		
		if(data <= root->data) {
            cur = insert(root->left, data);
            root->left = cur;
		} else {
            cur = insert(root->right, data);
            root->right = cur;
		}
	
		return root;
	}
}

/* you only have to complete the function given below.  
node is defined as  

struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};

*/
void display(struct node *root) {
     if (root == NULL)  
        return;  
    display(root->left);
    printf("%d ", root->data);
    display(root->right); 
}
void delete_tree(struct node *root) {
if (root) {
delete_tree(root->left);
delete_tree(root->right);
free(root);
}

}


int main() {
  
    struct node* root = NULL;
    
    int t;
    int data,choice=2;

    scanf("%d", &t);

    while(t-- > 0) {
        scanf("%d", &data);
        root = insert(root, data);
    }
    //printf("\n Enter choice:1-display 2-delete\n");
    switch(choice)
    {
    case 1:
	display(root);
	break;
	case 2:
	delete_tree(root);
	printf("Deleted successfully");
	break;
	default:
	printf("Enetr a valid choice\n");
	break;
    }
    return 0;
}
```

Complete the  function in your editor below, which has  parameter: a pointer to the root of a binary tree. It must print the values in the tree's inorder traversal as a single line of space-separated values.

Input Format

Our hidden tester code passes the root node of a binary tree to your $inOrder* function.

Constraints

       

Output Format

Print the tree's inorder traversal as a single line of space-separated values.

Sample Input

1 2 5 3 6 4
Sample Output

1 2 3 4 5 6 

For example:

Input	Result
6
1 2 5 3 6 4
1 2 3 4 5 6 

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};

struct node* insert( struct node* root, int data ) {
		
	if(root == NULL) {
	
        struct node* node = (struct node*)malloc(sizeof(struct node));

        node->data = data;

        node->left = NULL;
        node->right = NULL;
        return node;
	  
	} else {
      
		struct node* cur;
		
		if(data <= root->data) {
            cur = insert(root->left, data);
            root->left = cur;
		} else {
            cur = insert(root->right, data);
            root->right = cur;
		}
	
		return root;
	}
}

/* you only have to complete the function given below.  
node is defined as  

struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};

*/
void inOrder( struct node *root) {
if(root==NULL)
return;
inOrder(root->left);
printf("%d ",root->data);
inOrder(root->right);
}


int main() {
  
    struct node* root = NULL;
    
    int t;
    int data;

    scanf("%d", &t);

    while(t-- > 0) {
        scanf("%d", &data);
        root = insert(root, data);
    }
  
	inOrder(root);
    return 0;
}
```

### Day 2
You are given a pointer to the root of a binary search tree and values to be inserted into the tree. Insert the values into their appropriate position in the binary search tree and return the root of the updated binary tree. You just have to complete the function.

Input Format

You are given a function,

Node * insert (Node * root ,int data) {


}


Constraints

No. of nodes in the tree

500

Output Format

Returns the values of BST in pre-order traversal after insertion.

Sample Input:

       4

       / \

      2   7

     / \

    1   3


For example:

Input	Result
6
4 2 3 1 7 6
4 2 1 3 7 6

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
 
struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};
 
void preOrder( struct node *root) {
  
    if( root == NULL ) 
      return;
    printf("%d ",root->data);
    preOrder(root->left);
    preOrder(root->right);
  
}
 
/* you only have to complete the function given below.  
node is defined as  
 
struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};
 
*/
void search(struct node*);
struct node *temp;
struct node* insert( struct node* root, int data ) 
{
   temp = (struct node *)malloc(1*sizeof(struct node));
   temp->data = data;
   temp->left = temp->right = NULL; 
   if (root == NULL)
       root = temp;
   else
    search(root);
return root;
}
void search(struct node *t)
{
   if ((temp->data > t->data) && (t->right != NULL))      /* value more than root node value insert at right */
       search(t->right);
   else if ((temp->data > t->data) && (t->right == NULL))
       t->right = temp;
   else if ((temp->data < t->data) && (t->left != NULL))    /* value less than root node value insert at left */
       search(t->left);
   else if ((temp->data < t->data) && (t->left == NULL))
       t->left = temp;  
    
}
 
 
int main() {
  
    struct node* root = NULL;
    
    int t;
    int data;
 
    scanf("%d", &t);
 
    while(t-- > 0) {
        scanf("%d", &data);
        root = insert(root, data);
    }
  
    preOrder(root);
    return 0;
}
```

Write a C program to perform pre-order,in-order and post-order traversal in the binary search tree.


For example:

Input	Result
4
18 67 23 45
18 67 23 45
18 23 45 67
45 23 67 18

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
 
struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};
 
void preOrder( struct node *root) {
  
    if( root == NULL ) 
      return;
    printf("%d ",root->data);
    preOrder(root->left);
    preOrder(root->right);
  
}
 void inOrder( struct node *root) {
  
    if( root == NULL ) 
      return;
    
    inOrder(root->left);
    printf("%d ",root->data);
    inOrder(root->right);
  
}
void postOrder( struct node *root) {
  
    if( root == NULL ) 
      return;
    
    postOrder(root->left);
    postOrder(root->right);
    printf("%d ",root->data);
  
}
 
/* you only have to complete the function given below.  
node is defined as  
 
struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};
 
*/
void search(struct node*);
struct node *temp;
struct node* insert( struct node* root, int data ) 
{
   temp = (struct node *)malloc(1*sizeof(struct node));
   temp->data = data;
   temp->left = temp->right = NULL; 
   if (root == NULL)
       root = temp;
   else
    search(root);
return root;
}
void search(struct node *t)
{
   if ((temp->data > t->data) && (t->right != NULL))      /* value more than root node value insert at right */
       search(t->right);
   else if ((temp->data > t->data) && (t->right == NULL))
       t->right = temp;
   else if ((temp->data < t->data) && (t->left != NULL))    /* value less than root node value insert at left */
       search(t->left);
   else if ((temp->data < t->data) && (t->left == NULL))
       t->left = temp;  
    
}
 
 
int main() {
  
    struct node* root = NULL;
    
    int t;
    int data;
 
    scanf("%d", &t);
 
    while(t-- > 0) {
        scanf("%d", &data);
        root = insert(root, data);
    }
  
    preOrder(root);
    printf("\n");
    inOrder(root);
     printf("\n");
    postOrder(root);
     printf("\n");
    return 0;
}
```

Write a C program to delete an element in a binary search tree.




For example:

Input	Result
5
1 4 6 3 2
2
1 -> 3 -> 4 -> 6 -> 

```c
#include<stdio.h>
#include<stdlib.h>
struct btnode
{
   int value;
   struct btnode *l;
   struct btnode *r;
}*root = NULL, *temp = NULL, *t2, *t1;
 
void delete1();
struct btnode *insert(struct btnode *root,int data);
void delete(struct btnode *root);
void inorder(struct btnode *t);
void create();
struct btnode *search(struct btnode *t);

void search1(struct btnode *t,int data);
int smallest(struct btnode *t);
int largest(struct btnode *t);


int flag = 1;
 
int main()
{
   int n,data;
   struct btnode *root = NULL;
   scanf("%d",&n);
   for(int i=0;i<n;i++)
   {
       scanf("%d",&data);
       root = insert(root, data);
   }

           delete(root);
           inorder(root);
           return 0;
}
 /* To insert a node in the tree */
struct btnode *insert(struct btnode* root,int data)
{
   temp = (struct btnode *)malloc(1*sizeof(struct btnode));
   temp->value = data;
   temp->l = temp->r = NULL;
   if (root == NULL)
       root = temp;
   else   
       root=search(root);   
    return root;
}
/* Function to search the appropriate position to insert the new node */
struct btnode *search(struct btnode *t)
{
   if ((temp->value > t->value) && (t->r != NULL))      /* value more than root node value insert at right */
       search(t->r);
   else if ((temp->value > t->value) && (t->r == NULL))
       t->r = temp;
   else if ((temp->value < t->value) && (t->l != NULL))    /* value less than root node value insert at left */
       search(t->l);
   else if ((temp->value < t->value) && (t->l == NULL))
       t->l = temp;
    return t;
}
 
/* recursive function to perform inorder traversal of tree */
void inorder(struct btnode *t)
{
   if (t)
  {
    inorder(t->l);
    printf("%d -> ", t->value);
    inorder(t->r);
}
}
 
/* To check for the deleted node */
void delete(struct btnode *root)
{
   int data;
   /*if (root == NULL)
   {
       printf("No elements in a tree to delete");
       return;
   }*/
   //printf("Enter the data to be deleted : ");
   scanf("%d",&data);
   t1 = root;
   t2 = root;
   search1(root,data);
}
 

 
/* Search for the appropriate position to insert the new node */
void search1(struct btnode *t, int data)
{
   if ((data>t->value))
   {
       t1 = t;
       search1(t->r,data);
   }
   else if ((data < t->value))
   {
       t1 = t;
       search1(t->l,data);
   }
   else if ((data==t->value))
   {
       delete1(t);
   }
}
int smallest(struct btnode *t)
{
   t2 = t;
   if (t->l != NULL)
   {
       t2 = t;
       return(smallest(t->l));
   }
   else   
       return (t->value);
}
 
/* To find the largest element in the left sub tree */
int largest(struct btnode *t)
{
   if (t->r != NULL)
   {
       t2 = t;
       return(largest(t->r));
   }
   else   
       return(t->value);
}
void delete1(struct btnode *t)
{
   int k;
   /* To delete leaf node */
   if ((t->l == NULL) && (t->r == NULL))
   {
       if (t1->l == t)
       {
           t1->l = NULL;
       }
       else
       {
           t1->r = NULL;
       }
       t = NULL;
       free(t);
       return;
   }
   /* To delete node having one left hand child */
   else if ((t->r == NULL))
   {
       if (t1 == t)
       {
           root = t->l;
           t1 = root;
       }
       else if (t1->l == t)
       {
           t1->l = t->l;
 
       }
       else
       {
           t1->r = t->l;
       }
       t = NULL;
       free(t);
       return;
   }
 
   /* To delete node having right hand child */
   else if (t->l == NULL)
   {
       if (t1 == t)
       {
           root = t->r;
           t1 = root;
       }
       else if (t1->r == t)
           t1->r = t->r;
       else
           t1->l = t->r;
       //t == NULL;
       free(t);
       return;
   }
 
   /* To delete node having two child */
   else if ((t->l != NULL) && (t->r != NULL)) 
   {
       t2 = root;
       if (t->r != NULL)
       {
           k = smallest(t->r);
           flag = 1;
       }
       else
       {
           k =largest(t->l);
           flag = 2;
       }
       search1(root, k);
       t->value = k;
   }
 
}
```

### Day 3
Write a C program to construct an Expression Tree for the given Postfix Expression.Display the output in the format of In-order,Pre-order and Post-order traversal.


For example:

Input	Result
445+*9/
4*4+5/9
/*4+459
445+*9/

```c
#include <stdio.h>
#include<stdlib.h>
struct n {
   char d;
   struct n *l;
   struct n *r;
};
char pf[50];
int top = -1;
struct n *a[50];
int r(char inputch) {
   if (inputch == '+' || inputch == '-' || inputch == '*' || inputch== '/')
      return (-1);
   else if (inputch >= 'A' || inputch <= 'Z')
      return (1);
   else if (inputch >= 'a' || inputch <= 'z')
      return (1);
   else
      return (-100);
}
void push(struct n *tree) {
   top++;
   a[top] = tree;
}
struct n *pop() {
   top--;
   return (a[top + 1]);
}
void construct_expression_tree(char *suffix) {
   char s;
   struct n *newl, *p1, *p2;
   int flag;
   s = suffix[0];
   for (int i = 1; s != 0; i++) {
      flag = r(s);
      if (flag == 1) {
         newl=(struct n *)malloc(1*sizeof(struct n));

         newl->d = s;
         newl->l = NULL;
         newl->r = NULL;
         push(newl);
      } else {
         p1 = pop();
         p2 = pop();
         newl=(struct n *)malloc(1*sizeof(struct n));
         newl->d = s;
         newl->l = p2;
         newl->r = p1;
         push(newl);
      }
      s = suffix[i];
   }
}
void preOrder(struct n *tree) {
   if (tree != NULL) {
      printf("%c",tree->d);
      preOrder(tree->l);
      preOrder(tree->r);
   }
}
void inOrder(struct n *tree) {
   if (tree != NULL) {
      inOrder(tree->l);
      printf("%c",tree->d);
      inOrder(tree->r);
   }
}
void postOrder(struct n *tree) {
   if (tree != NULL) {
      postOrder(tree->l);
      postOrder(tree->r);
      printf("%c",tree->d);
   }
}
int main() {
 
   scanf("%s",pf);
   construct_expression_tree(pf);
  // printf("\nIn-Order Traversal : ");
   inOrder(a[0]);
   printf("\n");
   //printf("\nPre-Order Traversal : ");
   preOrder(a[0]);
   printf("\n");
   //printf("\nPost-Order Traversal : ");
   postOrder(a[0]);
   printf("\n");
   return 0;
}
```

Write a C program to implement Expression Tree algorithm(Convert the given post fix expression into infix expression)

For example:

Input	Result
365+-9/
3-6+5/9

```c
#include <stdio.h>
#include<stdlib.h>

struct n//node declaration 
{  char d;
   struct n *l;
   struct n *r;
};
char pf[50];
int top = -1;
struct n *a[50];
int r(char inputch)//check the symbol whether it is an operator or an operand. 
{
   if (inputch == '+' || inputch == '-' || inputch == '*' || inputch == '/')
      return (-1);
   else if (inputch >= 'A' || inputch <= 'Z')
      return (1);
   else if (inputch >= 'a' || inputch <= 'z')
      return (1);
   else
      return (-100);
}
void push(struct n *tree)//push elements in stack 
{
   top++;
   a[top] = tree;
}
struct n *pop() {
   top--;
   return (a[top + 1]);
}
void construct_expression_tree(char *suffix) {
   char s;
   struct n *newl, *p1, *p2;
   int flag;
   s = suffix[0];
   for (int i = 1; s!= 0; i++) {
      flag = r(s);
      if (flag == 1) {
         newl=(struct n *)malloc(1*sizeof(struct n));
         newl->d = s;
         newl->l = NULL;
         newl->r = NULL;
         push(newl);
      } else {
         p1 = pop();
         p2 = pop();
         newl=(struct n *)malloc(1*sizeof(struct n));
         newl->d = s;
         newl->l = p2;
         newl->r = p1;
         push(newl);
      }
      s = suffix[i];
   }
}

void inOrder(struct n *tree)//perform inorder traversal 
{
   if(tree != NULL) {
      inOrder(tree->l);
      printf("%c",tree->d);
      inOrder(tree->r);
   }
}

int main() {
   
   scanf("%s",pf);
   construct_expression_tree(pf);
   inOrder(a[0]);
   return 0;
}
```

### Day 4

Write a C program to delete an element in a Heap Tree.

For example:

Input	Result
5
1 6 3 5 2
6
After deleting an element: 5 2 3 1 

```c
#include <stdio.h>
int size = 0;
void swap(int *a, int *b)
{
  int temp = *b;
  *b = *a;
  *a = temp;
}
void heapify(int array[], int size, int i)
{
  if (size == 1)
  {
    printf("Single element in the heap");
  }
  else
  {
    int largest = i;
    int l = 2 * i + 1;
    int r = 2 * i + 2;
    if (l < size && array[l] > array[largest])
      largest = l;
    if (r < size && array[r] > array[largest])
      largest = r;
    if (largest != i)
    {
      swap(&array[i], &array[largest]);
      heapify(array, size, largest);
    }
  }
}
void insert(int array[], int newNum)
{
  if (size == 0)
  {
    array[0] = newNum;
    size += 1;
  }
  else
  {
    array[size] = newNum;
    size += 1;
    for (int i = size / 2 - 1; i >= 0; i--)
    {
      heapify(array, size, i);
    }
  }
}
void deleteRoot(int array[], int num)
{
  int i;
  for (i = 0; i < size; i++)
  {
    if (num == array[i])
      break;
  }

  swap(&array[i], &array[size - 1]);
  size -= 1;
  for (int i = size / 2 - 1; i >= 0; i--)
  {
    heapify(array, size, i);
  }
}
void printArray(int array[], int size)
{
  for (int i = 0; i < size; ++i)
    printf("%d ", array[i]);
  printf("\n");
}
int main()
{
  int array[10],n,data,x;
  scanf("%d",&n);
  for(int i=0;i<n;i++)
  {
      scanf("%d",&data);
      insert(array, data);
  }

  //printf("Max-Heap array: ");
  //printArray(array, size);
  scanf("%d",&x);

  deleteRoot(array, x);

  printf("After deleting an element: ");

  printArray(array, size);
}
```
Write a C program to insert the elements in a Max Heap Tree.

For example:

Input	Result
5
1 6 3 7 2
Max-Heap array: 7 6 3 1 2

```c
#include <stdio.h>
int size = 0;
void swap(int *a, int *b)
{
  int temp = *b;
  *b = *a;
  *a = temp;
}
void heapify(int array[], int size, int i)
{
  if (size == 1)
  {
    printf("Single element in the heap");
  }
  else
  {
    int largest = i;
    int l = 2 * i + 1;
    int r = 2 * i + 2;
    if (l < size && array[l] > array[largest])
      largest = l;
    if (r < size && array[r] > array[largest])
      largest = r;
    if (largest != i)
    {
      swap(&array[i], &array[largest]);
      heapify(array, size, largest);
    }
  }
}
void insert(int array[], int newNum)
{
  if (size == 0)
  {
    array[0] = newNum;
    size += 1;
  }
  else
  {
    array[size] = newNum;
    size += 1;
    for (int i = size / 2 - 1; i >= 0; i--)
    {
      heapify(array, size, i);
    }
  }
}

void printArray(int array[], int size)
{
  for (int i = 0; i < size; ++i)
    printf("%d ", array[i]);
  printf("\n");
}
int main()
{
  int array[10],n,data;
  scanf("%d",&n);
  for(int i=0;i<n;i++)
  {
      scanf("%d",&data);
      insert(array, data);
  }

  printf("Max-Heap array: ");
  printArray(array, size);

 
}
```

## Module 16
### Day 1

Write a C program to perform LL Rotation for an AVL Tree.

For example:

Input	Result
5
5 8 3 2 9
5(Bf=0)3(Bf=1)2(Bf=0)8(Bf=-1)9(Bf=0)

```c
#include<stdio.h>
#include<stdlib.h>
 
typedef struct node
{
int data;
struct node *left,*right;
int ht;
}node;
node *insert(node *,int);
//node *Delete(node *,int);
void preorder(node *);
//void inorder(node *);
int height( node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);
 
int main()
{
node *root=NULL;
int x,n,i;
scanf("%d",&n);
//printf("\nEnter tree data:");
root=NULL;
for(i=0;i<n;i++)
{
scanf("%d",&x);
root=insert(root,x);
}
//printf("\nPreorder sequence:\n");
preorder(root);
return 0;
}
 
node * insert(node *T,int x)
{
if(T==NULL)
{
T=(node*)malloc(sizeof(node));
T->data=x;
T->left=NULL;
T->right=NULL;
}
else
if(x > T->data) // insert in right subtree
{
T->right=insert(T->right,x);
if(BF(T)==-2)
{
if(x>T->right->data)
T=RR(T);
else
T=RL(T);
}}
else
if(x<T->data)
{
T->left=insert(T->left,x);
if(BF(T)==2)
{
if(x < T->left->data)
T=LL(T);
else
T=LR(T);
}}
T->ht=height(T);
return(T);
}
 
int height(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
if(lh>rh)
return(lh);
return(rh);
}
 
node * rotateright(node *x)
{
node *y;
y=x->left;
x->left=y->right;
y->right=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * rotateleft(node *x)
{
node *y;
y=x->right;
x->right=y->left;
y->left=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * RR(node *T)
{
T=rotateleft(T);
return(T);
}
 
node * LL(node *T)
{
T=rotateright(T);
return(T);
}
 
node * LR(node *T)
{
T->left=rotateleft(T->left);
T=rotateright(T);
return(T);
}
 
node * RL(node *T)
{
T->right=rotateright(T->right);
T=rotateleft(T);
return(T);
}
 
int BF(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
 
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
 
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
 
return(lh-rh);
}
 
void preorder(node *T)
{
if(T!=NULL)
{
printf("%d(Bf=%d)",T->data,BF(T));
preorder(T->left);
preorder(T->right);
}
}
```

Create a C program to delete an element from an AVL Tree.

For example:

Input	Result
5
6 2 8 3 4
3
6(Bf=1)4(Bf=1)2(Bf=0)8(Bf=0)

```c
#include<stdio.h>
#include<stdlib.h>
 
typedef struct node
{
int data;
struct node *left,*right;
int ht;
}node;
 
node *insert(node *,int);
node *Delete(node *,int);
void preorder(node *);
void inorder(node *);
int height( node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);
 
int main()
{
node *root=NULL;
int x,n,i;
scanf("%d",&n);
//printf("\nEnter tree data:");
root=NULL;
for(i=0;i<n;i++)
{
scanf("%d",&x);
root=insert(root,x);
}
//printf("\nEnter a data:");
scanf("%d",&x);
root=Delete(root,x);
//printf("\nPreorder sequence:\n");
preorder(root);
return 0;
}
 
node * insert(node *T,int x)
{
if(T==NULL)
{
T=(node*)malloc(sizeof(node));
T->data=x;
T->left=NULL;
T->right=NULL;
}
else
if(x > T->data) // insert in right subtree
{
T->right=insert(T->right,x);
if(BF(T)==-2)
{
if(x>T->right->data)
T=RR(T);
else
T=RL(T);
}}
else
if(x<T->data)
{
T->left=insert(T->left,x);
if(BF(T)==2)
{
if(x < T->left->data)
T=LL(T);
else
T=LR(T);
}}
T->ht=height(T);
return(T);
}
 
node * Delete(node *T,int x)
{
node *p;
if(T==NULL)
{
return NULL;
}
else
if(x > T->data) // insert in right subtree
{
T->right=Delete(T->right,x);
if(BF(T)==2)
{
if(BF(T->left)>=0)
T=LL(T);
else
T=LR(T);
}}
else
if(x<T->data)
{
T->left=Delete(T->left,x);
if(BF(T)==-2) //Rebalance during windup
{
if(BF(T->right)<=0)
T=RR(T);
else
T=RL(T);
}}
else
{
//data to be deleted is found
if(T->right!=NULL)
{ //delete its inorder succesor
p=T->right;
while(p->left!= NULL)
p=p->left;
T->data=p->data;
T->right=Delete(T->right,p->data);
if(BF(T)==2)//Rebalance during windup
{
if(BF(T->left)>=0)
T=LL(T);
else
T=LR(T);}}
else
return(T->left);
}
T->ht=height(T);
return(T);
}
 
int height(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
if(lh>rh)
return(lh);
return(rh);
}
 
node * rotateright(node *x)
{
node *y;
y=x->left;
x->left=y->right;
y->right=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * rotateleft(node *x)
{
node *y;
y=x->right;
x->right=y->left;
y->left=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * RR(node *T)
{
T=rotateleft(T);
return(T);
}
 
node * LL(node *T)
{
T=rotateright(T);
return(T);
}
 
node * LR(node *T)
{
T->left=rotateleft(T->left);
T=rotateright(T);
return(T);
}
 
node * RL(node *T)
{
T->right=rotateright(T->right);
T=rotateleft(T);
return(T);
}
 
int BF(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
 
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
 
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
 
return(lh-rh);
}
 
void preorder(node *T)
{
if(T!=NULL)
{
printf("%d(Bf=%d)",T->data,BF(T));
preorder(T->left);
preorder(T->right);
}
}
 
void inorder(node *T)
{
if(T!=NULL)
{
inorder(T->left);
printf("%d(Bf=%d)",T->data,BF(T));
inorder(T->right);
}
}
```
Write a C program to create an AVL Tree with the input elements.

For example:

Input	Result
5
23 67 87 45 34


67(Bf=1)34(Bf=0)23(Bf=0)45(Bf=0)87(Bf=0)
```c
#include<stdio.h>
#include<stdlib.h>

typedef struct node
{
int data;
struct node *left,*right;
int ht;
}node;
node *insert(node *,int);
void preorder(node *);
//void inorder(node *);
int height(node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);
 
int main()
{
node *root=NULL;
int x,n,i;
scanf("%d",&n);
root=NULL;
for(i=0;i<n;i++)
{
scanf("%d",&x);
root=insert(root,x);
}
//printf("\nPreorder sequence:\n");
preorder(root);
//printf("\n\nInorder sequence:\n");
//inorder(root);
//printf("\n");
return 0;
}
 
node * insert(node *T,int x)
{
if(T==NULL)
{
T=(node*)malloc(sizeof(node));
T->data=x;
T->left=NULL;
T->right=NULL;
}
else
if(x > T->data) // insert in right subtree
{
T->right=insert(T->right,x);
if(BF(T)==-2)
{
if(x>T->right->data)
T=RR(T);
else
T=RL(T);
}
}
else
if(x<T->data)
{
T->left=insert(T->left,x);
if(BF(T)==2)
{
    if(x < T->left->data)
T=LL(T);
else
T=LR(T);
}
}
T->ht=height(T);
return(T);
}
 
int height(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
if(lh>rh)
return(lh);
return(rh);
}

 
node * rotateright(node *x)
{
node *y;
y=x->left;
x->left=y->right;
y->right=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * rotateleft(node *x)
{
node *y;
y=x->right;
x->right=y->left;
y->left=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * RR(node *T)
{
T=rotateleft(T);
return(T);
}
 
node * LL(node *T)
{
T=rotateright(T);
return(T);
}
 
node * LR(node *T)
{
T->left=rotateleft(T->left);
T=rotateright(T);
return(T);
}
 
node * RL(node *T)
{
T->right=rotateright(T->right);
T=rotateleft(T);
return(T);
}
 
int BF(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
 
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
 
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
 
return(lh-rh);
}
 
void preorder(node *T)
{
if(T!=NULL)
{
printf("%d(Bf=%d)",T->data,BF(T));
preorder(T->left);
preorder(T->right);
}
}
```
Write a C program to perform Pre-order and In-order traversal for an AVL Tree.

For example:

Input	Result
6
10 23 45 32 22 33
23(Bf=0)10(Bf=-1)22(Bf=0)33(Bf=0)32(Bf=0)45(Bf=0)
10(Bf=-1)22(Bf=0)23(Bf=0)32(Bf=0)33(Bf=0)45(Bf=0)

```c
#include<stdio.h>
#include<stdlib.h>
 
typedef struct node
{
int data;
struct node *left,*right;
int ht;
}node;
node *insert(node *,int);
void preorder(node *);
void inorder(node *);
int height( node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);
 
int main()
{
node *root=NULL;
int x,n,i;
scanf("%d",&n);
//printf("\nEnter tree data:");
root=NULL;
for(i=0;i<n;i++)
{
scanf("%d",&x);
root=insert(root,x);
}
//printf("\nPreorder sequence:\n");
preorder(root);
printf("\n");
inorder(root);
return 0;
}
 
node * insert(node *T,int x)
{
if(T==NULL)
{
T=(node*)malloc(sizeof(node));
T->data=x;
T->left=NULL;
T->right=NULL;
}
else
if(x > T->data) // insert in right subtree
{
T->right=insert(T->right,x);
if(BF(T)==-2)
{
if(x>T->right->data)
T=RR(T);
else
T=RL(T);
}}
else
if(x<T->data)
{
T->left=insert(T->left,x);
if(BF(T)==2)
{
if(x < T->left->data)
T=LL(T);
else
T=LR(T);
}}
T->ht=height(T);
return(T);
}
 
int height(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
if(lh>rh)
return(lh);
return(rh);
}
 
node * rotateright(node *x)
{
node *y;
y=x->left;
x->left=y->right;
y->right=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * rotateleft(node *x)
{
node *y;
y=x->right;
x->right=y->left;
y->left=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * RR(node *T)
{
T=rotateleft(T);
return(T);
}
 
node * LL(node *T)
{
T=rotateright(T);
return(T);
}
 
node * LR(node *T)
{
T->left=rotateleft(T->left);
T=rotateright(T);
return(T);
}
 
node * RL(node *T)
{
T->right=rotateright(T->right);
T=rotateleft(T);
return(T);

}
 
int BF(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
 
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
 
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
 
return(lh-rh);
}
 
void preorder(node *T)
{
if(T!=NULL)
{
printf("%d(Bf=%d)",T->data,BF(T));
preorder(T->left);
preorder(T->right);
}
}
void inorder(node *T)
{
if(T!=NULL)
{
inorder(T->left);
printf("%d(Bf=%d)",T->data,BF(T));
inorder(T->right);
}
}
```
Write a C program to perform RL rotation in an AVL Tree.
For example:

Input	Result
11
2 6 7 12 15 65 32 37 25 10 16
12(Bf=0)6(Bf=-1)2(Bf=0)7(Bf=-1)10(Bf=0)32(Bf=0)16(Bf=0)15(Bf=0)25(Bf=0)65(Bf=1)37(Bf=0)

```c
#include<stdio.h>
#include<stdlib.h>
 
typedef struct node
{
int data;
struct node *left,*right;
int ht;
}node;
node *insert(node *,int);
//node *Delete(node *,int);
void preorder(node *);
//void inorder(node *);
int height( node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);
 
int main()
{
node *root=NULL;
int x,n,i;
scanf("%d",&n);
//printf("\nEnter tree data:");
root=NULL;
for(i=0;i<n;i++)
{
scanf("%d",&x);
root=insert(root,x);
}
//printf("\nPreorder sequence:\n");
preorder(root);
return 0;
}
 
node * insert(node *T,int x)
{
if(T==NULL)
{
T=(node*)malloc(sizeof(node));
T->data=x;
T->left=NULL;
T->right=NULL;
}
else
if(x > T->data) // insert in right subtree
{
T->right=insert(T->right,x);
if(BF(T)==-2)
{
if(x>T->right->data)
T=RR(T);
else
T=RL(T);
}}
else
if(x<T->data)
{
T->left=insert(T->left,x);
if(BF(T)==2)
{
if(x < T->left->data)
T=LL(T);
else
T=LR(T);
}}
T->ht=height(T);
return(T);
}
 
int height(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
if(lh>rh)
return(lh);
return(rh);
}
 
node * rotateright(node *x)
{
node *y;
y=x->left;
x->left=y->right;
y->right=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * rotateleft(node *x)
{
node *y;
y=x->right;
x->right=y->left;
y->left=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * RR(node *T)
{
T=rotateleft(T);
return(T);
}
 
node * LL(node *T)
{
T=rotateright(T);
return(T);
}
 
node * LR(node *T)
{
T->left=rotateleft(T->left);
T=rotateright(T);
return(T);
}
 
node * RL(node *T)
{
T->right=rotateright(T->right);
T=rotateleft(T);
return(T);
}
 
int BF(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
 
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
 
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
 
return(lh-rh);
}
 
void preorder(node *T)
{
if(T!=NULL)
{
printf("%d(Bf=%d)",T->data,BF(T));
preorder(T->left);
preorder(T->right);
}
}
```

### Day 2
Write a C program to perform post-order traversal in an AVL Tree.

For example:

Input	Result
5
12 13 4 23 67
4(Bf=0)13(Bf=0)67(Bf=0)23(Bf=0)12(Bf=-1)

```c
#include<stdio.h>
#include<stdlib.h>
 
typedef struct node
{
int data;
struct node *left,*right;
int ht;
}node;
node *insert(node *,int);
//node *Delete(node *,int);
void postorder(node *);
//void inorder(node *);
int height( node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);
 
int main()
{
node *root=NULL;
int x,n,i;
scanf("%d",&n);
//printf("\nEnter tree data:");
root=NULL;
for(i=0;i<n;i++)
{
scanf("%d",&x);
root=insert(root,x);
}
//printf("\nPreorder sequence:\n");
postorder(root);
return 0;
}
 
node * insert(node *T,int x)
{
if(T==NULL)
{
T=(node*)malloc(sizeof(node));
T->data=x;
T->left=NULL;
T->right=NULL;
}
else
if(x > T->data) // insert in right subtree
{
T->right=insert(T->right,x);
if(BF(T)==-2)
{
if(x>T->right->data)
T=RR(T);
else
T=RL(T);
}}
else
if(x<T->data)
{
T->left=insert(T->left,x);
if(BF(T)==2)
{
if(x < T->left->data)
T=LL(T);
else
T=LR(T);
}}
T->ht=height(T);
return(T);
}
 
int height(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
if(lh>rh)
return(lh);
return(rh);
}
 
node * rotateright(node *x)
{
node *y;
y=x->left;
x->left=y->right;
y->right=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * rotateleft(node *x)
{
node *y;
y=x->right;
x->right=y->left;
y->left=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * RR(node *T)
{
T=rotateleft(T);
return(T);
}
 
node * LL(node *T)
{
T=rotateright(T);
return(T);
}
 
node * LR(node *T)
{
T->left=rotateleft(T->left);
T=rotateright(T);
return(T);
}
 
node * RL(node *T)
{
T->right=rotateright(T->right);
T=rotateleft(T);
return(T);
}
 
int BF(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
 
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
 
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
 
return(lh-rh);
}
 
void postorder(node *T)
{
if(T!=NULL)
{

postorder(T->left);
postorder(T->right);
printf("%d(Bf=%d)",T->data,BF(T));
}
}
```

Write a C program to perform LR rotation in an AVL Tree.
For example:

Input	Result
4
20 60 40 55
40(Bf=-1)20(Bf=0)60(Bf=1)55(Bf=0)

```c
#include<stdio.h>
#include<stdlib.h>
 
typedef struct node
{
int data;
struct node *left,*right;
int ht;
}node;
node *insert(node *,int);
//node *Delete(node *,int);
void preorder(node *);
//void inorder(node *);
int height( node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);
 
int main()
{
node *root=NULL;
int x,n,i;
scanf("%d",&n);
//printf("\nEnter tree data:");
root=NULL;
for(i=0;i<n;i++)
{
scanf("%d",&x);
root=insert(root,x);
}
//printf("\nPreorder sequence:\n");
preorder(root);
return 0;
}
 
node * insert(node *T,int x)
{
if(T==NULL)
{
T=(node*)malloc(sizeof(node));
T->data=x;
T->left=NULL;
T->right=NULL;
}
else
if(x > T->data) // insert in right subtree
{
T->right=insert(T->right,x);
if(BF(T)==-2)
{
if(x>T->right->data)
T=RR(T);
else
T=RL(T);
}}
else
if(x<T->data)
{
T->left=insert(T->left,x);
if(BF(T)==2)
{
if(x < T->left->data)
T=LL(T);
else
T=LR(T);
}}
T->ht=height(T);
return(T);
}
 
int height(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
if(lh>rh)
return(lh);
return(rh);
}
 
node * rotateright(node *x)
{
node *y;
y=x->left;
x->left=y->right;
y->right=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * rotateleft(node *x)
{
node *y;
y=x->right;
x->right=y->left;
y->left=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * RR(node *T)
{
T=rotateleft(T);
return(T);
}
 
node * LL(node *T)
{
T=rotateright(T);
return(T);
}
 
node * LR(node *T)
{
T->left=rotateleft(T->left);
T=rotateright(T);
return(T);
}
 
node * RL(node *T)
{
T->right=rotateright(T->right);
T=rotateleft(T);
return(T);
}
 
int BF(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
 
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
 
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
 
return(lh-rh);
}
 
void preorder(node *T)
{
if(T!=NULL)
{
printf("%d(Bf=%d)",T->data,BF(T));
preorder(T->left);
preorder(T->right);
}
}
```
Write a C program to perform RR rotation in AVL Tree.

For example:

Input	Result
11
2 6 7 12 15 65 32 37 25 10 16
12(Bf=0)6(Bf=-1)2(Bf=0)7(Bf=-1)10(Bf=0)32(Bf=0)16(Bf=0)1

```c
#include<stdio.h>
#include<stdlib.h>
 
typedef struct node
{
int data;
struct node *left,*right;
int ht;
}node;
node *insert(node *,int);
//node *Delete(node *,int);
void preorder(node *);
//void inorder(node *);
int height( node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);
 
int main()
{
node *root=NULL;
int x,n,i;
scanf("%d",&n);
//printf("\nEnter tree data:");
root=NULL;
for(i=0;i<n;i++)
{
scanf("%d",&x);
root=insert(root,x);
}
//printf("\nPreorder sequence:\n");
preorder(root);
return 0;
}
 
node * insert(node *T,int x)
{
if(T==NULL)
{
T=(node*)malloc(sizeof(node));
T->data=x;
T->left=NULL;
T->right=NULL;
}
else
if(x > T->data) // insert in right subtree
{
T->right=insert(T->right,x);
if(BF(T)==-2)
{
if(x>T->right->data)
T=RR(T);
else
T=RL(T);
}}
else
if(x<T->data)
{
T->left=insert(T->left,x);
if(BF(T)==2)
{
if(x < T->left->data)
T=LL(T);
else
T=LR(T);
}}
T->ht=height(T);
return(T);
}
 
int height(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
if(lh>rh)
return(lh);
return(rh);
}
 
node * rotateright(node *x)
{
node *y;
y=x->left;
x->left=y->right;
y->right=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * rotateleft(node *x)
{
node *y;
y=x->right;
x->right=y->left;
y->left=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * RR(node *T)
{
T=rotateleft(T);
return(T);
}
 
node * LL(node *T)
{
T=rotateright(T);
return(T);
}
 
node * LR(node *T)
{
T->left=rotateleft(T->left);
T=rotateright(T);
return(T);
}
 
node * RL(node *T)
{
T->right=rotateright(T->right);
T=rotateleft(T);
return(T);
}
 
int BF(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
 
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
 
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
 
return(lh-rh);
}
 
void preorder(node *T)
{
if(T!=NULL)
{
printf("%d(Bf=%d)",T->data,BF(T));
preorder(T->left);
preorder(T->right);
}
}
```

Write a C program to perform left rotation in an AVL Tree.
For example:

Input	Result
11
2 6 7 12 15 65 32 37 25 10 16
12(Bf=0)6(Bf=-1)2(Bf=0)7(Bf=-1)10(Bf=0)32(Bf=0

```c
#include<stdio.h>
#include<stdlib.h>
 
typedef struct node
{
int data;
struct node *left,*right;
int ht;
}node;
node *insert(node *,int);
//node *Delete(node *,int);
void preorder(node *);
//void inorder(node *);
int height( node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);
 
int main()
{
node *root=NULL;
int x,n,i;
scanf("%d",&n);
//printf("\nEnter tree data:");
root=NULL;
for(i=0;i<n;i++)
{
scanf("%d",&x);
root=insert(root,x);
}
//printf("\nPreorder sequence:\n");
preorder(root);
return 0;
}
 
node * insert(node *T,int x)
{
if(T==NULL)
{
T=(node*)malloc(sizeof(node));
T->data=x;
T->left=NULL;
T->right=NULL;
}
else
if(x > T->data) // insert in right subtree
{
T->right=insert(T->right,x);
if(BF(T)==-2)
{
if(x>T->right->data)
T=RR(T);
else
T=RL(T);
}}
else
if(x<T->data)
{
T->left=insert(T->left,x);
if(BF(T)==2)
{
if(x < T->left->data)
T=LL(T);
else
T=LR(T);
}}
T->ht=height(T);
return(T);
}
 
int height(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
if(lh>rh)
return(lh);
return(rh);
}
 
node * rotateright(node *x)
{
node *y;
y=x->left;
x->left=y->right;
y->right=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * rotateleft(node *x)
{
node *y;
y=x->right;
x->right=y->left;
y->left=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * RR(node *T)
{
T=rotateleft(T);
return(T);
}
 
node * LL(node *T)
{
T=rotateright(T);
return(T);
}
 
node * LR(node *T)
{
T->left=rotateleft(T->left);
T=rotateright(T);
return(T);
}
 
node * RL(node *T)
{
T->right=rotateright(T->right);
T=rotateleft(T);
return(T);
}
 
int BF(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
 
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
 
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
 
return(lh-rh);
}
 
void preorder(node *T)
{
if(T!=NULL)
{
printf("%d(Bf=%d)",T->data,BF(T));
preorder(T->left);
preorder(T->right);
}
}
```

Write a C program to perform right rotation in an AVL Tree.
For example:

Input	Result
4
20 60 40 55
40(Bf=-1)20(Bf=0)60(Bf=1)55(Bf=0)

```c
#include<stdio.h>
#include<stdlib.h>
 
typedef struct node
{
int data;
struct node *left,*right;
int ht;
}node;
node *insert(node *,int);
//node *Delete(node *,int);
void preorder(node *);
//void inorder(node *);
int height( node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);
 
int main()
{
node *root=NULL;
int x,n,i;
scanf("%d",&n);
//printf("\nEnter tree data:");
root=NULL;
for(i=0;i<n;i++)
{
scanf("%d",&x);
root=insert(root,x);
}
//printf("\nPreorder sequence:\n");
preorder(root);
return 0;
}
 
node * insert(node *T,int x)
{
if(T==NULL)
{
T=(node*)malloc(sizeof(node));
T->data=x;
T->left=NULL;
T->right=NULL;
}
else
if(x > T->data) // insert in right subtree
{
T->right=insert(T->right,x);
if(BF(T)==-2)
{
if(x>T->right->data)
T=RR(T);
else
T=RL(T);
}}
else
if(x<T->data)
{
T->left=insert(T->left,x);
if(BF(T)==2)
{
if(x < T->left->data)
T=LL(T);
else
T=LR(T);
}}
T->ht=height(T);
return(T);
}
 
int height(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
if(lh>rh)
return(lh);
return(rh);
}
 
node * rotateright(node *x)
{
node *y;
y=x->left;
x->left=y->right;
y->right=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * rotateleft(node *x)
{
node *y;
y=x->right;
x->right=y->left;
y->left=x;
x->ht=height(x);
y->ht=height(y);
return(y);
}
 
node * RR(node *T)
{
T=rotateleft(T);
return(T);
}
 
node * LL(node *T)
{
T=rotateright(T);
return(T);
}
 
node * LR(node *T)
{
T->left=rotateleft(T->left);
T=rotateright(T);
return(T);
}
 
node * RL(node *T)
{
T->right=rotateright(T->right);
T=rotateleft(T);
return(T);
}
 
int BF(node *T)
{
int lh,rh;
if(T==NULL)
return(0);
 
if(T->left==NULL)
lh=0;
else
lh=1+T->left->ht;
 
if(T->right==NULL)
rh=0;
else
rh=1+T->right->ht;
 
return(lh-rh);
}
 
void preorder(node *T)
{
if(T!=NULL)
{
printf("%d(Bf=%d)",T->data,BF(T));
preorder(T->left);
preorder(T->right);
}
}
```

### Day 3

Write a C program to insert the elements in a B Tree.
For example:

Input	Result
6 
12 34 56 33 23 11
11 12 23 33 34 56 

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 3
#define MIN 2

struct BTreeNode {
  int val[MAX + 1], count;
  struct BTreeNode *link[MAX + 1];
};

struct BTreeNode *root;

// Create a node
struct BTreeNode *createNode(int val, struct BTreeNode *child) {
  struct BTreeNode *newNode;
  newNode = (struct BTreeNode *)malloc(sizeof(struct BTreeNode));
  newNode->val[1] = val;
  newNode->count = 1;
  newNode->link[0] = root;
  newNode->link[1] = child;
  return newNode;
}

// Insert node
void insertNode(int val, int pos, struct BTreeNode *node,
        struct BTreeNode *child) {
  int j = node->count;
  while (j > pos) {
    node->val[j + 1] = node->val[j];
    node->link[j + 1] = node->link[j];
    j--;
  }
  node->val[j + 1] = val;
  node->link[j + 1] = child;
  node->count++;
}

// Split node
void splitNode(int val, int *pval, int pos, struct BTreeNode *node,
         struct BTreeNode *child, struct BTreeNode **newNode) {
  int median, j;

  if (pos > MIN)
    median = MIN + 1;
  else
    median = MIN;

  *newNode = (struct BTreeNode *)malloc(sizeof(struct BTreeNode));
  j = median + 1;
  while (j <= MAX) {
    (*newNode)->val[j - median] = node->val[j];
    (*newNode)->link[j - median] = node->link[j];
    j++;
  }
  node->count = median;
  (*newNode)->count = MAX - median;

  if (pos <= MIN) {
    insertNode(val, pos, node, child);
  } else {
    insertNode(val, pos - median, *newNode, child);
  }
  *pval = node->val[node->count];
  (*newNode)->link[0] = node->link[node->count];
  node->count--;
}

// Set the value
int setValue(int val, int *pval,
           struct BTreeNode *node, struct BTreeNode **child) {
  int pos;
  if (!node) {
    *pval = val;
    *child = NULL;
    return 1;
  }

  if (val < node->val[1]) {
    pos = 0;
  } else {
    for (pos = node->count;
       (val < node->val[pos] && pos > 1); pos--)
      ;
    if (val == node->val[pos]) {
      //printf("Duplicates are not permitted\n");
      return 0;
    }
  }
  if (setValue(val, pval, node->link[pos], child)) {
    if (node->count < MAX) {
      insertNode(*pval, pos, node, *child);
    } else {
      splitNode(*pval, pval, pos, node, *child, child);
      return 1;
    }
  }
  return 0;
}

// Insert the value
void insert(int val) {
  int flag, i;
  struct BTreeNode *child;

  flag = setValue(val, &i, root, &child);
  if (flag)
    root = createNode(i, child);
}


// Traverse then nodes
void traversal(struct BTreeNode *myNode) {
  int i;
  if (myNode) {
    for (i = 0; i < myNode->count; i++) {
      traversal(myNode->link[i]);
      printf("%d ", myNode->val[i + 1]);
    }
    traversal(myNode->link[i]);
  }
}

int main() {
   int n,x;
  scanf("%d",&n);
  for(int i=0;i<n;i++)
  {
      scanf("%d",&x);
      insert(x);
  }
 traversal(root);
}
```
Write a C program to delete an element in a B Tree.

For example:

Input	Result
5
1 6 3 5 2
3
1 2 5 6 

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 3
#define MIN 2

struct BTreeNode {
  int item[MAX + 1], count;
  struct BTreeNode *linker[MAX + 1];
};

struct BTreeNode *root;

// Node creation
struct BTreeNode *createNode(int item, struct BTreeNode *child) {
  struct BTreeNode *newNode;
  newNode = (struct BTreeNode *)malloc(sizeof(struct BTreeNode));
  newNode->item[1] = item;
  newNode->count = 1;
  newNode->linker[0] = root;
  newNode->linker[1] = child;
  return newNode;
}

// Add value to the node
void addValToNode(int item, int pos, struct BTreeNode *node,
          struct BTreeNode *child) {
  int j = node->count;
  while (j > pos) {
    node->item[j + 1] = node->item[j];
    node->linker[j + 1] = node->linker[j];
    j--;
  }
  node->item[j + 1] = item;
  node->linker[j + 1] = child;
  node->count++;
}

// Split the node
void splitNode(int item, int *pval, int pos, struct BTreeNode *node,
         struct BTreeNode *child, struct BTreeNode **newNode) {
  int median, j;

  if (pos > MIN)
    median = MIN + 1;
  else
    median = MIN;

  *newNode = (struct BTreeNode *)malloc(sizeof(struct BTreeNode));
  j = median + 1;
  while (j <= MAX) {
    (*newNode)->item[j - median] = node->item[j];
    (*newNode)->linker[j - median] = node->linker[j];
    j++;
  }
  node->count = median;
  (*newNode)->count = MAX - median;

  if (pos <= MIN) {
    addValToNode(item, pos, node, child);
  } else {
    addValToNode(item, pos - median, *newNode, child);
  }
  *pval = node->item[node->count];
  (*newNode)->linker[0] = node->linker[node->count];
  node->count--;
}

// Set the value in the node
int setValueInNode(int item, int *pval,
           struct BTreeNode *node, struct BTreeNode **child) {
  int pos;
  if (!node) {
    *pval = item;
    *child = NULL;
    return 1;
  }

  if (item < node->item[1]) {
    pos = 0;
  } else {
    for (pos = node->count;
       (item < node->item[pos] && pos > 1); pos--)
      ;
    if (item == node->item[pos]) {
      printf("Duplicates not allowed\n");
      return 0;
    }
  }
  if (setValueInNode(item, pval, node->linker[pos], child)) {
    if (node->count < MAX) {
      addValToNode(*pval, pos, node, *child);
    } else {
      splitNode(*pval, pval, pos, node, *child, child);
      return 1;
    }
  }
  return 0;
}

// Insertion operation
void insertion(int item) {
  int flag, i;
  struct BTreeNode *child;

  flag = setValueInNode(item, &i, root, &child);
  if (flag)
    root = createNode(i, child);
}

// Copy the successor
void copySuccessor(struct BTreeNode *myNode, int pos) {
  struct BTreeNode *dummy;
  dummy = myNode->linker[pos];

  for (; dummy->linker[0] != NULL;)
    dummy = dummy->linker[0];
  myNode->item[pos] = dummy->item[1];
}

// Remove the value
void removeVal(struct BTreeNode *myNode, int pos) {
  int i = pos + 1;
  while (i <= myNode->count) {
    myNode->item[i - 1] = myNode->item[i];
    myNode->linker[i - 1] = myNode->linker[i];
    i++;
  }
  myNode->count--;
}

// Do right shift
void rightShift(struct BTreeNode *myNode, int pos) {
  struct BTreeNode *x = myNode->linker[pos];
  int j = x->count;

  while (j > 0) {
    x->item[j + 1] = x->item[j];
    x->linker[j + 1] = x->linker[j];
  }
  x->item[1] = myNode->item[pos];
  x->linker[1] = x->linker[0];
  x->count++;

  x = myNode->linker[pos - 1];
  myNode->item[pos] = x->item[x->count];
  myNode->linker[pos] = x->linker[x->count];
  x->count--;
  return;
}

// Do left shift
void leftShift(struct BTreeNode *myNode, int pos) {
  int j = 1;
  struct BTreeNode *x = myNode->linker[pos - 1];

  x->count++;
  x->item[x->count] = myNode->item[pos];
  x->linker[x->count] = myNode->linker[pos]->linker[0];

  x = myNode->linker[pos];
  myNode->item[pos] = x->item[1];
  x->linker[0] = x->linker[1];
  x->count--;

  while (j <= x->count) {
    x->item[j] = x->item[j + 1];
    x->linker[j] = x->linker[j + 1];
    j++;
  }
  return;
}

// Merge the nodes
void mergeNodes(struct BTreeNode *myNode, int pos) {
  int j = 1;
  struct BTreeNode *x1 = myNode->linker[pos], *x2 = myNode->linker[pos - 1];

  x2->count++;
  x2->item[x2->count] = myNode->item[pos];
  x2->linker[x2->count] = myNode->linker[0];

  while (j <= x1->count) {
    x2->count++;
    x2->item[x2->count] = x1->item[j];
    x2->linker[x2->count] = x1->linker[j];
    j++;
  }

  j = pos;
  while (j < myNode->count) {
    myNode->item[j] = myNode->item[j + 1];
    myNode->linker[j] = myNode->linker[j + 1];
    j++;
  }
  myNode->count--;
  free(x1);
}

// Adjust the node
void adjustNode(struct BTreeNode *myNode, int pos) {
  if (!pos) {
    if (myNode->linker[1]->count > MIN) {
      leftShift(myNode, 1);
    } else {
      mergeNodes(myNode, 1);
    }
  } else {
    if (myNode->count != pos) {
      if (myNode->linker[pos - 1]->count > MIN) {
        rightShift(myNode, pos);
      } else {
        if (myNode->linker[pos + 1]->count > MIN) {
          leftShift(myNode, pos + 1);
        } else {
          mergeNodes(myNode, pos);
        }
      }
    } else {
      if (myNode->linker[pos - 1]->count > MIN)
        rightShift(myNode, pos);
      else
        mergeNodes(myNode, pos);
    }
  }
}

// Delete a value from the node
int delValFromNode(int item, struct BTreeNode *myNode) {
  int pos, flag = 0;
  if (myNode) {
    if (item < myNode->item[1]) {
      pos = 0;
      flag = 0;
    } else {
      for (pos = myNode->count; (item < myNode->item[pos] && pos > 1); pos--)
        ;
      if (item == myNode->item[pos]) {
        flag = 1;
      } else {
        flag = 0;
      }
    }
    if (flag) {
      if (myNode->linker[pos - 1]) {
        copySuccessor(myNode, pos);
        flag = delValFromNode(myNode->item[pos], myNode->linker[pos]);
        if (flag == 0) {
          printf("Given data is not present in B-Tree\n");
        }
      } else {
        removeVal(myNode, pos);
      }
    } else {
      flag = delValFromNode(item, myNode->linker[pos]);
    }
    if (myNode->linker[pos]) {
      if (myNode->linker[pos]->count < MIN)
        adjustNode(myNode, pos);
    }
  }
  return flag;
}

// Delete operaiton
void delete (int item, struct BTreeNode *myNode) {
  struct BTreeNode *tmp;
  if (!delValFromNode(item, myNode)) {
    printf("Not present\n");
    return;
  } else {
    if (myNode->count == 0) {
      tmp = myNode;
      myNode = myNode->linker[0];
      free(tmp);
    }
  }
  root = myNode;
  return;
}

void searching(int item, int *pos, struct BTreeNode *myNode) {
  if (!myNode) {
    return;
  }

  if (item < myNode->item[1]) {
    *pos = 0;
  } else {
    for (*pos = myNode->count;
       (item < myNode->item[*pos] && *pos > 1); (*pos)--)
      ;
    if (item == myNode->item[*pos]) {
      printf("%d present in B-tree", item);
      return;
    }
  }
  searching(item, pos, myNode->linker[*pos]);
  return;
}

void traversal(struct BTreeNode *myNode) {
  int i;
  if (myNode) {
    for (i = 0; i < myNode->count; i++) {
      traversal(myNode->linker[i]);
      printf("%d ", myNode->item[i + 1]);
    }
    traversal(myNode->linker[i]);
  }
}

int main() {
   int n,x,y;
  scanf("%d",&n);
  for(int i=0;i<n;i++)
  {
      scanf("%d",&x);
      insertion(x);
  }
  // traversal(root);
  //traversal(root);
  scanf("%d",&y);
  delete (y, root);
  traversal(root);
}
```

Write a C program to search an element in a B Tree.
For example:

Input	Result
11
1 4 6 8 2 5 3 9 7 12 35
9 
9 is found

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 3
#define MIN 2

struct BTreeNode {
  int val[MAX + 1], count;
  struct BTreeNode *link[MAX + 1];
};

struct BTreeNode *root;

// Create a node
struct BTreeNode *createNode(int val, struct BTreeNode *child) {
  struct BTreeNode *newNode;
  newNode = (struct BTreeNode *)malloc(sizeof(struct BTreeNode));
  newNode->val[1] = val;
  newNode->count = 1;
  newNode->link[0] = root;
  newNode->link[1] = child;
  return newNode;
}

// Insert node
void insertNode(int val, int pos, struct BTreeNode *node,
        struct BTreeNode *child) {
  int j = node->count;
  while (j > pos) {
    node->val[j + 1] = node->val[j];
    node->link[j + 1] = node->link[j];
    j--;
  }
  node->val[j + 1] = val;
  node->link[j + 1] = child;
  node->count++;
}

// Split node
void splitNode(int val, int *pval, int pos, struct BTreeNode *node,
         struct BTreeNode *child, struct BTreeNode **newNode) {
  int median, j;

  if (pos > MIN)
    median = MIN + 1;
  else
    median = MIN;

  *newNode = (struct BTreeNode *)malloc(sizeof(struct BTreeNode));
  j = median + 1;
  while (j <= MAX) {
    (*newNode)->val[j - median] = node->val[j];
    (*newNode)->link[j - median] = node->link[j];
    j++;
  }
  node->count = median;
  (*newNode)->count = MAX - median;

  if (pos <= MIN) {
    insertNode(val, pos, node, child);
  } else {
    insertNode(val, pos - median, *newNode, child);
  }
  *pval = node->val[node->count];
  (*newNode)->link[0] = node->link[node->count];
  node->count--;
}

// Set the value
int setValue(int val, int *pval,
           struct BTreeNode *node, struct BTreeNode **child) {
  int pos;
  if (!node) {
    *pval = val;
    *child = NULL;
    return 1;
  }

  if (val < node->val[1]) {
    pos = 0;
  } else {
    for (pos = node->count;
       (val < node->val[pos] && pos > 1); pos--)
      ;
    if (val == node->val[pos]) {
      //printf("Duplicates are not permitted\n");
      return 0;
    }
  }
  if (setValue(val, pval, node->link[pos], child)) {
    if (node->count < MAX) {
      insertNode(*pval, pos, node, *child);
    } else {
      splitNode(*pval, pval, pos, node, *child, child);
      return 1;
    }
  }
  return 0;
}

// Insert the value
void insert(int val) {
  int flag, i;
  struct BTreeNode *child;

  flag = setValue(val, &i, root, &child);
  if (flag)
    root = createNode(i, child);
}

// Search node
void search(int val, int *pos, struct BTreeNode *myNode) {
  if (!myNode) {
    return;
  }

  if (val < myNode->val[1]) {
    *pos = 0;
  } else {
    for (*pos = myNode->count;
       (val < myNode->val[*pos] && *pos > 1); (*pos)--)
      ;
    if (val == myNode->val[*pos]) {
      printf("%d is found",val);
      return;
    }
  }
  search(val, pos, myNode->link[*pos]);

  return;
}

// Traverse then nodes
void traversal(struct BTreeNode *myNode) {
  int i;
  if (myNode) {
    for (i = 0; i < myNode->count; i++) {
      traversal(myNode->link[i]);
      printf("%d ", myNode->val[i + 1]);
    }
    traversal(myNode->link[i]);
  }
}

int main() {
   int ch,n,x,y;
  scanf("%d",&n);
  for(int i=0;i<n;i++)
  {
      scanf("%d",&x);
      insert(x);
  }
  scanf("%d",&y);

 // traversal(root);

  //printf("\n");
  search(y, &ch, root);
}
```
### Day 4

Write a C program to traverse the elements in a B+ Tree.

For example:

Input	Result
9
13  45 22 77 55 66 11 57 62 
11 13 22 45 55 57 62 66 77

```c
#include<stdio.h>
#include<stdio.h>
#include<stdlib.h>

struct B_TreeNode
{
    int *data;
    struct B_TreeNode **child_ptr;
    int leaf;
    int n;
};
struct B_TreeNode *root = NULL, *np = NULL, *x = NULL;
struct B_TreeNode * init()
{
    int i;
    np = (struct B_TreeNode *)malloc(sizeof(struct B_TreeNode));
    np->data =(int*)malloc(5*sizeof(int));
    np->child_ptr = (struct B_TreeNode **)malloc(6*sizeof(struct B_TreeNode**));
    np->leaf = 1;
    np->n = 0;
    for (i = 0; i < 6; i++)
    {
        np->child_ptr[i] = NULL;
    }
    return np;
}
void traverse(struct B_TreeNode *p)
{
    //printf("\n");
    int i;
    for (i = 0; i < p->n; i++)
    {
        if (p->leaf == 0)
        {
            traverse(p->child_ptr[i]);
        }
        printf("%d ",p->data[i]);
    }
    if (p->leaf == 0)
    {
        traverse(p->child_ptr[i]);
    }
    //printf("\n");
}
void sort(int *p, int n)
{
    int i, j, temp;
    for (i = 0; i < n; i++)
    {
        for (j = i; j <= n; j++)
        {
            if (p[i] > p[j])
            {
                temp = p[i];
                p[i] = p[j];
                p[j] = temp;
            }
        }
    }
}
int split_child(struct B_TreeNode *x, int i)
{
    int j, mid;
    struct B_TreeNode *np1, *np3, *y;
    np3 = init();
    np3->leaf = 1;
    if (i == -1)
    {
        mid = x->data[2];
        x->data[2] = 0;
        x->n--;
        np1 = init();
        np1->leaf = 0;
        x->leaf = 1;
        for (j = 3; j < 5; j++)
        {
            np3->data[j - 3] = x->data[j];
            np3->child_ptr[j - 3] = x->child_ptr[j];
            np3->n++;
            x->data[j] = 0;
            x->n--;
        }
        for(j = 0; j < 6; j++)
        {
            x->child_ptr[j] = NULL;
        }
        np1->data[0] = mid;
        np1->child_ptr[np1->n] = x;
        np1->child_ptr[np1->n + 1] = np3;
        np1->n++;
        root = np1;
    }
    else
    {
        y = x->child_ptr[i];
        mid = y->data[2];
        y->data[2] = 0;
        y->n--;
        for (j = 3; j < 5; j++)
        {
            np3->data[j - 3] = y->data[j];
            np3->n++;
            y->data[j] = 0;
            y->n--;
        }
        x->child_ptr[i + 1] = y;
        x->child_ptr[i + 1] = np3;
    }
    return mid;
}
void insert(int a)
{
    int i, temp;
    x = root;
    if (x == NULL)
    {
        root = init();
        x = root;
    }
    else
    {
        if (x->leaf == 1 && x->n == 5)
        {
            temp = split_child(x, -1);
            x = root;
            for (i = 0; i < (x->n); i++)
            {
                if ((a > x->data[i]) && (a < x->data[i + 1]))
                {
                    i++;
                    break;
                }
                else if (a < x->data[0])
                {
                    break;
                }
                else
                {
                    continue;
                }
            }
            x = x->child_ptr[i];
        }
        else
        {
            while (x->leaf == 0)
            {
            for (i = 0; i < (x->n); i++)
            {
                if ((a > x->data[i]) && (a < x->data[i + 1]))
                {
                    i++;
                    break;
                }
                else if (a < x->data[0])
                {
                    break;
                }
                else
                {
                    continue;
                }
            }
                if ((x->child_ptr[i])->n == 5)
                {
                    temp = split_child(x, i);
                    x->data[x->n] = temp;
                    x->n++;
                    continue;
                }
                else
                {
                    x = x->child_ptr[i];
                }
            }
        }
    }
    x->data[x->n] = a;
    sort(x->data, x->n);
    x->n++;
}
int main()
{
    int i, n, t;
    scanf("%d",&n);
    for(i = 0; i < n; i++)
    {
      
        scanf("%d",&t);
        insert(t);
    }
    //cout<<"traversal of constructed tree\n";
    traverse(root);
 
}
```

Write a C program to insert the elements in a B+ Tree.

For example:

Input	Result
5
12 56 35 23 11
11 12 23 35 56

```c
#include<stdio.h>
#include<stdio.h>
#include<stdlib.h>

struct B_TreeNode
{
    int *data;
    struct B_TreeNode **child_ptr;
    int leaf;
    int n;
};
struct B_TreeNode *root = NULL, *np = NULL, *x = NULL;
struct B_TreeNode * init()
{
    int i;
    np = (struct B_TreeNode *)malloc(sizeof(struct B_TreeNode));
    np->data =(int*)malloc(5*sizeof(int));
    np->child_ptr = (struct B_TreeNode **)malloc(6*sizeof(struct B_TreeNode**));
    np->leaf = 1;
    np->n = 0;
    for (i = 0; i < 6; i++)
    {
        np->child_ptr[i] = NULL;
    }
    return np;
}
void traverse(struct B_TreeNode *p)
{
    //printf("\n");
    int i;
    for (i = 0; i < p->n; i++)
    {
        if (p->leaf == 0)
        {
            traverse(p->child_ptr[i]);
        }
        printf("%d ",p->data[i]);
    }
    if (p->leaf == 0)
    {
        traverse(p->child_ptr[i]);
    }
    //printf("\n");
}
void sort(int *p, int n)
{
    int i, j, temp;
    for (i = 0; i < n; i++)
    {
        for (j = i; j <= n; j++)
        {
            if (p[i] > p[j])
            {
                temp = p[i];
                p[i] = p[j];
                p[j] = temp;
            }
        }
    }
}
int split_child(struct B_TreeNode *x, int i)
{
    int j, mid;
    struct B_TreeNode *np1, *np3, *y;
    np3 = init();
    np3->leaf = 1;
    if (i == -1)
    {
        mid = x->data[2];
        x->data[2] = 0;
        x->n--;
        np1 = init();
        np1->leaf = 0;
        x->leaf = 1;
        for (j = 3; j < 5; j++)
        {
            np3->data[j - 3] = x->data[j];
            np3->child_ptr[j - 3] = x->child_ptr[j];
            np3->n++;
            x->data[j] = 0;
            x->n--;
        }
        for(j = 0; j < 6; j++)
        {
            x->child_ptr[j] = NULL;
        }
        np1->data[0] = mid;
        np1->child_ptr[np1->n] = x;
        np1->child_ptr[np1->n + 1] = np3;
        np1->n++;
        root = np1;
    }
    else
    {
        y = x->child_ptr[i];
        mid = y->data[2];
        y->data[2] = 0;
        y->n--;
        for (j = 3; j < 5; j++)
        {
            np3->data[j - 3] = y->data[j];
            np3->n++;
            y->data[j] = 0;
            y->n--;
        }
        x->child_ptr[i + 1] = y;
        x->child_ptr[i + 1] = np3;
    }
    return mid;
}
void insert(int a)
{
    int i, temp;
    x = root;
    if (x == NULL)
    {
        root = init();
        x = root;
    }
    else
    {
        if (x->leaf == 1 && x->n == 5)
        {
            temp = split_child(x, -1);
            x = root;
            for (i = 0; i < (x->n); i++)
            {
                if ((a > x->data[i]) && (a < x->data[i + 1]))
                {
                    i++;
                    break;
                }
                else if (a < x->data[0])
                {
                    break;
                }
                else
                {
                    continue;
                }
            }
            x = x->child_ptr[i];
        }
        else
        {
            while (x->leaf == 0)
            {
            for (i = 0; i < (x->n); i++)
            {
                if ((a > x->data[i]) && (a < x->data[i + 1]))
                {
                    i++;
                    break;
                }
                else if (a < x->data[0])
                {
                    break;
                }
                else
                {
                    continue;
                }
            }
                if ((x->child_ptr[i])->n == 5)
                {
                    temp = split_child(x, i);
                    x->data[x->n] = temp;
                    x->n++;
                    continue;
                }
                else
                {
                    x = x->child_ptr[i];
                }
            }
        }
    }
    x->data[x->n] = a;
    sort(x->data, x->n);
    x->n++;
}
int main()
{
    int i, n, t;
    scanf("%d",&n);
    for(i = 0; i < n; i++)
    {
      
        scanf("%d",&t);
        insert(t);
    }
    //cout<<"traversal of constructed tree\n";
    traverse(root);
 
}
```

Write a C program to sort the elements in a B+ Tree.

For example:

Input	Result
7
12 45 33 78 65 22 66
12 22 33 45 65 66 78

```c
#include<stdio.h>
#include<stdio.h>
#include<stdlib.h>

struct B_TreeNode
{
    int *data;
    struct B_TreeNode **child_ptr;
    int leaf;
    int n;
};
struct B_TreeNode *root = NULL, *np = NULL, *x = NULL;
struct B_TreeNode * init()
{
    int i;
    np = (struct B_TreeNode *)malloc(sizeof(struct B_TreeNode));
    np->data =(int*)malloc(5*sizeof(int));
    np->child_ptr = (struct B_TreeNode **)malloc(6*sizeof(struct B_TreeNode**));
    np->leaf = 1;
    np->n = 0;
    for (i = 0; i < 6; i++)
    {
        np->child_ptr[i] = NULL;
    }
    return np;
}
void traverse(struct B_TreeNode *p)
{
    //printf("\n");
    int i;
    for (i = 0; i < p->n; i++)
    {
        if (p->leaf == 0)
        {
            traverse(p->child_ptr[i]);
        }
        printf("%d ",p->data[i]);
    }
    if (p->leaf == 0)
    {
        traverse(p->child_ptr[i]);
    }
    //printf("\n");
}
void sort(int *p, int n)
{
    int i, j, temp;
    for (i = 0; i < n; i++)
    {
        for (j = i; j <= n; j++)
        {
            if (p[i] > p[j])
            {
                temp = p[i];
                p[i] = p[j];
                p[j] = temp;
            }
        }
    }
}
int split_child(struct B_TreeNode *x, int i)
{
    int j, mid;
    struct B_TreeNode *np1, *np3, *y;
    np3 = init();
    np3->leaf = 1;
    if (i == -1)
    {
        mid = x->data[2];
        x->data[2] = 0;
        x->n--;
        np1 = init();
        np1->leaf = 0;
        x->leaf = 1;
        for (j = 3; j < 5; j++)
        {
            np3->data[j - 3] = x->data[j];
            np3->child_ptr[j - 3] = x->child_ptr[j];
            np3->n++;
            x->data[j] = 0;
            x->n--;
        }
        for(j = 0; j < 6; j++)
        {
            x->child_ptr[j] = NULL;
        }
        np1->data[0] = mid;
        np1->child_ptr[np1->n] = x;
        np1->child_ptr[np1->n + 1] = np3;
        np1->n++;
        root = np1;
    }
    else
    {
        y = x->child_ptr[i];
        mid = y->data[2];
        y->data[2] = 0;
        y->n--;
        for (j = 3; j < 5; j++)
        {
            np3->data[j - 3] = y->data[j];
            np3->n++;
            y->data[j] = 0;
            y->n--;
        }
        x->child_ptr[i + 1] = y;
        x->child_ptr[i + 1] = np3;
    }
    return mid;
}
void insert(int a)
{
    int i, temp;
    x = root;
    if (x == NULL)
    {
        root = init();
        x = root;
    }
    else
    {
        if (x->leaf == 1 && x->n == 5)
        {
            temp = split_child(x, -1);
            x = root;
            for (i = 0; i < (x->n); i++)
            {
                if ((a > x->data[i]) && (a < x->data[i + 1]))
                {
                    i++;
                    break;
                }
                else if (a < x->data[0])
                {
                    break;
                }
                else
                {
                    continue;
                }
            }
            x = x->child_ptr[i];
        }
        else
        {
            while (x->leaf == 0)
            {
            for (i = 0; i < (x->n); i++)
            {
                if ((a > x->data[i]) && (a < x->data[i + 1]))
                {
                    i++;
                    break;
                }
                else if (a < x->data[0])
                {
                    break;
                }
                else
                {
                    continue;
                }
            }
                if ((x->child_ptr[i])->n == 5)
                {
                    temp = split_child(x, i);
                    x->data[x->n] = temp;
                    x->n++;
                    continue;
                }
                else
                {
                    x = x->child_ptr[i];
                }
            }
        }
    }
    x->data[x->n] = a;
    sort(x->data, x->n);
    x->n++;
}
int main()
{
    int i, n, t;
    scanf("%d",&n);
    for(i = 0; i < n; i++)
    {
      
        scanf("%d",&t);
        insert(t);
    }
    //cout<<"traversal of constructed tree\n";
    traverse(root);
 
}
```
