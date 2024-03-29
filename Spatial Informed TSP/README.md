# Spatially Informed TSP
## Introduction
This directory contains example of how to use 'Spatially Informed TSP' library.

### What is TSP ?
To learn more, refer to the information from [Wikipedia](https://en.wikipedia.org/wiki/Travelling_salesman_problem).
or refer to the [documentation](https://github.com/whkim15/Geog510-wkim15_2/pulls) 

<img src="https://co-enzyme.fr/wp-content/uploads/2020/06/tsp.jpg" width="300" />

### Contents
Here is a list of features that are demonstrated in the examples:
- Frist step : Standard TSP
- Second step : Spatially Informed TSP(I will upload it soon)


## Make LP file for solving in the Cplex by using Python
```python
#### First Step : Standard TSP
import pulp
###1_Distance Matrix of 25x25 TSP 
distance_matrix = [
[0.0, 24.21, 9.9, 4.47, 19.42, 10.82, 11.7, 18.44, 4.12, 17.09, 12.04, 13.6, 22.67, 12.0, 6.4, 8.0, 7.28, 14.14, 5.39, 20.12, 21.47, 16.12, 15.13, 17.03, 16.28],
[24.21, 0.0, 25.06, 19.85, 19.0, 35.0, 13.6, 7.07, 26.17, 21.21, 12.21, 23.09, 4.47, 33.02, 18.03, 20.25, 27.8, 17.72, 22.02, 24.02, 5.0, 27.02, 13.6, 18.11, 8.06],
[9.9, 25.06, 0.0, 9.49, 12.37, 16.03, 11.7, 21.59, 6.71, 9.06, 15.13, 22.83, 25.3, 8.6, 12.37, 16.55, 5.0, 8.6, 5.39, 11.18, 20.81, 25.81, 12.04, 24.74, 18.68],
[4.47, 19.85, 9.49, 0.0, 16.16, 15.26, 7.28, 14.42, 6.71, 14.42, 7.81, 13.6, 18.6, 14.56, 3.0, 7.21, 9.22, 10.77, 4.12, 17.8, 17.0, 16.97, 11.0, 15.3, 12.04],
[19.42, 19.0, 12.37, 16.16, 0.0, 28.07, 11.31, 19.31, 18.0, 3.61, 15.62, 28.6, 21.38, 20.62, 17.49, 22.47, 17.26, 5.39, 14.14, 5.1, 14.0, 32.45, 7.21, 27.66, 16.55],
[10.82, 35.0, 16.03, 15.26, 28.07, 0.0, 22.36, 29.0, 10.2, 25.0, 22.8, 19.65, 33.24, 10.82, 17.03, 16.64, 11.05, 23.35, 14.56, 27.17, 32.25, 20.02, 25.3, 25.08, 27.02],
[11.7, 13.6, 11.7, 7.28, 11.31, 22.36, 0.0, 10.05, 12.81, 11.18, 4.47, 17.49, 13.6, 19.42, 7.07, 11.7, 14.21, 6.71, 8.49, 14.76, 10.0, 21.47, 4.47, 16.4, 7.07],
[18.44, 7.07, 21.59, 14.42, 19.31, 29.0, 10.05, 0.0, 21.1, 20.4, 6.71, 16.03, 4.24, 28.64, 12.04, 13.42, 23.26, 16.12, 17.46, 23.77, 8.06, 20.0, 12.37, 11.4, 3.0],
[4.12, 26.17, 6.71, 6.71, 18.0, 10.2, 12.81, 21.1, 0.0, 15.13, 14.42, 17.72, 25.24, 8.06, 9.49, 12.04, 3.16, 13.15, 4.47, 17.72, 22.8, 20.12, 15.23, 21.0, 18.6],
[17.09, 21.21, 9.06, 14.42, 3.61, 25.0, 11.18, 20.4, 15.13, 0.0, 15.65, 27.59, 23.02, 17.09, 16.28, 21.26, 14.04, 4.47, 11.7, 3.61, 16.28, 31.24, 8.06, 27.46, 17.46],
[12.04, 12.21, 15.13, 7.81, 15.62, 22.8, 4.47, 6.71, 14.42, 15.65, 0.0, 13.93, 10.82, 21.93, 5.83, 9.0, 16.55, 11.18, 10.77, 19.24, 10.2, 18.03, 8.49, 12.04, 4.24],
[13.6, 23.09, 22.83, 13.6, 28.6, 19.65, 17.49, 16.03, 17.72, 27.59, 13.93, 0.0, 19.42, 25.32, 11.31, 6.4, 20.88, 23.43, 17.49, 31.11, 23.19, 4.12, 21.95, 6.4, 16.12],
[22.67, 4.47, 25.3, 18.6, 21.38, 33.24, 13.6, 4.24, 25.24, 23.02, 10.82, 19.42, 0.0, 32.65, 16.28, 17.49, 27.29, 19.03, 21.47, 26.17, 8.06, 23.19, 15.0, 14.0, 6.71],
[12.0, 33.02, 8.6, 14.56, 20.62, 10.82, 19.42, 28.64, 8.06, 17.09, 21.93, 25.32, 32.65, 0.0, 17.46, 20.0, 5.39, 17.2, 11.18, 18.25, 29.07, 27.2, 20.52, 29.02, 25.94],
[6.4, 18.03, 12.37, 3.0, 17.49, 17.03, 7.07, 12.04, 9.49, 16.28, 5.83, 11.31, 16.28, 17.46, 0.0, 5.0, 12.17, 12.21, 7.07, 19.8, 15.81, 15.0, 11.4, 12.37, 10.0],
[8.0, 20.25, 16.55, 7.21, 22.47, 16.64, 11.7, 13.42, 12.04, 21.26, 9.0, 6.4, 17.49, 20.0, 5.0, 0.0, 15.13, 17.2, 11.18, 24.76, 19.1, 10.0, 16.16, 9.06, 12.37],
[7.28, 27.8, 5.0, 9.22, 17.26, 11.05, 14.21, 23.26, 3.16, 14.04, 16.55, 20.88, 27.29, 5.39, 12.17, 15.13, 0.0, 13.0, 5.83, 16.12, 24.04, 23.26, 15.81, 24.02, 20.59],
[14.14, 17.72, 8.6, 10.77, 5.39, 23.35, 6.71, 16.12, 13.15, 4.47, 11.18, 23.43, 19.03, 17.2, 12.21, 17.2, 13.0, 0.0, 9.0, 8.06, 13.0, 27.2, 4.12, 23.02, 13.15],
[5.39, 22.02, 5.39, 4.12, 14.14, 14.56, 8.49, 17.46, 4.47, 11.7, 10.77, 17.49, 21.47, 11.18, 7.07, 11.18, 5.83, 9.0, 0.0, 14.76, 18.44, 20.62, 10.77, 19.42, 14.76],
[20.12, 24.02, 11.18, 17.8, 5.1, 27.17, 14.76, 23.77, 17.72, 3.61, 19.24, 31.11, 26.17, 18.25, 19.8, 24.76, 16.12, 8.06, 14.76, 0.0, 19.03, 34.71, 11.4, 31.06, 20.88],
[21.47, 5.0, 20.81, 17.0, 14.0, 32.25, 10.0, 8.06, 22.8, 16.28, 10.2, 23.19, 8.06, 29.07, 15.81, 19.1, 24.04, 13.0, 18.44, 19.03, 0.0, 27.29, 8.94, 19.31, 7.07],
[16.12, 27.02, 25.81, 16.97, 32.45, 20.02, 21.47, 20.0, 20.12, 31.24, 18.03, 4.12, 23.19, 27.2, 15.0, 10.0, 23.26, 27.2, 20.62, 34.71, 27.29, 0.0, 25.94, 9.49, 20.22],
[15.13, 13.6, 12.04, 11.0, 7.21, 25.3, 4.47, 12.37, 15.23, 8.06, 8.49, 21.95, 15.0, 20.52, 11.4, 16.16, 15.81, 4.12, 10.77, 11.4, 8.94, 25.94, 0.0, 20.52, 9.49],
[17.03, 18.11, 24.74, 15.3, 27.66, 25.08, 16.4, 11.4, 21.0, 27.46, 12.04, 6.4, 14.0, 29.02, 12.37, 9.06, 24.02, 23.02, 19.42, 31.06, 19.31, 9.49, 20.52, 0.0, 12.53],
[16.28, 8.06, 18.68, 12.04, 16.55, 27.02, 7.07, 3.0, 18.6, 17.46, 4.24, 16.12, 6.71, 25.94, 10.0, 12.37, 20.59, 13.15, 14.76, 20.88, 7.07, 20.22, 9.49, 12.53, 0.0]
]

### 2_Objective function
objective_function = "Minimize\nobj: "

variables = [
    (i, j, distance_matrix[i][j])
    for i in range(len(distance_matrix))
    for j in range(len(distance_matrix[i]))
    if i != j
]

variables.sort(key=lambda x: (x[0], x[1]))

variables_str = " + ".join([f"{coef} X_{i+1}_{j+1}" for i, j, coef in variables])   
#variables_str = " + ".join([f"{coef:.3f} X_{i+1}_{j+1}" for i, j, coef in variables])  # coef:.3f - 소수 셋째자리까지
objective_function += variables_str
print(objective_function)


# Make Constraints for 25x25 TSP 
def create_constraints_for_25x25_TSP():
    constraints = []
    # Entered City must be one
    for i in range(1, 26):
        constraints.append(f"Con_{i}: " + " + ".join(f"X_{i}_{j}" for j in range(1, 26) if j != i) + " = 1")
    # Entered Road must be one
    for j in range(1, 26):
        constraints.append(f"Con_{25 + j}: " + " + ".join(f"X_{i}_{j}" for i in range(1, 26) if i != j) + " = 1")

    return constraints

# Add Text
constraints_list = create_constraints_for_25x25_TSP()
constraints_text = "\n".join(constraints_list)
print(constraints_text)

###3_ # MTZ Constraints for 25x25 TSP 
def create_MTZ_constraints(n=25):
    MTZ_constraints = []
    big_M = n + 1  # 일반적으로 큰 M 값은 도시의 수보다 큰 값을 사용.

    # U_i - U_j + n * X_ij <= n-1 for all 1 <= i != j <= n
    # 여기서 U_i는 도시 i의 순서를 나타내는 변수.
    for i in range(2, n + 1):
        for j in range(2, n + 1):
            if i != j and i != 1:  # U_1과 관련된 제약 조건을 제외.
                MTZ_constraints.append(f"MTZ_{i}_{j}: U_{i} - U_{j} + {n} X_{i}_{j} <= {n - 1}")

    # 1 <= U_i <= n for all 2 <= i <= n-1
    for i in range(2, n + 1):
        MTZ_constraints.append(f"1 <= U_{i} <= {n-1}")

    return MTZ_constraints

# MTZ Constraints Export
mtz_constraints = create_MTZ_constraints()
for constraint in mtz_constraints:
    print(constraint)
    
    
###4_ # 이진 변수와 일반 정수 변수를 지정된 형식에 맞추어 출력하는 함수
def print_variable_types_in_lp_format(n=25):
    # 이진 변수 줄력
    print("Binaries")
    for i in range(1, n + 1):
        binary_vars_line = " ".join(f"X_{i}_{j}" for j in range(1, n + 1) if i != j)
        print(binary_vars_line)
    
    # 일반 정수 변수 출력
    print("\nGenerals")
    general_vars_line = " ".join(f"U_{i}" for i in range(2, n + 1))
    print(general_vars_line)

# 함수 호출
print_variable_types_in_lp_format()



```


## Demos


