# INPUTS

# Values
values = "10,3,4,7" # You can change these.
values = [int(v) for v in values.split(',')]

# Weights
weights = "2,5,1,3" # You can change these.
weights = [int(w) for w in weights.split(',')]

# Knapsack total capacity
capacity = 10


def fractional_knapsack(values, weights, capacity):
    # index = [0, 1, 2, ..., n - 1] for n items
    index = list(range(len(values)))
    
    # value/weight ratio
    ratio = [v / w for v, w in zip(values, weights)]
    
    # index sorted by descending value/weight ratio
    index.sort(key=lambda i: ratio[i], reverse=True)
    print(index)
    
    max_value = 0
    
    fractions = [0] * len(values)
    
    for i in index:
        if weights[i] <= capacity:
            fractions[i] = 1
            max_value += values[i]
            capacity -= weights[i]

        else:
            
            fractions[i] = capacity / weights[i]
            max_value += values[i] * capacity / weights[i]
            break

    return max_value, fractions

# FUNCTION CALL
max_value, fractions = fractional_knapsack(values, weights, capacity)

print('Total value that can be carried:', max_value)
print('Fractions by which to multiply the items:', fractions)
