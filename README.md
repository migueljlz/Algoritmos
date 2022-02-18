# Algoritmos

Conozca y use algunos los algoritmos más populares que existen.

## Algoritmo bubble sort

El algoritmo de **burbuja o bubble sort** dada una colección de elementos compara los dos primeros elementos de la colección y los intercambia en función de su orden si es necesario.

A continuación realiza la comparación para el segundo y tercer elemento de la colección y los intercambia en función de su orden.

Este proceso se repite hasta llegar al último elemento de la colección, como resultado se tiene que en la última posición de la colección estará el elemento con mayor valor.

El proceso se repite de nuevo comenzando desde la primera posición de la colección sin incluir la posición del elemento ya ordenado anteriormente, como resultado dará al siguiente elemento de mayor orden. Se repite esta ordenación tantas veces como elementos tenga la colección menos uno.

Esta es una interfaz que define un método para ordenar una colección, se proporciona la colección y una clase Comparator.

    package bigtec.com;

    import java.util.Collection;
    import java.util.Comparator;
    import java.util.List;

    public interface SortAlgorithm<T> {
        List<T> sort(Collection<T> collection, Comparator<T> comparator);

        default void swap(List<T> list, int i, int j){
            T ti = list.get(i);
            T tj = list.get(j);
            list.set(j, ti);
            list.set(i, tj);
        }
    }

El programa Java crea una colección de 25 elementos con un valor aleatorio entre 0 y 100, y los ordena con cada uno de los algoritmos.

    package bigtec.com;

    import java.util.List;
    import java.util.Random;
    import java.util.stream.Collectors;

    public class App 
    {
        public static void main( String[] args )
        {
            List<Integer> integers = randomList(25);
            List<Integer> bubbleSort = new BubbleSort<Integer>().sort(integers, Integer::compareTo);
            System.out.printf("Integers (%s):    %s%n", integers.size(), integers.stream().map(i -> i.toString()).collect(Collectors.joining(",")));
            System.out.printf("Bubble Sort (%s): %s%n", bubbleSort.size(), bubbleSort.stream().map(i -> i.toString()).collect(Collectors.joining(",")));
        }

        public static List<Integer> randomList(int elements){
            return new Random().ints(elements, 0, 100).boxed().collect(Collectors.toList());
        }
    }

Esta es la implementación del algoritmos de burbuja.

<p align="center">
  <img src="https://picodotdev.github.io/blog-bitix/2021/06/implementacion-de-los-algoritmos-de-ordenacion-bubble-sort-merge-sort-y-quicksort-en-java/images/bubble-sort.gif" alt="Burble sort method" />
</p>

    package bigtec.com;

    import java.util.ArrayList;
    import java.util.Collection;
    import java.util.Comparator;
    import java.util.List;

    public class BubbleSort<T> implements SortAlgorithm<T> {
        
        public List<T> sort(Collection<T> collection, Comparator<T> comparator) {
            List<T> list = new ArrayList<>(collection);
            for (int i = 0; i < list.size(); ++i) {
                for (int j = 1; j < list.size(); ++j){
                    T a = list.get(j - 1);
                    T b = list.get(j);
                    if (comparator.compare(a, b) > 0) {
                        swap(list, j - 1, j);
                    }
                }
            }
            return list;
        }
    }
