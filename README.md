# Operating-System-Algorithm-Practicals-Outputs-

## 1. Write a program to demonstrate the use of FCFS CPU Scheduling algorithm.

```
#include <stdio.h>
int main()
{
int n, i;
printf("Enter number of processes: ");
scanf("%d", &n);
int pid[n], bt[n], wt[n], tat[n];
float avg_wt = 0, avg_tat = 0;
for (i = 0; i < n; i++)
{
printf("Enter Process ID and Burst Time for process %d: ", i + 1);
scanf("%d %d", &pid[i], &bt[i]);
}
/* First process always has waiting time = 0 */
wt[0] = 0;
/* Calculate waiting time: WT[i] = WT[i-1] + BT[i-1] */
for (i = 1; i < n; i++)
{
wt[i] = wt[i - 1] + bt[i - 1];
}
/* Calculate turnaround time: TAT[i] = BT[i] + WT[i] */
for (i = 0; i < n; i++)
{
tat[i] = wt[i] + bt[i];
avg_wt += wt[i];
avg_tat += tat[i];
}
printf("\nPID\tBurst Time\tWaiting Time\tTurnaround Time\n");
for (i = 0; i < n; i++)
{
printf("%d\t%d\t\t%d\t\t%d\n", pid[i], bt[i], wt[i], tat[i]);
}
printf("\nAverage Waiting Time : %.2f", avg_wt / n);
printf("\nAverage Turnaround Time : %.2f\n", avg_tat / n);
return 0;
}
```
### Output 
```
Enter number of processes: 3
Enter Process ID and Burst Time for process 1: 1 5
Enter Process ID and Burst Time for process 2: 2 3 
Enter Process ID and Burst Time for process 3: 3 8

PID     Burst Time      Waiting Time    Turnaround Time
1       5               0               5
2       3               5               8
3       8               8               16

Average Waiting Time : 4.33
Average Turnaround Time : 9.67
```
## 2.Write a program to demonstrate the use of SJF CPU Scheduling algorithm.

```
#include <stdio.h>
int main()
{
int n, i, j;
printf("Enter number of processes: ");
scanf("%d", &n);
int pid[n], bt[n], wt[n], tat[n], temp;
float avg_wt = 0, avg_tat = 0;
for (i = 0; i < n; i++)
{
printf("Enter Process ID and Burst Time for process %d: ", i + 1);
scanf("%d %d", &pid[i], &bt[i]);
}
/* Sort processes in ascending order of burst time using bubble sort */
for (i = 0; i < n - 1; i++)
{
for (j = 0; j < n - i - 1; j++)
{
if (bt[j] > bt[j + 1])
{
temp = bt[j]; bt[j] = bt[j + 1]; bt[j + 1] = temp;
temp = pid[j]; pid[j] = pid[j + 1]; pid[j + 1] = temp;
}
}
}
/* First process has 0 waiting time */
wt[0] = 0;
for (i = 1; i < n; i++)
wt[i] = wt[i - 1] + bt[i - 1];
for (i = 0; i < n; i++)
{
tat[i] = wt[i] + bt[i];
avg_wt += wt[i];
avg_tat += tat[i];
}
printf("\nPID\tBurst Time\tWaiting Time\tTurnaround Time\n");
for (i = 0; i < n; i++)
printf("%d\t%d\t\t%d\t\t%d\n", pid[i], bt[i], wt[i], tat[i]);
printf("\nAverage Waiting Time : %.2f", avg_wt / n);
printf("\nAverage Turnaround Time : %.2f\n", avg_tat / n);
return 0;
}
```
### Output
```
Enter number of processes: 3
Enter Process ID and Burst Time for process 1: 1 6
Enter Process ID and Burst Time for process 2: 2 2
Enter Process ID and Burst Time for process 3: 3 8

PID     Burst Time      Waiting Time    Turnaround Time
2       2               0               2
1       6               2               8
3       8               8               16

Average Waiting Time : 3.33
Average Turnaround Time : 8.67
```
## 3.Write a program to demonstrate the use of Priority CPU Scheduling algorithm.

