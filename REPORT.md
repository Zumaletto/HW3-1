# Отчёт о тестировании  Credit Card Number Validator

## Краткое описание

08.08.2021 было проведена проверка области эквивалентных значений номер разных банковских карт, вводимых в поле "номер карты" кода при помощи IntelliJ IDEA

На тестирование затрачено: 4 часа 30 минут

В результате тестирования выявлены следующие дефекты:
* [Не прошли валидацию номера карт Visa](https://github.com/Zumaletto/HW3-1/issues/1)
* [Не прошли валидацию номера карт American Express](https://github.com/Zumaletto/HW3-1/issues/2)
* [Не прошли валидацию номера карт Discover](https://github.com/Zumaletto/HW3-1/issues/3)
* [Не прошли валидацию номера карт JSB](https://github.com/Zumaletto/HW3-1/issues/4)

## Описание процесса тестирования

В процессе тестирования использовались следующие артефакты:
* Часть кода:
```java
public class Main {
  public static void main(String[] args) {
    // TODO: подставлять номер карты нужно сюда между двойными кавычками, без пробелов
    String number = "5351719427810741";
    System.out.println(String.format("Result is %s", isValidCardNumber(number) ? "OK" : "FAIL"));
  }

  public static boolean isValidCardNumber(String number) {
    if (number == null) {
      return false;
    }

    if (number.length() != 16) {
      return false;
    }

    long result = 0;
    for (int i = 0; i < number.length(); i++) {
      int digit;
      try {
        digit = Integer.parseInt(number.charAt(i) + "");
      } catch (NumberFormatException e) {
        return false;
      }

      if (i % 2 == 0) {
        digit *= 2;
        if (digit > 9) {
          digit -= 9;
        }
      }
      result += digit;
    }

    return (result != 0) && (result % 10 == 0);
  }
}
```
* [чек лист](https://docs.google.com/spreadsheets/d/1havtTzycP32JXS4J5ANKa2nhsGBDnsEKH_QKTfgGdSk/edit?usp=sharing)
* [сайт-генератор номеров кредитных карт](https://cardguru.io/)

В качестве тестовых данных использовались данные с сайтов:
* https://www.businessyeti.com/Apps/CreditCardGenerator/
* https://www.freeformatter.com/credit-card-number-generator-validator.html

Тестирование производилось в следующем окружении:
* Windows 10 домашняя версия 20H
* версия Java 11.0.11
