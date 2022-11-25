
# research 
 сначала происходит загрузка классов во внутреннюю память:applicationclassloader делегирует загрузку класса platformclassloader  -> bootstrapclassloader, который пытается найти и загузить классы из области своей памяти ->platformclassloader-> applicationclassloader, который ищет нужный класс по всему проекту 

public class JvmComprehension { 

    public static void main(String[] args) { в стеке создается память для метода main
        int i = 1;                      // 1 переменная создается в стеке
        Object o = new Object();        // 2 объект создается в куче, а в стеке создается ссылка на него
        Integer ii = 2;                 // 3 тут тоже объект создается в куче, а в стеке - ссылка на него 
        printAll(o, i, ii);             // 4 создается новая память под метод  в стеке, в памяти метода создаются ссылки на объекты o, ii из кучи  
        System.out.println("finished"); // 7 создается память в стеке под метод println, после чего выполнение main заканчивается, и память для него очищается 
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5 создается переменная в куче, которая потом удаляется GC, т.к. она не используется 
        System.out.println(o.toString() + i + ii);  // 6 под метод println создается память в стеке, куда передаются : ссылка на объект типа стринг "o.toString", переменная i и ссылка на ii  
    }
} 