```
#include <stdio.h>
int main()
{
int n, i, j;
printf("Enter number of processes: ");
scanf("%d", &n);
int pid[n], bt[n], priority[n], wt[n], tat[n], temp;
float avg_wt = 0, avg_tat = 0;
for (i = 0; i < n; i++)
{
printf("Enter PID, Burst Time, Priority for process %d: ", i + 1);
scanf("%d %d %d", &pid[i], &bt[i], &priority[i]);
}
/* Sort by priority (lower number = higher priority) using bubble sort */
for (i = 0; i < n - 1; i++)
{
for (j = 0; j < n - i - 1; j++)
{
if (priority[j] > priority[j + 1])
{
temp = priority[j]; priority[j] = priority[j+1]; priority[j+1] = temp;
temp = bt[j]; bt[j] = bt[j+1]; bt[j+1] = temp;
temp = pid[j]; pid[j] = pid[j+1]; pid[j+1] = temp;
}
}
}
/* Calculate waiting time */
wt[0] = 0;
for (i = 1; i < n; i++)
wt[i] = wt[i - 1] + bt[i - 1];
/* Calculate turnaround time */
for (i = 0; i < n; i++)
{
tat[i] = wt[i] + bt[i];
avg_wt += wt[i];
avg_tat += tat[i];
}
printf("\nPID\tBurst\tPriority\tWaiting Time\tTurnaround Time\n");
for (i = 0; i < n; i++)
printf("%d\t%d\t%d\t\t%d\t\t%d\n", pid[i], bt[i], priority[i], wt[i], tat[i]);
printf("\nAverage Waiting Time : %.2f", avg_wt / n);
printf("\nAverage Turnaround Time : %.2f\n", avg_tat / n);
return 0;
}
```

### Output
```
Enter number of processes: 3
Enter PID, Burst Time, Priority for process 1: 1 6 2
Enter PID, Burst Time, Priority for process 2: 2 4 1
Enter PID, Burst Time, Priority for process 3: 3 5 3

PID     Burst   Priority        Waiting Time    Turnaround Time
2       4       1               0               4
1       6       2               4               10
3       5       3               10              15

Average Waiting Time : 4.67
Average Turnaround Time : 9.67
```

## 4. Write a program to demonstrate the use of Round Robin CPU Scheduling algorithm.

```
#include <stdio.h>
int main()
{
int n, quantum, i, time = 0;
printf("Enter number of processes: ");
scanf("%d", &n);
int pid[n], bt[n], remaining[n], wt[n], tat[n];
float avg_wt = 0, avg_tat = 0;
for (i = 0; i < n; i++)
{
printf("Enter Process ID and Burst Time for process %d: ", i + 1);
scanf("%d %d", &pid[i], &bt[i]);
remaining[i] = bt[i];
}
printf("Enter Time Quantum: ");
scanf("%d", &quantum);
/* Keep cycling until all processes are finished */
int done = 0;
while (done < n)
{
done = 0;
for (i = 0; i < n; i++)
{
if (remaining[i] > 0)
{
if (remaining[i] > quantum)
{
time += quantum;
remaining[i] -= quantum;
}
else
{
/* Process finishes in this turn */
time += remaining[i];
wt[i] = time - bt[i];
remaining[i] = 0;
}
}
else
done++;
}
}
printf("\nPID\tBurst Time\tWaiting Time\tTurnaround Time\n");
for (i = 0; i < n; i++)
{
tat[i] = wt[i] + bt[i];
avg_wt += wt[i];
avg_tat += tat[i];
printf("%d\t%d\t\t%d\t\t%d\n", pid[i], bt[i], wt[i], tat[i]);
}
printf("\nAverage Waiting Time : %.2f", avg_wt / n);
printf("\nAverage Turnaround Time : %.2f\n", avg_tat / n);
return 0;
}
```

### Output
```Enter number of processes: 3
Enter Process ID and Burst Time for process 1: 1 5
Enter Process ID and Burst Time for process 2: 2 8
Enter Process ID and Burst Time for process 3: 3 6
Enter Time Quantum: 2

PID     Burst Time      Waiting Time    Turnaround Time
1       5               8               13
2       8               11              19
3       6               11              17

Average Waiting Time : 10.00
Average Turnaround Time : 16.33
```
## 5.Write a program to demonstrate the use of FIFO Page Replacement algorithm.

