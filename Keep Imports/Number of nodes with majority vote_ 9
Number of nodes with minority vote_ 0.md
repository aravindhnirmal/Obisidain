[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

# Initialize the counters
num_nodes_majority = 0
num_nodes_minority = 0

# Loop through all the nodes in the tree and find the majority and minority votes
for node_num in range(tree.tree_.node_count):
    # Get the class counts for the current node
    class_counts = tree.tree_.value[node_num][0]
    # Find the majority and minority class based on the class counts
    majority_class = class_counts.argmax()
    minority_class = class_counts.argmin()
    # Check if the majority and minority classes are different
    if majority_class != minority_class:
        # Count the node as either having majority or minority vote
        if class_counts[majority_class] > class_counts[minority_class]:
            num_nodes_majority += 1
        else:
            num_nodes_minority += 1

# Print the results
print(f"Number of nodes with majority vote: {num_nodes_majority}")
print(f"Number of nodes with minority vote: {num_nodes_minority}")
