# CODIGOS-PYTHON
import math

class calculadora:
    
    def __init__(self):
        self.resultado = 0.0

    def reiniciar(self):
        self.resultado = 0.0
        print("calculadora inicializada nuevamente en 0")

    def mos_valor(self):
        return self.resultado
    
    # operaciones basicas
    def sumar(self, numero):
        self.resultado += numero
    
    def restar(self, numero):
        self.resultado -= numero
    
    def multiplicacion(self, numero):
        self.resultado *= numero
    
    def division(self, numero):
        if numero != 0:
            self.resultado /= numero
        else:
            print("no se puede dividir entre 0")

    # operaciones trigonometricas
    def seno(self, angulo):
        self.resultado = math.sin(math.radians(angulo))
    
    def coseno(self, angulo):
        self.resultado = math.cos(math.radians(angulo))
    
    def tangente(self, angulo):
        self.resultado = math.tan(math.radians(angulo))

    # operaciones avanzadas
    def raiz_n(self, n):
        if n == 0:
            raise ValueError("no existe raiz 0")
        if self.resultado < 0 and n % 2 == 0:
            raise ValueError("resultado imaginario")
        if self.resultado < 0:
            self.resultado = -(-self.resultado) ** (1 / n)
        else:
            self.resultado = self.resultado ** (1 / n)

    # potencia enesima
    def potenci_n(self, n):
        try:
            valor = self.resultado ** n
            if isinstance(valor, complex):
                raise ValueError("resultado imaginario")
            self.resultado = valor
        except OverflowError:
            raise ValueError("Math Error")

    def factorial(self):
        if self.resultado < 0 or not self.resultado.is_integer():
            raise ValueError("factorial solo esta definido para enteros no negativos")
        self.resultado = math.factorial(int(self.resultado))

    # serie fibonacci
    def fibonacci(self, n):
        if n < 0:
            raise ValueError("fibonacci solo esta definido para enteros no negativos")
        if n == 0:
            self.resultado = 1
            return
        a, b = 0, 1
        for _ in range(2, int(n) + 1):
            a, b = b, a + b
        self.resultado = float(b)

    # mcm
    def mcm(self, diferente_numero):
        if not self.resultado.is_integer() or not float(diferente_numero).is_integer():
            raise ValueError("mcm solo acepta numeros enteros")
        a = int(self.resultado)
        b = int(diferente_numero)
        if a == 0 or b == 0:
            self.resultado = 0
        else:
            mcm_val = math.gcd(a, b)
            self.resultado = abs(a * b) // mcm_val

    # mcd
    def mcd(self, diferente_numero):
        if not self.resultado.is_integer() or not float(diferente_numero).is_integer():
            raise ValueError("mcd solo acepta numeros enteros")
        a = int(self.resultado)
        b = int(diferente_numero)
        self.resultado = math.gcd(a, b)

    # calcular iva
    def calc_iva(self, porcentaje):
        if porcentaje < 0:
            raise ValueError("el porcentaje no puede ser negativo")
        self.resultado += self.resultado * (porcentaje / 100)

    def obtener_valor(self, promt="Ingrese un numero entero"):
        while True:
            try:
                return float(input(promt))
            except ValueError:
                print("entrada no valida, por favor ingrese un numero entero")

    def obtener_entero(self, promt="ingrese un numero entero"):
        while True:
            try:
                valor = float(input(promt))
                if valor.is_integer():
                    return int(valor)
                print("se necesita un numero entero")
            except ValueError:
                print("valor no valido")

    def menu(self):
        calc = calculadora()

        print("---Bienvenido al Menu---")
        # valor por defecto 0
        while True:
            print("MENÚ PRINCIPAL:")
            print("-" * 30)
            print("1. Operaciones Básicas (Varios números)")
            print("2. Funciones Trigonométricas (Sobre el acumulado)")
            print("3. Operaciones Avanzadas (Raíz, Potencia, Factorial, Fibonacci)")
            print("4. Utilidades (MCM, MCD, IVA)")
            print("5. Reiniciar Calculadora (A cero)")
            print("6. Ingresar un nuevo valor base manualmente")
            print("0. Salir")
            print("-" * 30)

            try:
                opcion = int(input("Elija una opcion: "))
            except ValueError:
                print("opcion no valida, intente nuevamente")
                continue

            if opcion == 0:
                print("!gracias por usar esta calculadora¡")
                break
            elif opcion == 1:
                while True:
                    print("Operaciones Básicas:")
                    print("1. Sumar")
                    print("2. Restar")
                    print("3. Multiplicar")
                    print("4. Dividir")
                    print("5. Volver al menú principal")

                    operacion = input("Elija una operación: ")
                    if operacion in ['1', '2', '3', '4']:
                        print("ingrese los numeros a operar, para terminar escribe 'fin' o '='")
                        while True:
                            numero = input("numero: ")
                            if numero in ['=', 'fin']:
                                break
                            try:
                                numero = float(numero)
                                if operacion == '1':
                                    calc.sumar(numero)
                                elif operacion == '2':
                                    calc.restar(numero)
                                elif operacion == '3':
                                    calc.multiplicacion(numero)
                                    print(f"parcial: {calc.mos_valor()}")
                                elif operacion == '4':
                                    calc.division(numero)
                            except ValueError:
                                print("entrada no valida, por favor ingrese un numero")
                        print(f"Resultado actual: {calc.mos_valor()}")
                    else:
                        print("opcion no valida, intente nuevamente")
            elif opcion == 2:
                while True:
                    print("Funciones Trigonométricas:")
                    print("1. Seno")
                    print("2. Coseno")
                    print("3. Tangente")
                    print("4. Volver al menú principal")

                    operacion = int(input("Elija una operación: "))
                    if operacion == 4:
                        break
                    elif operacion in [1, 2, 3]:
                        angulo = calc.obtener_valor("Ingrese un ángulo en grados: ")
                        if operacion == 1:
                            calc.seno(angulo)
                        elif operacion == 2:
                            calc.coseno(angulo)
                        elif operacion == 3:
                            try:
                                calc.tangente(angulo)
                            except ValueError:
                                print("Error: Resultado imaginario.")
                        print(f"Resultado actual: {calc.mos_valor()}")
                    else:
                        print("opcion no valida, intente nuevamente")
            elif opcion == 3:
                while True:
                    print("Operaciones Avanzadas:")
                    print("1. Raíz n-ésima")
                    print("2. Potencia n-ésima")
                    print("3. Factorial")
                    print("4. Fibonacci")
                    print("5. Volver al menú principal")

                    operacion = input("Elija una operación: ")
                    if operacion == '5':
                        break
                    elif operacion == '1':
                        n = calc.obtener_entero("Ingrese el valor de n para la raíz n-ésima: ")
                        try:
                            calc.raiz_n(n)
                        except ValueError as e:
                            print(f"Error: {e}")
                    elif operacion == '2':
                        n = calc.obtener_entero("Ingrese el valor de n para la potencia n-ésima: ")
                        try:
                            calc.potenci_n(n)
                        except ValueError as e:
                            print(f"Error: {e}")
                    elif operacion == '3':
                        try:
                            calc.factorial()
                        except ValueError as e:
                            print(f"Error: {e}")
                    elif operacion == '4':
                        n = calc.obtener_entero("Ingrese el valor de n para la serie Fibonacci: ")
                        try:
                            calc.fibonacci(n)
                        except ValueError as e:
                            print(f"Error: {e}")
                    else:
                        print("opcion no valida, intente nuevamente")
                    print(f"Resultado actual: {calc.mos_valor()}")
            elif opcion == 4:
                while True:
                    print("Utilidades:")
                    print("1. MCM")
                    print("2. MCD")
                    print("3. Calcular IVA")
                    print("4. Volver al menú principal")

                    operacion = input("Elija una operación: ")
                    if operacion == '4':
                        break
                    elif operacion in ['1', '2']:
                        numero = calc.obtener_entero("Ingrese un número entero: ")
                        try:
                            if operacion == '1':
                                calc.mcm(numero)
                            elif operacion == '2':
                                calc.mcd(numero)
                        except ValueError as e:
                            print(f"Error: {e}")
                    elif operacion == '3':
                        porcentaje = calc.obtener_valor("Ingrese el porcentaje de IVA: ")
                        try:
                            calc.calc_iva(porcentaje)
                        except ValueError as e:
                            print(f"Error: {e}")
                    else:
                        print("opcion no valida, intente nuevamente")
                    print(f"Resultado actual: {calc.mos_valor()}")
            elif opcion == 5:
                calc.reiniciar()
            elif opcion == 6:
                nuevo_valor = calc.obtener_valor("Ingrese un nuevo valor base: ")
                calc.resultado = nuevo_valor
                print(f"Nuevo valor base establecido: {calc.mos_valor()}")
            else:
                print("opcion no valida, intente nuevamente")
if __name__ == "__main__":    calc = calculadora()
calc.menu()

                



