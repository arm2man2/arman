#include<stdio.h>
#include<conio.h>
#define Max 5
#define Quantum 4

int avgTT=0;
int avgWT=0;

class process
{
	
	public:
		bool Empty=true;
		process()
		{
			Empty=true;
		}
		process(int p,int a, int b)
		{
			Empty=false;
			pid=p;
			arrivalTime=a;
			bursttime=b;
			TurnaroundTime=(arrivalTime+bursttime)-arrivalTime;
			waitingTime=TurnaroundTime-arrivalTime;
			avgTT+=TurnaroundTime;
			avgWT+=waitingTime;
		}
	int pid;
	int arrivalTime;
	int bursttime;
	int TurnaroundTime;
	//Calculate Properties
	int waitingTime;
	
	
	
};

class Queue
{
	public:
		int Qid;
		int priority;
	process p[Max];
	//Methods
	int RoundRobin(void)
	{
		for(int i=0;i<Max;i++)
		{
			if(p[i].Empty==false)
			{printf("\nP%d->%d",p[i].pid,p[i].bursttime);
		p[i].bursttime=p[i].bursttime-Quantum;
			}
		}
		for(int k=0;k<20;k++)
		{
		
				for(int i=0;i<Max;i++)
		{
			if(p[i].Empty==false && p[i].bursttime>0)
			{  
				printf("\nP%d->%d",p[i].pid,p[i].bursttime);
				p[i].bursttime=p[i].bursttime-Quantum;
			}
			
		}
		
		}	
	
	}
	int ShowTurnaroundTime()
	{
		for(int i=0;i<Max;i++)
	{
	
			if(p[i].Empty==false)
			{printf("\nCompletion Time of P%d CT->%d",i,p[i].TurnaroundTime);
			printf("\nWaiting Time of P%d WT->%d",i,p[i].waitingTime);
			}
		}
	}
};
void ShowQue(Queue q)
{
	
	printf("\n Que ID:%d \nPriority: %d",q.Qid,q.priority);
	for(int i=0;i<Max;i++)
	{
		if(q.p[i].Empty!=true)
		printf(" \nProcessId: P%d",q.p[i].pid);
	
	}
	
	
}
int main()
{
	Queue q[3];
	
	Priority:
	for(int i=0;i<3;i++)
	{
		printf("\nEnter Priority for Que %c:",i+65);
		scanf("%d",&q[i].priority);
		if(q[i].priority>3||q[i].priority<1)
		 {
		 	printf("Choose priority from range 1-3 for 3 queues.");
		 	goto Priority;
		 }
	}
	

	int n;		
	printf("\nEnter the No.of processes :");
	scanf("%d",&n);
	fflush(stdin);
	for(int j=0;j<n;j++)
	{	int p,a,b;
	    printf("\nEnter the Details of process P%d:",j+1);
		
		printf("\nEnter the Pid process P%d:",j+1);		
		scanf("%d",&p);
		printf("\nEnter the Arrival time process P%d:",j+1);		
		scanf("%d",&a);
		printf("\nEnter the burst time of process P%d:",j+1);
		
		scanf("%d",&b);
		process P(p,a,b);
		printf("\nWhich Que?");
		int qno;
		scanf("%d",&qno);
		if(qno>3)printf("Que not available.");
		else
		{
			q[qno-1].p[j]=P;
		}
			
	}
	Queue pList[3];
	for(int i=0;i<3;i++)
	{
		if(q[i].priority==1)
		pList[0]=q[i];
		
		if(q[i].priority==2)
		pList[1]=q[i];
		
		if(q[i].priority==3)
		pList[2]=q[i];
	}
	for(int i=0;i<3;i++)
	{
	
		printf("\n************************************Queue %d***********************************************",i+1);
	pList[i].RoundRobin();
		printf("\n------------------Stats-------------------------------------------------------");
	pList[i].ShowTurnaroundTime();
	
		
	}
	printf("\n------------------------------------------------------------------------------------------");
	printf("\nAVG TURNING AROUND TIME->%d",avgTT/n);
	printf("\nAVG WAITING AROUND TIME->%d",avgWT/n);
	getch();
}
