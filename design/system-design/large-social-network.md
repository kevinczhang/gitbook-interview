# Large social network

How would you design the data structures for a very large social network (Facebook, LinkedIn, etc)? Describe how you would design an algorithm to show the connection, or path, between two people (e.g., Me -> Bob -> Susan -> Jason -> You).

## SOLUTION&#x20;

### Approach:&#x20;

Forget that we’re dealing with millions of users at first. Design this for the simple case. We can construct a graph by assuming every person is a node and if there is an edge between two nodes, then the two people are friends with each other.&#x20;

```java
class Person { 
    Person[] friends; 
    // Other info 
}
```

&#x20;If I want to find the connection between two people, I would start with one person and do a simple breadth first search.

But... oh no! Millions of users! When we deal with a service the size of Orkut or Facebook, we cannot possibly keep all of our data on one machine. That means that our simple Person data structure from above doesn’t quite work—our friends may not live on the same machine as us. Instead, we can replace our list of friends with a list of their IDs, and traverse as follows:&#x20;

1. For each friend ID: int machine\_index = lookupMachineForUserID(id);
2. Go to machine machine\_index
3. Person friend = lookupFriend(machine\_index);&#x20;

There are more optimizations and follow up questions here than we could possibly discuss, but here are just a few thoughts.

### Optimization:

Reduce Machine Jumps Jumping from one machine to another is expensive. Instead of randomly jumping from machine to machine with each friend, try to batch these jumps—e.g., if 5 of my friends live on one machine, I should look them up all at once.

Optimization: Smart Division of People and Machines People are much more likely to be friends with people who live in the same country as them. Rather than randomly dividing people up across machines, try to divvy them up by country, city, state, etc. This will reduce the number of jumps.

### Question:&#x20;

Breadth First Search usually requires “marking” a node as visited. How do you do that in this case? Usually, in BFS, we mark a node as visited by setting a flag visited in its node class. Here, we don’t want to do that (there could be multiple searches going on at the same time, so it’s bad to just edit our data). In this case, we could mimic the marking of nodes with a hash table to lookup a node id and whether or not it’s been visited.&#x20;

### Other Follow-Up Questions:&#x20;

* In the real world, servers fail. How does this affect you?&#x20;
* How could you take advantage of caching?
* Do you search until the end of the graph (infinite)? How do you decide when to give up?
* In real life, some people have more friends of friends than others, and are therefore more likely to make a path between you and someone else. How could you use this data to pick where you start traversing?

The following code demonstrates our algorithm:

```java
public class Server {
    ArrayList<Machine> machines = new ArrayList<Machine>();
}

public class Machine {
    public ArrayList<Person> persons = new ArrayList<Person>();
    public int machineID;
}

public class Person {
    private ArrayList<Integer> friends;
    private int ID;
    private int machineID;
    private String info;
    private Server server = new Server();

    public String getInfo() { return info; }
    public void setInfo(String info) {
       this.info = info;
    }

    public int[] getFriends() {
        int[] temp = new int[friends.size()];
        for (int i = 0; i < temp.length; i++) {
            temp[i] = friends.get(i);
        }
        return temp;
    }
    public int getID() { return ID; }
    public int getMachineID() { return machineID; }
    public void addFriend(int id) { friends.add(id); }

    // Look up a person given their ID and Machine ID
    public Person lookUpFriend(int machineID, int ID) {
        for (Machine m : server.machines) {
            if (m.machineID == machineID) {
                for (Person p : m.persons) {
                    if (p.ID == ID){
                        return p;
                    }
                }
            }
        }
        return null;
    }

     // Look up a machine given the machine ID
     public Machine lookUpMachine(int machineID) {
         for (Machine m:server.machines) {
             if (m.machineID == machineID)
             return m;
         }
         return null;
     }

      public Person(int iD, int machineID) {
          ID = iD;
          this.machineID = machineID;
      }
}
```

