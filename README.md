# **Game Project**

**Para correr el juego se deben seguir las instrucciones en terminal.**


```sh
cd game
python3 main.py 
```
============================================================================================
### **App/Charts**

**1)** **_Importación de Matplotlib:_**
Se importa la biblioteca Matplotlib con la alias plt.

````
import matplotlib.pyplot as plt
````

**2)** **_Función generate_bar_chart:_**
Esta función toma tres parámetros: name (nombre del gráfico), labels (etiquetas del eje x) y values (valores del eje y).
Crea una figura y ejes usando plt.subplots().
Utiliza ax.bar(labels, values) para generar un gráfico de barras con las etiquetas y valores proporcionados.
Guarda el gráfico como una imagen en la carpeta './imgs' con el nombre proporcionado y la extensión '.png'.
Cierra la figura para liberar recursos.

````
def generate_bar_chart(name, labels, values):
    fig, ax = plt.subplots()
    ax.bar(labels, values)
    plt.savefig(f'./imgs/{name}.png')
    plt.close()
````

**3)** **_Función generate_pie_chart:_**
Esta función toma dos parámetros: labels (etiquetas de las porciones del pastel) y values (valores asociados a cada etiqueta).
Crea una figura y ejes usando plt.subplots().
Utiliza ax.pie(values, labels=labels) para generar un gráfico circular con las etiquetas y valores proporcionados.
Establece ax.axis('equal') para asegurarse de que el gráfico sea un círculo perfecto.
Guarda el gráfico como una imagen con el nombre 'bar.png'.
Cierra la figura para liberar recursos.

````
def generate_pie_chart(labels, values):
    fig, ax = plt.subplots()
    ax.pie(values, labels=labels)
    ax.axis('equal')
    plt.savefig('bar.png')
    plt.close()
````
    
**4)** **_Bloque __main__:_**
Se definen listas labels y values con datos de ejemplo.
Se llama a la función generate_pie_chart con las listas de etiquetas y valores para generar un gráfico circular.

````
if __name__ == '__main__':
    labels = ['a', 'b', 'c']
    values = [10, 40, 800]
    generate_pie_chart(labels, values)
````
============================================================================================
### **App/Main**

**1)** **_Importación de Módulos:_**
Se importan tres módulos: utils, read_csv y charts. Estos módulos parecen contener funciones y utilidades necesarias para realizar diversas operaciones.

````
import utils
import read_csv
import charts
````

**2)** **_Función run:**
La función run se encarga de coordinar la ejecución del programa.
Lee datos desde un archivo CSV usando la función read_csv.read_csv('./data.csv') y filtra los datos para mantener solo aquellos relacionados con 'South America'.

````
def run():
    data = read_csv.read_csv('./data.csv')
    data = list(filter(lambda item: item['Continent'] == 'South America', data))

````   
**Crea listas de países y porcentajes utilizando funciones de mapeo en las columnas 'Country' y 'World Population Percentage' respectivamente.**

    countries = list(map(lambda x: x['Country'], data))
    percentages = list(map(lambda x: x['World Population Percentage'], data))
    
**Llama a la función charts.generate_pie_chart para generar un gráfico circular con las listas de países y porcentajes.**

    charts.generate_pie_chart(countries, percentages)
    
**Solicita al usuario que ingrese un país, lo imprime y utiliza funciones del módulo utils para obtener información sobre la población de ese país.**

    country = input('Type Country =>')
    print(country)
    result = utils.population_by_country(data, country)
    
**Si se encuentra información sobre el país ingresado, se extraen etiquetas y valores de población y se llama a charts.generate_bar_chart para generar un gráfico de barras.**

    if len(result) > 0:
        country = result[0]
        print(country)
        labels, values = utils.get_population(country)
        charts.generate_bar_chart(country['Country'], labels, values)
        
**3)** **_Bloque __main__:_**
Se ejecuta la función run() cuando el script es ejecutado directamente.

````
if __name__ == '__main__':
    run()
````
============================================================================================
### **Charts/Charts**

**Importación de Matplotlib:**
Se importa la biblioteca Matplotlib con la alias plt.

````
import matplotlib.pyplot as plt
````

**Función generate_pie_chart:**
Esta función no toma parámetros y está diseñada para generar un gráfico de pastel con datos predefinidos ('A', 'B', 'C' como etiquetas y 200, 34, 120 como valores).

````
def generate_pie_chart():
    labels = ['A', 'B', 'C']
    values = [200, 34, 120]
````


**Crea una figura y ejes usando plt.subplots().**

    fig, ax = plt.subplots()
    
**Utiliza ax.pie(values, labels=labels) para generar un gráfico circular con las etiquetas y valores proporcionados.**

    ax.pie(values, labels=labels)
    
**Guarda el gráfico como una imagen con el nombre 'pie.png' utilizando plt.savefig().**

    plt.savefig('pie.png')
    
**Cierra la figura para liberar recursos.**

    plt.close()
    
**Bloque __main__:**
Si este script es ejecutado directamente, la función generate_pie_chart se llama.

````
if __name__ == '__main__':
    generate_pie_chart()
````
============================================================================================
### **Charts/Main**

**Importación del Módulo charts:**
Se importa el módulo charts que probablemente contiene la función generate_pie_chart.

````
import charts
````

**Función run:**
La función run es simple y llama a la función generate_pie_chart del módulo charts.

````
def run():
    charts.generate_pie_chart()
````

**Bloque __main__:**
Si este script es ejecutado directamente (no importado como un módulo en otro script), se ejecuta la función run.

````
if __name__ == '__main__':
    run()
````
============================================================================================
### **Game/Main**

**Este código implementa un juego simple de "piedra, papel o tijera" entre un usuario y la computadora. Aquí está la explicación detallada:**

**Función choose_options:**
Define las opciones del juego ('piedra', 'papel', 'tijera').
Solicita al usuario que ingrese su elección y la convierte a minúsculas.
Si la opción ingresada por el usuario no está en las opciones, se imprime un mensaje y se devuelve None para indicar que la opción no es válida.
La computadora elige aleatoriamente una opción.
Se imprime la elección de la computadora.
Devuelve las opciones elegidas por el usuario y la computadora.

````
def choose_options():
    options = ('piedra', 'papel', 'tijera')
    user_option = input('    piedra, papel o tijera -> ')
    user_option = user_option.lower()

    if not user_option in options:
        print('!!! Esa opcion no es valida')
        return None, None

    computer_option = random.choice(options)

    print('')
    print('Oponente =>', computer_option)
    return user_option, computer_option
````
    
**Función check_rules:**
Verifica las reglas del juego para determinar el ganador de una ronda.
Actualiza los puntajes según el resultado y devuelve los puntajes actualizados.


````
def check_rules(user_option, computer_option, user_wins, computer_wins):
    # ... (código omitido para brevedad)
    return user_wins, computer_wins
````
    
**Función run_game:**
Inicializa las variables para el número de victorias de la computadora, el usuario y el número de rondas.
Ejecuta un bucle infinito para cada ronda del juego.
Llama a las funciones anteriores para que el usuario elija y se determinen los resultados.
Imprime el puntaje actualizado después de cada ronda.
El juego termina cuando uno de los jugadores alcanza dos victorias.

````
def run_game():
    # ... (código omitido para brevedad)
    run_game()
````

**Bloque __main__:**
Llama a la función run_game para iniciar el juego cuando el script es ejecutado directamente.

````
if __name__ == '__main__':
    run_game()
````

**En resumen, este código implementa un juego simple de "piedra, papel o tijera" entre un usuario y la computadora, con un bucle que continúa hasta que uno de los jugadores alcanza dos victorias.**