```
#include <stdio.h>
int main()
{
int frames, pages, i, j, k;
int faults = 0;
printf("Enter number of frames: ");
scanf("%d", &frames);
printf("Enter number of pages in reference string: ");
scanf("%d", &pages);
int ref[pages];
printf("Enter the page reference string: ");
for (i = 0; i < pages; i++)
scanf("%d", &ref[i]);
int frame[frames], front = 0;
for (i = 0; i < frames; i++)
frame[i] = -1;
printf("\nPage\tFrames\t\t\tStatus\n");
for (i = 0; i < pages; i++)
{
int found = 0;
/* Check if page is already in a frame */
for (j = 0; j < frames; j++)
{
if (frame[j] == ref[i])
{
found = 1;
break;
}
}
if (!found)
{
/* Page fault: replace the oldest page (FIFO) */
frame[front] = ref[i];
front = (front + 1) % frames;
faults++;
printf("%d\t", ref[i]);
for (k = 0; k < frames; k++)
(frame[k] != -1) ? printf("%d ", frame[k]) : printf("- ");
printf("\t\tPage Fault\n");
}
else
{
printf("%d\t", ref[i]);
for (k = 0; k < frames; k++)
(frame[k] != -1) ? printf("%d ", frame[k]) : printf("- ");
printf("\t\tPage Hit\n");
}
}
printf("\nTotal Page Faults : %d\n", faults);
printf("Total Page Hits : %d\n", pages - faults);
return 0;
}
```

### Output
```
Enter number of frames: 3
Enter number of pages in reference string: 12
Enter the page reference string: 1 2 3 4 1 2 5 1 2 3 4 5

Page    Frames                  Status
1       1 - -           Page Fault
2       1 2 -           Page Fault
3       1 2 3           Page Fault
4       4 2 3           Page Fault
1       4 1 3           Page Fault
2       4 1 2           Page Fault
5       5 1 2           Page Fault
1       5 1 2           Page Hit
2       5 1 2           Page Hit
3       5 3 2           Page Fault
4       5 3 4           Page Fault
5       5 3 4           Page Hit

Total Page Faults : 9
Total Page Hits : 3
```
## 6.Write a program to demonstrate the use of LRU Page Replacement algorithm.


```
#include <stdio.h>
int main()
{
int frames, pages, i, j, faults = 0;
printf("Enter number of frames: ");
scanf("%d", &frames);
printf("Enter number of pages in reference string: ");
scanf("%d", &pages);
int ref[pages];
printf("Enter the page reference string: ");
for (i = 0; i < pages; i++)
scanf("%d", &ref[i]);
int frame[frames], time_used[frames];
for (i = 0; i < frames; i++)
{
frame[i] = -1;
time_used[i] = 0;
}
printf("\nPage\tFrames\t\t\tStatus\n");
for (i = 0; i < pages; i++)
{
int found = 0;
/* Check if page is already in a frame (page hit) */
for (j = 0; j < frames; j++)
{
if (frame[j] == ref[i])
{
found = 1;
time_used[j] = i + 1; /* Update last used time on hit */
break;
}
}
if (!found)
{
/* Find the least recently used frame */
int lru = 0;
for (j = 1; j < frames; j++)
{
if (time_used[j] < time_used[lru])
lru = j;
}
frame[lru] = ref[i];
time_used[lru] = i + 1;
faults++;
printf("%d\t", ref[i]);
for (j = 0; j < frames; j++)
(frame[j] != -1) ? printf("%d ", frame[j]) : printf("- ");
printf("\t\tPage Fault\n");
}
else
{
printf("%d\t", ref[i]);
for (j = 0; j < frames; j++)
(frame[j] != -1) ? printf("%d ", frame[j]) : printf("- ");
printf("\t\tPage Hit\n");
}
}
printf("\nTotal Page Faults : %d\n", faults);
printf("Total Page Hits : %d\n", pages - faults);
return 0;
}
```

### Output
```
Enter number of frames: 3
Enter number of pages in reference string: 12
Enter the page reference string: 1 2 3 4 1 2 5 1 2 3 4 5

Page    Frames                  Status
1       1 - -           Page Fault
2       1 2 -           Page Fault
3       1 2 3           Page Fault
4       4 2 3           Page Fault
1       4 1 3           Page Fault
2       4 1 2           Page Fault
5       5 1 2           Page Fault
1       5 1 2           Page Hit
2       5 1 2           Page Hit
3       3 1 2           Page Fault
4       3 4 2           Page Fault
5       3 4 5           Page Fault

Total Page Faults : 10
Total Page Hits : 2
```

