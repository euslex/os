import java.util.Scanner;

public class PriorityScheduling {
    Scanner console = new Scanner(System.in);
    int processes;
    String[] pids;
    int[] burstTimes;
    int[] completionTimes;
    int[] waitingTimes;
    int[] turnAroundTimes;
    int[] priorities;
    double totalTurnArroundTime = 0;
    double totalWaitingTime = 0;

    public PriorityScheduling() {
        System.out.print("Enter number of processes : ");
        this.processes = console.nextInt();

        pids = new String[processes];
        burstTimes = new int[processes];
        completionTimes = new int[processes];
        waitingTimes = new int[processes];
        turnAroundTimes = new int[processes];
        priorities = new int[processes];
    }

    void run() {
        for (int i = 0; i < processes; i++) {
            System.out.print("Enter PID of process " + (i + 1) + " : ");
            pids[i] = console.next();
        }
        System.out.println();

        for (int i = 0; i < processes; i++) {
            System.out.print("Enter burst time of process " + pids[i] + " : ");
            burstTimes[i] = console.nextInt();
        }
        System.out.println();

        for (int i = 0; i < processes; i++) {
            System.out.print("Enter prioroty of process " + pids[i] + " : ");
            priorities[i] = console.nextInt();
        }
        System.out.println();

        int prevMinIndex = -1;
        int[] temp = priorities.clone();
        for (int i = 0; i < processes; i++) {
            int minIndex = findMin(temp);
            temp[minIndex] = 99999; // assign a positive infinity.

            // calculate times;
            int completionTime = i == 0 ? burstTimes[minIndex] : completionTimes[prevMinIndex] + burstTimes[minIndex];
            int turnAroundTime = completionTime;
            int waitingTime = turnAroundTime - burstTimes[minIndex];

            prevMinIndex = minIndex;

            completionTimes[minIndex] = completionTime;
            turnAroundTimes[minIndex] = turnAroundTime;
            waitingTimes[minIndex] = waitingTime;

            totalWaitingTime += waitingTime;
            totalTurnArroundTime += turnAroundTime;
        }

        // print
        System.out.println("PID" + "\t" + "BT" + "\t" + "PT" + "\t" + "CT" + "\t" + "TAT" + "\t" + "WT");
        for (int i = 0; i < processes; i++) {
            System.out.println(pids[i] + "\t" + burstTimes[i] + "\t" + priorities[i] + "\t" + completionTimes[i] + "\t"
                    + turnAroundTimes[i] + "\t" + waitingTimes[i]);
        }
        System.out.println();

        System.out.println("Avaerage waiting time " + totalWaitingTime / processes);
        System.out.println("Avaerage turn arround time " + totalTurnArroundTime / processes);
    }

    int findMin(int[] array) {
        int len = array.length;
        int MIN = 0;
        for (int i = 0; i < len; i++) {
            if (array[i] < array[MIN])
                MIN = i;
        }
        return MIN;
    }
}
