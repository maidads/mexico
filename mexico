import java.util.Random;
import java.util.Scanner;

import static java.lang.System.*;


public class Mexico {

    public static void main(String[] args) {
        new Mexico().program();
    }

    final Random rand = new Random();
    final Scanner sc = new Scanner(in);
    final int maxRolls = 3;      // No player may exceed this
    final int startAmount = 3;   // Money for a player. Select any
    final int mexico = 1000;     // A value greater than any other

    void program() {

        int pot = 0;         // What the winner will get
        Player[] players;    // The players (array of Player objects)
        Player current;      // Current player
        Player leader;       // Player starting the round

        players = getPlayers();
        current = getRandomPlayer(players);
        leader = current;

        out.println("Mexico Game Started");
        statusMsg(players);

        while (players.length > 1) {   // game over when only one player left

            // ----- In ----------
        String cmd = getPlayerChoice(current);
        if ("r".equals(cmd)) {

            // --- Process ------
            if (current == leader && current.nRolls < maxRolls) {
                current = rollDice(current);
                roundMsg(current);
            } else if (current.nRolls < leader.nRolls && current != leader) {
                current = rollDice(current);
                roundMsg(current);
            } else {
                current = next(players, current);     
            }

                    // ---- Out --------

            } else if ("n".equals(cmd) && current.nRolls > 0) {

            current = next(players, current);
                 // Process
            } else {
                out.println("?");
            }

            if (allRolled(players, leader)) {          
                // --- Process -----
                Player loser = getLoser(players);
                loser.amount--;
                pot++;
                if (loser.amount <= 0) {
                    current = next(players, loser);
                    leader = next(players, loser);
                    players = removeLoser(players, loser);    

                }
                
                players = clearRoundResults(players);

                // ----- Out --------------------
               // out.println(getLoser(players).name);
                out.println("Round done, " + loser.name + " lost!");
                out.println("Next to roll is " + current.name);

                statusMsg(players);
            }
        }
        out.println("Game Over, winner is " + players[0].name + ". Will get " + pot + " from pot");
    }


    // ---- Game logic methods --------------

    // TODO implement and test methods (one at the time)


    int indexOf(Player[] players, Player player) {         
        for (int i = 0; i < players.length; i++) {
            if (players[i] == player) {
                return i;
            }
        }
        return -1;                                          
    }

    Player next(Player[] players, Player player) {
        int current = indexOf(players, player);
        if (current == players.length - 1) {                
            return players[0];
        } else {
            return players[current + 1];
        }
    }

    Player getRandomPlayer(Player[] players) {
        return players[rand.nextInt(players.length)];
    }


    int getScore(Player player) {
        int score;
        if(player.fstDice > player.secDice) {
            score = player.fstDice * 10 + player.secDice;
        } else if(player.fstDice == player.secDice) {
            score = (player.fstDice * 10 + player.secDice) * 10;
        } else {
            score = player.secDice * 10 + player.fstDice;
        }
        if (score == 21) {
            return mexico;
        } else {
            return score;
        }
    }

    Player getLoser (Player[] players) {
        Player loserPlayer = players[0];
        for (int i = 0; i < players.length; i++) {
            if (getScore(loserPlayer) > getScore(players[i])) {
                loserPlayer = players[i];
            }
        }
        return loserPlayer;
    }

    Player[] removeLoser (Player[] players, Player loser) {
        Player[] left = new Player[players.length - 1];
        int j = 0;                                                  
            for (int i = 0; i < players.length; i++){
                   if (players[i] != loser) {                        
                       left[j] = players[i];
                        j++;                        
           }
        }   return left;
    }

    Player[] clearRoundResults(Player[] players){    
        for (int i = 0; i < players.length; i++){
            players[i].nRolls = 0;
            players[i].fstDice = 0;
            players[i].secDice = 0;
        }
        return players;
    }

    Player rollDice (Player player) {
        player.fstDice = rand.nextInt(6) + 1;
        player.secDice = rand.nextInt(6)+ 1;
        player.nRolls++;
        return player;
    }

    boolean allRolled(Player[] players, Player leader){
        for (int i = 0; i < players.length; i++){
            if (players[i].nRolls == 0){                            
                return false;
            }
        }
        return true;
    }

    // ---------- IO methods (nothing to do here) -----------------------

    Player[] getPlayers() {
        Player[] players = new Player[3];
        Player p1 = new Player();
        p1.name = "Olle";
        p1.amount = startAmount;
        Player p2 = new Player();
        p2.name = "Fia";
        p2.amount = startAmount;
        Player p3 = new Player();
        p3.name = "Lisa";
        p3.amount = startAmount;
        players[0] = p1;
        players[1] = p2;
        players[2] = p3;
        return players;
    }

    void statusMsg(Player[] players) {
        out.print("Status: ");
        for (int i = 0; i < players.length; i++) {
            out.print(players[i].name + " " + players[i].amount + " ");
        }
        out.println();
    }

    void roundMsg(Player current) {
        out.println(current.name + " got " +
                current.fstDice + " and " + current.secDice);
    }

    String getPlayerChoice(Player player) {
        out.print("Player is " + player.name + " > ");
        return sc.nextLine();
    }


    String toString(Player p) {
        return p.name + ", " + p.amount + ", " + p.fstDice + ", "
                + p.secDice + ", " + p.nRolls;
    }

    // Class for a player
    class Player {
        String name;
        int amount;   // Start amount (money)
        int fstDice;  // Result of first dice
        int secDice;  // Result of second dice
        int nRolls;   // Current number of rolls
     }
    }
