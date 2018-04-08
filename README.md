#include<stdio.h>
#include<conio.h>
#include<malloc.h>
int *at1,*at2,*bt1,*bt2,*pr2,*p1,p,n,j=0,k=0;
int count,j,time,total,avg_wt,tat[10],remain,flag=0,time_quantum; 
int avg_tat,wait_time=0,turnaround_time=0,rt[10],pos,pr[10];
void AA()
{
int i;
	for(i=0;i<n;i++)
	{
		if(bt1[i]%2!=0 || bt2[i]%2!=0)
	    {
		    printf("\n\nYou have entered the burst time that is not the multiple of 2 !!");
		    main();
	    }
	    else
	    {
	        
            for(time=0,count=0;remain!=0;) 
            { 
                if(rt[count]<=time_quantum && rt[count]>0) 
                { 
                    time+=rt[count]; 
                    rt[count]=0; 
                    flag=1; 
                } 
                else if(bt2[count]>0) 
                { 
                    rt[count]-=time_quantum; 
                    time+=time_quantum; 
                } 
                if(rt[count]==0 && flag==1) 
                { 
                    remain--; 
                    printf("P[%d]\t|\t%d\t|\t%d\n",count+1,time-at2[count],time-at2[count]-bt2[count]); 
                    wait_time+=time-at2[count]-bt2[count]; 
                    turnaround_time+=time-at2[count]; 
                    flag=0; 
                } 
                if(count==n-1) 
                    count=0; 
                else if(at2[count+1]<=time) 
                    count++; 
                else 
                    count=0; 
                } 
                    printf("\nAverage Waiting Time= %f\n",wait_time*1.0/n); 
                    printf("Avg Turnaround Time = %f",turnaround_time*1.0/n); 
		}
    }	
    
    for(i=0;i<n;i++)
    {
        pos=i;
        for(j=i+1;j<n;j++)
        {
            if(pr[j]<pr[pos])
                pos=j;
        }
 
        int temp=pr[i];
        pr[i]=pr[pos];
        pr[pos]=temp;
 
        temp=bt1[i];
        bt1[i]=bt1[pos];
        bt1[pos]=temp;
    }
      int wt[10];
    wt[0]=0;
    for(i=1;i<n;i++)
    {
        wt[i]=0;
        for(j=0;j<i;j++)
            wt[i]+=bt1[j];
 
        total+=wt[i];
    }
 
    avg_wt=total/n;      
    total=0;
 
    printf("\nProcess\t    Burst Time    \tWaiting Time\tTurnaround Time");
    for(i=0;i<j;i++)
    {
        tat[i]=bt1[i]+wt[i];  
        total+=tat[i];
        printf("\nP[%d]\t\t  %d\t\t    %d\t\t\t%d",p1[i],bt1[i],wt[i],tat[i]);
    }
 
    avg_tat=total/n;    
    printf("\n\nAverage Waiting Time=%d",avg_wt);
    printf("\nAverage Turnaround Time=%d\n",avg_tat);
}
int main()
{
	printf("Enter the number of the processes:");
	scanf("%d",&n);
	int i;
	at1=(int *)malloc(n*sizeof(int));
	at2=(int *)malloc(n*sizeof(int));
	bt1=(int *)malloc(n*sizeof(int));
	bt2=(int *)malloc(n*sizeof(int));
	pr2=(int *)malloc(n*sizeof(int));
	p1=(int *)malloc(n*sizeof(int));
	for(i=0;i<n;i++)
	{
		printf("\nEnter the priority of the process:");
	    scanf("%d",&p);
	    if(p==2)
	    {
		    printf("\nEnter the Burst time(multiple of 2) for P%d:",i);
		    scanf("%d",&bt1[j]);
		    printf("\nEnter the Arrival Time for P%d:",i);
		    scanf("%d",&at1[j]);
		    j=j+1;
	    }
	    else if(p==1)
	    {
	    	printf("\nEnter the Burst time(multiple of 2) for P%d:",i);
		    scanf("%d",&bt2[k]);
		    printf("\nEnter the Arrival Time for P%d:",i);
		    scanf("%d",&at2[k]);
		    printf("\nEnter the priority of the P%d:",i);
		    scanf("%d",&pr2[i]);
		    k=k+1;
		}
		printf("Enter Time Quantum:\t"); 
        scanf("%d",&time_quantum);
	}
	AA();
}
