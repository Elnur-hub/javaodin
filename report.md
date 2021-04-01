# Отчет о тестировании приложения Credit Card Number Validator

31.03.2021 было проведено функциональное тестирование приложения Credit Card Number Validator
На тестирование затрачено: 1 час

В результате тестирования выявлены следующие дефекты:
* Приложение не реагирует на значения больше или меньше 16 символов. [скриншот] (https://sun9-9.userapi.com/impf/DmFA7Mgv4tE_5eqXfN4GtbdaejfiI401ti08ow/Z2iOMuEyNgo.jpg?size=916x398&quality=96&sign=fb262a847f87c2ece1aa04d79e4a3d42&type=album)

## Описание процесса тестирования

В процессе тестирования использовались следующие артефакты:

*Тестовый сценарий:

1. Использовать представленный ниже код
2. Ввести в строке #4 числа, сгенерированные сайтом [freeformatter](https://www.freeformatter.com/credit-card-number-generator-validator.html), подставлять номера банковских карт JCB,American Express, Diners CLub-International 
3. Воспроизвести код нажатием на кнопку Run или CTRL+SHIFT+F10
4. Зафиксировать результаты проведенных запусков 

Код:

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

В качестве тестовых данных использовались данные сайта-генератора банковских карт [freeformatter](https://www.freeformatter.com/credit-card-number-generator-validator.html):
*American Express 370085890868840
*JCB 3535650149078171279
*Diners Club - International 36558770958085

Тестирование производилось в следующем окружении:
* Windows 10 Home 64-bit
* Java 11.0.10+9
* IntelliJ IDEA Community Edition 2020.3.3