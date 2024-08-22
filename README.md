import java.util.HashMap;
import java.util.Scanner;

public class Main {

    private static HashMap<String, Boolean> voterRegistry = new HashMap<>();
    private static HashMap<String, Integer> candidates = new HashMap<>();

    public static void main(String[] args) {
        registerVoters();
        registerCandidates();

        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter your Voter ID:");
        String voterID = scanner.nextLine();

        if (isEligibleToVote(voterID)) {
            System.out.println("Choose your candidate:");
            for (String candidate : candidates.keySet()) {
                System.out.println(candidate);
            }
            String chosenCandidate = scanner.nextLine();

            if (candidates.containsKey(chosenCandidate)) {
                castVote(voterID, chosenCandidate);
                System.out.println("Vote cast successfully!");
            } else {
                System.out.println("Invalid candidate selection.");
            }
        } else {
            System.out.println("You have already voted or are not registered.");
        }

        scanner.close();
        displayResults();
    }

    private static void registerVoters() {
        voterRegistry.put("Voter1", false);
        voterRegistry.put("Voter2", false);
        voterRegistry.put("Voter3", false);
    }

    private static void registerCandidates() {
        candidates.put("CandidateA", 0);
        candidates.put("CandidateB", 0);
        candidates.put("CandidateC", 0);
    }

    private static boolean isEligibleToVote(String voterID) {
        return voterRegistry.containsKey(voterID) && !voterRegistry.get(voterID);
    }

    private static void castVote(String voterID, String candidate) {
        voterRegistry.put(voterID, true);
        candidates.put(candidate, candidates.get(candidate) + 1);
    }

    private static void displayResults() {
        System.out.println("Voting results:");
        for (String candidate : candidates.keySet()) {
            System.out.println(candidate + ": " + candidates.get(candidate) + " votes");
        }
    }
}
10:05 pm
