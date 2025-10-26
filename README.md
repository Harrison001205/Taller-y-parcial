# Taller-y-parcial
Profe creo que esto es el taller y el parcial si no me dices porfa 

import time
import random
import matplotlib.pyplot as plt

# Algoritmos de ordenación (se mantienen igual por ser funciones separadas)
def burbuja(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left_half = arr[:mid]
    right_half = arr[mid:]
    left_half = merge_sort(left_half)
    right_half = merge_sort(right_half)
    return merge(left_half, right_half)

def merge(left, right):
    merged_list, i, j = [], 0, 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            merged_list.append(left[i])
            i += 1
        else:
            merged_list.append(right[j])
            j += 1
    merged_list.extend(left[i:])
    merged_list.extend(right[j:])
    return merged_list

#---
## Versión compacta y principal
---

def main_compacto():
    """
    Versión compacta del script para comparar algoritmos de ordenación.
    """
    tamanos = [100, 1000, 5000, 10000]
    algoritmos = {
        'Algoritmo Burbuja': (burbuja, []),
        'Algoritmo Merge Sort': (merge_sort, [])
    }

    for tam in tamanos:
        lista_original = [random.randint(0, 100000) for _ in range(tam)]
        print(f"Probando con una lista de tamaño {tam}...")
        
        for nombre, (algoritmo, tiempos) in algoritmos.items():
            lista_copia = lista_original.copy()
            inicio = time.perf_counter()
            algoritmo(lista_copia)
            fin = time.perf_counter()
            tiempos.append(fin - inicio)
            print(f" - Tiempo {nombre}: {tiempos[-1]:.6f} segundos")

    plt.figure(figsize=(10, 6))
    for nombre, (_, tiempos) in algoritmos.items():
        plt.plot(tamanos, tiempos, 'o-', label=nombre)

    plt.title('Comparación de Tiempos de Ejecución')
    plt.xlabel('Tamaño de la Lista')
    plt.ylabel('Tiempo de Ejecución (segundos)')
    plt.legend()
    plt.grid(True)
    plt.show()

    print("\n--- Análisis ---")
    print("El **algoritmo de burbuja** escala peor, con un tiempo que aumenta exponencialmente (O(n²)), mientras que el **Merge Sort** es mucho más eficiente a medida que la lista crece (O(n log n)).")
    print("Para listas pequeñas, la diferencia es mínima, pero para listas grandes, el **Merge Sort** es claramente superior.")

if __name__ == "__main__":
    main_compacto()



    matriz = np.random.randint(1, 10, (n, n))
    
    # Guardar en archivo de texto
    np.savetxt(f"{filename}.txt", matriz, fmt="%d")
    print(f"Matriz guardada en {filename}.txt")
    
    # Guardar en archivo binario
    np.save(f"{filename}.npy", matriz)
    print(f"Matriz guardada en {filename}.npy")
    
    return matriz

def verificar_y_calcular(filename):
    """Lee los archivos, verifica la consistencia y realiza los cálculos."""
    # Leer archivo de texto
    matriz_txt = np.loadtxt(f"{filename}.txt", dtype=int)
    
    # Leer archivo binario
    matriz_npy = np.load(f"{filename}.npy")
    
    # Verificar consistencia
    if np.array_equal(matriz_txt, matriz_npy):
        print("\n¡Los datos de los archivos son consistentes!")
    else:
        print("\n¡Los datos de los archivos son inconsistentes!")

    print("\n--- Cálculos sobre la matriz ---\n")
    print("Matriz:\n", matriz_npy)

    # Calcular la traza
    traza = np.trace(matriz_npy)
    print(f"\nTraza (suma de la diagonal principal): {traza}")
    
    # Calcular el determinante
    determinante = np.linalg.det(matriz_npy)
    print(f"Determinante: {determinante:.2f}")

if __name__ == "__main__":
    n = 3 # Puedes cambiar el tamaño de la matriz
    nombre_archivo = "matriz_integrador"
    
    matriz_original = generar_y_guardar_matriz(n, nombre_archivo)
    verificar_y_calcular(nombre_archivo)




#Mayormente, lo que aprendí fue a usar más librerías, ya que antes solía usar mucho código cuando hay mucha librería que ayuda demasiado. Hay cosas que sí o sí toca hacer con librerías, como los gráficos. Lo que sí no sabía hacer muy bien era hacer un código más eficiente; el profesor nos alcanzó a medio enseñar cómo hacerlo. Ahora, contigo me doy cuenta de que con la librería sys es mucho más rápido. Igual, aún me cuesta bastante el meter código en sí, pues pensar en cómo resolver el problema no, pero ya pasar lo que pienso a código es más complicado porque uno se queda como pausado en algún punto y no sabe qué más hacer. Pero con el profesor Daniel, mayormente aprendí fue a agilizar un código y lo de listas enlazadas, ya que la mayoría de las otras cosas ya las había visto en Computación Científica 1.
