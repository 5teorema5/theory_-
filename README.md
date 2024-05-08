<h2>Уд (критические темы прошлого семестра)</h2>

<details>
<summary><h3>1. Указатели и ссылки – сходства, отличия, зачем нужны.</h3></summary>

Указатели и ссылки предоставляют косвенный доступ к данным (переменным, массивам, структурам и тп), т.е. позволяют работать с объектами (которые могут быть а) очень большими, б) зарыты в памяти компьютера), не копируя их напрямую.

Указатели:

  * Хранят адрес объекта в памяти.
  * Могут быть null, указывая на отсутствие объекта.
  * Могут быть перенаправлены на другой объект после инициализации.
  * Требуют ручного управления памятью (выделение и освобождение!).
    
Ссылки:

  * Являются псевдонимами для существующих объектов.
  * Не могут быть null (не может быть ссылки на несуществующий элемент).
  * Не могут быть перенаправлены после инициализации.
  * Автоматически управляются системой (не требуют ручного выделения/освобождения памяти).

Зачем нужны:

* Передача больших объектов в функции: Используя указатели и ссылки, мы избегаем ненужного копирования, что повышает производительность.
* Динамическое выделение памяти: Позволяют создавать объекты в куче.
* Полиморфизм: Позволяют работать с объектами разных типов через общий интерфейс.

</details>

<h3>2. Сложность алгоритма. Сортировка за О(N 2), O(NlogN).</h3>

Любой алгоритм можно оценить по уровню сложности исходя из пропорциональности выполнения операции и количества элементов. 

O(N^2): 
  * Алгоритмы с квадратичной сложностью выполняют операции пропорционально квадрату количества элементов. 
  * Примеры: сортировка пузырьком, сортировка вставками, сортировка выбором.
  * Подходят для небольших наборов данных.

O(NlogN):
  * Алгоритмы с логарифмической сложностью выполняют операции пропорционально N*log(N).
  * Примеры: быстрая сортировка, сортировка методом Хоара, сортировка расчёсткой.
  * Более эффективны для больших наборов данных.
  * 
Важно помнить, что в разных ситуациях нужно применять разные алгоритмы разной сложности. Нет смысла сортировать учеников одной группы по баллам, используя метод рассчёски.

<h3>3. Сложность алгоритма. Поиск числа в отсортированном и неотсортированном массиве, доступ к произвольному элементу массива.</h3>

Сложность алгоритмов смотри предыдущий вопрос.

Поиск в отсортированном массиве:

  * Бинарный поиск: O(logN) - эффективен благодаря делению массива пополам на каждом шаге. А поскольку массив отсортирован, то с одно стороны элементы больше (или равны) искомому, а с другой стороны -- меньше (или равны).

Поиск в неотсортированном массиве:

  * Линейный поиск: O(N) - необходимо проверить каждый элемент.

Доступ к произвольному элементу массива: 
  * O(1) - прямой доступ по индексу.

<h3>4. Модель памяти .flat. Правила работы стека локальных переменных. Правила работы кучи.</h3>

В этой модели все сегменты памяти (код, данные, стек, куча) располагаются в едином адресном пространстве.
    * Упрощает управление памятью и доступ к данным.

Модель памяти .flat представляет собой сегменты памятиЮ которые располагаются в едином адресном пространстве:
	Глобальные переменные → текст программы (машинный код) → стек локальных 	переменных → куча. 
В стеке локальных переменных хранятся указатели на переменные, объявленные, но не инициализированные данные, оболочка объектов. В куче хранятся сами данные, на которые указываю переменные из стека локальных переменных. Именно в ней хранятся элементы массивов, других структур. Когда мы обращается к переменной, мы обращается в стеку локальных переменных, откуда мы перенаправляемся на адрес в куче, по которому «живёт» наш объект.  

Стек:

  * Используется для хранения локальных переменных и информации о вызовах функций.
  * Автоматически управляется системой (выделение и освобождение памяти).

Куча:
  * Область памяти для динамического выделения.
  * Программист сам управляет памятью (выделение с помощью new, освобождение с помощью delete).
  * Позволяет создавать объекты произвольного размера и времени жизни.
  * Важно помнить, что кучу необходимо очищать, нельзя удалять указатели на объекты, не удаляя данные по этим ссылкам. Это приводит к утечке данных — не приятно.



<h2>Хор (основные механики ООП и STL)</h2>

<h3>1. Инкапсуляция. Что это такое и зачем нужно.</h3>

