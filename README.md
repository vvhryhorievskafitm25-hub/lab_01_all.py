import timeit
from collections import namedtuple


# ============================================================
# ЗАВДАННЯ 1. СПИСКИ: ІНДЕКСАЦІЯ, ЗРІЗИ ТА МУТАЦІЇ
# ============================================================

def task_1_lists():
    print("\n" + "=" * 65)
    print("ЗАВДАННЯ 1. СПИСКИ")
    print("=" * 65)

    # Початковий список цілих чисел
    numbers = [10, 20, 30, 40, 50, 60, 70, 80]

    print("Початковий список:", numbers)

    # Додатна та від'ємна індексація
    print("\nІндексація:")
    print("Елемент з індексом 0:", numbers[0])
    print("Елемент з індексом 3:", numbers[3])
    print("Останній елемент:", numbers[-1])
    print("Передостанній елемент:", numbers[-2])

    # Три різні зрізи
    print("\nЗрізи списку:")
    print("Перші чотири елементи:", numbers[:4])
    print("Елементи з індексів 2 до 6:", numbers[2:6])
    print("Кожен другий елемент:", numbers[::2])
    print("Список у зворотному порядку:", numbers[::-1])

    # Мутація 1 — додавання елемента
    print("\nМутація 1 — додавання елемента:")
    numbers.append(90)
    print("Після append(90):", numbers)

    # Мутація 2 — вставлення елемента
    print("\nМутація 2 — вставлення елемента:")
    numbers.insert(2, 25)
    print("Після insert(2, 25):", numbers)

    # Мутація 3 — видалення елемента
    print("\nМутація 3 — видалення елемента:")
    numbers.pop(4)
    print("Після pop(4):", numbers)

    # Створення нового списку через зріз
    copied_numbers = numbers[:]
    print("\nКопія списку через зріз:", copied_numbers)

    print("Фінальний список:", numbers)
    print("Довжина фінального списку:", len(numbers))


# ============================================================
# ЗАВДАННЯ 2. КОРТЕЖІ ТА РОЗПАКУВАННЯ ДАНИХ
# ============================================================

def task_2_tuples():
    print("\n" + "=" * 65)
    print("ЗАВДАННЯ 2. КОРТЕЖІ")
    print("=" * 65)

    # Кортежі моделюють записи товарів:
    # (ідентифікатор, назва, кількість, ціна)

    products = [
        (1, "Ноутбук", 2, 25000.0),
        (2, "Миша", 5, 500.0),
        (3, "Клавіатура", 3, 1200.0)
    ]

    # Функція розпакування одного кортежу
    def show_product(product):
        product_id, name, quantity, price = product

        print(
            f"ID: {product_id}, "
            f"Назва: {name}, "
            f"Кількість: {quantity}, "
            f"Ціна: {price:.2f} грн"
        )

    # Функція обчислення загальної вартості
    def calculate_total(items):
        total = 0

        for product_id, name, quantity, price in items:
            total += quantity * price

        return total

    print("\nСписок товарів:")
    for product in products:
        show_product(product)

    total_price = calculate_total(products)

    print(f"\nЗагальна вартість товарів: {total_price:.2f} грн")

    # Демонстрація незмінності кортежу
    print("\nПеревірка незмінності кортежу:")

    example = (10, 20, 30)

    try:
        example[0] = 100
    except TypeError as error:
        print("Помилка при зміні кортежу:", error)

    # Кортеж із вкладеним змінюваним списком
    print("\nКортеж із вкладеним списком:")

    student = ("Вікторія", [90, 85, 95])

    print("До зміни:", student)

    student[1].append(100)

    print("Після зміни вкладеного списку:", student)


# ============================================================
# ЗАВДАННЯ 3. СЛОВНИКИ ТА ОБЛІК ЧАСТОТ
# ============================================================

def task_3_dictionaries():
    print("\n" + "=" * 65)
    print("ЗАВДАННЯ 3. СЛОВНИКИ")
    print("=" * 65)

    # Текст для аналізу
    text = """
    Python — популярна мова програмування.
    Python використовується для розробки програм,
    аналізу даних та автоматизації.
    """

    # Нормалізація тексту
    text = text.lower()

    for symbol in ",.!?;:-—":
        text = text.replace(symbol, "")

    # Розбиття тексту на слова
    words = text.split()

    print("Текст для аналізу:")
    print(text)

    # Створення словника частот
    frequency = {}

    for word in words:
        frequency[word] = frequency.get(word, 0) + 1

    print("\nКількість появ кожного слова:")

    # Сортування за ключем
    for word in sorted(frequency):
        print(f"{word}: {frequency[word]}")

    # Сортування за спаданням частоти
    print("\nСортування за спаданням частоти:")

    sorted_frequency = sorted(
        frequency.items(),
        key=lambda item: (-item[1], item[0])
    )

    for word, count in sorted_frequency:
        print(f"{word}: {count}")

    # Безпечне отримання значення
    print("\nБезпечний доступ до словника:")

    print("Частота слова 'python':", frequency.get("python", 0))
    print("Частота слова 'комп'ютер':", frequency.get("комп'ютер", 0))

    # Dict comprehension — слова, які зустрічаються більше одного разу
    repeated_words = {
        word: count
        for word, count in frequency.items()
        if count > 1
    }

    print("\nСлова з частотою більше одного:")
    print(repeated_words)


