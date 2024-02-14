# Importing necessay Libraries
from pulp import LpProblem, LpMaximize, LpVariable

# Create a LP minimization problem
model = LpProblem(name="Production_planning", sense=LpMaximize)

#Define Decision Variables
x1 = LpVariable('x1', lowBound=0) # Quantity of Product A
x2 = LpVariable('x2', lowBound=0) # Quantity of Product B

# Define the objective function
model += 4 * x1 + 2 * x2, "Objective"

# Define inequalities as constraints
model += 2 * x1 + 3 * x2 <= 60, "Labour_Resource_Constraint"
model += 4 * x1 + 2 * x2 <= 80, "Raw_Material_Resource_constraint"

# Solve the linear programming problem
model.solve()

# Display the results
print("Optimal Solution:")
print(f"Quantity of Product A x1:", pulp.value(x1))
print(f"Quantity of Product A x2:", pulp.value(x2))
print(f"Maximum Profit (Z): {model.objective.value()}")