Если писать объекты с отрытым доступом, то может возникнуть ряд проблем:
1) вызывающий код может всё сломать;
2) вызывающий код обязан знать внутреннюю логику, как минимум вызывать init и finalize, хотя это внутренне дело объекта;
3) вызывающий код зачем то должен знать объект со всеми его полями, хотя логически хочет видеть просто объект.

Для решения эти проблем используют инкапсуляцию — скрытие данных объекта. С помощью инкапсуляции мы сами регулируем то, как именно пользователь будет обращаться к объекту, ставим ему чёткие рамки.

Теперь:
1) Вызывающий код не может ничего сломать, по крайней мере, очевидным образом;
2) Аналоги init и finalize срабатывают сами в нужный момент;
3) Вызывающий код не должен знать про изнанку реализации;
4) Код чище и читаемее.

<h3>2. Наследование. Что это такое и зачем нужно.</h3>

Общая идея наследования заключается в выделении общего поведения у разных классов в отдельный класс-предок. То есть всё наследование — это про то, как не писать повторно один и тот же код для «почти одинаковых» сущностей.

Пример, мы хотим работать с системой зоопарка. Для этого мы можем написать классы под каждого сотрудника, где будут прописаны его обязанности, данные, зп,.. Нам так же нужен класс для каждого животного в котором будут прописаны все особенности… Ну это капец! Мы лучше создадим Два класса-родителя Humans и Animals, в котором пропишем все общие черты людей/животных, а дальше будем создавать классы наследники, для которых нам останется написать только особенности каждой зверушки.

<h3>3. Полиморфизм – концепция и примеры.</h3>

Суть полиморфизма заключается в том, что некоторая сущность может вести себя по-разному в разных ситуациях. Сущность, которая обладает этим свойством, сама подстраивается к этим ситуациям, и не заставляет крутиться весь мир вокруг неё.

```
#include <iostream>
...
void funk(char a) {
  std::cout << "This char" << '\n';
}

void funk(int a) {
  std::cout << "This int" << '\n';
}

void funk(double a, unsigned int b) {
  std::cout << "This double & unsigned int" << '\n';
}
...
int main() {
  funk('A');
  funk('7');
  funk(3.14, 3);
  return 0;
}
```

<h3>4. Конструкторы, деструкторы. Когда вызываются, зачем нужны.</h3>

Каждый класс необходимо сначая создать, в конце работы с ним необходимо удалить - чтобы лишнюю память не занимал. За это и отвечают конструкторы и деструкторы.

```
...
class stack {
private:
  int size;
public:
  //конструктор создаёт стек нулевого размера
  stack() {};
  //конструктор создаёт стэк нужного размера
  stack(int size) {};
  //деструктор удаляет стек
  ~stack();
}
...
```

 * Конструктор -- это специальный метод, который, очевидно, вызывают перед началом работы с объектор данного класса (при его создании). Используется для инициализации полей объекта, причём с помощью полиморфизма можно сделать несколько конструкторов, которые будут создавать объект по-разному.
 * Деструктор -- специальный метод, который, опять же очевидно, вызывается в конце работы с объектом класса (при удалении объекта). Можно, конечно же, не вызвать, после окончания работы с программой автоматически вызовятся все деструкторы всех объектов всех классов, которые были использованы. Этот метод используется для освобождения ресурсов, выделенных объектом.

<h3>5. Виртуальные поля и методы. Пояснить на примере, как работает механика виртуальности.</h3>

Иногда в родительском классе можно сказать только "здесь должен быть вот такой метод", но нельзя написать его реализацию.

 * заведомо предполагается, что классы будут унаследованы;
 * метод для них всех нужен, можно в общем виде сказатьб, что метод должен делать;
 * реализация будет кардинально разной в разных унаследованных классах.

В это случае возникают виртуальные методы. Они объявляются с ключевым словом `virtual` в базовом классе.

```
//класс предок
class Figure {
private:
	...
public:
	...
	virtual square() = 0;
}
//классы потомки
class Triangle : public Figure {
private:
	float a, b, c;
	...
public:
	...
	//реализация виртуального метода
	float square() {
		float p = (a + b + c) / 3;
		return (sqrtf(p*(p-a)*(p-b)*(p-c)));
	}
}
class Rectangle : public Figure {
private:
	float a, b;
	...
public:
	...
	//реализация виртуального метода
	float square() {
		return (a*b);
	}
}
```