# ============================================================
# ЗАВДАННЯ 4. МНОЖИНИ: УНІКАЛЬНІСТЬ ТА ОПЕРАЦІЇ
# ============================================================

def task_4_sets():
    print("\n" + "=" * 65)
    print("ЗАВДАННЯ 4. МНОЖИНИ")
    print("=" * 65)

    # Початкові колекції з повтореннями
    group_a = [101, 102, 103, 104, 104, 105, 105]
    group_b = [103, 104, 105, 106, 106, 107]

    # Перетворення списків на множини
    set_a = set(group_a)
    set_b = set(group_b)

    print("Початкова колекція A:", group_a)
    print("Початкова колекція B:", group_b)

    print("\nМножина A:", sorted(set_a))
    print("Множина B:", sorted(set_b))

    # Перетин
    print("\nПеретин множин:")
    print(sorted(set_a & set_b))

    # Об'єднання
    print("\nОб'єднання множин:")
    print(sorted(set_a | set_b))

    # Симетрична різниця
    print("\nСиметрична різниця:")
    print(sorted(set_a ^ set_b))

    # Перевірка підмножини
    print("\nПеревірка підмножин:")

    print(
        "{103, 104} є підмножиною A:",
        {103, 104} <= set_a
    )

    print(
        "{101, 999} є підмножиною A:",
        {101, 999} <= set_a
    )

    # Демонстрація frozenset
    print("\nДемонстрація frozenset:")

    frozen = frozenset([1, 2, 3])
    frozen_dict = {frozen: "Незмінний набір"}

    print("Незмінна множина:", frozen)
    print("Використання frozenset як ключа:", frozen_dict)


# ============================================================
# ЗАВДАННЯ 5. АЛГОРИТМІЧНА СКЛАДНІСТЬ І TIMEIT
# ============================================================

def task_5_performance():
    print("\n" + "=" * 65)
    print("ЗАВДАННЯ 5. ДОСЛІДЖЕННЯ ПРОДУКТИВНОСТІ")
    print("=" * 65)

    # Три різні розміри тестових наборів
    sizes = [300, 3000, 30000]

    print(
        f"\n{'n':>8} | {'list search':>14} | "
        f"{'set search':>14} | {'dict search':>14}"
    )
    print("-" * 65)

    for n in sizes:
        # Дані створюються детерміновано
        data = [i % 1000 for i in range(n)]

        data_list = data
        data_set = set(data)
        data_dict = {value: True for value in data_set}

        # Шукаємо останній елемент списку
        target = data[-1]

        # Вимірювання пошуку у списку
        list_timer = timeit.Timer(
            lambda: target in data_list
        )

        # Вимірювання пошуку у множині
        set_timer = timeit.Timer(
            lambda: target in data_set
        )

        # Вимірювання пошуку ключа у словнику
        dict_timer = timeit.Timer(
            lambda: target in data_dict
        )

        # Три повтори, результат — середній час у мілісекундах
        list_time = min(list_timer.repeat(repeat=3, number=1000)) / 1000 * 1000
        set_time = min(set_timer.repeat(repeat=3, number=1000)) / 1000 * 1000
        dict_time = min(dict_timer.repeat(repeat=3, number=1000)) / 1000 * 1000

        print(
            f"{n:>8} | {list_time:>14.6f} | "
            f"{set_time:>14.6f} | {dict_time:>14.6f}"
        )

    # Порівняння побудови унікальних значень
    print("\nПобудова унікальних значень:")

    print(
        f"\n{'n':>8} | {'list method (ms)':>18} | "
        f"{'set method (ms)':>18}"
    )
    print("-" * 55)

    for n in sizes:
        data = [i % 1000 for i in range(n)]

        def unique_with_list():
            result = []

            for item in data:
                if item not in result:
                    result.append(item)

            return result

        def unique_with_set():
            result = set()

            for item in data:
                result.add(item)

            return result

        list_build_timer = timeit.Timer(unique_with_list)
        set_build_timer = timeit.Timer(unique_with_set)

        # Кілька повторів; обираємо найкращий результат
        list_build_time = min(
            list_build_timer.repeat(repeat=3, number=1)
        ) * 1000

        set_build_time = min(
            set_build_timer.repeat(repeat=3, number=1)
        ) * 1000

        print(
            f"{n:>8} | {list_build_time:>18.4f} | "
            f"{set_build_time:>18.4f}"
        )

    print("\nЕксперимент завершено.")
    print("Час вимірювання залежить від характеристик комп'ютера.")


def main():
    print("=" * 65)
    print("ЛАБОРАТОРНА РОБОТА №1")
    print("Структури даних у Python")
    print("=" * 65)

    task_1_lists()
    task_2_tuples()
    task_3_dictionaries()
    task_4_sets()
    task_5_performance()

    print("\n" + "=" * 65)
    print("УСІ П'ЯТЬ ЗАВДАНЬ УСПІШНО ВИКОНАНО!")
    print("=" * 65)


if __name__ == "__main__":
    main()
