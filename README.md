# Exerc-cio-03-Notifica-o-de-Gastos-Suspeitos
def calcular_mediana(contagem, d):
    soma = 0
    if d % 2 == 1: 
        mediana_pos = d // 2 + 1
        for i in range(len(contagem)):
            soma += contagem[i]
            if soma >= mediana_pos:
                return i
    else:  
        primeira_pos = d // 2
        segunda_pos = primeira_pos + 1
        m1 = None
        m2 = None
        for i in range(len(contagem)):
            soma += contagem[i]
            if m1 is None and soma >= primeira_pos:
                m1 = i
            if soma >= segunda_pos:
                m2 = i
                break
        return (m1 + m2) / 2

def activityNotifications(expenditure, d):
    notificacoes = 0
    contagem = [0] * 201  

    for i in range(d):
        contagem[expenditure[i]] += 1

    for i in range(d, len(expenditure)):
        mediana = calcular_mediana(contagem, d)

        if expenditure[i] >= 2 * mediana:
            notificacoes += 1

        contagem[expenditure[i - d]] -= 1
        contagem[expenditure[i]] += 1

    return notificacoes

def main():
    
    entrada = input().strip().split()
    n, d = int(entrada[0]), int(entrada[1])
    gastos = list(map(int, input().strip().split()))
    
    resultado = activityNotifications(gastos, d)
    
    print(resultado)

if __name__ == '__main__':
    main()

