def ResponseTime(processes, num_p, b_t,rt, quantum):
	copy_bt = [0] * num_p

	
	for i in range(num_p):
		copy_bt[i] = b_t[i]
	t =0

	while(1):
		flag = True
		
		for i in range(num_p):
			if (copy_bt[i] > 0) :
				flag = False
				
				if (copy_bt[i] > quantum) :
					t += quantum
					copy_bt[i] -= quantum
					
				else:
					t = t + copy_bt[i]
					rt[i] = t - b_t[i]
					copy_bt[i] = 0
				
		if (flag == True):
			break
			

def findTurnAroundTime(processes,num_p, b_t, rt, TurnAroundTime):
	for i in range(num_p):
		TurnAroundTime[i] = b_t[i] + rt[i]

def findavgTime(processes,num_p, b_t, quantum):
	rt = [0] * num_p
	TurnAroundTime = [0] * num_p
	ResponseTime(processes,num_p, b_t,rt, quantum)
	findTurnAroundTime(processes,num_p, b_t,rt,TurnAroundTime)
	#print("Processes"," Burst Time"	," Response Time","  Turn-Around Time")
	total_rt = 0
	total_TurnAroundTime = 0
	
	
	
	for i in range(num_p):
		total_rt = total_rt + rt[i]
		total_TurnAroundTime = total_TurnAroundTime + TurnAroundTime[i]
		print("Processes"," Burst Time"	," Response Time","  Turn-Around Time")
		print(" ", i+1, "\t\t", b_t[i],"\t\t", rt[i], "\t\t", TurnAroundTime[i])
			
	print("\nCPU Scheduling Alg : RR(%.5f) "%(quantum))
	print("Average response time = %.5f "%(total_rt /num_p) )
	print("Average turn around time = %.5f "% (total_TurnAroundTime / num_p))
	
	
	
if __name__ == "__main__":
	proc = [1, 2, 3, 4, 5]
	num_p = 5
	quantum =9
	burst_time = [10, 5, 8,8,56]
	findavgTime(proc,num_p, burst_time, quantum)