Замечания по виртульным методам:

 * могут определяться в любой точке иерархии наследования;
 * класс с виртуальными методами называется абстрактным;
 * в иерархии наследования может быть много абстрактных классов;
 * создать экземпляр абстрактного класса нельзя, те если мы попытаемся сделать так, вы прилетит ошибка...
```
int main() {
	Figure obj;
	return 0;
}
``` 
Некоторые фишки, основанные на виртуальных методах:
 * `Интерфейс` -- абстрактный класс, у которого все методы виртуальный (задаёт, но не реализует, то, что должно быть);
 * `Реализация` -- какой-либо класс, унаследованный от интерфейса и реализующий все его виртуальные методы.

<h3>6. Статические и дружественные поля и методы класса.</h3>

`static` -- глобальная переменная/функция, внесённая в namespace класса.

Статическое поле класса:
 * привязано ко всех экземплярам класса сразу, никому из них лично не принадлежит;
 * при изменении (любым экземплярам класса или просто так) меняется для всех объектов сразу.

Статический метод класса:
 * привязан ко всех экземплярам класса сразу, вызывается вне контекста конкретного экземпляра (у него нет this);
 * может работать только с локальными переменными и статическими полями класса.

```
class A {
public:
	//нестатическое поле
	int non_static_int = 0;
	//статическое поле
	int static_int
	//статический метод
	static void static_method() {
		static_int++;		//можно
		non_static_int++;	//нельзя
	}
};
//Это объявление статического поля, без него будет ругаться линкер
int A::static_int = 0;

int main() {
	//Один экземпляр
	A a1;
	//ВТорой экземпляр
	A a2;
	//Обновляем статичекое поле класса через один из экземпляров
	a1.static_int = 7;
	//Обновляем статическое поле класса без использования экземпляров
	A::static_int = 8;
	//Вызываем статический метод
	// а) через экземпляры класса
	a1.static_method;
	a2.static_method;
	// б) без экземпляров класса
	A::static_method;
	return 0;
}
```

`friend` -- указание, кому всё-таки можно обращаться к приватным полям

```
class A {
	//Теперь класс B наш друг))))
	friend class B;
private:
	int secret;
public:
	A(int s) {
		secret = s;
	}
	void describe() {
		std::cout << "I'm A, my secret is " << secret << '\n';
	}
}
class B {
public:
	B() {}
	void run(A* a) {
		a->describe();
		std::cout << "I'm B, I know secret A: " << a->secret << '\n';
		//можно так же изменять значения дружественного класса
		a->secret--;
	}
}
```
`friend` -- исключение из правил, имеет доступ ко всему, включая private-поля. С одной стороны, нарушает всей строгой конструкции. С другой стороны, даёт возможностьне городить public для всех.
В примере, `class A` -- это друг `class B`, но не наоборот!!


<h3>7. ООП и память. Правило трех.</h3>

ООП и память??

<h4>Правило трёх</h4>

Если классу требуется пользовательский **деструктор**, пользовательский **конструктор копирования** или пользовательский **оператор присваивания копированием**, он почти наверняка требует все три.

Если один из них должен быть определен программистом, то это означает, что версия, сгенерированная компилятором, не удовлетворяет потребностям класса в одном случае и, вероятно, не удовлетворит в остальных случаях. Если же не реализовать какой-либо метод, то компилятор будет использовать базовые методы, идея которых может кардинально отличайться от нужд программиста. В результате может произойти следующее:

 - деструктор удалит не все используемыне ячейки в памяти, произойдёт утечка данных;
 - конструктор копирования выполняет "поверхностное копирование" (копирование данных без дублирования базового ресурса), в результате чего скопированный объект будет влаеть теми же ячейками в памяти, что и исходный объект;
 - оператор присваивания копированием так же буде выполнять поверхносное копирование.

<h3>8. Схема сборки многофайловой программы – препроцессор, компилятор, линкер.</h3>

1. **Препроцессор:** Обрабатывает директивы препроцессора (#include, #define).
2. **Компилятор:** Переводит код каждого исходного файла (.cpp) в объектный файл (.obj).
3. **Линкер:** Объединяет объектные файлы и библиотеки в исполняемый файл (.exe). 


<h3>9. Системы контроля версий – классификация, зачем нужны. Git и Github – основы использования.</h3>

<h3>10. Стандарты С++. Какие есть, зачем нужны. Краткий обзор.</h3>

<h3>11. Контейнеры STL – какие есть, на каких структурах данных основаны, для чего применяются.</h3>
