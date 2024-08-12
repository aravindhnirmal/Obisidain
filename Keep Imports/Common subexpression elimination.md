[[Keep/Colour/DEFAULT]] [[Keep/Attachments]] [[Keep/Archived]] 

# input expressions
t = "a + b*c"
y = "d + b*c"

# split expressions into tokens
t_tokens = t.split()
y_tokens = y.split()

# find common subexpression
common_subexpr = ""
for i in range(len(t_tokens)):
    if t_tokens[i] == y_tokens[i]:
        common_subexpr += t_tokens[i] + " "
    else:
        break

# remove common subexpression from both expressions
t = t.replace(common_subexpr, "")
y = y.replace(common_subexpr, "")

# generate new expressions with common subexpression factored out
new_t = common_subexpr.strip() + " + " + t
new_y = common_subexpr.strip() + " + " + y

# print the original expressions and the new expressions
print("Original expressions:")
print("t = " + t_tokens[0] + " = " + t)
print("y = " + y_tokens[0] + " = " + y)

print("\nAfter common subexpression elimination:")
print("t = " + new_t)
print("y = " + new_y)



![[187d764dc61.b33d57ea64c20082.jpg]]