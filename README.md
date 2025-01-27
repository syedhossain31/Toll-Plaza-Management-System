import java.util.ArrayList;
import java.util.Scanner;

class Vehicle {
    private String registrationNumber;
    private String vehicleType;

    public Vehicle(String registrationNumber, String vehicleType) {
        this.registrationNumber = registrationNumber;
        this.vehicleType = vehicleType;
    }

    public String getRegistrationNumber() {
        return registrationNumber;
    }

    public String getVehicleType() {
        return vehicleType;
    }
}

class TollPlaza {
    private ArrayList<Vehicle> vehicles;
    private double totalRevenue;

    public TollPlaza() {
        vehicles = new ArrayList<>();
        totalRevenue = 0;
    }

    public void registerVehicle(String registrationNumber, String vehicleType) {
        Vehicle vehicle = new Vehicle(registrationNumber, vehicleType);
        vehicles.add(vehicle);
        System.out.println("Vehicle registered successfully!");
    }

    public double calculateToll(String vehicleType) {
        switch (vehicleType.toLowerCase()) {
            case "car":
                return 50.0;
            case "truck":
                return 100.0;
            case "bus":
                return 80.0;
            case "bike":
                return 20.0;
            default:
                return 0.0;
        }
    }

    public void processPayment(String registrationNumber) {
        for (Vehicle vehicle : vehicles) {
            if (vehicle.getRegistrationNumber().equals(registrationNumber)) {
                double toll = calculateToll(vehicle.getVehicleType());
                if (toll > 0) {
                    totalRevenue += toll;
                    System.out.println("Toll paid: $" + toll);
                } else {
                    System.out.println("Invalid vehicle type!");
                }
                return;
            }
        }
        System.out.println("Vehicle not found!");
    }

    public void generateReport() {
        System.out.println("\n--- Daily Report ---");
        System.out.println("Total vehicles processed: " + vehicles.size());
        System.out.println("Total revenue collected: $" + totalRevenue);
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        TollPlaza tollPlaza = new TollPlaza();

        while (true) {
            System.out.println("\n--- Toll Plaza Management System ---");
            System.out.println("1. Register Vehicle");
            System.out.println("2. Process Toll Payment");
            System.out.println("3. Generate Report");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter registration number: ");
                    String regNo = scanner.next();
                    System.out.print("Enter vehicle type (car, truck, bus, bike): ");
                    String type = scanner.next();
                    tollPlaza.registerVehicle(regNo, type);
                    break;
                case 2:
                    System.out.print("Enter registration number: ");
                    String regNumber = scanner.next();
                    tollPlaza.processPayment(regNumber);
                    break;
                case 3:
                    tollPlaza.generateReport();
                    break;
                case 4:
                    System.out.println("Exiting...");
                    scanner.close();
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid choice! Please try again.");
            }
        }
    }
}
