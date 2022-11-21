# Monday's Homework

## Initial greeting code


```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Please enter the time to the nearest hour");
        Scanner userInput = new Scanner(System.in);
        int timeOfDay = userInput.nextInt();

        System.out.println(greeting(timeOfDay));

    }

    public static String greeting(int timeOfDay){
        String greeting;
        if(timeOfDay >= 5 && timeOfDay < 12) {
            greeting = "Good morning!";
        } else if (timeOfDay >= 12 && timeOfDay < 18) {
            greeting = "Good afternoon!";
        } else if (timeOfDay >= 18 && timeOfDay < 22) {
            greeting = "Good Evening!";
        } else {
            greeting = "Why are you still awake?";
        }
        return greeting;
    }
}
```

## Parameterized Testing of the code
```java
class MainTest {
    @ParameterizedTest
    @ValueSource(ints = {5, 8, 11})
    @DisplayName("Given a time between 5 and 11, greeting returns Good morning!")
    public void GivenATimeBetween5and12_Greeting_ReturnsGoodMorning(int time){
        String expectedGreeting = "Good morning!";
        String result = Main.greeting(time);
        assertEquals(expectedGreeting, result);
    } //Test passed

    @ParameterizedTest
    @ValueSource(ints = {12, 15, 17})
    @DisplayName("Given a time between 12 and 17, greeting returns Good afternoon!")
    public void GivenATimeBetween12and17_Greeting_ReturnsGoodAfternoon(int time){
        String expectedGreeting = "Good afternoon!";
        String result = Main.greeting(time);
        assertEquals(expectedGreeting, result);
    } //Test passed

    @ParameterizedTest
    @ValueSource(ints = {18, 20, 22})
    @DisplayName("Given a time between 18 and 22, greeting returns Good evening!")
    public void GivenATimeBetween5and12_Greeting_ReturnsGoodEvening(int time){
        String expectedGreeting = "Good evening!";
        String result = Main.greeting(time);
        assertEquals(expectedGreeting, result);
    } //Test passed

    @ParameterizedTest
    @ValueSource(ints = {23, 1, 4})
    @DisplayName("Given a time after 22 and before 5, greeting returns Why are you still awake?")
    public void GivenATimeAfter22andBefore5_Greeting_ReturnsWhyAreYouStillAwake(int time){
        String expectedGreeting = "Why are you still awake?";
        String result = Main.greeting(time);
        assertEquals(expectedGreeting, result);
    } //Test passed
```

## Film Classification Code

```java
public class FilmClassifications {
    public static void main(String[] args) {

        System.out.println("Welcome to the cinema, what is your age?");
        Scanner userInput = new Scanner(System.in);
        int ageOfViewer = userInput.nextInt();

        System.out.println(availableClassifications(ageOfViewer));
    }



    public static String availableClassifications(int ageOfViewer) {
        String result;
        if (ageOfViewer < 12) {
            result = "U & PG films are available.";
        } else if (ageOfViewer >= 12 && ageOfViewer < 15) {
            result = "U, PG, 12 films are available.";
        } else if (ageOfViewer >= 15 && ageOfViewer < 18) {
            result = "U, PG, 12 & 15 films are available.";
        } else {
            result = "All films are available.";
        }
        return result;
    }
}
```
## Classification Tests

```java
class Classification_Tests {
    @ParameterizedTest
    @ValueSource(ints = {2, 5, 11})
    @DisplayName("Given the viewer is under 12, result returns U & PG films")
    public void GivenTheViewerIsUnder12_Result_ReturnsUandPG(int age) {
        String expectedResult = "U & PG films are available.";
        String result = FilmClassifications.availableClassifications(age);
        assertEquals(expectedResult, result);
    } // Test Passed

    @ParameterizedTest
    @ValueSource(ints = {12, 13, 14})
    @DisplayName("Given the viewer is 12 or over and under 15, result returns U, PG and 12 films")
    public void GivenTheViewerIs12orOverAndUnder15_Result_ReturnsUandPGand12(int age) {
        String expectedResult = "U, PG and 12 films are available.";
        String result = FilmClassifications.availableClassifications(age);
        assertEquals(expectedResult, result);
    } // Test Passed

    @ParameterizedTest
    @ValueSource(ints = {15, 16, 17})
    @DisplayName("Given the viewer is 15 or over and under 18, result returns U & PG films")
    public void GivenTheViewerIs15orOverAndUnder18_Result_ReturnsUandPGand12and15(int age) {
        String expectedResult = "U, PG, 12 and 15 films are available.";
        String result = FilmClassifications.availableClassifications(age);
        assertEquals(expectedResult, result);
    } // Test Passed

    @ParameterizedTest
    @ValueSource(ints = {18, 56, 90})
    @DisplayName("Given the viewer is 18 or over, result returns all films available")
    public void GivenTheViewerIs18orOver_Result_ReturnsAllFilmsAvailable(int age) {
        String expectedResult = "All films are available.";
        String result = FilmClassifications.availableClassifications(age);
        assertEquals(expectedResult, result);
    } // Test Passed
}
```
## Film Classification Code With Lower and Upper Age Limits

```java
public static String availableClassifications(int ageOfViewer) {
        String result;
        if (ageOfViewer < 0 && ageOfViewer < 115) {
            if (ageOfViewer < 12) {
                result = "U and PG films are available.";
            } else if (ageOfViewer >= 12 && ageOfViewer < 15) {
                result = "U, PG and 12 films are available.";
            } else if (ageOfViewer >= 15 && ageOfViewer < 18) {
                result = "U, PG, 12 and 15 films are available.";
            } else {
                result = "All films are available.";
            }
        } else {
            result = "That value is not correct";
        }
        return result;
    }
```
## Test Of Updated code
```java
@ParameterizedTest
    @ValueSource(ints = {-3, 0, 190})
    @DisplayName("Given the viewer has provided an inappropriate vlaue, result returns inappropriate value")
    public void GivenTheViewerProvidesInappriopriateValue_Result_ReturnsInappropriateValue(int age) {
        String expectedResult = "That value is not appropriate";
        String result = FilmClassifications.availableClassifications(age);
        assertEquals(expectedResult, result);
    } // Test Passed
```
## Greetings With Check For Correct Input And Prompt
```java
public class Main {
    public static void main(String[] args) {
        int timeOfDay = 0;
        boolean correctTime = false;

        while (correctTime == false) {
            System.out.println("Please enter the time to the nearest hour");
            Scanner userInput = new Scanner(System.in);
            int timeOfDayTest = userInput.nextInt();
            if (timeOfDayTest < 0 || timeOfDayTest > 24) {
                correctTime = false;
                System.out.println("That is not a valid hour");
            } else {
                correctTime = true;
                timeOfDay = timeOfDayTest;
            }
        }
```
