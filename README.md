#include <stdio.h>
#include <string.h>

struct Process
{
    char pid[10];
    int at;   
    int bt;   
    int wt;   
    int tat;  
    int done; 
};

int main()
{
    int n, i, time = 0, completed = 0;
    float total_wt = 0, total_tat = 0;

    printf("Enter number of processes: ");
    scanf("%d", &n);

    struct Process p[n];

    
    for(i = 0; i < n; i++)
    {
        scanf("%s %d %d", p[i].pid, &p[i].at, &p[i].bt);
        p[i].done = 0;
    }

  
    while(completed < n)
    {
        int idx = -1;
        int min_bt = 10000;

        for(i = 0; i < n; i++)
        {
            if(p[i].at <= time && p[i].done == 0)
            {
                if(p[i].bt < min_bt)
                {
                    min_bt = p[i].bt;
                    idx = i;
                }
            }
        }

        if(idx != -1)
        {
            p[idx].wt = time - p[idx].at;
            time += p[idx].bt;
            p[idx].tat = p[idx].wt + p[idx].bt;

            p[idx].done = 1;
            completed++;

            total_wt += p[idx].wt;
            total_tat += p[idx].tat;
        }
        else
        {
            time++; 
        }
    }

    
    printf("\nWaiting Time:\n");
    for(i = 0; i < n; i++)
    {
        printf("%s %d\n", p[i].pid, p[i].wt);
    }

    printf("\nTurnaround Time:\n");
    for(i = 0; i < n; i++)
    {
        printf("%s %d\n", p[i].pid, p[i].tat);
    }

    printf("\nAverage Waiting Time: %.2f\n", total_wt/n);
    printf("Average Turnaround Time: %.2f\n", total_tat/n);

    return 0;
}
