#include<stdio.h>
#include<conio.h>
#include<malloc.h>
int *bt,*at,*c;
int n;
void process_A(int n)
{
	int i;
	 
	bt=(int *)malloc(n*sizeof(int));
	at=(int *)malloc(n*sizeof(int));
	c=(int *)malloc(n*sizeof(int));
	for(i=0;i<n;i++)
	{
		printf("\nEnter the Burst time(multiple of 2) for P%d:",i);
		scanf("%d",&bt[i]);
		printf("\nEnter the Arrival Time for P%d:",i);
		scanf("%d",&at[i]);
		printf("\nEnter the priority(select either 1 or 2) for P%d:",i);
		scanf("%d",&c[i]);
	}
	
}
void process_B()
{
	int i;
	for(i=0;i<n;i++)
	{
		if(bt[i]%2!=0)
	    {
		    printf("\n\nYou have entered the burst time (not in the multiple of 2)for the process P%d!!!\n\n",i);
		    main();
	    }
	    else
	    {
	    	int count,j,time,remain,flag=0,time_quantum; 
            int wait_time=0,turnaround_time=0,rt[10];
	        printf("Enter Time Quantum:\t"); 
            scanf("%d",&time_quantum); 
            printf("\n\nProcess\t|Turnaround Time|Waiting Time\n\n"); 
            for(time=0,count=0;remain!=0;) 
            { 
                if(rt[count]<=time_quantum && rt[count]>0) 
                { 
                    time+=rt[count]; 
                    rt[count]=0; 
                    flag=1; 
                } 
                else if(rt[count]>0) 
                { 
                    rt[count]-=time_quantum; 
                    time+=time_quantum; 
                } 
                if(rt[count]==0 && flag==1) 
                { 
                    remain--; 
                    printf("P[%d]\t|\t%d\t|\t%d\n",count+1,time-at[count],time-at[count]-bt[count]); 
                    wait_time+=time-at[count]-bt[count]; 
                    turnaround_time+=time-at[count]; 
                    flag=0; 
                } 
                if(count==n-1) 
                    count=0; 
                else if(at[count+1]<=time) 
                    count++; 
                else 
                    count=0; 
                } 
                    printf("\nAverage Waiting Time= %f\n",wait_time*1.0/n); 
                    printf("Avg Turnaround Time = %f",turnaround_time*1.0/n); 
		}
    }
}
void process_C()
{
	
}
int main()
{
	
	printf("Enter the number of the processes in scheduling:");
	scanf("%d",&n);
	process_A(n);
	process_B();
}
