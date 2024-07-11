# Course Card Section Component

This Vue component is designed to display a set of categorized course cards in a visually appealing and interactive manner. It includes functionality for category navigation and dynamic content display using Splide, a flexible and lightweight carousel library.

## Features

- **Category Navigation**: Users can navigate through different course categories using a horizontal slider. Each category contains a specific set of course cards.
- **Dynamic Content Display**: The component dynamically adjusts the number of visible course cards based on the screen size and user interactions.
- **Responsive Design**: The component is fully responsive, providing an optimal viewing experience across various devices.
- **Expandable Content**: Users can toggle between viewing a limited number of course cards and an expanded view displaying all cards in the selected category.
- **Smooth Transitions**: The component includes smooth transition effects when navigating between categories and expanding/collapsing the card view.
- **Custom Buttons**: Includes primary and secondary buttons for additional interactions, such as expanding content and viewing all courses.

## Key Parts of the Component

### Imports and Setup

- **Vue Imports**: Importing essential Vue functionalities such as `ref`, `reactive`, `onMounted`, and `computed`.
- **Splide Imports**: Importing Splide and its Vue integration for creating carousels.
- **Button Components**: Importing custom button components for primary and secondary actions.

### Data and Reactive State

- **Categories and Slides**: Defining a set of categories, each with a collection of course slides.
- **Reactive State**: Managing the state of the component, including the active category, progress, and visibility of content.

### Computed Properties

- **Active Slides**: Filtering the slides based on the selected category.
- **Visible Slides**: Controlling the number of slides displayed, with logic for expanding and collapsing the view.
- **Show More Button**: Determining the visibility of the "Show more" button based on the number of slides.

### Methods

- **Category Click Handler**: Updating the active category and resetting the content slider.
- **Slide Navigation**: Functions to navigate to the previous and next slides.
- **Expand and Collapse**: Toggling the expanded state of the content and handling scrolling to the section.
- **Update Initial Card Count**: Adjusting the number of visible cards based on the screen size.

### Lifecycle Hooks

- **onMounted**: Setting up event listeners and initial state updates when the component is mounted.

### Template

- **Category Navigation Slider**: Using Splide to create a horizontal slider for categories.
- **Course Cards Grid**: Displaying the course cards in a responsive grid layout.
- **Expand/Collapse Button**: Providing a button to toggle the expanded state of the card view.

### Styles

- **Scoped Styles**: Custom styles for the component, including transition effects for the card list.

## How to Use

1. **Install Dependencies**: Ensure you have installed the necessary dependencies, including Vue and Splide.
2. **Import Component**: Import the component into your Vue project.
3. **Use in Template**: Add the component to your template and pass any necessary props or data.
4. **Customize as Needed**: Adjust the styles, categories, and content as per your requirements.

## Example

```vue
<template>
  <CourseCardSection />
</template>

<script>
import CourseCardSection from "@/components/CourseCardSection.vue";

export default {
  components: {
    CourseCardSection,
  },
};
</script>
