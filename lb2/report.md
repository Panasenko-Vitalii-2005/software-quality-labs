# Лабораторна робота №2

## Проєктування тестів. Checklist, Test Cases та Decision Table

### Мета роботи

Навчитися визначати умови тестування на основі наданих вимог, формувати checklist, описувати детальні test cases, розрізняти позитивні та негативні перевірки, застосовувати Decision Table для систематизації комбінацій умов та фіксувати результати виконання тестів.

## Test Conditions

- TCND-01 — успішна авторизація валідного користувача;
- TCND-02 — авторизація з неправильним Username;
- TCND-03 — авторизація з неправильним Password;
- TCND-04 — авторизація з порожнім Username;
- TCND-05 — авторизація з порожнім Password;
- TCND-06 — авторизація заблокованого користувача.

## Checklist

- [ ] Успішна авторизація з валідними обліковими даними.
- [ ] Відхилення авторизації з неправильним Username.
- [ ] Відхилення авторизації з неправильним Password.
- [ ] Відхилення авторизації з порожнім Username та відображення повідомлення `Epic sadface: Username is required`.
- [ ] Відхилення авторизації з порожнім Password та відображення повідомлення `Epic sadface: Password is required`.
- [ ] Відхилення авторизації для заблокованого користувача та відображення повідомлення `Epic sadface: Sorry, this user has been locked out`.

## Test Cases

### TC-LOGIN-01

**Title:** Успішна авторизація standard_user

**Type:** Positive

**Preconditions:**

- Відкрита сторінка Login SauceDemo.
- Користувач не авторизований.

**Test Data:**

- Username: `standard_user`
- Password: `secret_sauce`

**Steps:**

1. У поле Username ввести `standard_user`.
2. У поле Password ввести `secret_sauce`.
3. Натиснути кнопку `Login`.

**Expected Result:**  
Після введення `standard_user` і правильного пароля та натискання `Login` користувач успішно авторизується і переходить на сторінку Products.

**Actual Result:**  
<img width="2048" height="941" alt="image" src="https://github.com/user-attachments/assets/d97aea15-c683-4370-bf70-ee1a9d62344c" />
Після введення `standard_user` і правильного пароля та натискання `Login` відкрилася сторінка Products.

**Result:** Pass

### TC-LOGIN-02

**Title:** Авторизація standard_user з неправильним паролем

**Type:** Negative

**Preconditions:**

- Відкрита сторінка Login SauceDemo.
- Користувач не авторизований.

**Test Data:**

- Username: `standard_user`
- Password: `wrong_password`

**Steps:**

1. У поле Username ввести `standard_user`.
2. У поле Password ввести `wrong_password`.
3. Натиснути кнопку `Login`.

**Expected Result:**  
Після введення `standard_user` і неправильного пароля `wrong_password` та натискання `Login` авторизація відхиляється і відображається повідомлення `Epic sadface: Username and password do not match any user in this service`.

**Actual Result:**  
<img width="1470" height="589" alt="image" src="https://github.com/user-attachments/assets/cf56004c-14e4-4b1b-96ae-9fb7e10dfbf1" />
Після введення `standard_user` і неправильного пароля `wrong_password` та натискання `Login` авторизацію відхилено і відображено повідомлення `Epic sadface: Username and password do not match any user in this service`.

**Result:** Pass

### TC-LOGIN-03

**Title:** Авторизація заблокованого користувача locked_out_user

**Type:** Negative

**Preconditions:**

- Відкрита сторінка Login SauceDemo.
- Користувач не авторизований.

**Test Data:**

- Username: `locked_out_user`
- Password: `secret_sauce`

**Steps:**

1. У поле Username ввести `locked_out_user`.
2. У поле Password ввести `secret_sauce`.
3. Натиснути кнопку `Login`.

**Expected Result:**  
Після введення `locked_out_user` і правильного пароля та натискання `Login` авторизація відхиляється і відображається повідомлення `Epic sadface: Sorry, this user has been locked out`.

**Actual Result:**  
<img width="1288" height="586" alt="image" src="https://github.com/user-attachments/assets/9c22624e-4763-4250-84b9-85672972dea4" />
Після введення `locked_out_user` і правильного пароля та натискання `Login` авторизацію відхилено і відображено повідомлення `Epic sadface: Sorry, this user has been locked out`.

**Result:** Pass

## Decision Table

Для перевірки комбінацій Username та Password використано Decision Table.

| Умова / Дія                                               | R1  | R2  | R3  | R4  | R5  |
| --------------------------------------------------------- | --- | --- | --- | --- | --- |
| Username входить до списку допустимих?                    | T   | T   | F   | T   | F   |
| Password правильний?                                      | T   | T   | T   | F   | F   |
| Користувач заблокований?                                  | F   | T   | -   | -   | -   |
| **A1: Перейти до Products**                               | X   |     |     |     |     |
| **A2: Показати повідомлення про блокування**              |     | X   |     |     |     |
| **A3: Показати повідомлення про неправильні credentials** |     |     | X   | X   | X   |

Позначення:

- `T` — True;
- `F` — False;
- `-` — значення не впливає на результат;
- `X` — дія, яка повинна виконатися.

### Покриття Decision Table тест-кейсами

- `TC-LOGIN-01` покриває правило **R1**.
- `TC-LOGIN-02` покриває правило **R4**.
- `TC-LOGIN-03` покриває правило **R2**.
- Правила **R3** та **R5** залишилися без окремих Test Cases.

## Результати виконання

| Test Case   | Type     | Result |
| ----------- | -------- | ------ |
| TC-LOGIN-01 | Positive | Pass   |
| TC-LOGIN-02 | Negative | Pass   |
| TC-LOGIN-03 | Negative | Pass   |

## Висновок

Під час виконання лабораторної роботи було визначено Test Conditions для функціональності Login, сформовано checklist, створено один позитивний та два негативні Test Cases і побудовано Decision Table для перевірки комбінацій облікових даних.

Усі три створені Test Cases було виконано в SauceDemo. Фактичні результати відповідали очікуваним, тому TC-LOGIN-01, TC-LOGIN-02 та TC-LOGIN-03 отримали результат Pass. За допомогою Decision Table також було визначено, що правила R3 та R5 не покриті окремими Test Cases.
