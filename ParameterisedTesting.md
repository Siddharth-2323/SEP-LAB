// TicketReservation.java
import java.util.Scanner;

public class TicketReservation {
    private String train_name;
    private String date;
    private int no_of_passengers;
    private String booking_class;
    private double amount;

    // Method to read reservation details
    public void read_details() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter Train Name: ");
        train_name = sc.nextLine();

        System.out.print("Enter Date (DD/MM/YYYY): ");
        date = sc.nextLine();

        System.out.print("Enter Number of Passengers: ");
        no_of_passengers = sc.nextInt();
        sc.nextLine(); // consume newline

        System.out.print("Enter Booking Class (Tier 1 AC / Tier 1 Non-AC / Tier 2 AC / Tier 2 Non-AC / Coupe): ");
        booking_class = sc.nextLine();

        calculate_amount();
        sc.close();
    }

    // Method to calculate total amount based on booking class
    public void calculate_amount() {
        if (booking_class.equalsIgnoreCase("Tier 1 AC")) {
            amount = 1500 * no_of_passengers;
        } else if (booking_class.equalsIgnoreCase("Tier 1 Non-AC")) {
            amount = 1250 * no_of_passengers;
        } else if (booking_class.equalsIgnoreCase("Tier 2 AC")) {
            amount = 1000 * no_of_passengers;
        } else if (booking_class.equalsIgnoreCase("Tier 2 Non-AC")) {
            amount = 750 * no_of_passengers;
        } else if (booking_class.equalsIgnoreCase("Coupe")) {
            amount = 500 * no_of_passengers;
        } else {
            amount = 0; // default case for invalid input
        }
    }

    // Method to display reservation details
    public void disp_details() {
        System.out.println("\n--- Reservation Details ---");
        System.out.println("Train Name     : " + train_name);
        System.out.println("Date           : " + date);
        System.out.println("Booking Class  : " + booking_class);
        System.out.println("No. of Passengers: " + no_of_passengers);
        System.out.println("Total Amount   : Rs." + amount);
    }

    // Setters and Getters (used for testing)
    public void setTrainName(String train_name) {
        this.train_name = train_name;
    }

    public void setDate(String date) {
        this.date = date;
    }

    public void setNoOfPassengers(int no_of_passengers) {
        this.no_of_passengers = no_of_passengers;
    }

    public void setBookingClass(String booking_class) {
        this.booking_class = booking_class;
    }

    public double getAmount() {
        return amount;
    }

    public String getBookingClass() {
        return booking_class;
    }
}

// TicketReservationTest.java
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

public class TicketReservationTest {

    @Test
    void testCalculateAmount_Tier1AC() {
        TicketReservation t = new TicketReservation();
        t.setNoOfPassengers(2);
        t.setBookingClass("Tier 1 AC");
        t.calculate_amount();
        assertEquals(3000, t.getAmount());
    }

    @Test
    void testCalculateAmount_Tier1NonAC() {
        TicketReservation t = new TicketReservation();
        t.setNoOfPassengers(3);
        t.setBookingClass("Tier 1 Non-AC");
        t.calculate_amount();
        assertEquals(3750, t.getAmount());
    }

    @Test
    void testCalculateAmount_Tier2AC() {
        TicketReservation t = new TicketReservation();
        t.setNoOfPassengers(1);
        t.setBookingClass("Tier 2 AC");
        t.calculate_amount();
        assertEquals(1000, t.getAmount());
    }

    @Test
    void testCalculateAmount_Tier2NonAC() {
        TicketReservation t = new TicketReservation();
        t.setNoOfPassengers(4);
        t.setBookingClass("Tier 2 Non-AC");
        t.calculate_amount();
        assertEquals(3000, t.getAmount());
    }

    @Test
    void testCalculateAmount_Coupe() {
        TicketReservation t = new TicketReservation();
        t.setNoOfPassengers(5);
        t.setBookingClass("Coupe");
        t.calculate_amount();
        assertEquals(2500, t.getAmount());
    }

    @Test
    void testCalculateAmount_InvalidClass() {
        TicketReservation t = new TicketReservation();
        t.setNoOfPassengers(2);
        t.setBookingClass("Luxury Sleeper");
        t.calculate_amount();
        assertEquals(0, t.getAmount());
    }

    @Test
    void testDisplayDetails() {
        TicketReservation t = new TicketReservation();
        t.setTrainName("Chennai Express");
        t.setDate("26/10/2025");
        t.setNoOfPassengers(2);
        t.setBookingClass("Tier 1 AC");
        t.calculate_amount();
        t.disp_details(); // ensures display method executes
        assertEquals("Tier 1 AC", t.getBookingClass());
    }
}
