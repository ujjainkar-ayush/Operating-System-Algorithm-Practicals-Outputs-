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

## 10.Write a program to simulate the paging technique and segmentation technique of memory management.

```
#include <stdio.h>
/* -------- PAGING SIMULATION -------- */
void paging()
{
int page_size, num_pages, i;
printf("\n--- PAGING ---\n");
printf("Enter page size (in bytes): ");
scanf("%d", &page_size);
printf("Enter number of pages: ");
scanf("%d", &num_pages);
int page_table[num_pages];
printf("Enter frame number for each page (page table):\n");
for (i = 0; i < num_pages; i++)
{
printf(" Page %d -> Frame: ", i);
scanf("%d", &page_table[i]);
}
int logical_addr;
printf("Enter logical address to translate: ");
scanf("%d", &logical_addr);
int page_num = logical_addr / page_size;
int offset = logical_addr % page_size;
int phys_addr = page_table[page_num] * page_size + offset;
printf("\nLogical Address : %d", logical_addr);
printf("\nPage Number (p) : %d", page_num);
printf("\nPage Offset (d) : %d", offset);
printf("\nFrame Number (f) : %d (from page table)", page_table[page_num]);
printf("\nPhysical Address : %d [f * page_size + d = %d * %d + %d]\n",
phys_addr, page_table[page_num], page_size, offset);
}
/* -------- SEGMENTATION SIMULATION -------- */
void segmentation()
{
int num_seg, i;
printf("\n--- SEGMENTATION ---\n");
printf("Enter number of segments: ");
scanf("%d", &num_seg);
int base[num_seg], limit[num_seg];
for (i = 0; i < num_seg; i++)
{
printf("Segment %d - Enter base address and limit: ", i);
scanf("%d %d", &base[i], &limit[i]);
}
int seg_num, offset;
printf("Enter segment number: ");
scanf("%d", &seg_num);
printf("Enter offset within segment: ");
scanf("%d", &offset);
printf("\nSegment Base : %d", base[seg_num]);
printf("\nSegment Limit : %d", limit[seg_num]);
printf("\nRequested Offset: %d\n", offset);
if (offset < limit[seg_num])
{
int phys_addr = base[seg_num] + offset;
printf("Physical Address : %d [base + offset = %d + %d]\n",
phys_addr, base[seg_num], offset);
}
else
{
printf("SEGMENTATION FAULT! Offset (%d) >= Limit (%d). Access denied.\n",
offset, limit[seg_num]);
}
}
int main()
{
int choice;
printf("===== Memory Management Simulation =====\n");
printf("1. Paging\n");
printf("2. Segmentation\n");
printf("Enter your choice: ");
scanf("%d", &choice);
if (choice == 1)
paging();
else if (choice == 2)
segmentation();
else
printf("Invalid choice. Please enter 1 or 2.\n");
return 0;
}
```
