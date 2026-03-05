# BlackJack-python
import random

while True:
    suits = ["Hearts", "Diamonds", "Clubs", "Spades"]
    ranks = [2, 3, 4, 5, 6, 7, 8, 9, 10, "Jack", "Queen", "King", "Ace"]

    deck = []
    for suit in suits:
        for rank in ranks:
            card = {"rank": rank, "suit": suit}
            deck.append(card)

    random.shuffle(deck)

    def deal_card(deck):
        return deck.pop(0)

    def hand_value(hand):
        total = 0
        for card in hand:
            rank = card["rank"]
            if rank == "Jack" or rank == "Queen" or rank == "King":
                total = total + 10
            elif rank == "Ace":
                total = total + 11
            else:
                total = total + rank
        return total

    player_hand = []
    dealer_hand = []

    player_hand.append(deal_card(deck))
    player_hand.append(deal_card(deck))
    dealer_hand.append(deal_card(deck))
    dealer_hand.append(deal_card(deck))

    print("Your hand:", player_hand)
    print("Dealer hand:", dealer_hand)
    print("Your total:", hand_value(player_hand))
    print("Dealer total:", hand_value(dealer_hand))

    player_bust = False

    while True:
        choice = input("Do you want to hit or stand? (h/s): ")
        if choice == "h":
            player_hand.append(deal_card(deck))
            print("Your hand:", player_hand)
            print("Your total:", hand_value(player_hand))
            if hand_value(player_hand) > 21:
                print("Bust! You lose!")
                player_bust = True
                break
        elif choice == "s":
            print("You stand!")
            break

    if not player_bust:
        print("\nDealer's turn!")
        while hand_value(dealer_hand) < 17:
            dealer_hand.append(deal_card(deck))
            print("Dealer hits!")
            print("Dealer hand:", dealer_hand)
            print("Dealer total:", hand_value(dealer_hand))

        if hand_value(dealer_hand) > 21:
            print("Dealer busts! You win!")
        elif hand_value(dealer_hand) >= hand_value(player_hand):
            print("Dealer wins!")
        else:
            print("You win!")

    play_again = input("\nPlay again? (y/n): ")
    if play_again == "n":
        print("Thanks for playing!")
        break
