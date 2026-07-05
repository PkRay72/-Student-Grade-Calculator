# -Student-Grade-Calculator

import java.util.Scanner;
public class StudentGradeCalculator {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // ---------- PHASE I: INPUT (The Gatekeeper) ----------
        int numberOfSubjects = readValidSubjectCount(sc);

        int totalMarks = 0; // Gear 1: The Accumulator

        for (int i = 1; i <= numberOfSubjects; i++) {
            int mark = readValidMark(sc, i);
            totalMarks += mark; // total += currentMark;
        }

        // ---------- PHASE II: PROCESS (The Engine Room) ----------

        // Gear 2: The Math & Truncation Trap fix
        // Explicitly cast to double BEFORE dividing, so we don't lose decimals.
        double averagePercentage = (double) totalMarks / numberOfSubjects;

        // Gear 3: The Logic Ladder — check the strictest condition first
        char grade = calculateGrade(averagePercentage);

        // ---------- PHASE III: OUTPUT (The Presentation Layer) ----------
        printReport(numberOfSubjects, totalMarks, averagePercentage, grade);

        sc.close();
    }

    
    private static int readValidSubjectCount(Scanner sc) {
        int count = -1;
        while (count <= 0) {
            System.out.print("Enter the number of subjects: ");
            String line = sc.nextLine().trim();
            try {
                count = Integer.parseInt(line);
                if (count <= 0) {
                    System.out.println("Invalid input. Number of subjects must be greater than 0.");
                }
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a whole number.");
            }
        }
        return count;
    }

    
    private static int readValidMark(Scanner sc, int subjectNumber) {
        int mark = -1;
        boolean valid = false;

        while (!valid) {
            System.out.print("Enter marks for Subject " + subjectNumber + " (out of 100): ");
            String line = sc.nextLine().trim();
            try {
                mark = Integer.parseInt(line);
                if (mark < 0 || mark > 100) {
                    System.out.println("Invalid marks. Value must be between 0 and 100.");
                } else {
                    valid = true;
                }
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a whole number between 0 and 100.");
            }
        }
        return mark;
    }

    
    private static char calculateGrade(double percentage) {
        if (percentage >= 90) {
            return 'A';
        } else if (percentage >= 80) {
            return 'B';
        } else if (percentage >= 70) {
            return 'C';
        } else if (percentage >= 60) {
            return 'D';
        } else {
            return 'F';
        }
    }

    
    private static void printReport(int numberOfSubjects, int totalMarks,
                                     double averagePercentage, char grade) {
        System.out.println();
        System.out.println("========== STUDENT GRADE REPORT ==========");
        System.out.printf("Number of Subjects : %d%n", numberOfSubjects);
        System.out.printf("Total Marks         : %d / %d%n", totalMarks, numberOfSubjects * 100);
        System.out.printf("Average Percentage  : %.2f%%%n", averagePercentage);
        System.out.printf("Grade               : %c%n", grade);
        System.out.println("===========================================");
    }
}
