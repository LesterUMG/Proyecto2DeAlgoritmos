# TAREA 4 DE ALGORITMOS
# Lester López
## El siguiente programa muestra 4 ejercicios cada uno presentado en c++ y python.
>Algoritmo en C++ | Ejercicio 1
 ```C++
 /*-Un estacionamiento cobra una cuota mínima de $2.00 por estacionarse hasta tres horas
-El estacionamiento cobra $0.50 adicionales por cada hora o fracción que se pase de tres horas
-El cargo máximo para cualquier periodo dado de 24 horas es de $10.00
-Ningún automóvil se estaciona durante más de 24 horas a la vez
*/
#include <iostream>
#include <iomanip>
#include <cmath>

using namespace std;

double calcularCargos(double horas) {
    double cargo = 0.0;
    if (horas <= 3) {
        cargo = 2.0;
    } else if (horas <= 24) {
        cargo = 2.0 + 0.5 * ceil(horas - 3);
        if (cargo > 10.0) {
            cargo = 10.0;
        }
    } else {
        cout << "Error: El tiempo de estacionamiento no puede ser mayor a 24 horas." << endl;
    }
    return cargo;
}

int main() {
    double horas[3];
    double cargos[3];
    double total = 0.0;
    double total2 = 0.0;

    for (int i = 0; i < 3; i++) {
        cout << "Introduzca las horas de estacionamiento para el cliente " << i + 1 << ": ";
        cin >> horas[i];
        cargos[i] = calcularCargos(horas[i]);
        total += cargos[i];
        total2 += horas[i];
    }

    cout << fixed << setprecision(2);
    cout << "Cliente" << setw(20) << "Horas" << setw(20) << "Cargo" << endl;
    for (int i = 0; i < 3; i++) {
        cout << i + 1 << setw(20) << horas[i] << setw(20) << cargos[i] << endl;
    }
    cout << "Total" << setw(20) << total2 << setw(20) << total << endl;

    return 0;
}
  ```
---
---
>Algoritmo en Python | Ejercicio 1
 ```Python
def calcularCargos(horas):
    if horas <= 3:
        return 2.00
    elif horas <= 24:
        return 2.00 + 0.50 * (horas - 3)
    else:
        return 10.00

total = 0
print("Cliente\tHoras\tCargo")
for i in range(3):
    horas = float(input(f"Ingrese las horas de estacionamiento del cliente {i + 1}: "))
    cargo = calcularCargos(horas)
    total += cargo
    print(f"{i + 1}\t{horas}\t${cargo:.2f}")
print(f"Total\t\t${total:.2f}")
 ```
---
---
>Algoritmo en C++ | Ejercicio 2
 ```C++
/*Aplicación que le pregunte al usuario cuántas filas y cuántas columnas de una matriz 
quiere ingresar, luego que reciba todos los valores, seguido debe imprimir el número mayor de
la matriz y los datos de la matriz ingresada y el promedio de la matriz
*/
#include <iostream>
#include <iomanip>

using namespace std;

int main() {
    int filas, columnas;
    double matriz[100][100];
    double mayor = 0.0;
    double suma = 0.0;
    double promedio = 0.0;

    cout << "Ingrese el numero de filas: ";
    cin >> filas;
    cout << "Ingrese el numero de columnas: ";
    cin >> columnas;

    for (int i = 0; i < filas; i++) {
        for (int j = 0; j < columnas; j++) {
            cout << "Ingrese el valor para la fila " << i + 1 << " y la columna " << j + 1 << ": ";
            cin >> matriz[i][j];
            if (matriz[i][j] > mayor) {
                mayor = matriz[i][j];
            }
            suma += matriz[i][j];
        }
    }

    promedio = suma / (filas * columnas);

    cout << fixed << setprecision(2);
    cout << "El numero mayor de la matriz es: " << mayor << endl;
    cout << "Los datos de la matriz son:" << endl;
    for (int i = 0; i < filas; i++) {
        for (int j = 0; j < columnas; j++) {
            cout << setw(10) << matriz[i][j] << " ";
        }
        cout << endl;
    }
    cout << "El promedio de la matriz es: " << promedio << endl;

    return 0;
}
 ```
