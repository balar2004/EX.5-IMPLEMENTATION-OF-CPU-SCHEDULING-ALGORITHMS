## EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS
## 1-IMPLEMENTATION OF FIRST COME FIRST SERVE SCHEDULING.
## Aim:
To implement the first come first serve scheduling algorithm
## Algorithm:
1. Start the process
2. Get the number of processes to be inserted
3. Get the value for burst time of each process from the user
4. Having allocated the burst time(bt) for individual processes , Start with the first
process from its initial position let other process to be in queue
5. Calculate the waiting time(wt) and turnaround time(tat) as
6. Wt(pi) = wt(pi-1) + tat(pi-1) (i.e. wt of current process = wt of previous process + tat of
previous process)
7. tat(pi) = wt(pi) + bt(pi) (i.e. tat of current process = wt of current process + bt of
current process)
8. Calculate the total and average waiting time and turnaround time
9. Display the values
# Program:
```
#include<stdio.h>
int main()
{
    int bt[20],p[20],wt[20],tat[20],i,j,n,total=0,pos,temp; float
    avg_wt,avg_tat;
    printf("Enter number of process:");
    scanf("%d",&n);
    printf("\nEnter Burst Time:\n");
    for(i=0;i<n;i++)
    {
        printf("p % d:",i+1);
        scanf("%d",&bt[i]);
        p[i]=i+1;
    }
    wt[0]=0;
    for(i=1;i<n;i++)
    {
        wt[i]=0;
        for(j=0;j<i;j++)
        {
            wt[i]+=bt[j];
            total+=wt[i];
        }    
    }
    avg_wt=(float)total/n;
    total=0;
    printf("\nProcess\t Burst Time \tWaiting Time\tTurnaround Time");
    for(i=0;i<n;i++)
    {
        tat[i]=bt[i]+wt[i];
        total+=tat[i];
    printf("\np%d\t\t %d\t\t%d\t\t\t%d",p[i],bt[i],wt[i],tat[i]);
    }
    avg_tat=(float)total/n;
    printf("\n\nAverage Waiting Time=%f",avg_wt);
    printf("\nAverage Turnaround Time=%f\n",avg_tat);
}
```
## Output:
![cpu](https://github.com/balar2004/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/118791778/d4e5257a-ab9b-463b-b13d-81313e1ab61f)
## Result:
Thus, the first come first serve scheduling algorithm is implemented successfully.

## 2-IMPLEMENTATION OF SHORTEST JOB FIRST SCHEDULING.
## Aim:
To implement the Shortest Job First scheduling algorithm
## Algorithm :
1. Start the process
2. Get the number of processes to be inserted
3. Sort the processes according to the burst tiine and allocate the one with shortest burst to
execute first
4. If two process have same burst length then FCFS scheduling algorithm is used
5. Calculate the total and average waiting time and turn around time
6. Display the values
7. Stop the process
## Program:
```
#include<stdio.h>
int main()
{
    int bt[20],p[20],wt[20],tat[20],i,j,n,total=0,pos,temp; float
    avg_wt,avg_tat;
    printf("Enter number of process:");
    scanf("%d",&n);
    printf("\nEnter Burst Time:\n");
    for(i=0;i<n;i++)
    {
        printf("p%d:",i+1);
        scanf("%d",&bt[i]);
        p[i]=i+1;
    }
    for(i=0;i<n;i++)
    {
        pos=i;
        for(j=i+1;j<n;j++)
        {
            if(bt[j]<bt[pos])
            {
                pos=j;
            }
        }
        temp=bt[i];
        bt[i]=bt[pos];
        bt[pos]=temp;
        temp=p[i];
        p[i]=p[pos];
        p[pos]=temp;
    }
    wt[0]=0;
    for(i=1;i<n;i++)
    {
        wt[i]=0;for(j=0;j<i;j++)
        wt[i]+=bt[j];
        total+=wt[i];
    }
    avg_wt=(float)total/n;
    total=0;
    printf("\nProcess\tBurst Time\tWaiting Time\tTurnaround Time");
    for(i=0;i<n;i++)
    {
        tat[i]=bt[i]+wt[i];
        total+=tat[i];
        printf("\np%d\t\t %d\t\t%d\t\t\t%d",p[i],bt[i],wt[i],tat[i]);
    }
    avg_tat=(float)total/n;
    printf("\n\nAverage Waiting Time=%f",avg_wt);
    printf("\nAverage Turnaround Time=%f\n",avg_tat);
}
```
## Output:
![cpu2](https://github.com/balar2004/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/118791778/385ad97c-d5e3-48ec-bced-812dd2dbcee2)
## Result:
Thus, the Shortest Job First scheduling algorithm is implemented successfully.

## 3-IMPLEMENTATION OF PRIORITY SCHEDULING.
## Aim:
To implement priority scheduling algorithm
## Algorithm:
1.Start the process
2.Get the number of processes to be inserted
3.Get the corresponding priority of processes
4.
Sort the processes according to the priority and allocate the one with highest priority
to execute first
5.If two process have same priority then FCFS scheduling algorithm is used
6.Calculate the total and average waiting time and turnaround time
7.Display the values
8.Stop the process
## Program:
```
#include<stdio.h>
int main()
{
    int bt[20],p[20],wt[20],tat[20],pri[20],i,j,k,n,total=0,pos,temp; float
    avg_wt,avg_tat;
    printf("Enter number of process:");
    scanf("%d",&n);
    printf("\nEnter Burst Time:\n");
    for(i=0;i<n;i++)
    {
        printf("p%d:",i+1);
        scanf("%d",&bt[i]);
        p[i]=i+1;
    }
    printf("Enter priority of the process \n");
    for(i=0;i<n;i++)
    {
        p[i] = i;
        printf("p%d ",i+1);
        scanf("%d",&pri[i]);
    }
    for(i=0;i<n;i++)
    {
        for(k=i+1;k<n;k++)
        {
            if(pri[i] > pri[k])
            {
                temp=p[i];
                p[i]=p[k];
                p[k]=temp;
                temp=bt[i];
                bt[i]=bt[k];
                bt[k]=temp;
                temp=pri[i];
                pri[i]=pri[k];
                pri[k]=temp;
            }
        }
    }
    wt[0]=0;
    for(i=1;i<n;i++)
    {
        wt[i]=0;
        for(j=0;j<i;j++)
        wt[i]+=bt[j];
        total+=wt[i];
    }
    avg_wt=(float)total/n;
    total=0;
    printf("\nProcess\tBurst Time \tPriority \tWaiting Time\tTurnaround Time");
    for(i=0;i<n;i++)
    {
        tat[i]=bt[i]+wt[i];
        total+=tat[i];
        printf("\np%d\t\t %d\t\t %d\t\t %d\t\t\t%d",p[i],bt[i],pri[i],wt[i],tat[i]);
    }
    avg_tat=(float)total/n;
    printf("\n\nAverage Waiting Time=%f",avg_wt);
    printf("\nAverage Turnaround Time=%f\n",avg_tat);
}
```
## Output:
![cpu3](https://github.com/balar2004/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/118791778/e2ef803b-38ad-479f-bb1b-918ee4a3a708)
## Result:
Thus, priority scheduling algorithm is implemented successfully.

## 4-IMPLEMENTATION OF ROUND-ROBIN SCHEDULING.
## Aim:
To implement round robin scheduling algorithm
## Algorithm:
1.Start the process
2.Get the number of elements to be inserted
3.Get the value for burst time for individual processes
4.Get the value for time quantum
5.Make the CPU scheduler go around the ready queue allocating CPU to each process for the time interval specified
6.Make the CPU scheduler pick the first process and set time to interrupt after quantum.
And after it's expiry dispatch the process
7.If the process has burst time less than the time quantum then the process is released by
the CPU
8.If the process has burst time greater than time quantum then it is interrupted by the OS
and the process is put to the tail of ready queue and the schedule selects next
process from head of the queue
9.Calculate the total and average waiting time and turnaround time
10.Display the results
## Program:
```
#include<stdio.h>
int main()
{
    int st[10],bt[10],wt[10],tat[10],n,tq; int
    i,count=0,swt=0,stat=0,temp,sq=0;
    float awt,atat;
    printf("Enter the number of processes:");
    scanf("%d",&n);
    printf("Enter the burst time of each process:\n");
    for(i=0;i<n;i++)
    {
        printf("p%d:",i+1);
        scanf("%d",&bt[i]);
        st[i]=bt[i];
    }
    printf("Enter the time quantum:");
    scanf("%d",&tq);
    while(1)
    {
        for(i=0,count=0;i<n;i++)
        {
            temp=tq;
            if(st[i]==0)
            {
                count++;
                continue;
            }
            if(st[i]>tq)
            st[i]=st[i]-tq;
            else
            if(st[i]>=0){
            temp=st[i];
            st[i]=0;
        }
        sq=sq+temp;
        tat[i]=sq;
    }
    if(n==count)
    break;
    }
    for(i=0;i<n;i++)
    {
        wt[i]=tat[i]-bt[i];
        swt=swt+wt[i];
        stat=stat+tat[i];
    }
    awt=(float)swt/n;
    atat=(float)stat/n;
    printf("Process no\t burst time\t waiting time\t turnaround time\n");
    for(i=0;i<n;i++)
    printf("%d\t\t %d\t\t %d\t\t %d\n",i+1,bt[i],wt[i],tat[i]); printf("avgwt time=%f,avg turn around time=%f",awt,atat);
}
```
## Output:
![cpu4](https://github.com/balar2004/EX.5-IMPLEMENTATION-OF-CPU-SCHEDULING-ALGORITHMS/assets/118791778/972d4d45-377f-4056-8647-e6e343606685)
## Result:
Thus, round robin scheduling algorithm implemented successfully.
