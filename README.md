# goit-rdb-hw-04

DML та DDL команди. Складні SQL вирази:

### Завдання 1:

> Створіть базу даних для керування бібліотекою книг згідно зі структурою, наведеною нижче. Використовуйте DDL-команди для створення необхідних таблиць та їх зв'язків.

---

```sql
CREATE DATABASE LibraryManagement;
```

_p1_create_schema.png_
![p1_create_schema.png](./p1_create_schema.png)

---

```sql
CREATE TABLE authors (
    author_id INT AUTO_INCREMENT PRIMARY KEY,
    author_name VARCHAR(255)
);
CREATE TABLE genres (
    genre_id INT AUTO_INCREMENT PRIMARY KEY,
    genre_name VARCHAR(255)
);
CREATE TABLE books (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255),
    publication_year YEAR,
    author_id INT,
    genre_id INT,
    FOREIGN KEY (author_id) REFERENCES authors (author_id),
    FOREIGN KEY (genre_id) REFERENCES genres (genre_id)
);
CREATE TABLE users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255),
    email VARCHAR(255)
);
CREATE TABLE borrowed_books (
    borrow_id INT AUTO_INCREMENT PRIMARY KEY,
    book_id INT,
    user_id INT,
    borrow_date DATE,
    return_date DATE,
    FOREIGN KEY (book_id) REFERENCES books (book_id),
    FOREIGN KEY (user_id) REFERENCES users (user_id)
);
```

_p1_create_tables.png_
![p1_create_tables.png](./p1_create_tables.png)

---

### Завдання 2:

> Заповніть таблиці простими видуманими тестовими даними. Достатньо одного-двох рядків у кожну таблицю.

---

```sql
INSERT INTO authors (author_name) VALUES
('Тарас Шевченко'),
('Ліна Костенко'),
('Іван Франко');

INSERT INTO genres (genre_name) VALUES
('Поезія'),
('Проза'),
('Історичний роман');

INSERT INTO books (title, publication_year, author_id, genre_id) VALUES
('Кобзар', 1950, 1, 1),
('Маруся Чурай', 1979, 2, 3),
('Захар Беркут', 1983, 3, 2);

INSERT INTO users (username, email) VALUES
('ivan123', 'ivan@example.com'),
('olena456', 'olena@example.com'),
('petro789', 'petro@example.com');

INSERT INTO borrowed_books (book_id, user_id, borrow_date, return_date) VALUES
(1, 1, '2025-05-01', '2025-05-10'),
(2, 2, '2025-05-03', '2025-05-12'),
(3, 3, '2025-05-05', NULL);
```

_p2_adding_data.png_
![p2_adding_data.png](./p2_adding_data.png)

---

### Завдання 3:

> Перейдіть до бази даних, з якою працювали у темі 3. Напишіть запит за допомогою операторів FROM та INNER JOIN, що об'єднує всі таблиці даних, які ми завантажили з файлів: order_details, orders, customers, products, categories, employees, shippers, suppliers. Для цього ви маєте знайти спільні ключі.
>
> Перевірте правильність виконання запиту.

---

```sql
SELECT *
FROM order_details
INNER JOIN orders ON order_details.order_id = orders.id
INNER JOIN customers ON orders.customer_id = customers.id
INNER JOIN employees ON orders.employee_id = employees.employee_id
INNER JOIN shippers ON orders.shipper_id = shippers.id
INNER JOIN products ON order_details.product_id = products.id
INNER JOIN categories ON products.category_id = categories.id
INNER JOIN suppliers ON products.supplier_id = suppliers.id;
```

**Results:** [p3.csv](./p3.csv)

_p3_join.png_
![p3_join.png](./p3_join.png)

---
