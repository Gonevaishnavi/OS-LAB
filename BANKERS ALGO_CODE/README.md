Aim: Write a C program to implement the various process scheduling mechanisms such as Bankers Algorithm.

Algorithm: Let ‘n’ be the number of processes in the system and ‘m’ be the number of resources types.
Available : 

It is a 1-d array of size ‘m’ indicating the number of available resources of each type.
Available[ j ] = k means there are ‘k’ instances of resource type Rj
Max :

It is a 2-d array of size ‘n*m’ that defines the maximum demand of each process in a system.
Max[ i, j ] = k means process Pi may request at most ‘k’ instances of resource type Rj.
Allocation :

It is a 2-d array of size ‘n*m’ that defines the number of resources of each type currently allocated to each process.
Allocation[ i, j ] = k means process Pi is currently allocated ‘k’ instances of resource type Rj
Need :

 It is a 2-d array of size ‘n*m’ that indicates the remaining resource need of each process.
Need [ i,   j ] = k means process Pi currently need ‘k’ instances of resource type Rj
for its execution.

Need [ i,   j ] = Max [ i,   j ] – Allocation [ i,   j ]



Allocationi specifies the resources currently allocated to process Pi and Needi specifies the additional resources that process Pi may still request to complete its task.

Banker’s algorithm consists of Safety algorithm and Resource request algorithm.

Program:
#include <stdio.h>
 
int current[5][5], maximum_claim[5][5], available[5];
int allocation[5] = {0, 0, 0, 0, 0};
int maxres[5], running[5], safe = 0;
int counter = 0, i, j, exec, resources, processes, k = 1;
 
int main()
{
printf("\nEnter number of processes: ");
     scanf("%d", &processes);
 
     for (i = 0; i < processes; i++)
{
         running[i] = 1;
         counter++;
     }
 
     printf("\nEnter number of resources: ");
     scanf("%d", &resources);
 
     printf("\nEnter Claim Vector:");
     for (i = 0; i < resources; i++)
{
        scanf("%d", &maxres[i]);
     }
 
   printf("\nEnter Allocated Resource Table:\n");
     for (i = 0; i < processes; i++)
{
        for(j = 0; j < resources; j++)
{
   scanf("%d", &current[i][j]);
         }
     }
 
     printf("\nEnter Maximum Claim Table:\n");
     for (i = 0; i < processes; i++)
{
         for(j = 0; j < resources; j++)
{
             scanf("%d", &maximum_claim[i][j]);
         }
     }
 
printf("\nThe Claim Vector is: ");
     for (i = 0; i < resources; i++)
{
        printf("\t%d", maxres[i]);
}
 
     printf("\nThe Allocated Resource Table:\n");
     for (i = 0; i < processes; i++)
{
        for (j = 0; j < resources; j++)
{
             printf("\t%d", current[i][j]);
         }
printf("\n");
     }
 
     printf("\nThe Maximum Claim Table:\n");
     for (i = 0; i < processes; i++)
{
         for (j = 0; j < resources; j++)
{
        printf("\t%d", maximum_claim[i][j]);
         }
         printf("\n");
     }
 
     for (i = 0; i < processes; i++)
{
         for (j = 0; j < resources; j++)
{
             allocation[j] += current[i][j];
         }
     }
 
     printf("\nAllocated resources:");
     for (i = 0; i < resources; i++)
{
         printf("\t%d", allocation[i]);
     }
 
     for (i = 0; i < resources; i++)
{
        available[i] = maxres[i] - allocation[i];
}
 
     printf("\nAvailable resources:");
     for (i = 0; i < resources; i++)
{
         printf("\t%d", available[i]);
     }
     printf("\n");
 
     while (counter != 0)
{
         safe = 0;
         for (i = 0; i < processes; i++)
{
             if (running[i])
{
                 exec = 1;
                 for (j = 0; j < resources; j++)
{
                     if (maximum_claim[i][j] - current[i][j] > available[j])
{
                         exec = 0;
                         break;
                     }
                 }
                 if (exec)
{
                     printf("\nProcess%d is executing\n", i + 1);
                     running[i] = 0;
                     counter--;
                     safe = 1;
 
                     for (j = 0; j < resources; j++)
{
                         available[j] += current[i][j];
                     }
                break;
                 }
             }
         }
         if (!safe)
{
             printf("\nThe processes are in unsafe state.\n");
             break;
         }
else
{
             printf("\nThe process is in safe state");
             printf("\nAvailable vector:");
 
             for (i = 0; i < resources; i++)
{
                 printf("\t%d", available[i]);
             }
 
        printf("\n");
         }
     }
     return 0;
}