## 7.Write a program to demonstrate the use of the deadlock detection algorithm.


```
#include <stdio.h>
#define MAX 10
int main()
{
int n, r, i, j;
int alloc[MAX][MAX], max_res[MAX][MAX], need[MAX][MAX];
int avail[MAX], work[MAX], finish[MAX];
printf("Enter number of processes: ");
scanf("%d", &n);
printf("Enter number of resource types: ");
scanf("%d", &r);
printf("Enter Allocation Matrix:\n");
for (i = 0; i < n; i++)
for (j = 0; j < r; j++)
scanf("%d", &alloc[i][j]);
printf("Enter Maximum Matrix:\n");
for (i = 0; i < n; i++)
for (j = 0; j < r; j++)
{
scanf("%d", &max_res[i][j]);
/* Compute need matrix */
need[i][j] = max_res[i][j] - alloc[i][j];
}
printf("Enter Available Resources:\n");
for (j = 0; j < r; j++)
scanf("%d", &avail[j]);
/* Initialize Work and Finish */
for (j = 0; j < r; j++) work[j] = avail[j];
for (i = 0; i < n; i++) finish[i] = 0;
int count = 0, safe_seq[MAX];
while (count < n)
{
int found = 0;
for (i = 0; i < n; i++)
{
if (!finish[i])
{
/* Check if Need[i] <= Work */
int ok = 1;
for (j = 0; j < r; j++)
if (need[i][j] > work[j]) { ok = 0; break; }
if (ok)
{
/* Pi can run; release its allocation to Work */
for (j = 0; j < r; j++)
work[j] += alloc[i][j];
safe_seq[count++] = i;
finish[i] = 1;
found = 1;
}
}
}
if (!found) break; /* No progress possible */
}
if (count == n)
{
printf("\nSystem is in a SAFE state.\n");
printf("Safe Sequence: ");
for (i = 0; i < n; i++)
printf("P%d ", safe_seq[i]);
printf("\n");
}
else
{
printf("\nSystem is in DEADLOCK state!\n");
printf("Deadlocked Processes: ");
for (i = 0; i < n; i++)
if (!finish[i]) printf("P%d ", i);
printf("\n");
}
return 0;
}
```

### Output
```
Enter number of processes: 5
Enter number of resource types: 3
Enter Allocation Matrix:
0 1 0
2 0 0
3 0 2
2 1 1
0 0 2
Enter Maximum Matrix:
7 5 3
3 2 2
9 0 2
2 2 2
4 3 3
Enter Available Resources:
3 3 2

System is in a SAFE state.
Safe Sequence: P1 P3 P4 P0 P2
```


## 8.Write a program to demonstrate the use of FCFS disk scheduling algorithm.


```
#include <stdio.h>
#include <stdlib.h>
int main()
{
int n, i;
int head, total_movement = 0;
printf("Enter initial head position: ");
scanf("%d", &head);
printf("Enter number of disk requests: ");
scanf("%d", &n);
int req[n];
printf("Enter disk request queue: ");
for (i = 0; i < n; i++)
scanf("%d", &req[i]);
printf("\nServicing Order\t\tHead Movement\n");
int current = head;
for (i = 0; i < n; i++)
{
int movement = abs(req[i] - current);
total_movement += movement;
printf("%d -> %d\t\t%d cylinders\n", current, req[i], movement);
current = req[i];
}
printf("\nTotal Head Movement: %d cylinders\n", total_movement);
return 0;
}
```

### Output


```
Enter initial head position: 50
Enter number of disk requests: 8
Enter disk request queue: 55 58 60 70 18 90 150 38

Servicing Order         Head Movement
50 -> 55                5 cylinders
55 -> 58                3 cylinders
58 -> 60                2 cylinders
60 -> 70                10 cylinders
70 -> 18                52 cylinders
18 -> 90                72 cylinders
90 -> 150               60 cylinders
150 -> 38               112 cylinders

Total Head Movement: 316 cylinders
```
## 9.Write a program to demonstrate the use of SCAN disk scheduling algorithm.

