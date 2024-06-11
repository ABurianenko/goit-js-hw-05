# goit-js-hw-05

-----КОЛБЕК-ФУНКЦІЇ-----

Функція зворотного виклику (callback, колбек) — це функція, яка передається іншій функції як аргумент, а та у свою чергу використовує передану функцію.

Функція вищого порядку (higher order function) — функція, яка приймає в якості параметрів інші функції або повертає функцію в якості результату.

function greet(name) {
console.log(`Welcome ${name}!`);
}

function notify(name) {
console.log(`Dear ${name}, your room will be ready in 30 minutes`);
}

function registerGuest(name, callback) {
console.log(`Registering ${name}!`);
callback(name);
}

registerGuest("Mango", greet); // "Registering Mango!"// "Welcome Mango!"

registerGuest("Mango", notify); // "Registering Mango!"// "Dear Mango, your room will be ready in 30 minutes"

Якщо колбек-функція маленька і потрібна тільки для передачі аргументом, її можна оголосити безпосередньо на момент виклику функції, в яку передаємо колбек. Такі функції називаються інлайн-колбеки.

registerGuest("Mango", function greet(name) {
console.log(`Welcome ${name}!`);
});

registerGuest("Poly", function notify(name) {
console.log(`Dear ${name}, your room will be ready in 30 minutes`);
});

Метод forEach(callback) — це метод перебирання масиву, який використовується для заміни циклів for і for...of в роботі з колекцією.
Перервати виконання методу forEach не можна, він завжди перебирає масив до кінця.

-----СТРІЛОЧНІ ФУНКЦІЇ-----

Стрілочні функції (сленг — “стрілки”) мають скорочений, лаконічніший синтаксис, що зменшує обсяг коду, особливо коли функція маленька або якщо вона використовується як колбек.

// Звичайне оголошення функції
function classicAdd(a, b, c) {
return a + b + c;
}

// Те саме стрілочною функцією
const arrowAdd = (a, b, c) => {
return a + b + c;
};

Якщо параметрів декілька, то вони перераховуються через кому в круглих дужках, між знаками рівності = і стрілкою =>.
Якщо параметр один, його можна оголошувати без круглих дужок.

Якщо є фігурні дужки і функція повинна повертати якесь значення, необхідно явно поставити return. Це називається явне повернення (explicit return).
Такий синтаксис використовується в тому випадку, якщо в тілі функції потрібно виконати ще якісь інструкції, окрім повернення значення.

Якщо фігурні дужки відсутні, то повертається результат виразу, який стоїть після =>. Це називається неявне повернення (implicit return).
Він доречний тільки тоді, коли в тілі функції не потрібно виконувати жодних додаткових інструкцій, окрім повернення значення.

У стрілочних функцій немає локальної змінної arguments, що містить усі аргументи. Якщо необхідно зібрати всі аргументи в масив, використовується операція rest.

-----МЕТОДИ МАР ТА FLATMAP-----

Функція з побічними ефектами — це функція, яка в процесі виконання може:
змінювати або використовувати глобальні змінні
змінювати значення аргументів посилального типу
виконувати операції введення-виведення тощо

Чиста функція (pure function) — це функція, результат якої залежить тільки від значень переданих аргументів. За умови однакових аргументів вона завжди повертає один і той самий результат і не має побічних ефектів, тобто не змінює значення аргументів.

Більшість із перебираючих методів масивів — це чисті функції.
Усі перебираючі методи масивів мають схожий синтаксис. На вихідному масиві array викликається перебираючий метод method , у який аргументом передається колбек-функція callback .

Метод map(callback) використовується для трансформації масиву. Він викликає колбек-функцію для кожного елемента вихідного масиву, а результат її роботи записує в новий масив, який і буде результатом виконання методу.
array.map((element, index, array) => {
// Тіло колбек-функції
});
Використовуючи метод map(), можна перебрати масив об'єктів, і в колбек-функції повернути значення властивості кожного з них.

Метод flatMap(callback) аналогічний методу map(), але застосовується у випадках, коли результат — це багатовимірний масив, який необхідно «розгладити».
Метод flatMap викликає колбек-функцію для кожного елемента вихідного масиву, а результат її роботи записує в новий масив. Відмінність від map() полягає в тому, що новий масив «розгладжується» на глибину, що дорівнює одиниці (одна вкладеність). Цей розгладжений (плоский) масив і є результатом роботи flatMap().

-----МЕТОДИ FILTER ТА FIND-----

Метод filter(callback) використовується для єдиної операції — фільтрації масиву. Під фільтрацією масиву мається на увазі відбір усіх елементів з колекції за певним критерієм.

Під час роботи з масивом об'єктів виконується фільтрація за значенням певної властивості. У підсумку утворюється новий масив відфільтрованих об'єктів.

Метод find(callback) дозволяє знайти і повернути перший відповідний елемент, що задовольняє умову, після чого перебирання масиву припиняється. Тобто він, на відміну від методу filter(callback), шукає до першого збігу.

-----МЕТОДИ EVERY, SOME I REDUCE-----

Метод every(callback) перевіряє, чи задовольняють усі елементи умову колбек-функції.
Під час роботи з масивом об'єктів перевіряється значення якоїсь їхньої властивості. Наприклад, перебираючи масив об'єктів товарів, ми можемо перевірити, чи всі товари є в наявності.

Метод some(callback) перевіряє, чи задовольняє хоча б один елемент умову колбек-функції.

Метод reduce(callback, initialValue) використовується для послідовної обробки кожного елемента масиву із збереженням проміжного результату.
Метод reduce() очікує 2 параметри:
1-й параметр (обов’язковий) — колбек-функція, яка "опрацьовує" кожен елемент масиву;
2-й параметр (не обов’язковий) — initialValue початкове значення акумулятора.

Колбек-функція з параметра редьюса очікує в свою чергу чотири параметри.
1-й параметр (previousValue) — це акумулятор, тобто проміжний результат. Значення, яке поверне колбек-функція на поточній ітерації, буде значенням цього параметра на наступній ітерації;
2-й параметр — поточний елемент масиву;
3-й параметр — індекс поточної ітерації;
4-й параметр — посилання на вихідний масив.

-----МЕТОД TOSORTED----

Метод toSorted() сортує елементи масиву.
Сортує вихідний масив
Повертає новий масив
За замовчуванням сортує за зростанням

Оскільки за замовчуванням перед сортуванням метод toSorted() приводить усі елементи масиву до рядків, то фактично елементи сортуються як рядки, тобто на основі їхніх значень у таблиці Unicode.

Масив рядків сортується за алфавітом. Водночас порядковий номер великих літер менший, ніж у малих.

Для зазначення свого порядку сортування методу toSorted(compareFunction) потрібно передати колбек-функцію з двома параметрами.
Це функція порівняння (compare function), порядок сортування залежить від її результату. Метод toSorted() буде викликати її для двох довільних елементів

Сортування за зростанням
const ascendingScores = scores.toSorted((a, b) => a - b);

Сортування за спаданням
const descendingScores = scores.toSorted((a, b) => b - a);

Для сортування рядків в алфавітному порядку, за зростанням або спаданням, використовується метод рядків localeCompare()

Під час роботи з масивом об'єктів сортування виконується за числовим або рядковим значенням певної властивості.
