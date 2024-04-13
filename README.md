# Métodos de Ordenación
## Creación del código en lenguaje Java:

public class MetodosOrdenamiento {
    public static void main(String[] args) {
        Scanner entrada = new Scanner(System.in);
        
        int[] arregloDes1 = generar(1000);
        int[] arregloDes2 = generar(10000);
        int[] arregloDes3 = generar(100000);

        // Ordenar el arreglo usando el método Quicksort
        long inicio = System.nanoTime();
        quickSort(arregloDes1);
        long fin = System.nanoTime();
        long tiempoEjecucion = fin - inicio;
        
        double tiempoEnMilisegundos = (double) tiempoEjecucion / 1_000_000.0;
        
        System.out.println( tiempoEnMilisegundos);
        
        burbuja(arregloDes1);
        baraja(arregloDes1);
    }

    // Método para generar un arreglo en orden descendente
    public static int[] generar(int tamaño) {
        int[] arreglo = new int[tamaño];
        for (int i = 0; i < tamaño; i++) {
            arreglo[i] = tamaño - i;
        }
        return arreglo;
    }

    // Método de ordenación Burbuja
    public static void burbuja(int[] arreglo) {
        int n = arreglo.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (arreglo[j] > arreglo[j + 1]) {
                    // Intercambiar elementos si están en el orden incorrecto
                    int temp = arreglo[j];
                    arreglo[j] = arreglo[j + 1];
                    arreglo[j + 1] = temp;
                }
            }
        }
    }

    // Método de ordenación Inserción Directa (Baraja)
    public static void baraja(int[] arreglo) {
        int n = arreglo.length;
        for (int i = 1; i < n; ++i) {
            int clave = arreglo[i];
            int j = i - 1;
            while (j >= 0 && arreglo[j] > clave) {
                arreglo[j + 1] = arreglo[j];
                j = j - 1;
            }
            arreglo[j + 1] = clave;
        }
    }

    public static void quickSort(int[] arr) {
        Stack<Integer> stack = new Stack<>();
        stack.push(0);
        stack.push(arr.length - 1);

        while (!stack.isEmpty()) {
            int fin = stack.pop();
            int inicio = stack.pop();

            if (inicio < fin) {
                int indiceParticion = particion(arr, inicio, fin);
                stack.push(inicio);
                stack.push(indiceParticion - 1);
                stack.push(indiceParticion + 1);
                stack.push(fin);
            }
        }
    }

    public static int particion(int[] arr, int inicio, int fin) {
        int pivote = arr[fin];
        int i = inicio - 1;
        for (int j = inicio; j < fin; j++) {
            if (arr[j] <= pivote) {
                i++;
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
        int temp = arr[i + 1];
        arr[i + 1] = arr[fin];
        arr[fin] = temp;
        return i + 1;
    }
    
    public static void imprimir(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }
    
}
