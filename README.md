Of course! Here is a comprehensive README for your web project.

---

# Project README: STUDIO - A Digital Design Portfolio

This document provides a detailed overview of the "STUDIO" website project, a submission for PixxelHack 1.0. The project is a modern, responsive, and highly animated website for a fictional digital design studio.

## Live Demo

[A live demo of the project can be accessed here.](https://pixxelhack1.netlify.app/https/) *(Please replace with your actual deployment link.)*

## Project Description

STUDIO is a single-page portfolio website designed to showcase the skills of a digital design and development studio. It features a sleek, dark-themed aesthetic with a focus on fluid animations and user interactions. The site includes a main landing page (`index.html`) with sections for services, work, and contact information, as well as a separate `team.html` page to introduce the team and highlight past collaborations.

## Features

The website is packed with dynamic features to create an engaging user experience:

* **Loading Animation:** An initial loading screen with a counter from 0 to 100 ensures all assets are ready before revealing the main content.
* **Interactive Mouse Ripple Effect:** A subtle, real-time ripple effect follows the user's cursor, created using a `Three.js` shader on a WebGL canvas. This adds a layer of sophisticated interactivity without impacting performance.
* **Hero Text Scroll Animation:** The main headline "CREATIVE" is animated on scroll. Each letter segment slides into view and then slides out as the user scrolls down the page.
* **Text Scramble Effect:** The headlines in the hero section feature a "scramble" animation on mouseover, which cycles through random characters before revealing the original text.
* **On-Scroll Content Reveal:** As the user scrolls, content sections for About, Services, Work, and Contact gracefully fade and slide into view. This is implemented efficiently using the `IntersectionObserver` API.
* **Interactive Team Page:** The `team.html` page features:
    * An interactive avatar display where hovering over a team member's name reveals their picture.
    * An auto-scrolling marquee of "Worked With" client testimonials that pauses on hover or touch for better readability.
* **Fully Responsive Design:** The layout, animations, and typography are fully responsive, ensuring a seamless experience on desktops, tablets, and mobile devices.
* **Full-Screen Navigation:** A modern, hamburger-style menu opens into a full-screen overlay for clear and easy navigation.

## Technologies Used

The project is built using standard web technologies and leverages powerful JavaScript libraries for animations.

* **HTML5:** Semantic HTML for the structure of the pages.
* **CSS3:** Advanced styling using Flexbox, Grid, Custom Properties (variables), and keyframe animations for a responsive and modern design.
* **JavaScript (ES6+):** Powers all the dynamic and interactive features of the site.
* **GSAP (GreenSock Animation Platform):** Used for the initial loader animation to ensure a smooth and high-performance transition.
* **Three.js:** A 3D graphics library used to render the WebGL canvas for the interactive mouse ripple effect.

## File Structure

The project is organized into several files, each with a specific role:

* `index.html`: The main landing page of the website.
* `team.html`: The "Team" page showcasing team members and clients.
* `style.css`: The primary stylesheet containing global styles, layout, and responsive media queries.
* `team.css`: Contains styles specific to the `team.html` page, including the avatar display and scrolling marquee.
* `textanimation.css`: Dedicated CSS for the hero section's scroll-based text animation.
* `script.js`: Core JavaScript for `index.html`. Handles the loader, ripple effect, text scramble, navigation, and on-scroll reveals.
* `team.js`: JavaScript for `team.html`. Manages the interactive avatar display and controls the pause/resume functionality of the client marquee.
* `textanimation.js`: The JavaScript logic that drives the `translateY` transformation of the hero text based on scroll position.
* `image.png` & `image1.png`: Background assets used in the design.

## Code Highlights & Explanation

### 1. Mouse Ripple Effect (`script.js`)

This effect is achieved by rendering a plane geometry on a `Three.js` canvas that covers the viewport. A custom fragment shader is used to create the visual effect.

* **Logic:** The script listens for the `mousemove` event to update a `u_mouse` uniform variable with the cursor's normalized coordinates.
* **Shader:** The GLSL fragment shader calculates the distance between each pixel (`vUv`) and the mouse's position (`u_mouse`). It uses this distance to calculate a `strength` value via `smoothstep`, which determines the opacity of the colored ripple. This creates a soft-edged circle of color that follows the mouse.

$$\text{dist} = \text{distance}(\text{vUv}, \text{u\_mouse}) \times \text{u\_max\_dist}$$
$$\text{strength} = \text{smoothstep}(0.7, 0.0, \text{dist}) - \text{smoothstep}(1.0, 0.7, \text{dist})$$

### 2. Scroll-Based Text Animation (`textanimation.js`)

This animation creates the effect of text being "pushed up" and out of view on scroll.

* **Logic:** An event listener on the `scroll` event triggers the `checkAllDivs` function.
* **Calculation:** For each `.word-box-wrapper`, the script calculates its center (`divCenter`) relative to the viewport. It then determines a `scrollProgress` value based on how far the user has scrolled past a certain point. This progress is clamped between 0 and 100 and used to set a `translateY` percentage on the inner `.word-box`, causing it to slide vertically inside its masked parent container.

### 3. Team Page Interactivity (`team.js`)

* **Avatar Switching:** The `showAvatar(index)` function is called on `mouseenter` or `touchstart`. It works by toggling `active` and `selected` classes. It iterates through all avatar and name elements, adding the class only to the element whose index matches the one passed to the function and removing it from all others.
* **Marquee Control:** The script adds event listeners (`mouseenter`, `mouseleave`, etc.) to the `.scroll-container`. The handler functions, `pauseScroll` and `resumeScroll`, simply toggle the CSS `animationPlayState` property between `"paused"` and `"running"`.
