# unique-react-rating-stars

A customizable React component for displaying star ratings.

## Installation

Install the package using npm:

```bash
npm install unique-react-rating-stars
```
Or with yarn:

```bash
yarn add unique-react-rating-stars
```
Peer Dependencies
Ensure you have react and react-dom installed in your project:

```bash
npm install react react-dom
```
## Usage
Import the RatingHandler component and use it in your React application.

## TypeScript Support
Type definitions are included with the package, allowing seamless integration in TypeScript projects.

## Author
Mais Aburabie

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
## Props

### `value` (required)

- **Type:** `number`
- **Description:** The current rating value.

### `onChange`

- **Type:** `(value: number) => void`
- **Description:** Callback function called when the rating changes.

### `readOnly`

- **Type:** `boolean`
- **Default:** `false`
- **Description:** If `true`, the rating component is read-only.

### `max`

- **Type:** `number`
- **Default:** `5`
- **Description:** The maximum number of stars to display.

## Advanced Example
Here's a more detailed example demonstrating all available props:

```

import React, { useState } from 'react';
import RatingHandler from 'unique-react-rating-stars';

const ProductReview = () => {
  const [rating, setRating] = useState(0);

  const handleRatingChange = (value) => {
    console.log('Selected rating:', value);
    setRating(value);
  };

  return (
    <div>
      <h2>Rate Our Product</h2>
      <RatingHandler
        value={rating}
        onChange={handleRatingChange}
        readOnly={false}
        max={10}
      />
      <p>Your rating: {rating}</p>
    </div>
  );
};

export default ProductReview;


```

## License
This project is licensed under the ISC License.
