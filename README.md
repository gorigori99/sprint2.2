Este proyecto tiene como objetivo limpiar y transformar datos de clientes, así como realizar análisis sobre sus hábitos de consumo para una tienda ficticia llamada **Store 1**. A lo largo de este proyecto, se aplicaron técnicas de limpieza de datos, análisis de gastos y creación de funciones automatizadas para la gestión de la información.

---

## ✅ **Paso 1: Limpieza de datos de un cliente**

Se crea una función `clean_user()` que:

- Elimina espacios y guiones bajos del nombre.
- Convierte la edad a número entero.
- Separa nombre y apellido en una sublista.

```python
def clean_user(user_info, user_name_index, user_age_index):
    user_name_1 = user_info[user_name_index].strip().lower().replace('_',' ')
    user_age_1 = int(user_info[user_age_index])
    user_name_1 = user_name_1.split()
    user_info[user_name_index] = user_name_1
    user_info[user_age_index] = user_age_1
    return user_info
🔡 Paso 2: Transformar categorías favoritas a minúsculas
Convertimos todas las categorías a minúsculas en una nueva lista.

python
Copy code
fav_categories = ['ELECTRONICS', 'SPORT', 'BOOKS']
fav_categories_low = []

for element in fav_categories:
    fav_categories_low.append(element.lower())

print(fav_categories_low)
👥 Paso 3: Aplicar conversión de categorías a todos los usuarios
Aplicamos el mismo proceso a la lista users.

python
Copy code
users_categories_low = []
for user in users:
    categories_low = []
    for category in user[3]:
        categories_low.append(category.lower())
    user[3] = categories_low
    users_categories_low.append(user)
🧹 Paso 4: Limpieza completa de cada usuario
La función clean_user se mejora para incluir también la limpieza de categorías favoritas.

python
Copy code
def clean_user(user_info, name_index, age_index, cat_index):
    user_name_1 = user_info[name_index].strip().replace('_',' ').lower().split()
    user_age_1 = int(user_info[age_index])
    categories = [category.lower() for category in user_info[cat_index]]
    user_info[name_index] = user_name_1
    user_info[age_index] = user_age_1
    user_info[cat_index] = categories
    return user_info
Se aplica la función a todos los usuarios:

python
Copy code
users_cleaned = []
for user in users:
    user_cleaned = clean_user(user, 1, 2, 3)
    users_cleaned.append(user_cleaned)
💰 Paso 5: Calcular ingresos totales
Se calcula el ingreso total sumando los gastos de todos los usuarios.

python
Copy code
revenue = 0
for user in users:
    spending_list = user[4]
    total_spendings = sum(spending_list)
    revenue += total_spendings

print(revenue)  # Resultado: 9189
🎯 Paso 6: Simular compras hasta llegar a una meta
Se simulan compras aleatorias hasta alcanzar un objetivo de gasto ($1500).

python
Copy code
from random import randint

total_amount_spent = 1280
target_amount = 1500

while total_amount_spent < target_amount:
    new_purchase = randint(30, 80)
    total_amount_spent += new_purchase

print(total_amount_spent)
👶 Paso 7: Mostrar clientes menores de 30 años
python
Copy code
for user in users:
    if user[2] < 30:
        print(user[1])
👕 Paso 8: Clientes menores de 30 con gastos superiores a $1000
python
Copy code
for user in users:
    if user[2] < 30 and sum(user[4]) >= 1000:
        print(user[1])
🧾 Paso 9: Mostrar nombre y edad de usuarios que compraron ropa (clothes)
python
Copy code
for user in users:
    if 'clothes' in user[3]:
        print(user[1], user[2])
📋 Paso 10: Función para obtener clientes por categoría
Función que filtra usuarios por categoría de compra y devuelve su ID, nombre, edad y gasto total.

python
Copy code
def get_client_by_cat(users, id_index, name_index, age_index, category_index, amounts_index, filter_category):
    result = []
    for user in users:
        if filter_category in user[category_index]:
            total_spent = sum(user[amounts_index])
            result.append([user[id_index], user[name_index], user[age_index], total_spent])
    return result
Ejemplo de uso:

python
Copy code
result = get_client_by_cat(users, 0, 1, 2, 3, 4, 'home')
for element in result:
    print(element)
## Conclusión
Este proyecto permitió aplicar técnicas fundamentales de limpieza y análisis de datos en Python, manipulando listas anidadas, estructuras condicionales, bucles y funciones. El resultado es un sistema más limpio y organizado para el análisis de usuarios, con potencial para extenderlo a visualizaciones o modelos predictivos.
