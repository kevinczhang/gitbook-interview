---
description: Design a parking lot using object-oriented principles.
---

# Parking Lot

The wording of this question is vague, just as it would be in an actual interview. This requires you to have a conversation with your interviewer about what types of vehicles it can support, whether the parking lot has multiple levels, and so on.&#x20;

For our purposes right now, we'll make the following assumptions. We made these specific assumptions to add a bit of complexity to the problem without adding too much. If you made different assumptions, that's totally fine.

* The parking lot has multiple levels. Each level has multiple rows of spots.
* The parking lot can park motorcycles, cars, and buses.
* The parking lot has motorcycle spots, compact spots, and large spots.
* A motorcycle can park in any spot.
* A car can park in either a single compact spot or a single large spot.
* A bus can park in five large spots that are consecutive and within the same row. it cannot park in small spots.

In the below implementation, we have created an abstract class Vehicle, from which Car, Bus, and Motorcycle inherit. To handle the different parking spot sizes, we have just one class Parking Spot which has a member variable indicating the size.

```java
public enum VehicleSize { Motorcycle, Compact, Large }

public abstract class Vehicle {
    protected ArrayList<ParkingSpot> parkingSpots = new ArrayList<ParkingSpot>();
    protected String licensePlate;
    protected int spotsNeeded;
    protected VehicleSize size;

    public int getSpotsNeeded() { return spotsNeeded; }
    public VehicleSize getSize{} { return size; }

    /* Park vehicle in this spot (among others, potentially) */
    public void parkInSpot(ParkingSpot s) { parkingSpots.add(s); )

    /* Remove car from spot, and notify spot that it's gone */
    public void clearSpotsQ { ... }

    /* Checks if the spot is big enough for the vehicle (and is available). This
    * compares the SIZE only. It does not check if it has enough spots. */
    public abstract boolean canFitInSpot(ParkingSpot spot);
}

public class Bus extends Vehicle {
    public Bus() {
        spotsNeeded = 5;
        size = VehicleSize.Large;
    }

    /* Checks if the spot is a Large. Doesn't check num of spots */
    public boolean canFitInSpot(ParkingSpot spot) { ... }
}

public class Car extends Vehicle {
    public Car() {
        spotsNeeded = 1;
        size = VehicleSize.Compact;
    }

    /* Checks if the spot is a Compact or a Large. */
    public boolean canFitInSpot(ParkingSpot spot) { ... }
}

public class Motorcycle extends Vehicle {
    public Motorcycle() {
        spotsNeeded = 1;
        size = VehicleSize.Motorcycle;
    }

    public boolean canFitInSpot(ParkingSpot spot) { ... }
}
```

The Parking Lot class is essentially a wrapper class for an array of Levels. By implementing it this way, we are able to separate out logic that deals with actually finding free spots and parking cars out from the broader actions of the Parking Lot. If we didn’t do it this way, we would need to hold parking spots in some sort of double array (or hash table which maps from a level number to the list of spots). It's cleaner to just separate Parking Lot from Level.

```java
public class ParkingLot {
    private Level[ ] levels;
    private final int NUM_LEVELS = 5;

    public ParkingLot() { ... }

    /* Park the vehicle in a spot (or multiple spots).
    * Return false if failed. */
    public boolean parkVehicle(Vehicle vehicle) { ... }
}

/* Represents a level in a parking garage */
public class Level {
    private int floor;
    private ParkingSpot[ ] spots;
    private int availableSpots = 0; // number of free spots
    private static final int SPOTS_PER_ROW = 10;

    public Level(int flr, int numberSpots) { ... }

    public int availableSpots() { return availableSpots; }

    /* Find a place to park this vehicle. Return false if failed. */
    public boolean parkVehicle(Vehicle vehicle) { ... }

    /* Park a vehicle starting at the spot spotNumber, and
    * continuing until vehicle.spotsNeeded. */
    private boolean parkStartingAtSpot(int num, Vehicle v) { ... }

    /* Find a spot to park this vehicle. Return index of spot, or -1
    * on failure. */
    private int findAvailableSpots(Vehicle vehicle) { ... }

    /* When a car was removed from the spot, increment
    * availableSpots */
    public void spotFreed() { availableSpots++; }
}
```

The parking Spot is implemented by having just a variable which represents the size of the spot. We could have implemented this by having classes for Large Spot, Compact Spot, and Motorcycle Spot which inherit from Parking Spot, but this is probably overkill. The spots probably do not have different behaviors, other than their sizes.

```java
public class ParkingSpot {
    private Vehicle vehicle;
    private VehicleSize spotSize;
    private int row;
    private int spotNumber;
    private Level level;

    public ParkingSpot(Level Ivl, int r, int n, VehicleSize s) {...}

    public boolean isAvailable() { return vehicle == null; }

    /* Check if the spot is big enough and is available */
    public boolean canFitVehicle(Vehicle vehicle) { ... }

    /* Park vehicle in this spot. */
    public boolean park(Vehicle v) { ... }

    public int getRow() { return row; }
    public int getSpotNumber() { return spotNumber; }

    /* Remove vehicle from spot, and notify level that a new spot is
    * available */
    public void removeVehicle() { ... }
}
```

