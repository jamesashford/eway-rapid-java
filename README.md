# eWAY Rapid Java Library

[![Latest version on Maven Central][ico-version]][link-maven]
[![Software License][ico-license]](LICENSE.md)
[![Build Status][ico-travis]][link-travis]

A Java library to integrate with eWAY's Rapid Payment API.

Sign up with eWAY at:
 - Australia:    https://www.eway.com.au/
 - New Zealand:  https://eway.io/nz/
 - Hong Kong:    https://eway.io/hk/
 - Malaysia:     https://eway.io/my/
 - Singapore:    https://eway.io/sg/

For testing, get a free eWAY Partner account: https://www.eway.com.au/developers

## Install

### Include with Maven

The eWAY Rapid Java library can be easily added to your Maven project's pom.xml:

```xml
    <dependency>
      <groupId>com.ewaypayments</groupId>
      <artifactId>eway-rapid-java</artifactId>
      <version>1.3.0</version>
    </dependency>
```

### Building

The eWAY Rapid Java library can also be built with Maven. To do so:

 1. Clone the eWAY Rapid GitHub project or download the zip
 2. Navigate to the folder with the pom.xml file and run
```bash
$ mvn package
```
 3. The compiled jar file will be in the "target" directory

## Usage

See the [eWAY Rapid API Reference](https://eway.io/api-v3/) for usage details.

A simple Direct payment example:

```java
import com.eway.payment.rapid.sdk.*;
import com.eway.payment.rapid.sdk.beans.external.*;
import com.eway.payment.rapid.sdk.output.*;

public class EwayRapid {
    public static void main(String[] args) {
        String apiKey = "Rapid API Key";
        String password = "Rapid API Password";
        String rapidEndpoint = "Sandbox";

        RapidClient client = RapidSDK.newRapidClient(apiKey, password, rapidEndpoint);

        CardDetails cardDetails = new CardDetails();
        cardDetails.setName("John Smith");
        cardDetails.setNumber("4444333322221111");
        cardDetails.setExpiryMonth("12");
        cardDetails.setExpiryYear("25");
        cardDetails.setCVN("123");

        Customer customer = new Customer();
        customer.setCardDetails(cardDetails);

        PaymentDetails paymentDetails = new PaymentDetails();
        paymentDetails.setTotalAmount(1000);

        Transaction transaction = new Transaction();
        transaction.setCustomer(customer);
        transaction.setPaymentDetails(paymentDetails);
        transaction.setTransactionType(TransactionType.Purchase);

        PaymentMethod method = PaymentMethod.Direct;
        CreateTransactionResponse response = client.create(method, transaction);

        if (response.getTransactionStatus().isStatus()) {
            System.out.println("Transaction successful! ID: " + response.getTransactionStatus().getTransactionID());
        }
    }
}
```

## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Testing

Tests are written with JUnit and can be run using Maven:

```bash
$ mvn test
```

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

[ico-version]: https://img.shields.io/maven-central/v/com.ewaypayments/eway-rapid-java.svg?style=flat-square
[ico-license]: https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square
[ico-travis]: https://img.shields.io/travis/eWAYPayment/eway-rapid-java/master.svg?style=flat-square

[link-maven]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22eway-rapid-java%22
[link-travis]: https://travis-ci.org/eWAYPayment/eway-rapid-java
