import React from 'react';

const Rating = ({ value, maxValue, onChange }) => {
  const handleClick = (newValue) => {
    // Calculate the new value based on the clicked star position
    const newValue1 = value === newValue ? newValue - 0.5 : newValue;
    onChange(newValue1);
  };

  const stars = [];
  const roundedValue = Math.round(value * 2) / 2; // Round to the nearest 0.5
  for (let i = 1; i <= maxValue; i++) {
    let starClassName = 'star';
    if (i <= roundedValue) {
      starClassName = 'star filled';
    } else if (i - 0.5 === roundedValue) {
      starClassName = 'star half-filled';
    }
    stars.push(
      <span
        key={i}
        className={starClassName}
        onClick={() => handleClick(i)}
        title={i}
      >
        ★
      </span>
    );
  }

  return <div className="rating">{stars}</div>;
};

export default Rating;


import React from 'react';
import './style.css';
import Rating from './Rating';

export default function App() {
  const [rating, setRating] = React.useState(3.5);
  return (
      <Rating
        value={rating}
        maxValue={5}
        onChange={(value) => {
          debugger;
          setRating(value);
        }}
      />
  );
}


.rating {
  display: inline-block;
}

.star {
  font-size: 2rem;
  color: #ccc;
  cursor: pointer;
}

.filled {
  color: #ffcc00; /* Color for filled stars */
}

.half-filled {
  position: relative;
  display: inline-block;
}

.half-filled:after {
  content: '★';
  position: absolute;
  left: 0;
  overflow: hidden;
  width: 50%;
  color: #ffcc00; /* Color for the half star */
}
