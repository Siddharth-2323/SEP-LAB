// ConversionLogic.java
import java.util.Scanner;

public class ConversionLogic {

    // Convert Binary to Decimal
    public int bintodec(String binary) {
        int decimal = 0;
        try {
            decimal = Integer.parseInt(binary, 2);
        } catch (NumberFormatException e) {
            System.out.println("Invalid binary input!");
        }
        return decimal;
    }

    // Convert Decimal to Binary
    public String dectobin(int decimal) {
        return Integer.toBinaryString(decimal);
    }

    // Convert Octal to Decimal
    public int octtodec(String octal) {
        int decimal = 0;
        try {
            decimal = Integer.parseInt(octal, 8);
        } catch (NumberFormatException e) {
            System.out.println("Invalid octal input!");
        }
        return decimal;
    }

    // Convert Decimal to Octal
    public String dectooct(int decimal) {
        return Integer.toOctalString(decimal);
    }

    // Main method for standalone testing
    public static void main(String[] args) {
        ConversionLogic cl = new ConversionLogic();
        Scanner sc = new Scanner(System.in);

        System.out.println("=== Number System Conversion Utility ===");
        System.out.println("1. Binary to Decimal");
        System.out.println("2. Decimal to Binary");
        System.out.println("3. Octal to Decimal");
        System.out.println("4. Decimal to Octal");
        System.out.print("Enter your choice: ");
        int choice = sc.nextInt();

        switch (choice) {
            case 1:
                System.out.print("Enter Binary Number: ");
                String binary = sc.next();
                System.out.println("Decimal Value: " + cl.bintodec(binary));
                break;
            case 2:
                System.out.print("Enter Decimal Number: ");
                int dec1 = sc.nextInt();
                System.out.println("Binary Value: " + cl.dectobin(dec1));
                break;
            case 3:
                System.out.print("Enter Octal Number: ");
                String oct = sc.next();
                System.out.println("Decimal Value: " + cl.octtodec(oct));
                break;
            case 4:
                System.out.print("Enter Decimal Number: ");
                int dec2 = sc.nextInt();
                System.out.println("Octal Value: " + cl.dectooct(dec2));
                break;
            default:
                System.out.println("Invalid choice!");
        }

        sc.close();
    }
}

// ConversionLogicTest.java
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

public class ConversionLogicTest {

    ConversionLogic cl = new ConversionLogic();

    @Test
    void testBinaryToDecimal() {
        assertEquals(10, cl.bintodec("1010"));
        assertEquals(0, cl.bintodec("abc")); // invalid binary input
    }

    @Test
    void testDecimalToBinary() {
        assertEquals("1111", cl.dectobin(15));
    }

    @Test
    void testOctalToDecimal() {
        assertEquals(15, cl.octtodec("17"));
        assertEquals(0, cl.octtodec("89")); // invalid octal input
    }

    @Test
    void testDecimalToOctal() {
        assertEquals("100", cl.dectooct(64));
    }
}
