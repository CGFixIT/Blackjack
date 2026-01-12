<!--
<hr>
#This is Blackjack, written in C++. Includes:<bR>
-User accounts (Includes tally of winnings and player rankings)<bR>
-Leaderboard<bR>
-Basic dealer AI (very basic lol but met criteria for project) / Level of difficulty <bR>
-Lots of other stuff that I will add<bR>
<hr>-->
### Casino Blackjack aka 21 (C++)

Fun old-school CMD console Blackjack game written in C++ as a school projects from many moons ago..

---

Single-player or multiplayer (up to 7 players), persistent accounts, basic dealer “AI”, and a simple leaderboard driven by a flat-file “database”.

> This is a **legacy / educational** project – not production-grade casino software. It’s here as a snapshot of where my C++ journey started.

---

<a href="https://github.com/lostSail0r/Blackjack/blob/master/Blackjack/Blackjack/main.cpp">Main Code:</a>

---

<a href="https://youtu.be/SngIHvvYaFI">Youtube Demo of Game</a>

---

## What You Get

- **Blackjack game loop**
  - Hit / Stand
  - Double Down (when initial total is 9, 10, or 11)
  - Insurance side bets when dealer shows an Ace
- **1–7 players (local hotseat)**
  - Solo: you vs dealer  
  - Multi: multiple human players taking turns at the same console
- **Persistent user accounts**
  - Simple `User` class: `name`, `email`, `username`, `pw`, `earnings`, `rank`
  - Accounts stored in `userDB.txt` between runs
- **Dealer difficulty levels**
  - **Beginner** – dealer stands on soft 17
  - **Expert** – dealer hits on soft 17 and uses basic Ace-adjustment logic
- **Leaderboard**
  - Players ranked by total lifetime earnings
  - Custom selection sort over the `User` array

---

## Game Rules & Payouts

The project follows standard, simplified Blackjack rules:

- **Card values**
  - Number cards: face value
  - J, Q, K: 10 points
  - A: 1 or 11 points (player chooses; dealer logic adjusts)
- **Blackjack**
  - Natural blackjack pays **3:2** (150% of your bet in profit)
- **Standard outcomes**
  - Win: you beat dealer without busting ⇒ you win an amount equal to your bet
  - Push: same total as dealer ⇒ your bet is returned
  - Loss: you bust or dealer is closer to 21 ⇒ you lose your bet
- **Insurance**
  - Offered if dealer’s face-up card is an Ace
  - You can bet up to half your original bet that the dealer has blackjack
  - Insurance pays **2:1** if the dealer *does* have blackjack

All players start each session with an initial bankroll of **$50**, and that bankroll is tracked per account across runs.

---

## Project Layout

The repo is intentionally small:

- `Blackjack/Blackjack/main.cpp`  
  Core of the program:
  - User auth / signup (`userSignIn`)
  - Game loop (`playFirstHand`)
  - Betting, insurance, and double-down logic
  - Dealer AI (`hitUntilStandAI`, `checkSoftOrHardAI`)
  - Hand evaluation (`CardValue`, `getHandValue`)
  - Leaderboard and ranking (`determineRank`, `selectionSort`, `displayResults`)
  - File I/O for user accounts (`loadAccounts`, `updateDB`, `updateEarnings`)

- `Blackjack/Blackjack/User.h`  
  Simple `User` class with public fields:
  - `string name`
  - `string email`
  - `string username`
  - `string pw`
  - `double earnings`
  - `int rank`

- `userDB.txt` (created/updated at runtime)  
  - Flat-file “database” containing:
    - Number of users
    - One block per user: name, email, username, password, earnings, rank

---

## Tech Stack & Constraints

- **Language**: C++ (written against a 2016-era toolchain)
- **Standard library**:
  - `<iostream>`, `<iomanip>`, `<string>`, `<fstream>`
  - `<algorithm>` (uses `random_shuffle` in this repo version)
  - `<cstdlib>`, `<ctime>`, `<limits>`
- **OS assumptions**: Windows
  - Uses `system("cls")` to clear the console
  - Uses `system("pause")` for “press any key to continue”
  - On Linux/macOS you’ll either need to stub these out or replace them

### V2 Updates / Shuffling

The version in this repo uses:

```cpp
void shuffle(int deck[], int size) {
    srand(time(0));
    int xRan = rand() % 50 + 5;
    random_shuffle(deck, deck + 51);
}
^no it doesnt lol fix with snippet from uncommented lines below soon

