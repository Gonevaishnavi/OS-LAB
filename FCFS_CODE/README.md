1)FCFS (First Come First Serve)

Aim: Write a C program to implement the various process scheduling mechanisms such as FCFS
scheduling.

Algorithm:
1: Start the process
2: Accept the number of processes in the ready Queue
3: For each process in the ready Q, assign the process id and accept the CPU burst time
4: Set the waiting of the first process as ‘0’ and its burst time as its turn around time
5: for each process in the Ready Q calculate
a. Waiting time for process(n)= waiting time of process (n-1) + Burst time of process(n-1)
b. Turnaround time for Process(n)= waiting time of Process(n)+ Burst time for process(n)
6: Calculate
a. Average waiting time = Total waiting Time / Number of process
b. Average Turnaround time = Total Turnaround Time / Number of process
7: Stop the process


Program: 

#include<stdio.h>
int main()
{
 int bt[20],p[20],wt[20],tat[20],i,j,n,total=0,pos,temp;
 float avg_wt,avg_tat;
 printf("Enter number of process:");
 scanf("%d",&n);
 printf("\nEnter Burst Time:\n");
 for(i=0;i<n;i++)
 {
 printf("p % d:",i+1);
 scanf("%d",&bt[i]);
 p[i]=i+1; //contains process number
 }
wt[0]=0; //waiting time for first process will be zero
//calculate waiting time
 for(i=1;i<n;i++)
 {
 wt[i]=0;
 for(j=0;j<i;j++)
 wt[i]+=bt[j];
 total+=wt[i];
 }
 avg_wt=(float)total/n; //average waiting time
 total=0;
 printf("\nProcess\t Burst Time \tWaiting Time\tTurnaround Time");
for(i=0;i<n;i++)
 {
 tat[i]=bt[i]+wt[i]; //calculate turnaround time
 total+=tat[i];
 printf("\np%d\t\t %d\t\t %d\t\t\t%d",p[i],bt[i],wt[i],tat[i]);
 }
 avg_tat=(float)total/n; //average turnaround time
 printf("\n\nAverage Waiting Time=%f",avg_wt);
 printf("\nAverage Turnaround Time=%f\n",avg_tat);
}



