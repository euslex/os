import java.util.Scanner;

public class RoundRobin {
    Scanner console = new Scanner(System.in);
    int processes;
    int quantum;
    String[] pids;
    int[] burstTimes;
    int[] completionTimes;
    int[] waitingTimes;
    int[] turnAroundTimes;
    double totalTurnArroundTime = 0;
    double totalWaitingTime = 0;

    public RoundRobin() {
        System.out.print("Enter number of processes : ");
        this.processes = console.nextInt();

        System.out.print("Enter time quantum : ");
        this.quantum = console.nextInt();

        pids = new String[processes];
        burstTimes = new int[processes];
        completionTimes = new int[processes];
        waitingTimes = new int[processes];
        turnAroundTimes = new int[processes];
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

        int index = 0;
        int time = 0;
        int maxIndex = findMax(burstTimes);

        while (index <= splitAccordingToQuantum(burstTimes[maxIndex], quantum).length) {
            for (int i = 0; i < processes; i++) {
                if (index < splitAccordingToQuantum(burstTimes[i], quantum).length
                        && splitAccordingToQuantum(burstTimes[i], quantum)[index] > 0) {
                    int completionTime = index == 0 ? time + splitAccordingToQuantum(burstTimes[i], quantum)[0]
                            : time + splitAccordingToQuantum(burstTimes[i], quantum)[index];
                    time += splitAccordingToQuantum(burstTimes[i], quantum)[index];

                    completionTimes[i] = completionTime;
                }
            }
            index++;
        }

        for (int i = 0; i < processes; i++) {
            int turnArroundTime = completionTimes[i];
            int waitingTime = turnArroundTime - burstTimes[i];

            turnAroundTimes[i] = turnArroundTime;
            totalTurnArroundTime += turnArroundTime;

            waitingTimes[i] = waitingTime;
            totalWaitingTime += waitingTime;
        }

        // print
        System.out.println("PID" + "\t" + "BT" + "\t" + "CT" + "\t" + "TAT" + "\t" + "WT");
        for (int i = 0; i < processes; i++) {
            System.out.println(pids[i] + "\t" + burstTimes[i] + "\t" + completionTimes[i] + "\t"
                    + turnAroundTimes[i] + "\t" + waitingTimes[i]);
        }
        System.out.println();

        System.out.println("Avaerage waiting time " + totalWaitingTime / processes);
        System.out.println("Avaerage turn arround time " + totalTurnArroundTime / processes);
    }

    int[] splitAccordingToQuantum(int num, int timeQuantum) {
        int[] result = new int[num / timeQuantum + 1];
        int i = 0;
        while (num > 0) {
            if (num >= timeQuantum) {
                result[i++] = timeQuantum;
                num -= timeQuantum;
            } else {
                result[i++] = num;
                num = 0;
            }
        }
        return result;
    }

    int findMax(int[] array) {
        int len = array.length;
        int MAX = 0;
        for (int i = 0; i < len; i++) {
            if (array[i] > array[MAX])
                MAX = i;
        }
        return MAX;
    }
}
