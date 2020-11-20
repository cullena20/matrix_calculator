# used to print integers without .0 after
def format_number(x):
    if x % 1 != 0:
        pass
    else:
        x = int(x)
    return x


def get_matrix(index):
    while True:
        try:
            row, col = map(int, input(f"Enter size of{index} matrix: ").strip().split(' '))
            while True:
                print('Enter matrix:')
                matrix = [[format_number(float(x)) for x in input().strip().split(' ')] for _ in range(row)]
                check_col = [len(matrix[x]) for x in range(len(matrix))]
                # is this the best way to check length?
                for x in range(len(matrix)):
                    if len(matrix[x]) != col:
                        check_col = False
                    else:
                        pass
                if len(matrix) != row or check_col is False:
                    print("Please enter a matrix with the same dimensions as you entered.")
                    matrix.clear()
                    continue
                else:
                    break
            return row, col, matrix
        except ValueError:
            print("Please enter a valid size (rows, columns).")


def print_matrix(matrix):
    print("The result is:")
    for row in matrix:
        print(*row)
    print()


def empty_matrix(row, col):
    matrix = [[0 for _ in range(col)] for _ in range(row)]
    return matrix


def add_matrices():
    row1, col1, matrix1 = get_matrix(' first')
    row2, col2, matrix2 = get_matrix(' second')
    if row1 == row2 and col1 == col2:
        result = [[a + b for a, b in zip(j, l)] for j, l in zip(matrix1, matrix2)]
        print_matrix(result)
    else:
        print("The operation cannot be performed.\n")


def multiply_scalar():
    row, col, matrix = get_matrix('')
    scalar = format_number(float(input("Enter constant: ")))
    result = [[scalar * a for a in i] for i in matrix]
    print_matrix(result)


def multiply_matrices():
    row1, col1, matrix1 = get_matrix(' first')
    row2, col2, matrix2 = get_matrix(' second')
    if col1 == row2:
        result = empty_matrix(row1, col2)
        for i in range(len(matrix1)):
            # iterates through rows of matrix1
            for j in range(len(matrix2[0])):
                # iterates through columns of matrix2
                for k in range(len(matrix2)):
                    # iterates through rows of matrix2
                    result[i][j] += matrix1[i][k] * matrix2[k][j]
        print_matrix(result)
    else:
        print("The operation cannot be performed.\n")


# this doesn't account for error if matrix can't be transposed
# dig into this
def transpose_matrix():
    while True:
        print("\n1. Main diagonal\n2. Side diagonal\n3. Vertical line\n4. Horizontal line")
        u_choice = input("Your choice: ")
        row, col, matrix = get_matrix('')
        if u_choice == "1":
            result = [[j for j in i] for i in zip(*matrix)]
            print_matrix(result)
            break
        elif u_choice == "2":
            result = [[j for j in i] for i in zip(*matrix[::-1])][::-1]
            print_matrix(result)
            break
        elif u_choice == "3":
            result = [i[::-1] for i in matrix]
            print_matrix(result)
            break
        elif u_choice == "4":
            result = matrix[::-1]
            print_matrix(result)
            break
        else:
            print("Sorry, I did not understand that.")
            continue


# could this be generalized to be called in inverse function too
def get_cofactor(matrix, count):
    new_matrix = list()
    for i in range(1, len(matrix[1:]) + 1):
        new_row = matrix[i][:count] + matrix[i][count+1:]
        new_matrix.append(new_row)
    return new_matrix


def determinant(matrix):
    if len(matrix) == 1:
        return matrix[0][0]
    if len(matrix) == 2:
        return matrix[0][0] * matrix[1][1] - matrix[0][1] * matrix[1][0]
    sum_cofactors = 0
    for column in range(len(matrix[0])):
        sign = (-1) ** (column + 2)
        sub_determinant = (determinant(get_cofactor(matrix, column)))
        sum_cofactors += (sign * matrix[0][column] * sub_determinant)
    return sum_cofactors


def inverse():
    row, col, matrix = get_matrix('')
    if row == col:
        cofactor_matrix = empty_matrix(row, col)
        for i in range(len(matrix)):
            for k in range(len(matrix[i])):
                mini_matrix = [row[:k] + row[k+1:] for row in matrix[:i] + matrix[i+1:]]
                cofactor_matrix[i][k] = determinant(mini_matrix)
                # matrix of minors
                if (i % 2 == 0 and k % 2 == 1) or (i % 2 == 1 and k % 2 == 0):
                    cofactor_matrix[i][k] *= -1
                # matrix of cofactors
        cofactor_matrix = [[j for j in i] for i in zip(*cofactor_matrix)]
        # transpose over diagonal (u_choice 1 in transpose function)
        try:
            scalar = (1 / determinant(matrix))
            inverse_matrix = [[format_number(round(scalar * a, 2)) for a in i] for i in cofactor_matrix]
            # multiply by 1 / determinant
            print_matrix(inverse_matrix)
        except ZeroDivisionError:
            print("This matrix doesn't have an inverse.\n")


def main():
    while True:
        print("1. Add matrices\n2. Multiply matrix by a constant\n3. Multiply matrices\n4. Transpose matrix\n5. Calculate a determinant\n6. Inverse matrix\n0. Exit")
        u_choice = input("Your choice: ")
        if u_choice == "1":
            add_matrices()
        elif u_choice == "2":
            multiply_scalar()
        elif u_choice == "3":
            multiply_matrices()
            continue
        elif u_choice == "4":
            transpose_matrix()
            continue
        elif u_choice == "5":
            while True:
                row, col, matrix = get_matrix('')
                if row == col:
                    print(determinant(matrix))
                    print()
                    break
                else:
                    print("Must be a square matrix.\n")
                    continue
        elif u_choice == "6":
            inverse()
        elif u_choice == "0":
            break
        else:
            print("Sorry, I did not understand that.\n")
            continue


if __name__ == "__main__":
    main()
