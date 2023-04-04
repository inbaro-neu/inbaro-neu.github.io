---
layout: page
title: Animation Generator
description: "Program to generate animations from a text description<br><b>Using: </b><em>Java, Java Swing</em>"
img: assets/img/buildings-interactive-screenshot.png
importance: 1
category: school
---

<em>Authors:</em> Inbar Ofer and Benjamin Levin

- Access to the GitHub repository may be provided upon request.

## Overview

This is an animation program developed using MVC (Model-View-Controller) design and tested extensively with JUnit tests to ensure proper code functionality.

User features:
- Create and visualize animations and export them as an SVG or a textual description
- Control animation via a clean and effective UI

## Design

As seen in the project directory structure below, we decided to use MVC design for this project. The Model-View-Controller architecture has several benefits:
- <b>Separation of concerns:</b> One of the main benefits of MVC is that it separates the different concerns of an application into distinct components. The model is responsible for handling data and business logic, the view is responsible for displaying information to the user, and the controller is responsible for handling user input and updating the model and view accordingly. This separation of concerns makes it easier to maintain and modify different parts of the application without affecting others.
- <b>Reusability:</b> Because the different components of the MVC architecture are separated and loosely coupled, they can be reused across different applications. For example, the same model could be used in different views or controllers, or the same controller could be used with different models.
- <b>Testability:</b> Because the different components of the MVC architecture are loosely coupled, they can be more easily tested in isolation. This makes it easier to write unit tests for each component, ensuring that the application functions correctly.
- <b>Flexibility:</b> Because the different components of the MVC architecture are decoupled, changes to one component can be made without affecting the others. This makes it easier to modify the application to meet changing requirements or to add new features.
- <b>Maintainability:</b> Because the different components of the MVC architecture are separated, it is easier to maintain the codebase over time. Developers can modify individual components without worrying about how those changes will affect the rest of the application, making it easier to fix bugs or add new features.

{% raw %}
```
---
├── projects/
│   ├── controller/
│   │   ├── AController.java
│   │   ├── Features.java
│   │   ├── IController.java
│   │   ├── InteractiveController.java
│   │   └── NonInteractiveController.java
│   ├── icons/...
│   ├── model/
│   │   ├── shape/
│   │   │   ├── AShape.java
│   │   │   ├── Ellipse.java
│   │   │   └── Rectangle.java
│   │   ├── state/
│   │   │   ├── action/
│   │   │   │   ├── AAction.java
│   │   │   │   ├── ColorAction.java
│   │   │   │   ├── HeightAction.java
│   │   │   │   ├── IAction.java
│   │   │   │   ├── WidthAction.java
│   │   │   │   ├── XPositionAction.java
│   │   │   │   └── YPositionAction.java
│   │   │   ├── AStep.java
│   │   │   ├── IStep.java
│   │   │   ├── OffStep.java
│   │   │   └── OnStep.java
│   │   ├── IModel.java
│   │   └── Model.java
│   └── view/
│       ├── AnimationPanel.java
│       ├── IInteractiveView.java
│       ├── INonInteractiveView.java
│       ├── IView.java
│       ├── InteractiveVisualView.java
│       ├── TextualView.java
│       ├── TextualViewWithTime.java
│       └── VisualView.java
---
```
{% endraw %}

<div class="caption">
    Project directory structure
</div>

Here is how MVC was used to organize this animation generator:
- <b>Model:</b> The Model component represents the application's data and business logic. It is responsible for managing the animation's state, including the shapes, actions, and steps involved in the animation. The Model defines the data structures and methods required to manipulate the data. In the project directory, the Model component is represented by the classes in the `model/` directory, including `IModel.java`, `Model.java`, and other classes and interfaces that define shapes, actions, and steps.
- <b>View:</b> The View component is responsible for rendering the animation data from the Model to the user. It defines how the data is visually represented and displayed. In this assignment, two types of views are implemented: a textual view (`TextualView.java`, `TextualViewWithTime.java`) and a visual animation view (`VisualView.java`, `InteractiveVisualView.java`). The textual view provides a textual description of the animation, while the visual animation view creates a graphical animation using Java Swing. The View component is represented by the classes and interfaces in the `view/` directory.
- <b>Controller:</b> The Controller component is responsible for mediating interactions between the Model and the View. It manages user input, updates the Model accordingly, and ensures that the View is updated to reflect any changes to the Model. The Controller also handles user interactions for interactive views. In the project directory, the Controller component is represented by the classes in the `controller/` directory, including `IController.java`, `AController.java`, `InteractiveController.java`, and `NonInteractiveController.java`.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/buildings-interactive-screenshot.png" title="Interface View" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This is an example of the interactive view of the program. This view allows the user to play/pause, enable/disable looping, restart, rewind, and fast-forward.
</div>

## Bubble Sort

We animated a bubble sort algorithm using our animation generator program.

{% raw %}
```java
private List<Color[]> bubbleSort(float[][] colors) {
  List<Color[]> switches = new ArrayList<>();
  float[][] sortedElements = Arrays.copyOf(this.elements, this.elements.length);
  for (int i = 0; i < sortedElements.length - 1; i++) {
    for (int j = 0; j < sortedElements.length - i - 1; j++) {
      if (sortedElements[j][0] > sortedElements[j + 1][0]) {
        switches.add(new Color[]{
            Color.getHSBColor(sortedElements[j][0], sortedElements[j][1], sortedElements[j][2]),
            Color.getHSBColor(sortedElements[j + 1][0], sortedElements[j + 1][1],
                sortedElements[j + 1][2])});
        float[] temp = sortedElements[j];
        sortedElements[j] = sortedElements[j + 1];
        sortedElements[j + 1] = temp;
      }
    }
  }
  return switches;
}
```
{% endraw %}

<!-- 633x1357 -->
<div class="row d-flex align-items-center">
    <div class="col-sm mt-3 mt-md-0">
    <p>The <code>bubbleSort(float[][] colors)</code> method sorts an array of HSB (Hue, Saturation, Brightness) colors into rainbow order based on the hue values. The method takes a 2D float array colors as an input, where each row represents a color in HSB format. The first element of each row represents the hue, the second element is the saturation, and the third element is the brightness.</p>
    <p>The method uses the bubble sort algorithm, a simple sorting algorithm that iteratively compares adjacent elements and swaps them if they are in the wrong order. The algorithm continues until the entire array is sorted.</p>
    <p>In this implementation, the method also records each switch (swap) of colors that occurs during the sorting process. The <code>switches</code> list contains arrays of two <code>Color</code> objects representing the colors being swapped. Each <code>Color</code> object is created using the <code>Color.</code> method, which converts the HSB values to the corresponding `Color` object.</p>
    <p>The sorted array of colors is returned in rainbow order, and the <code>switches</code> list provides a way to visualize or animate the sorting process, showing the steps taken to sort the colors. This implementation demonstrates the ability to work with algorithmic concepts, color representations, and data structures to achieve a specific goal.</p>
    </div>
    <div class="col-auto mt-3 mt-md-0">
        <video width="300" controls autoplay muted loop>
        <source src="../../assets/video/bubble_sort.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
    </div>
</div>