---
---
>Algoritmo en Python | Ejercicio 2
 ```Python
filas = int(input("Ingrese la cantidad de filas: "))
columnas = int(input("Ingrese la cantidad de columnas: "))
matriz = []
for i in range(filas):
    fila = []
    for j in range(columnas):
        fila.append(int(input(f"Ingrese el valor para la fila {i + 1}, columna {j + 1}: ")))
    matriz.append(fila)
mayor = matriz[0][0]
for fila in matriz:
    for valor in fila:
        if valor > mayor:
            mayor = valor
print("El número mayor de la matriz es:", mayor)
print("Los datos de la matriz son:")
for fila in matriz:
    for valor in fila:
        print(valor, end=" ")
    print()
promedio = sum(sum(matriz, [])) / (filas * columnas)
print("El promedio de la matriz es:", promedio)

 ```
---
---
>Algoritmo en C++ | Ejercicio 3
 ```C++
/*Escriba una función llamada esPerfecto que determine si el parámetro numero es un número perfecto
Use esta función en un programa que determine e imprima todos los números perfectos entre 1 y 1000
Imprima los divi-sores de cada número perfecto para confirmar que el número sea realmente perfecto
*/
#include <iostream>
using namespace std;

bool esPerfecto(int numero) {
    int suma = 0;
    for (int i = 1; i < numero; i++) {
        if (numero % i == 0) {
            suma += i;
        }
    }
    return suma == numero;
}

int main() {
    cout << "Numeros perfectos entre 1 y 1000:" << endl;
    for (int i = 1; i <= 1000; i++) {
        if (esPerfecto(i)) {
            cout << i << " es un numero perfecto." << endl;
            cout << "Sus divisores son: ";
            for (int j = 1; j < i; j++) {
                if (i % j == 0) {
                    cout << j << " ";
                }
            }
            cout << endl;
        }
    }
    return 0;
}

 ```
---
---
>Algoritmo en Python | Ejercicio 3
 ```Python
def esPerfecto(numero):
    suma = 0
    for i in range(1, numero):
        if numero % i == 0:
            suma += i
    return suma == numero

print("Números perfectos entre 1 y 1000:")
for i in range(1, 1001):
    if esPerfecto(i):
        print(f"{i} es un número perfecto.")
        print("Sus divisores son: ", end="")
        for j in range(1, i):
            if i % j == 0:
                print(j, end=" ")
        print()

 ```
---
---
>Algoritmo en C++ | Ejercicio 4
 ```C++
/*Aplicación que determine la mediana y el promedio de una lista (arreglo) de
números, donde el usuario indique la cantidad de dichos números. Es decir el debe decir cuánto
será la longitud del arreglo e ingresará cada número
*/
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
    int n;
    cout << "Ingrese la cantidad de numeros: ";
    cin >> n;
    int arr[n];
    for (int i = 0; i < n; i++) {
        cout << "Ingrese el numero " << i + 1 << ": ";
        cin >> arr[i];
    }
    sort(arr, arr + n);
    double promedio = 0;
    for (int i = 0; i < n; i++) {
        promedio += arr[i];
    }
    promedio /= n;
    double mediana;
    if (n % 2 == 0) {
        mediana = (arr[n / 2 - 1] + arr[n / 2]) / 2.0;
    } else {
        mediana = arr[n / 2];
    }
    cout << "El promedio es: " << promedio << endl;
    cout << "La mediana es: " << mediana << endl;
    return 0;
}
 ```
---
---
>Algoritmo en Python | Ejercicio 4
 ```Python
n = int(input("Ingrese la cantidad de números: "))
arr = []
for i in range(n):
    arr.append(int(input(f"Ingrese el número {i + 1}: ")))
arr.sort()
promedio = sum(arr) / n
if n % 2 == 0:
    mediana = (arr[n // 2 - 1] + arr[n // 2]) / 2
else:
    mediana = arr[n // 2]
print(f"El promedio es: {promedio}")
print(f"La mediana es: {mediana}")

 ```
---
---