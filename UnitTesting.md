// Weather.java
import java.util.Scanner;

public class Weather {
    private float temperature;
    private String result;

    // Reads temperature from user
    public void read() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter temperature in Celsius: ");
        temperature = sc.nextFloat();
        sc.close();
    }

    // Compute weather message based on temperature
    public void compute() {
        if (temperature < 0)
            result = "Freezing weather";
        else if (temperature >= 0 && temperature < 10)
            result = "Very Cold weather";
        else if (temperature >= 10 && temperature < 20)
            result = "Cold weather";
        else if (temperature >= 20 && temperature < 30)
            result = "Normal in Temp";
        else if (temperature >= 30 && temperature < 40)
            result = "Its Hot";
        else
            result = "Its Very Hot";
    }

    // Display the result
    public void display() {
        System.out.println(result);
    }

    // Setter and Getter for testing
    public void setTemperature(float temperature) {
        this.temperature = temperature;
    }

    public String getResult() {
        return result;
    }
}

// WeatherTest.java
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvSource;
import org.junit.jupiter.params.provider.CsvFileSource;

public class WeatherTest {

    // Test using inline CSV data
    @ParameterizedTest
    @CsvSource({
        "-5, Freezing weather",
        "5, Very Cold weather",
        "15, Cold weather",
        "25, Normal in Temp",
        "35, Its Hot",
        "45, Its Very Hot"
    })
    void testComputeUsingCsvSource(float temp, String expected) {
        Weather w = new Weather();
        w.setTemperature(temp);
        w.compute();
        assertEquals(expected, w.getResult());
    }

    // Test using external CSV file (weather_data.csv)
    @ParameterizedTest
    @CsvFileSource(resources = "/weather_data.csv", numLinesToSkip = 1)
    void testComputeUsingCsvFile(float temp, String expected) {
        Weather w = new Weather();
        w.setTemperature(temp);
        w.compute();
        assertEquals(expected, w.getResult());
    }
}
