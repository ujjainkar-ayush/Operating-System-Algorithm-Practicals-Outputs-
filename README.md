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