```
#include <stdio.h>
#include <stdlib.h>
int compare(const void *a, const void *b)
{
return (*(int*)a - *(int*)b);
}
int main()
{
int n, i, head;
printf("Enter initial head position: ");
scanf("%d", &head);
printf("Enter number of disk requests: ");
scanf("%d", &n);
int req[n];
printf("Enter disk request queue: ");
for (i = 0; i < n; i++)
scanf("%d", &req[i]);
/* Sort all requests in ascending order */
qsort(req, n, sizeof(int), compare);
int total_movement = 0, current = head;
printf("\nSCAN Scheduling (Elevator Algorithm):\n");
printf("\nForward sweep (toward higher cylinders):\n");
/* First pass: service requests >= initial head position */
for (i = 0; i < n; i++)
{
if (req[i] >= head)
{
total_movement += abs(req[i] - current);
printf("%d -> %d\n", current, req[i]);
current = req[i];
}
}
printf("\nReverse sweep (toward lower cylinders):\n");
/* Second pass: service remaining requests in reverse */
for (i = n - 1; i >= 0; i--)
{
if (req[i] < head)
{
total_movement += abs(req[i] - current);
printf("%d -> %d\n", current, req[i]);
current = req[i];
}
}
printf("\nTotal Head Movement: %d cylinders\n", total_movement);
return 0;
}
```

### Output


```
Enter initial head position: 50
Enter number of disk requests: 8
Enter disk request queue: 55 58 60 70 18 90 150 38

SCAN Scheduling (Elevator Algorithm):

Forward sweep (toward higher cylinders):
50 -> 55
55 -> 58
58 -> 60
60 -> 70
70 -> 90
90 -> 150

Reverse sweep (toward lower cylinders):
150 -> 38
38 -> 18

Total Head Movement: 232 cylinders
```
## 10.Write a program to simulate the paging technique of memory management.

```
#include<stdio.h>

int main(){
    int ps,ms,np,i,la,pg,off,f=0,pt[50];

    printf("Enter page size, memory size, no. of pages: ");
    scanf("%d%d%d",&ps,&ms,&np);

    int nf=ms/ps;
    printf("\nTotal Frames: %d\n\nPage\tFrame\n",nf);

    for(i=0;i<np;i++){
        pt[i]=(f<nf)?f++:-1;
        printf("%d\t%d\n",i,pt[i]);
    }

    char c='y';
    while(c=='y'){
        printf("\nEnter logical address: ");
        scanf("%d",&la);
        pg=la/ps; off=la%ps;
        if(pg<np && pt[pg]!=-1)
            printf("Physical address: %d\n",pt[pg]*ps+off);
        else
            printf("Page not found!\n");
        printf("Try another? (y/n): ");
        scanf(" %c",&c);
    }

    return 0;
}
```

### Output

```
Enter page size, memory size, no. of pages: 4 32 5

Total Frames: 8

Page    Frame
0       0
1       1
2       2
3       3
4       4

Enter logical address: 13
Physical address: 13

Try another? (y/n): y

Enter logical address: 99
Page not found!

Try another? (y/n): n
```
## 11.Write a program to simulate the segmentation technique of memory management.

```
#include<stdio.h>

int main(){
    int n, i, la, seg, off;
    printf("Enter number of segments: ");
    scanf("%d",&n);

    int base[n], limit[n];
    for(i=0;i<n;i++){
        printf("Base and limit of segment %d: ",i);
        scanf("%d%d",&base[i],&limit[i]);
    }

    char c='y';
    while(c=='y'){
        printf("\nEnter segment no. and offset: ");
        scanf("%d%d",&seg,&off);
        if(seg<n && off<limit[seg])
            printf("Physical address: %d\n", base[seg]+off);
        else
            printf("Segmentation fault!\n");
        printf("Try another? (y/n): ");
        scanf(" %c",&c);
    }

    return 0;
}
```

### Output 
```
Enter number of segments: 3
Base and limit of segment 0: 100 50
Base and limit of segment 1: 200 80
Base and limit of segment 2: 400 60

Enter segment no. and offset: 1 30
Physical address: 230

Try another? (y/n): y

Enter segment no. and offset: 2 70
Segmentation fault!

Try another? (y/n): n
```

