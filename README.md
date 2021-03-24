# xo
def show_field(field):

    print(*[' ', 0, 1, 2], '', sep=' | ')
    for i,row in enumerate(field):
        print([0, 1, 2][i], *row, '', sep=' | ')

def verification_input(data_input):
    if len(data_input) != 2:
        return False
    for n in data_input:
        if n not in ['0', '1', '2']:
            return False
    return True

def get_coordinates(chair, field):
    while True:
        data_input = input(f'Первыми ходят {chair}, введите номер строки и столбца через пробел:')
        data_input = data_input.split()
        if verification_input(data_input):
            data_input = list(map(int, data_input))
            if field[data_input[0]][data_input[1]] == ' ':
                return data_input
            else:
                print("Клетка занята!)")
        else:
            print('Не верный ввод, попробуйте снова ввести числа от 0 до 2 включительно. Ввод через пробел')

def check_win(field):
    new_field = [n for row in field for n in row] # Проверка игрового поля в виде одномерного массива
    win_coordinates = ((0,1,2),(3,4,5),(6,7,8),(0,3,6),(1,4,7),(2,5,8),(0,4,8),(2,4,6)) # выигрышные координаты
    for win_coordinate in win_coordinates:
        if new_field[win_coordinate[0]] == new_field[win_coordinate[1]] == new_field[win_coordinate[2]] != ' ':
            return True

def main():
    name_game = '**** Кресты - нули ****'
    rules_game = "\nВ поле 3х3 предлогается ввести координаты своего хода (строка и столбец)." \
                 "\nВвод двух чисел от 0 до 2, через пробел"
    print('\n', name_game, rules_game)
    chars = [['X', 'Кресты'], ['0', "Нули"]]
    while True:
        field = [[' ' for i in range(3)] for j in range(3)]
        show_field(field)
        for step in range(9):
            player = step % 2
            coordinates = get_coordinates(chars[player][1], field)
            field[coordinates[0]][coordinates[1]] = chars[player][0]
            show_field(field)
            if check_win(field):
                print(f'Победили {chars[player][1]}!\n')
                break
        else:
            print("ничья!\n")

if __name__ == "__main__":
    main()
