# PROYECTO 2 DE ALGORITMOS
# Lester López | Eliezer López
## El siguiente programa muestra 4 ejercicios cada uno presentado en c++ y python.
>Algoritmo en C++ | Ejercicio 1
 ```C++
 #include <iostream>
#include <fstream>
#include <vector>
using namespace std;

// Estructura para almacenar la información del producto
struct Producto {
    string nombre;
    string codigo;
    double precio;
    string proveedor;
    int existencia;
    char estado;
    double descuento;
};

// Función para guardar los datos en un archivo
void guardarDatos(const vector<Producto>& productos) {
    ofstream archivo("productos.txt");
    if (archivo.is_open()) {
        for (const Producto& producto : productos) {
            archivo << producto.nombre << " " << producto.codigo << " " << producto.precio << " " << producto.proveedor << " "
                    << producto.existencia << " " << producto.estado << " " << producto.descuento << "\n";
        }
        archivo.close();
    } else {
        cout << "No se pudo abrir el archivo para escritura." << endl;
    }
}

// Función para cargar los datos desde un archivo
vector<Producto> cargarDatos() {
    vector<Producto> productos;
    ifstream archivo("productos.txt");
    if (archivo.is_open()) {
        Producto producto;
        while (archivo >> producto.nombre >> producto.codigo >> producto.precio >> producto.proveedor >> producto.existencia >> producto.estado >> producto.descuento) {
            productos.push_back(producto);
        }
        archivo.close();
    } else {
        cout << "El archivo de datos no existe o no se puede abrir." << endl;
    }
    return productos;
}

// Función para agregar un producto
void agregarProducto(vector<Producto>& productos) {
    Producto producto;
    cout << "Nombre: ";
    cin >> producto.nombre;
    cout << "Codigo: ";
    cin >> producto.codigo;

    // Verificar que el código no se repita
    for (const Producto& p : productos) {
        if (p.codigo == producto.codigo) {
            cout << "El codigo de producto ya existe. No se puede agregar." << endl;
            return;
        }
    }

    cout << "Precio: ";
    cin >> producto.precio;
    cout << "Proveedor: ";
    cin >> producto.proveedor;
    cout << "Existencia: ";
    cin >> producto.existencia;
    cout << "Estado (A = Aprobado, R = Reprobado): ";
    cin >> producto.estado;
    cout << "Descuento: ";
    cin >> producto.descuento;

    productos.push_back(producto);
    guardarDatos(productos);
    cout << "Producto agregado con exito." << endl;
}

// Función para buscar un producto por código o nombre
void buscarProducto(const vector<Producto>& productos) {
    string criterio;
    cout << "Ingrese el criterio de busqueda (codigo o nombre): ";
    cin >> criterio;
    for (const Producto& producto : productos) {
        if (producto.codigo == criterio || producto.nombre.find(criterio) != string::npos) {
            cout << "Nombre: " << producto.nombre << endl;
            cout << "Código: " << producto.codigo << endl;
            cout << "Precio: " << producto.precio << endl;
            cout << "Proveedor: " << producto.proveedor << endl;
            cout << "Existencia: " << producto.existencia << endl;
            cout << "Estado: " << producto.estado << endl;
            cout << "Descuento: " << producto.descuento << endl;
            cout << "---------------------------" << endl;
        }
    }
}

// Función para modificar los datos de un producto
void modificarProducto(vector<Producto>& productos) {
    string codigo;
    cout << "Ingrese el codigo del producto que desea modificar: ";
    cin >> codigo;
    for (Producto& producto : productos) {
        if (producto.codigo == codigo) {
            cout << "Nuevo precio: ";
            cin >> producto.precio;
            cout << "Nuevo proveedor: ";
            cin >> producto.proveedor;
            cout << "Nueva existencia: ";
            cin >> producto.existencia;
            cout << "Nuevo estado (A = Aprobado, R = Reprobado): ";
            cin >> producto.estado;
            cout << "Nuevo descuento: ";
            cin >> producto.descuento;
            guardarDatos(productos);
            cout << "Producto modificado con exito." << endl;
            return;
        }
    }

    cout << "No se encontro ningun producto con el codigo proporcionado." << endl;
}

int main() {
    vector<Producto> productos = cargarDatos();

    while (true) {
        cout << "Menu:" << endl;
        cout << "1. Agregar producto" << endl;
        cout << "2. Buscar producto" << endl;
        cout << "3. Modificar datos de un producto" << endl;
        cout << "4. Salir" << endl;
        cout << "Seleccione una opcion: ";

        int opcion;
        cin >> opcion;

        switch (opcion) {
            case 1:
                agregarProducto(productos);
                break;
            case 2:
                buscarProducto(productos);
                break;
            case 3:
                modificarProducto(productos);
                break;
            case 4:
		    cout<<"Gracias por utilizar el programa"<<endl;
                return 0;
            default:
                cout << "Opcion no valida." << endl;
        }
    }
    return 0;
}

  ```
