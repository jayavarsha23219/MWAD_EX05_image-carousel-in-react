# MWAD_EX05_image-carousel-in-react
## Date: 20.05.205

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
### App.jsx
```
import React, { useState } from "react";
import "./App.css";

const images = [
  "https://images.unsplash.com/photo-1419242902214-272b3f66ee7a?w=620&auto=format&fit=crop&q=60&ixlib=rb-4.1.0",
  "https://images.unsplash.com/photo-1533573103248-543ca8890e42?w=620&auto=format&fit=crop&q=60&ixlib=rb-4.1.0",
  "https://images.unsplash.com/photo-1449034446853-66c86144b0ad?w=620&auto=format&fit=crop&q=60&ixlib=rb-4.1.0",
  "https://images.unsplash.com/photo-1519985176271-adb1088fa94c?auto=format&fit=crop&w=600&h=300&q=80"
];


function App() {
  const [currentIndex, setCurrentIndex] = useState(0);

  const prevSlide = () => {
    setCurrentIndex((prevIndex) =>
      prevIndex === 0 ? images.length - 1 : prevIndex - 1
    );
  };

  const nextSlide = () => {
    setCurrentIndex((prevIndex) =>
      prevIndex === images.length - 1 ? 0 : prevIndex + 1
    );
  };

  return (
    <div className="carousel-container">
      <h1>React Image Carousel</h1>
      <div className="carousel">
        <button className="nav-button" onClick={prevSlide}>
          ❮
        </button>
        <img src={images[currentIndex]} alt={`Slide ${currentIndex + 1}`} />
        <button className="nav-button" onClick={nextSlide}>
          ❯
        </button>
      </div>
      <div className="indicators">
        {images.map((_, index) => (
          <span
            key={index}
            className={`dot ${index === currentIndex ? "active" : ""}`}
            onClick={() => setCurrentIndex(index)}
          ></span>
        ))}
      </div>
    </div>
  );
}

export default App;

```
### App.css
```
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  margin: 0;
  padding: 0;
}

.carousel-container {
  max-width: 700px;
  margin: 40px auto;
  text-align: center;
  padding: 20px;
}

.carousel {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  border-radius: 10px;
}

.carousel img {
  width: 100%;
  max-height: 350px;
  object-fit: cover;
  border-radius: 10px;
  transition: transform 0.5s ease-in-out;
}

.nav-button {
  position: absolute;
  background-color: rgba(0, 0, 0, 0.4);
  color: white;
  border: none;
  font-size: 2rem;
  padding: 10px 20px;
  cursor: pointer;
  z-index: 2;
  top: 50%;
  transform: translateY(-50%);
  border-radius: 50%;
  user-select: none;
}

.nav-button:hover {
  background-color: rgba(0, 0, 0, 0.6);
}

.nav-button:first-of-type {
  left: 10px;
}

.nav-button:last-of-type {
  right: 10px;
}

.indicators {
  margin-top: 10px;
}

.dot {
  height: 12px;
  width: 12px;
  margin: 0 5px;
  background-color: #bbb;
  border-radius: 50%;
  display: inline-block;
  cursor: pointer;
}

.dot.active {
  background-color: #333;
}
```
## OUTPUT
![Screenshot 2025-05-20 224229](https://github.com/user-attachments/assets/aa75196e-9c0b-47fe-92dc-091aa4cd2b30)


## RESULT
The program for creating Image Carousel using React is executed successfully.
