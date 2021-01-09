---
layout: page
title: "New Example App: Number guessing Game"
description: "Implement a simple nuber guessing game with CloudUi"
---

### What it schould do

User can start a game at localhost:8080/start. First the user can input her or his name, the number range and how many guesses are allowed in maximum.

On a second view the user can input her or his guess until the maximum number of guesses is reached or she or he guess the right number. In case of a wrong guess a hint is schown whether the number is higher or lower the last guess.

When the game is over (right guess or maximum number of guesses reached) a result view is shown with the possibility to start again.

support for multiuser environment is out of the scope. To make things simple we assume there ist only one person who use the game in a local environment.

### Setup project on code.quarkus.io

### Add CloudUi Extension

Add the following dependency to your pom.xml file:

~~~
  <dependency>
      <groupId>net.moewes</groupId>
      <artifactId>cloud-ui-quarkus-extension</artifactId>
      <version>0.1.0-SNAPSHOT</version>
    </dependency>
~~~

[Setup Development Environment](../../../guides/1_setupDevEnvironment.html)

### First View

Let's build the StartView with Standard Html Components buildin in CloudUi. If there is an element missing you can declare it on the fly via the UiComponent class (see our input fields for example).

~~~

@CloudUiView("/start")
public class StartView extends Div {

    private UiComponent nameField = new UiComponent("input");
    private UiComponent numberOfTriesField = new UiComponent("input");
    private UiComponent numberRangeField = new UiComponent("input");
    
    public StartView() {

        add(new H1("Welcome to Number Guess Game"));

        add(new Label("Your Name:"));
        add(new UiComponent("br"));
        add(nameField);
        add(new UiComponent("br"));

        add(new Label("Number of tries:")); 
        add(new UiComponent("br"));
        add(numberOfTriesField);
        add(new UiComponent("br"));

        add(new Label("Number range:")); 
        add(new UiComponent("br"));
        add(numberRangeField);
        add(new UiComponent("br"));
        add(new UiComponent("br"));

        UiComponent startButton = new UiComponent("Button");
        startButton.setInnerHtml("Start Game");
        add(startButton);
    }
}
~~~

Let's check the results: do a mvn compile quarkus:dev and open your browser at http://localhost:8080/start.

### Our Game Bean

Next we need a bean where we store the game status. 

~~~~

@ApplicationScoped
public class GameBean {

    private String playersName = "nobody";
    private int numberRange = 10;
    private int maxNumberOfTries = 3;

    private int numberToGuess;
    private int numberOfTries;

    private String hint = "";
    private String result = "";
    private boolean ended = false;

    public void startGame() {

        Random random = new Random();
        numberToGuess = random.nextInt(numberRange + 1);
        numberOfTries = 0;
        ended = false;
    }

    public void evaluateGuess(int guess) {

        numberOfTries++;
        if (guess == numberToGuess) {
            ended = true;
            result = playersName + ", you have won!";
        } else {
            if (numberOfTries == maxNumberOfTries) {
                result = playersName + ", you have lost :-(";
                ended = true;
            } else {
                hint = (guess < numberToGuess) ? "Number is greater than " + guess : "Number is lower than " + guess;
            }
        }
    }

    public boolean hasEnded() {
        return ended;
    }

    public String getResult() {
        return result;
    }

    public String getHint() {
        return hint;
    }

    public void setPlayersName(String name) {
        playersName = name;
    }

    public void setNumberRange(int range) {
        numberRange = range;
    }

    public void setMaxNumberOfTries(int maxTries) {
        maxNumberOfTries = maxTries;
    }
}
~~~~

### Our Guessing View

This is where can input our guess and get feedback.
So we inject the GameBean. Also we inject an ui instance which will help us to navigate to a result view. To get get the value in the gameBean we use a binder.

~~~~

@CloudUiView("/guess")
public class GuessView extends Div {

    private int guess = 0;
    private UiComponent guessField = new UiComponent("input");
    
    @Inject
    public GuessView(GameBean gameBean, CloudUi ui) {

        add(new Label("Your Guess:")); 
        add(new UiComponent("br"));
        add(guessField);

        UiBinder binder = new UiBinder();
        binder.bind(guessField,this::getGuess,this::setGuess);

        add(new UiComponent("br"));
        add(new UiComponent("br"));
        
        UiComponent startButton = new UiComponent("Button");
        startButton.setInnerHtml("Guess");
        add(startButton);

        startButton.addEventListener("click", e -> {
            gameBean.evaluateGuess(guess);
            if (gameBean.hasEnded()) {
                ui.navigate(ResultView.class);
            } else {
                add(new Label(gameBean.getHint()));
            }
        });
    }

    public String getGuess() {
        return "" + guess;
    }

    public void setGuess(String value) {
        guess = Integer.parseInt(value);
    }
~~~~

### Connect the StartView with the GuessView

We also inject the GameBean an the ui instance in the StartView. Bind the value to the GameBean and implement the eventhandler to start the game and navigate

~~~~

@CloudUiView("/start")
public class StartView extends Div {

    private UiComponent nameField = new UiComponent("input");
    private UiComponent numberOfTriesField = new UiComponent("input");
    private UiComponent numberRangeField = new UiComponent("input");
    
    @Inject
    public StartView(GameBean gameBean, CloudUi ui) {

        add(new H1("Welcome to Number Guess Game"));

        add(new Label("Your Name:"));
        add(new UiComponent("br"));
        add(nameField);
        add(new UiComponent("br"));
        UiBinder nameBinder = new UiBinder();
        nameBinder.bind(nameField,() -> { return " "; },value -> {gameBean.setPlayersName(value);});

        add(new Label("Number of tries:")); 
        add(new UiComponent("br"));
        add(numberOfTriesField);
        add(new UiComponent("br"));
        UiBinder numberOfTriesBinder = new UiBinder();
        numberOfTriesBinder.bind(numberOfTriesField,() -> { return "3"; },value -> { gameBean.setMaxNumberOfTries(Integer.parseInt(value));});

        add(new Label("Number range:")); 
        add(new UiComponent("br"));
        add(numberRangeField);
        UiBinder numberRangeBinder = new UiBinder();
        numberRangeBinder.bind(numberRangeField, () -> { return "10"; }, value -> {
            gameBean.setNumberRange(Integer.parseInt(value));
        });

        add(new UiComponent("br"));
        add(new UiComponent("br"));

        UiComponent startButton = new UiComponent("Button");
        startButton.setInnerHtml("Start Game");
        add(startButton);

        startButton.addEventListener("click", e -> {
            gameBean.startGame();
            ui.navigate(GuessView.class);
        });
    }
}
~~~~~

### Last thing the result view

~~~~

@CloudUiView("/result")
public class ResultView extends Div {
    
    @Inject
    public ResultView(GameBean gameBean) {

        add(new H1(gameBean.getResult()));
    }
}
~~~~

###  Summary

We learnt a lot of things in this short example:

* setup a project
* define view in java (like you do with vaadin)
* bind data
* use events
* navigate between views

This was a small overview what you can with CloudUi so far. 