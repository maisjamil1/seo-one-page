# unique-react-rating-stars

A customizable React component for displaying star ratings.

## Installation

Install the package using npm:

```bash
npm install unique-react-rating-stars

Or with yarn:

```bash
yarn add unique-react-rating-stars

Peer Dependencies
Ensure you have react and react-dom installed in your project:

```bash
npm install react react-dom

## Usage
Import the RatingHandler component and use it in your React application.

## Basic Example

```
import React, { useState } from 'react';
import RatingHandler from 'unique-react-rating-stars';

const App = () => {
  const [rating, setRating] = useState(3);

  return (
    <div>
      <h1>Product Rating</h1>
      <RatingHandler value={rating} onChange={setRating} />
      <p>Your rating: {rating}</p>
    </div>
  );
};

export default App;


```
