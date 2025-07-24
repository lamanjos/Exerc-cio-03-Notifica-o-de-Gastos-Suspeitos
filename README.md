import random

def activityNotifications(expenditure, d):
    def find_median(count, d):
        cumul = 0
        if d % 2 == 1:
            mid = d // 2 + 1
            for i in range(201):
                cumul += count[i]
                if cumul >= mid:
                    return i
        else:
            mid1, mid2 = d // 2, d // 2 + 1
            m1 = None
            for i in range(201):
                cumul += count[i]
                if m1 is None and cumul >= mid1:
                    m1 = i
                if cumul >= mid2:
                    m2 = i
                    return (m1 + m2) / 2

    notifications = 0
    count = [0] * 201  # frequência de valores de 0 a 200

    # Preenche o histograma com os primeiros d dias
    for i in range(d):
        count[expenditure[i]] += 1

    for i in range(d, len(expenditure)):
        mediana = find_median(count, d)
        if expenditure[i] >= 2 * mediana:
            notifications += 1
        # Atualiza o histograma para próxima janela
        count[expenditure[i - d]] -= 1
        count[expenditure[i]] += 1

    return notifications

def gerar_dados(n, max_val=200):
    return [random.randint(0, max_val) for _ in range(n)]

def main():
    n, d = map(int, input("Digite o número total de dias e o número de dias anteriores (separados por espaço): ").split())
    gastos = gerar_dados(n)
    print(f"n = {n}, d = {d}")
    print("Gastos:", gastos)
    resultado = activityNotifications(gastos, d)
    print("Notificações:", resultado)

if __name__ == '__main__':
    main()
