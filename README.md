# Digital Clock

This JAVA programs print the digit clock like 👇

```bash
  _    _         _                   _  
  _|   _|   -    _|    |   -     |  |_| 
 |_    _|   -   |_     |   -     |   _|

```

## The code of this code is given below.

```java
import java.io.IOException;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class App {

    private static final int ROWS = 3;
    private static final int SECOND = 1000;
    private static final int COLON_INDEX = 10;
    private static final String[][] DIGITS_ARR = {
            {
                    "  _  ",
                    " | | ",
                    " |_| "
            },
            {
                    "     ",
                    "   | ",
                    "   | "
            },
            {
                    "  _  ",
                    "  _| ",
                    " |_  "
            },
            {
                    "  _  ",
                    "  _| ",
                    "  _| "
            },
            {
                    "     ",
                    " |_| ",
                    "   | "
            },
            {
                    "  _  ",
                    " |_  ",
                    "  _| "
            },
            {
                    "  _  ",
                    " |_  ",
                    " |_| "
            },
            {
                    "  _  ",
                    "   | ",
                    "   | "
            },
            {
                    "  _  ",
                    " |_| ",
                    " |_| "
            },
            {
                    "  _  ",
                    " |_| ",
                    "  _| "
            },
            {
                    "     ",
                    "  -  ",
                    "  -  "
            },
    };

    public static void main(String[] args) throws Exception {
        printTime();
    }

    // This funtion prints the formatted time in 1 second interval.
    private static void printTime() throws IOException, InterruptedException {
        while (true) {
            clear();
            String now = currTimeStamp();
            printFormattedTimeStamp(now);
            Thread.sleep(SECOND);
        }
    }

    // This function returns the current time string. like [ 13:45:09 ]
    private static String currTimeStamp() {
        LocalDateTime time = LocalDateTime.now();
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("HH:mm:ss");
        return time.format(formatter);
    }

    // This function clears the console.
    private static void clear() {
        try {
            new ProcessBuilder("clear")
                    .inheritIO()
                    .start().waitFor();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }

    // This function prints time stamp in (|, _) format.
    private static void printFormattedTimeStamp(String timeStamp) {
        for (int index = 0; index < ROWS; index++) {
            for (char ch : timeStamp.toCharArray()) {
                int intValue = ch - '0';

                if ((intValue >= 0) && (intValue <= 9))
                    System.out.print(DIGITS_ARR[intValue][index]);

                else
                    System.out.print(DIGITS_ARR[COLON_INDEX][index]);
            }
            System.out.println();
        }
    }
}

```