---
---
>Algoritmo en Python | Ejercicio 1
 ```Python
# Función para guardar los datos en un archivo
def guardarDatos(productos):
    with open("productos.txt", "w") as archivo:
        for producto in productos:
            archivo.write(f"{producto['nombre']} {producto['codigo']} {producto['precio']} {producto['proveedor']} {producto['existencia']} {producto['estado']} {producto['descuento']}\n")

# Función para cargar los datos desde un archivo
def cargarDatos():
    try:
        with open("productos.txt", "r") as archivo:
            productos = []
            for linea in archivo:
                datos = linea.strip().split()
                producto = {
                    'nombre': datos[0],
                    'codigo': datos[1],
                    'precio': float(datos[2]),
                    'proveedor': datos[3],
                    'existencia': int(datos[4]),
                    'estado': datos[5],
                    'descuento': float(datos[6])
                }
                productos.append(producto)
            return productos
    except FileNotFoundError:
        print("El archivo de datos no existe o no se puede abrir.")
        return []

# Función para agregar un producto
def agregarProducto(productos):
    producto = {}
    producto['nombre'] = input("Nombre: ")
    producto['codigo'] = input("Código: ")

    # Verificar que el código no se repita
    for p in productos:
        if p['codigo'] == producto['codigo']:
            print("El código de producto ya existe. No se puede agregar.")
            return

    producto['precio'] = float(input("Precio: "))
    producto['proveedor'] = input("Proveedor: ")
    producto['existencia'] = int(input("Existencia: "))
    producto['estado'] = input("Estado (A = Aprobado, R = Reprobado): ")
    producto['descuento'] = float(input("Descuento: "))

    productos.append(producto)
    guardarDatos(productos)
    print("Producto agregado con éxito.")

# Función para buscar un producto por código o nombre
def buscarProducto(productos):
    criterio = input("Ingrese el criterio de búsqueda (código o nombre): ")
    for producto in productos:
        if producto['codigo'] == criterio or criterio in producto['nombre']:
            print("Nombre:", producto['nombre'])
            print("Código:", producto['codigo'])
            print("Precio:", producto['precio'])
            print("Proveedor:", producto['proveedor'])
            print("Existencia:", producto['existencia'])
            print("Estado:", producto['estado'])
            print("Descuento:", producto['descuento'])
            print("---------------------------")

# Función para modificar los datos de un producto
def modificarProducto(productos):
    codigo = input("Ingrese el código del producto que desea modificar: ")
    for producto in productos:
        if producto['codigo'] == codigo:
            producto['precio'] = float(input("Nuevo precio: "))
            producto['proveedor'] = input("Nuevo proveedor: ")
            producto['existencia'] = int(input("Nueva existencia: "))
            producto['estado'] = input("Nuevo estado (A = Aprobado, R = Reprobado): ")
            producto['descuento'] = float(input("Nuevo descuento: "))
            guardarDatos(productos)
            print("Producto modificado con éxito.")
            return

    print("No se encontró ningún producto con el código proporcionado.")

# Función principal
def main():
    productos = cargarDatos()

    while True:
        print("Menú:")
        print("1. Agregar producto")
        print("2. Buscar producto")
        print("3. Modificar datos de un producto")
        print("4. Salir")
        opcion = input("Seleccione una opción: ")

        if opcion == "1":
            agregarProducto(productos)
        elif opcion == "2":
            buscarProducto(productos)
        elif opcion == "3":
            modificarProducto(productos)
        elif opcion == "4":
            return
        else:
            print("Opción no válida.")

if __name__ == "__main__":
    main()
 ```
---
---
