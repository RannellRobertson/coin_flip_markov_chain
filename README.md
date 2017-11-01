import numpy as np
import random as rm
import time

# Define the statespace

states = ["Heads","Tails"]

# Possible sequences of events

transition_Name = [["HH","HT"],["TT","TH"]]

# Probabilities matrix (Transition Matrix)

transition_Matrix = [[0.5,0.5],[0.2,0.8]]

# Check that probabilities add to 2. If not raise ValueError

if sum(transition_Matrix[0]) + sum(transition_Matrix[1]) != 2:
    print ("Error: Probabilities must add to 1. Please check transition matrix.")
    raise ValueError("Probabilities must add to 1")

# A function which implements the Markov chain model to predict the outcome of a coin toss

def coin_toss(coin_flips):
    # Picking a random state
    coin_side = rm.choice(states)
    i = 0
    print ("Coin facing: ", coin_side)
    while i < coin_flips:
        if coin_side == "Heads":
            # numpy.random.choice(a, size=None, replace=True, p=None)
            flip = np.random.choice(transition_Name[0], replace=True, p=transition_Matrix[0])
            if flip == "HH":
                pass
            else:
                coin_side = "Tails"
        elif coin_side == "Tails":
            flip = np.random.choice(transition_Name[1], replace=True, p=transition_Matrix[1])
            if flip == "TT":
                pass
            else:
                coin_side = "Heads"
        print (coin_side)
        i += 1
        time.sleep(0.2)

# Number of coin flips

coin_toss(100)
